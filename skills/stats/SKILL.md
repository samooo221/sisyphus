---
name: stats
description: Regenerate a course's progress note from drill and exam results; score curve, per-topic breakdown, drill-vs-real-exam rows. Use for "how am I trending" or after grading a drill.
---

# Stats

Read [the learning contract](../../references/learning-contract.md) before acting.

Reads **frontmatter only** — never prose — from result files, and regenerates each course's `progress.md`. Everything here is derived data; overwriting it is safe and correct.

## `sisyphus stats [COURSE]`

1. **Discover courses.** Glob the vault's MOC notes for frontmatter containing an `exam:` block; `code:` is the course key. With `[COURSE]` given, do just that one.
2. **Collect results.** In each course's private drills dir (`exam.drills_dir`, otherwise `<exam.corpus>/drills`), read the frontmatter of every file with `type: drill-result`, `type: exam-result` or `type: oral-result`:
   - `drill-result`: `attempt_id, batch_id, date, date_basis, created, started_at, elapsed_min, time_min, format_basis, student_exposure, conditions, feedback_before_sitting, paper_form, exam_equivalent, source_ids, graded, source, mode, raw_score, score, total, gates_passed, gate_results, cards_added, pending_misconceptions, questions: [{n, topic, section, scored, possible, source_id, rubric_source}]`
   - `exam-result` (real graded events, recorded by hand): `date, kind: final|midterm, score, total`
   - `oral-result` (mock defenses from `sisyphus oral`): `date, project, passed, score (of 10), stumbles`
   A file that should parse but doesn't goes in the report as a warning with its path — **never silently skip it**; a silently dropped result poisons the trend.
   Validate the raw question sum against `raw_score`, possible sum against `total`, and effective `score` against gate results in exam mode; practice keeps raw marks, with any `exam_format_diagnostic_score` separate. A gate failure legitimately makes effective score differ from summed question scores. Old files without gate metadata are legacy practice, not evidence of passing an exam gate. Existing legacy directories may be read for historical results, but never write assessment content into the vault. Deduplicate by course + attempt ID only when content agrees; conflicting records are errors. Same date is never a duplicate: two papers that day remain two result rows. Legacy records use their full original file path as identity. Sort by reported sitting time when known, then date and attempt sequence; mark unknown intra-day order, never infer it from modification time.
3. **Regenerate `<drills_dir>/progress.md`** (overwrite):
   - Frontmatter: `type: progress`, `course`, `updated`.
   - **Score over time** — date + attempt ID · effective score/total · raw score/total · gate verdict · exposure · conditions · mode · source. Add elapsed time only when reported. Separate rows for every paper in a batch; its average cannot conceal a failed gate. Plot exam-mode drills separately from practice quizzes, synthetic checks, legacy files and real midterms/finals. Different kinds and clocks are not interchangeable evidence. Oral results appear as `**oral 7/10**` rows with a ✓/✗ for `passed`, outside the score curve.
   - **Per-topic** — sum raw question `scored/possible`, explicitly labelled diagnostic marks; retain the practice/exam distinction and flag generated rubrics. A gate failure must not erase topic evidence or be hidden by good main-part marks. Show gate failures in a separate prominent count. Topics with fewer than ~6 possible points get a "thin data" mark instead of an arrow.
   - A mermaid `xychart-beta` only with ≥3 comparable exam-mode drill points: same course, format basis, clock, source class, intact/assembled form, explicitly `unseen-confirmed` exposure and `closed-book-timed-unaided` conditions. Use effective scores and unique attempt labels. Unknown/repeated/assisted attempts remain visible in separate practice rows. Synthetic drills do not join authentic FIT curves. Never manufacture a trend from an empty dataset.
   - **Volume and transfer:** show completed papers and questions, raw accuracy, source coverage, fresh versus repeat/unknown counts, and review/check evidence when present. Count unique source/exercise IDs rather than repeated attempts as new coverage; missing IDs mean unique coverage is unknown. More downloaded pages or bank entries are not student performance. Use separate fresh and repeat topic summaries so memorised repeats cannot dominate targeting. Question points are weighted marks, not number of correct questions.
   - **Review debt:** show `pending_misconceptions` at grading time, not a current unresolved total. Read optional separate `type: learning-check` frontmatter records with `course, date, misconception_id, own_words, unaided_transfer, evidence_path` for later resolution — `tutor` writes these when a previously pending misconception passes the own-words gate, and it is the only writer. Missing records mean current resolution is unknown, which is the normal state for a course whose misconceptions were all raised and closed in one session. Never invent deadlines, checks or pass claims. The student's own rewrite remains the card gate.
   - A one-line read at the top: current trend and weakest topic. Trending down = the study loop is lying somewhere; fix the loop, not the vibe.
   - **Danger list (endgame predictor).** If the MOC's `exam:` block has `test_terms: [YYYY-MM-DD, ...]` and today is within 72 h of the next term, append the exam-week priority order: topics ranked by per-topic scored/possible — below ~60 % is *danger*, a topic with zero drill coverage is a *blind spot* (listed last, loudest, since no data ≠ no risk). The last 72 h are won by triage, not re-reading; the `daily` brief draws its unaided checks from this list during exam week.
4. **Report** per course: one trend line, weakest topic, and any parse warnings.

## Recording real exams

When a real graded event comes back (midterm, final), record it the same day as `<drills_dir>/YYYY-MM-DD-NN-exam.md`, with `NN` allocated as `drill` allocates an attempt ID (`01`, then `02`, …) so two events on one day cannot collide. Existing date-only `YYYY-MM-DD-exam.md` files stay valid:

```yaml
---
type: exam-result
course: IZP
date: 2027-01-14
kind: final
score: 44
total: 54
---
```

Offer to write this file when the user mentions a real result. Without these rows there is nothing to correlate the drill curve against.
