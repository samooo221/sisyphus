---
name: drill
description: Build and grade timed closed-book drills from a course bank, matching known exam sections and gates, with fixed rubrics and fresh-session grading. Queue misconceptions until the student explains them in their own words. Use for exam practice ("new drill", "drill me on IZP", "grade my drill").
---

# Drill

Read [the learning contract](../../references/learning-contract.md) and [paper practice](../../references/paper-practice.md) before acting.

**During creation, never print a question, answer or topic list into chat.** Reply with paths, clock and source limitations only. During grading, summary scores and weak topics are allowed; question and answer text stays on disk. A drill already read is not an unseen drill.

## Course config

Find the course's MOC: a note with `type: moc` frontmatter (usually under a `MOCs/` folder) whose `code:` matches the course. Its `exam:` block is the single source of course facts:

The following schema example uses the historical IZP sample, not current course facts.

```yaml
exam:
  final_total: 54            # required — drill point values sum to this
  time_min: 90               # verified real exam clock; null when unknown
  time_status: verified     # verified | unverified
  corpus: ~/data/exams/IZP   # optional — dir of past-paper PDFs + question-bank.md
  topics:                    # required — canonical topic names; weight: invest|normal|skim (default normal)
    - {name: pointers, weight: invest}
    - {name: control-flow, weight: skim}
  sections:
    - {id: final, total: 54, questions: 8, question_points: [6, 8, 6, 8, 10, 6, 4, 6]}
  gates:
    - {scope: exam, min_points: 23, on_fail: zero_exam}
  drills_dir:                # optional — default <corpus>/drills, outside vault and repos
  flashcards:                # optional — default <Area>/Flashcards/<code> — flashcards.md
```

`<Area>` is the folder above the MOC's `MOCs/` directory (e.g. `University/`). No `exam:` block → stop and point at `sisyphus setup <COURSE>`; never guess course facts.

For a two-part paper, use `sections: [{id: short-test, total: 10, questions: 5, points_each: 2}, {id: main, total: 70, questions: 7, points_each: 10}]` and `gates: [{scope: short-test, min_points: 7, on_fail: zero_exam}]`. `scope: exam` means the raw whole-paper score. A legacy prose `gate` is not permission to ignore it: translate it from evidence before creating a drill. Freeze sections and gates in the drill and key, so later MOC edits cannot change grading. Section totals must sum to the paper total, and question counts and marks must match each section.

A MOC may record `historical_formats` separately. Never use a historical total, clock or question pattern to fill missing current facts, and never combine it with current gates. An explicitly requested historical rehearsal is labelled historical practice (`exam_equivalent: false`) and uses only its own frozen rubric. IZP’s 2024 sample is 54/23; the current 2026/27 card gives 53/25, with clock and detailed pattern unverified.

Default `mode: exam`. If the real clock or detailed format is unknown, explain the gap and offer `mode: practice` with an explicitly chosen clock and generated rubric. Practice can use complete `practice-quiz` questions with unstated marks; label its assigned marks `rubric_source: generated` and omit exam gates. Never present it as a predicted final score. The existing `drill new` request can specify “practice, 30 minutes”; no separate engine is needed.

## New drill — `drill new <COURSE> [whole-paper|practice] [count=N] [minutes=N]`

Default count is one; multiple papers on the same day are supported. An explicit pair chooses the longer solving budget; state review/break time separately and keep the daily default unchanged. For a batch, use `batch_id: COURSE-YYYY-MM-DD-NN`, with separate attempts and a metadata-only `<batch_id>-batch.json` listing their paths and clocks. Preflight source availability for the entire batch before issuing any paper.

`whole-paper` uses one complete FIT source variant per attempt, preserving order, sections, original marks, wording and figures. Consult `paper-inventory.json`: no withheld entry, no silent partial variant, no reweighting, no reserve unless explicitly requested. If there are not enough complete working variants, report the shortage before substituting a different product. IZP's held samples currently contain unresolved defects; do not claim they supply two intact usable finals.

In `practice`, select from `practice-sources.json` and the MOC's `resource_guide` as well as eligible banks. A document-level index is not a ready question bank: inspect, extract and bank the selected exercises with stable source references first. External question sets remain `source: external-practice`, `mode: practice`, `exam_equivalent: false`, with their original clock/marks or explicitly chosen practice values. Never apply FIT gates to MIT or textbook material. Keep solution-bearing pages sealed from the student.

