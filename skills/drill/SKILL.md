---
name: drill
description: Build and grade timed closed-book exam drills for any course with an `exam:` block in its MOC — questions from the course's question bank (or synthetic from its topic list), graded against the real point split, with every dropped point appended as a flashcard. Use for a monthly checkpoint or exam practice ("new drill", "drill me on IZP", "grade my drill").
---

# Drill

**Never print a question, an answer, or a topic list into the chat. Everything goes to disk; the reply is file paths only.** A drill you have already read is not a drill.

## Course config

Find the course's MOC: a note with `type: moc` frontmatter (usually under a `MOCs/` folder) whose `code:` matches the course. Its `exam:` block is the single source of course facts:

```yaml
exam:
  final_total: 54            # required — drill point values sum to this
  time_min: 90               # required — the real exam clock
  corpus: ~/data/exams/IZP   # optional — dir of past-paper PDFs + question-bank.md
  topics:                    # required — canonical topic names; weight: invest|normal|skim (default normal)
    - {name: pointers, weight: invest}
    - {name: control-flow, weight: skim}
  drills_dir:                # optional — default <Area>/exam-drill/<code>/
  flashcards:                # optional — default <Area>/Flashcards/<code> — flashcards.md
```

`<Area>` is the folder above the MOC's `MOCs/` directory (e.g. `University/`). No `exam:` block → stop and point at `sisyphus setup <COURSE>`; never guess course facts.

## New drill — `drill new <COURSE>`

1. **Pick the source.** If `exam.corpus` is set and `<corpus>/question-bank.md` has questions without a `used:` date, draw from those (`source: past-paper`). Otherwise generate from `exam.topics` (`source: synthetic`). Some of each → `source: mixed`.
2. **Weight it like the config says.** Most points on `weight: invest` topics, few on `skim`.
3. **Match the real paper.** Point values sum to `final_total`. Mix recall, read-and-analyze ("what does this print / where does this proof break"), and at least one produce-something question (write the code, the full proof, the worked computation — whatever the course grades).
4. **Write three files** to the drills dir, dated `YYYY-MM-DD`. If `<date>-drill.md` already exists, refuse — one drill per course per day; overwriting would destroy an answered paper.
   - `<date>-drill.md` — questions + point values. Frontmatter: `type: drill`, `course`, `source`, `created`, `total`, `time_min`, and the machine-readable map `questions: [{n: 1, topic: pointers, points: 4}, ...]` — every `topic` verbatim from `exam.topics`. No answers, no hints.
   - `<date>-key.md` — `type: drill-key`, opening with `> [!danger] Sealed — if you are reading this before you have answered, you are cheating yourself.` For every question: the answer **and a per-question point breakdown** (what earns each point). Grading follows this breakdown; it is fixed now so the grader can't drift later.
   - `<date>-answers.md` — `type: drill-answers`, one empty heading per question.
5. **Mark bank questions used.** Append today's date to the `used:` line of each bank question drawn.
6. **Reply with paths and the clock** (`time_min`). Nothing about what's on it.

## Grading — `drill grade <COURSE> <date>`

1. **Refuse if unanswered.** `<date>-answers.md` missing or every heading empty → say so and stop.
2. **Score each question against the key's point breakdown** — never re-derive points. Be a hostile examiner: unjustified answers score zero even when the conclusion is right; partial credit only where the breakdown provides it.
3. **Write `<date>-result.md`** — per-question notes and one *redo this problem type* line per dropped question, with frontmatter:
   ```yaml
   type: drill-result
   course: IZP
   date: 2026-09-15        # drill date
   graded: 2026-09-16
   source: past-paper
   score: 41
   total: 54
   cards_added: 6
   questions: [{n: 1, topic: pointers, scored: 2, possible: 4}]
   ```
   Topic names verbatim from `exam.topics` — stats joins on them, so an invented name fragments the curve.
4. **Turn pain into cards.** For every dropped point, **append** one atomic `- Q::A` bullet to the flashcards file, under a `## From drills` heading. One fact per card — never "list the 5 steps".
5. **Report** 3 lines: score, weakest topic, how many cards were added.

## Rules

- **Append only** to flashcard files. Never rewrite existing cards and never touch the HTML scheduling comments the Spaced Repetition plugin appends — deleting them destroys the review intervals, and the damage stays invisible for weeks.
- Grade in a **fresh session** where possible. A session that generated the drill has the key in context and cannot invigilate it.
- A `synthetic` drill tests recall of what you studied; it does **not** predict the real exam's style or difficulty. Say so in the result note, and say it again whenever the corpus is still empty.
- **Older drills without a `questions:` list still grade.** Assign each question a topic from `exam.topics` while grading and emit the full result frontmatter above anyway.
- Never edit a past result file — the dataset is append-only, like the flashcards.
- Follow the vault's `CLAUDE.md` conventions if one exists.
