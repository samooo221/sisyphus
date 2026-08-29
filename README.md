# sisyphus

**An agentic study engine for Obsidian vaults.** Past-paper drills under real exam conditions, hostile grading against the real point split, every dropped point turned into a spaced-repetition flashcard, and a longitudinal record of whether any of it is working.

There is no app. sisyphus is a [Claude Code](https://claude.com/claude-code) plugin made of prose skills — the agent is the engine, your vault is the database. Your data never leaves your disk in any format you didn't write yourself.

## The loop

```
setup ──▶ harvest ──▶ bank ──▶ drill new ──▶ (you answer, offline, on the clock) ──▶ drill grade ──▶ stats
  │           │         │           │                                                    │             │
exam:    public web  question    sealed paper                                     mistakes become   score curve
block    → corpus     bank       + key + answer sheet                              flashcards      vs. real exams

  lecture ──▶ pass-2 notes + cards (daily, sieve courses)     oral ──▶ mock obhajoba on your project (project weeks)
```

1. **`sisyphus setup <COURSE>`** — one interview; writes an `exam:` block into the course's MOC frontmatter (exam total, time limit, topic weights, optional past-paper directory).
2. **`sisyphus harvest <COURSE>`** — gathers publicly available past papers into the corpus dir from official pages, student archives and GitHub topics (anything behind a login becomes a manual TODO, never bypassed).
3. **`sisyphus bank <COURSE>`** — ingests your own past-paper PDFs into a topic-tagged question bank (kept outside the vault — exam text is copyrighted).
4. **`drill new <COURSE>`** — a sealed, timed, closed-book paper matching the real exam's point split, weighted toward the topics you marked `invest`. The agent never prints a question into chat: files only. Then you answer it offline, real clock, no notes, no AI.
5. **`drill grade <COURSE> <date>`** — in a fresh session (the one that wrote the key can't invigilate), graded hostilely against a point breakdown fixed at creation time. Every dropped point becomes one atomic flashcard for Obsidian's Spaced Repetition plugin.
6. **`sisyphus lecture <COURSE> <note> [slides.pdf]`** — the daily pass-2: answers your `> [!question]` cues, drafts atomic concept notes, and writes cards only after you've rewritten each note's core in your own words.
7. **`sisyphus oral <COURSE> <project-dir>`** — a mock obhajoba: reads your submitted project and cross-examines you one question at a time, ending in a verdict file; every stumble becomes a card. Read-only on your code, always.
8. **`sisyphus stats`** — score curve over time and per-topic breakdown, computed from result frontmatter, with your real exam results and oral verdicts interleaved.

## Install

In Claude Code:

```
/plugin marketplace add samooo221/sisyphus
/plugin install sisyphus@sisyphus
```

Requirements: an Obsidian vault (any layout — see below) and the [Spaced Repetition](https://github.com/st3v3nmw/obsidian-spaced-repetition) plugin for the flashcard half of the loop.

## Vault layout

sisyphus assumes one folder per subject area, with `MOCs/` and `Flashcards/` inside — and derives everything else:

```
YourVault/
  University/                    ← "area"
    MOCs/IZP — Programming.md    ← course MOC, carries the exam: block
    Flashcards/IZP — flashcards.md
    exam-drill/IZP/              ← drills, keys, answers, results, progress.md
```

Different layout? Two optional overrides in the `exam:` block (`drills_dir`, `flashcards`) cover it. `setup` scaffolds all of this for a bare vault.

## Schema reference

The schemas are the contract between the skills — `drill` writes what `stats` reads. Copied verbatim inside the relevant SKILL.md files; this is the human-readable reference.

### `exam:` block (course MOC frontmatter)

```yaml
code: IZP                        # course key (top-level, house-style field)
exam:
  final_total: 54                # required — drill point values sum to this
  time_min: 90                   # required — the real exam clock
  corpus: ~/data/exams/IZP       # optional — past-paper PDFs + question-bank.md; absent → synthetic drills
  topics:                        # required — canonical names; every skill joins on them
    - {name: pointers, weight: invest}
    - {name: control-flow, weight: skim}
    - {name: functions}          # weight defaults to normal
  drills_dir:                    # optional override; default <Area>/exam-drill/<code>/
  flashcards:                    # optional override; default <Area>/Flashcards/<code> — flashcards.md
```

> ⚠️ Obsidian's Properties panel mangles nested YAML — edit the `exam:` block in source mode.

### Drill result (written by `drill grade`)

```yaml
type: drill-result
course: IZP
date: 2026-09-15                 # drill date
graded: 2026-09-16
source: past-paper               # past-paper | synthetic | mixed
score: 41
total: 54
cards_added: 6
questions: [{n: 1, topic: pointers, scored: 2, possible: 4}]
```

Per-question topic tags only — no stored aggregates; anything derivable is derived. `stats` never reads prose.

### Oral verdict (written by `sisyphus oral`)

```yaml
type: oral-result
course: IZP
date: 2026-10-20
project: ~/school/izp/project2
passed: true               # would this survive the real obhajoba?
score: 7                   # of 10
questions_asked: 9
stumbles: 2
```

Lives in the drills dir like the other results. Orals measure *explanation*, not recall, so `stats` lists them alongside the curve without folding them into it.

### Real exam result (written by you, same day you get the grade)

```yaml
type: exam-result
course: IZP
date: 2027-01-14
kind: final                      # final | midterm
score: 44
total: 54
```

Lives in the same drills dir; picked up by the same glob. This is the ground-truth column.

## Data protocol

Follow this and, at semester's end, "is the tool working?" is a read-and-plot job:

- **One drill per course every two weeks** once term starts. Fewer than ~6 result points per course makes the curve noise.
- **Run an `oral` when a project is submission-ready**, and once more before the real defense — the second one measures whether the first one's cards stuck.
- **Record every real graded event** (midterm, final) as an `exam-result` file the day you get it.
- **Result files and flashcards are append-only, forever.** Never edit a past result; never touch the HTML scheduling comments Spaced Repetition appends to cards.
- Grade in a **fresh session** — the session that generated a drill has the key in context and cannot invigilate it.

## Rules that keep it honest

- **The no-print rule.** A drill you have already read is not a drill. Questions, answers, and topic lists go to disk, never into chat.
- **The key is fixed at creation.** Per-question point breakdowns are written into the sealed key when the drill is built; grading follows them and never re-derives — so the grader can't drift lenient or hostile across a semester.
- **Unjustified answers score zero**, even when the conclusion is right.
- **Synthetic drills carry a disclaimer.** Generated-from-topics drills test recall of what you studied; they don't predict the real paper's style.
- **Lecture drafts don't become cards on their own.** The own-words gate — you rewrite or approve each note's core before its cards are written — is what keeps the deck yours instead of the model's.

## Status

Built July 2026. In daily dogfooding for five VUT FIT (Brno) first-year courses (IZP, IDM, ILG, IEL, IUS) from September 2026; the past-paper path has been exercised only on mock PDFs until real corpora exist. Schemas are stable — the semester's dataset depends on them. Issues and PRs welcome.

## License

MIT