1. **Pick the source.** Read unused, eligible bank entries of the appropriate kind and section. Check paper inventory, all issued attempts and exposure events; exclude reserved variants and questions already allocated to this batch. Repeats require an explicit repeat request and remain labelled. Default adaptive selection applies to assembled drills only, not intact variants. Exclude `eligible: false`, unresolved errata and missing figures. Visually inspect every selected `pdf-required` entry against its source page, reconstructing intact notation and diagrams; never paste a whole page that exposes unselected questions. Reject an entry if it cannot be reproduced accurately. A sample midterm is not a final question pool; practice quizzes are practice only. Original question marks are not rescaled to make a total fit. For an assembled exam-format drill only, insufficient eligible questions → fill declared gaps with original synthetic questions and label `source: mixed`, or `synthetic` if none came from papers; report this limitation without revealing topics. A parse failure is an error, not an empty bank. Preserve source kind and bank ID per question. `source: practice-quiz` is allowed only in practice mode.
2. **For an assembled drill, weight it like the config says — then like your history says.** Most points on `weight: invest` topics, few on `skim`. Read per-question raw `scored/possible` from past results and upweight topics below ~50%; topics recently near full marks lose weight. Keep topic choices in the sealed key, never the reply. Section constraints take priority over weights.
3. **Match the real paper.** In exam mode, match every configured section's question count and point pattern, the total, clock and gates. Show the gate instructions on the paper, without tips or topic labels. Mix recall, analysis and production where the format permits. Record `format_basis` when the pattern comes from a sample rather than a current instruction. A short-test gate must actually be rehearsed, not replaced with a flat 80-point paper.
4. **Allocate an immutable attempt ID.** Use `YYYY-MM-DD-01`, then `-02`, etc., within the course. Scan all drill/key/answer/result filenames and batch manifests, including abandoned or partial attempts; never reuse a number or overwrite any existing file. Reserve an ID with an exclusive-create marker before writing. If a collision occurs, choose the next ID. Build and validate in a temporary directory outside vaults/repos, then publish the three complete files using exclusive creation. A partial failure keeps the ID occupied and is reported; never call it a ready paper. A historical `YYYY-MM-DD-*` attempt stays untouched. The following `<attempt>` means the full ID, not just the date.
   - `<attempt>-drill.md` — questions + point values. Frontmatter: `type: drill`, `course`, `attempt_id`, `batch_id` (null for a single), `mode`, `source`, `created` (ISO timestamp), `total`, `time_min`, `format_basis`, `sections`, `gates`, `exam_equivalent`, `paper_form: intact|assembled`. Copy attempt/batch IDs into all three files. Source identities and exposure detail belong in the sealed key and result, not on a paper where they may reveal topics. The public question map contains only `{n, section, points}`; keep topic labels in the sealed key so they cannot suggest a method. No answers or hints.
   - `<attempt>-key.md` — `type: drill-key`, opening with `> [!danger] Sealed — if you are reading this before you have answered, you are cheating yourself.` Record `questions: [{n, topic, section, points, bank_id, source_kind, rubric_source}]`, every topic verbatim from the MOC. For each question write the answer and a per-question point breakdown. Distinguish supplied official answers from generated answers/rubrics. Independently solve/check a generated key before sealing (compile isolated ungraded C snippets, check algebra/edge cases); if uncertain, replace the question. No student work is written. Store the frozen sections/gates and SHA-256 of the drill in the key; store the key digest in the answer sheet. Copy every required diagram or attachment into an immutable attempt-specific asset directory and record each relative path and SHA-256 in the key's `assets` list. Hashing a Markdown image link does not hash its target. Verify the rendered crops include all labels and contain no unselected questions or solutions. The rubric and assets are fixed now, so grading cannot drift later.
   - `<attempt>-answers.md` — `type: drill-answers`, one empty heading per question; `student_exposure: unknown`, `started_at: null`, `finished_at: null`, `elapsed_min: null`, `conditions: unreported`, and `feedback_before_sitting: false`. The student supplies these facts. Conditions may be `closed-book-timed-unaided`, `open-book`, `assisted`, or `interrupted`. No clock or condition is inferred from file modification time. State `permitted_tools` in the paper and freeze it in the key: an ungraded C practice task may explicitly allow an editor, terminal and compiler. This permission does not authorize AI help. Preserve pre-run predictions separately from later corrections whenever prediction is scored. Such a pack remains practice and is not evidence about a compiler-free exam.
5. **Record issuance.** After all files of an attempt validate, append an `issued` exposure event with its source/bank IDs and attempt ID, then append today's date to each drawn question's legacy `used:` line. An issued paper is occupied even if sitting never occurs. If bookkeeping fails, report and repair before issuing more; scan issued files to prevent duplicates. For a batch, only report it complete when every listed attempt validates.
6. **Reply with paths, clock and source/mode limitation only.** Nothing about its topics or contents. Record generator-session identity when available; otherwise explicitly require a new chat for grading. These are procedural seals, not access control: the owner can still open the files.

## Grading — `drill grade <COURSE> <attempt-id|batch-id>`

Accept historical date-only IDs unchanged. A bare date selects the sole matching attempt only; when several exist, list their IDs and ask which one or the whole batch. Never silently choose or overwrite a result. Batch grading writes one result per attempt and a derived summary; after interruption, skip already graded attempts and resume the others without mutating results.

