---
name: stats
description: Regenerate a per-course progress note from drill and exam result frontmatter — score curve over time, per-topic breakdown, real-exam rows for the drill-vs-reality comparison. Use for "how am I trending", "sisyphus stats", or after grading a drill.
---

# Stats

Reads **frontmatter only** — never prose — from result files, and regenerates each course's `progress.md`. Everything here is derived data; overwriting it is safe and correct.

## `sisyphus stats [COURSE]`

1. **Discover courses.** Glob the vault's MOC notes for frontmatter containing an `exam:` block; `code:` is the course key. With `[COURSE]` given, do just that one.
2. **Collect results.** In each course's drills dir (default `<Area>/exam-drill/<code>/`, or `exam.drills_dir`), read the frontmatter of every file with `type: drill-result`, `type: exam-result` or `type: oral-result`:
   - `drill-result`: `date, graded, source, score, total, cards_added, questions: [{n, topic, scored, possible}]`
   - `exam-result` (real graded events, recorded by hand): `date, kind: final|midterm, score, total`
   - `oral-result` (mock defenses from `sisyphus oral`): `date, project, passed, score (of 10), stumbles`
   A file that should parse but doesn't goes in the report as a warning with its path — **never silently skip it**; a silently dropped result poisons the trend.
3. **Regenerate `<drills_dir>/progress.md`** (overwrite):
   - Frontmatter: `type: progress`, `course`, `updated`.
   - **Score over time** — one table row per result, drills and real exams interleaved by date: date · score/total · % · source (`past-paper`/`synthetic`/`mixed`, or `**exam: final**` bolded — real exams are the ground truth the drill curve is judged against). Oral results appear as `**oral 7/10**` rows with a ✓/✗ for `passed` — they measure explanation, not recall, so they don't join the score curve.
   - **Per-topic** — summed over all drill `questions:` lists: topic · points scored/possible · % · trend arrow vs. the previous drill that touched the topic. Topics with fewer than ~6 possible points get a "thin data" mark instead of an arrow.
   - A mermaid `xychart-beta` of drill % over time, if there are ≥3 drill points to plot.
   - A one-line read at the top: current trend and weakest topic. Trending down = the study loop is lying somewhere; fix the loop, not the vibe.
4. **Report** per course: one trend line, weakest topic, and any parse warnings.

## Recording real exams

When a real graded event comes back (midterm, final), record it the same day as `<drills_dir>/YYYY-MM-DD-exam.md`:

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