1. **Check independence, integrity and answers.** Refuse in the creation/teaching session, with altered drill/key hashes, a missing or altered required asset, mismatched course/attempt IDs, an existing result, or if the answer file is missing/every heading empty. Verify every entry of the frozen `assets` list; resolve paths and symlinks before reading. A legacy paper with external figures but no asset hashes needs an integrity review before grading, not an invented assurance. The answer sheet may report student conditions; it cannot replace frozen marks, gates, permitted tools or source identity. Verify session provenance if available; when unknown, ask the student whether this is a fresh session. Do not mistake a different date for a different session. Empty individual answers score zero once any answers exist. Ask for missing exposure/conditions once or retain `unknown`/`unreported`; do not claim an unseen benchmark. Assisted, open-book or interrupted sitting is reported as practice even if the prepared paper had exam format. Keep the original paper/key immutable and record `prepared_mode` separately. Preserve frozen gate diagnostics but exclude such attempts from the comparable exam curve.
2. **Score against the fixed rubric.** Never re-derive points. Award only justified rubric items; apply explanation requirements actually stated by the task, not invented after submission. Calculate `raw_score` as the sum of question scores. In exam mode evaluate each frozen gate: a score strictly below `min_points` fails; exactly the threshold passes. Any `zero_exam` failure sets `score: 0`; otherwise `score: raw_score`. If the sitting is practice because of assistance or conditions, keep `score: raw_score` and store the frozen FIT gate calculation separately as `exam_format_diagnostic_score`; it is not an official or comparable exam mark. External practice has no FIT gate calculation. Keep per-question raw marks for diagnosis. On IDM/ILG, a 6/10 short test and 70/70 main yields raw 76/80, effective 0/80. Main-part diagnostic marks after a failed gate are practice feedback, not an official mark for a paper the examiner would leave unmarked.
3. **Write `<attempt>-result.md`** — per-question notes and one *redo this problem type* line per dropped question, with frontmatter:
   ```yaml
   # Historical-format example; current config must be read independently.
   type: drill-result
   course: IZP
   attempt_id: 2026-09-15-02
   batch_id: IZP-2026-09-15-01
   date: 2026-09-15        # sitting date, when supplied; otherwise creation date with date_basis
   date_basis: student-reported
   created: 2026-09-15T09:00:00+02:00
   started_at: null
   elapsed_min: null
   time_min: 90
   format_basis: historical-sample-final-2024
   student_exposure: unknown
   conditions: unreported
   feedback_before_sitting: false
   paper_form: assembled
   exam_equivalent: false # historical sample, not the current 53-point final
   source_ids: []        # actual stable paper/variant or external exercise IDs
   prepared_mode: practice
   graded: 2026-09-16
   source: past-paper
   mode: practice
   raw_score: 41
   score: 41
   total: 54
   exam_format_diagnostic_score: 41
   gates_passed: true
   gate_results: [{scope: exam, scored: 41, min_points: 23, passed: true}]
   cards_added: 0
   pending_misconceptions: 1
   questions: [{n: 1, topic: pointers, section: final, scored: 2, possible: 4, source_id: IZP:B01, rubric_source: generated}]
   ```
   Topic names verbatim from `exam.topics` — stats joins on them, so an invented name fragments the curve.
4. **Log completion and queue the misconceptions.** Append a completed exposure event after the result exists. If this fails, preserve the result and repair the log before the next issue.  Use the learning contract's own-words gate. Do not add cards from a grading summary or per dropped point automatically. Group repeated errors by concept; ask the student to explain the corrected model before any card exists. The result records cards created at grading time; later cards do not mutate this immutable result.
5. **Report** attempt ID, effective score, raw score if different, gate verdict, exposure, conditions, weakest topic and actual cards/pending counts. For a batch show each paper separately; never average away a failed gate. Offer review through `tutor` and a fresh transfer question, not an automatic answer dump. Question and answer content stays on disk.

## Rules

- **Append only** to flashcard files. Never rewrite existing cards and never touch the HTML scheduling comments the Spaced Repetition plugin appends — deleting them destroys the review intervals, and the damage stays invisible for weeks.
- Grade in a **fresh session**, always. A session that generated or taught the drill cannot grade it.
- A `synthetic` drill can test recall and application, but has not been calibrated to the real exam's style or difficulty. Say so in the result note, and say it again whenever the corpus is still empty.
- **Older drills still grade** with the original rubric. Add canonical topics to the result if the key lacks them. Missing historical gates/hashes mean `mode: legacy-practice`, with the limitation recorded; never invent an exam-equivalent result or retroactively change a key.
- Never edit a past result file — the dataset is append-only, like the flashcards.
- Follow the vault's `CLAUDE.md` conventions if one exists.
