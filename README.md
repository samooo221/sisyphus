# sisyphus

**An agentic study engine for Obsidian vaults.** Past-paper drills under real exam conditions, hostile grading against the real point split, mistakes revisited through the student's own explanations before any flashcard, and a longitudinal record of whether any of it is working.

There is no app. sisyphus is a [Claude Code](https://claude.com/claude-code) plugin made of prose skills — the agent is the engine, your vault is the database. The vault stores your notes; private corpora store assessment text. Materials an agent reads are processed by whichever model provider you choose; this is not an offline inference engine.

## The loop

```
setup ──▶ harvest ──▶ bank ──▶ drill new ──▶ (you answer, offline, on the clock) ──▶ drill grade ──▶ stats
  │           │         │           │                                                    │             │
exam:    public web  question    sealed paper                                     own-words gate    score curve
block    → corpus     bank       + key + answer sheet                              then cards       vs. real exams

  lecture ──▶ pass-2 notes + cards (daily, sieve courses)     oral ──▶ mock obhajoba on your project (project weeks)
  tutor ──▶ daily Socratic session — hint ladder, never the answer, closes unaided
  duck ──▶ no-fix C diagnosis — your hypothesis first, the mechanism to the line, the fix stays yours
  garden ──▶ weekly interleaved quiz across courses, aimed at your weakest topics
  daily ──▶ the Dawn Raid — a chosen timed block composed from everything due; free-time guard built in
  preview ──▶ pre-lecture prequiz with folded answers + a watch-for list, so lectures land as review
  moonshot ──▶ the past-exam evening: public harvest, then a precise click-list for the login-only archive
  gym ──▶ rest-period recall round — 6–8 short voice-friendly questions, banked after the last set
  factory ──▶ generator seat mass-produces weak-topic problems, a cross-vendor judge vetts them, you solve
  stress ──▶ adversarial explanation check — you explain, an attacker seat attacks, an auditor rules
  intel ──▶ weekly public-only sweep of course/faculty news and cohort reactions (never leaks)
  ambush ──▶ one sealed question about your own project, fired by cron once a week
```

1. **`sisyphus setup <COURSE>`** — one interview; writes an `exam:` block into the course's MOC frontmatter (exam total, time limit, topic weights, optional past-paper directory).
2. **`sisyphus harvest <COURSE>`** — gathers publicly available past papers into the corpus dir from official pages, student archives and GitHub topics (anything behind a login becomes a manual TODO, never bypassed).
3. **`sisyphus bank <COURSE>`** — ingests your own past-paper PDFs into a topic-tagged question bank (kept outside the vault — exam text is copyrighted).
4. **`drill new <COURSE>`** — a sealed, timed, closed-book paper matching the real exam's point split, weighted toward the topics you marked `invest`. The agent never prints a question into chat: files only. Then you answer it offline, real clock, no notes, no AI.
5. **`drill grade <COURSE> <attempt-id|batch-id>`** — in a fresh session (the one that wrote the key can't invigilate), graded hostilely against a point breakdown fixed at creation time. Misconceptions enter a review queue; cards are appended only after your own correct explanation.
6. **`sisyphus lecture <COURSE> <note> [slides.pdf]`** — the daily pass-2: answers your `> [!question]` cues, drafts atomic concept notes, and writes cards only after you've rewritten each note's core in your own words.
7. **`sisyphus oral <COURSE> <project-dir>`** — a mock obhajoba: reads your submitted project and cross-examines you one question at a time, ending in a verdict file; stumbles await your own explanation before becoming cards. Read-only on your code, always.
8. **`sisyphus stats`** — score curve over time and per-topic breakdown, computed from result frontmatter, with your real exam results and oral verdicts interleaved.
9. **`sisyphus tutor <COURSE> [topic]`** — the daily teaching session: retrieval warmup from the deck, problems worked on a hint ladder (one rung per attempt), and a mandatory closing problem solved completely unaided. Confusions await your own explanation before becoming cards. The tutor never states the answer — see the rules below.
10. **`sisyphus duck <file|fitcheck-out-dir>`** — rubber-duck debugging for C: reads your code and the fitcheck evidence, takes your hypothesis *first*, then diagnoses to the line and the memory mechanism. It never writes the fix — you type it, you re-run fitcheck.
11. **`sisyphus garden [COURSE ...]`** — the weekly 15-minute interleaved quiz: questions rotate across courses and problem types, aimed at the topics where your drill results are weakest. No quiz result is archived; misconceptions pass through the own-words gate.
12. **`sisyphus daily`** — a 90-minute default with substantial question practice. Verified commitments constrain the plan; example slots do not. An explicit longer block or paper pair overrides the budget for that session. No automatic extension and no daily paper-count limit.
13. **`sisyphus preview <COURSE> [slides.pdf]`** — a 10-question prequiz with folded answers and a "watch for" list, written the evening before a lecture. Pretesting before instruction makes the lecture stick; preview questions never become cards directly.
14. **`sisyphus moonshot <COURSE>`** — the past-exam acquisition evening: `harvest` takes the public papers, then you get a numbered click-list for everything behind the faculty login (your browser, your hands — nothing bypassed). Corpus coverage drives drill quality; gaps are tracked, never silent.
15. **`sisyphus gym [COURSE]`** — the rest-period recall round: 6–8 short questions from the due cards and the weakest topic, graded in three characters between sets, drops banked after the workout. Dead air in, retention out.
16. **`sisyphus factory <COURSE> [topic] [count]`** — checked variations, existing author exercises or simulators for extra volume. Generated keys need independent verification; model routes are used only when available and authorized.
17. **`sisyphus stress <COURSE> <topic>`** — adversarial explanation check: you explain closed-book, an attacker seat finds the holes, you defend, an auditor seat rules on fairness. Broken defenses enter the own-words queue.
18. **`sisyphus intel [COURSE ...]`** — the weekly public-only intel sweep: official course news, faculty calendar changes, cohort reactions. Leaked assessment content is dropped and named as dropped.
19. **`sisyphus ambush <COURSE> <project>`** — seals a 10-question pool about your own code; a weekly cron (Wednesday ~17:07) fires exactly one. Random-timing retrieval, tiny blast radius, ignorable by design.

## Install

In Claude Code:

```
/plugin marketplace add samooo221/sisyphus
/plugin install sisyphus@sisyphus
```

For a local checkout, the installed Claude Code CLI also supports:

```sh
claude plugin marketplace add ~/vutsamko/sisyphus
claude plugin install sisyphus@sisyphus --scope user
claude plugin details sisyphus@sisyphus
```

Start a fresh Claude Code session after installation. Skills appear as
`/sisyphus:bank IDM`, `/sisyphus:tutor IZP`, `/sisyphus:drill new ILG`, etc.
The natural-language requests below refer to those prose skills, not shell executables.
After changing the source checkout, update the installed plugin and verify its cached
skill files; do not assume an old cache automatically follows local edits.

Requirements: an Obsidian vault (any layout — see below) and the [Spaced Repetition](https://github.com/st3v3nmw/obsidian-spaced-repetition) plugin for the flashcard half of the loop.

## Paper practice and the resource library

In a fresh Claude Code session, examples are:

```text
/sisyphus:daily
/sisyphus:tutor IZP
/sisyphus:drill new ILG whole-paper count=2
/sisyphus:drill new IEL practice minutes=45
/sisyphus:bank ILG hefferon chapter 2
/sisyphus:drill grade ILG <attempt-id-or-batch-id>
```

Two 120-minute maths papers mean 240 minutes of solving, plus any break and
review you choose. Each has its own sealed key, answer sheet and result. IDs
`YYYY-MM-DD-01`, `-02`, etc. prevent same-day overwrites; old date-only attempts
remain valid. These are prose-skill arguments, not a new command-line program.

`resource_guide` in each course MOC points to a source map; `practice-sources.json`
indexes external documents for selected exercise intake. Sources and keys stay
outside the vault and repositories. Two IDM and two ILG variants are initially
reserved for later checks, with student exposure recorded as unknown until
confirmed. Full rules: [paper practice](references/paper-practice.md).

## Vault layout

sisyphus assumes one folder per subject area, with `MOCs/` and `Flashcards/` inside — and derives everything else:

```
YourVault/
  University/                    ← "area"
    MOCs/IZP — Programming.md    ← course MOC, carries the exam: block
    Flashcards/IZP — flashcards.md
PrivateCorpus/IZP/               ← outside the vault and every repository
  question-bank.md
  drills/                       ← sealed papers, keys, answers, results, progress.md
```

The corpus and drills must resolve outside the vault and every repo, including through symlinks. `drills_dir` defaults to `<corpus>/drills`; `flashcards` defaults to the existing area deck. `setup` records the paths in the MOC.

## Schema reference

The schemas are the contract between the skills — `drill` writes what `stats` reads. Copied verbatim inside the relevant SKILL.md files; this is the human-readable reference.

### `exam:` block (course MOC frontmatter)

The example below uses the historical IZP sample. Current 2026/27 IZP is 53 points with a 25-point gate; its clock and detailed pattern are unverified. Read the actual MOC. Never combine historical totals with current gates or use old clocks to fill unknown current ones.

```yaml
code: IZP                        # course key (top-level, house-style field)
exam:
  final_total: 54                # required — drill point values sum to this
  time_min: 90                   # real exam clock; null when unverified
  time_status: verified
  corpus: ~/data/fit-exams/IZP   # private source directory, even for synthetic drills
  topics:                        # required — canonical names; every skill joins on them
    - {name: pointers, weight: invest}
    - {name: control-flow, weight: skim}
    - {name: functions}          # weight defaults to normal
  test_terms: []                 # populate only verified dates; stats emits a 72h danger list
  sections:
    - {id: final, total: 54, questions: 8, question_points: [6, 8, 6, 8, 10, 6, 4, 6]}
  gates:
    - {scope: exam, min_points: 23, on_fail: zero_exam}
  drills_dir:                    # optional override; default <corpus>/drills
  flashcards:                    # optional override; default <Area>/Flashcards/<code> — flashcards.md
```

> ⚠️ Obsidian's Properties panel mangles nested YAML — edit the `exam:` block in source mode.

For IDM/ILG, use a 10-point `short-test` section (5 × 2), a 70-point
`main` section (7 × 10), and a gate with `scope: short-test, min_points: 7,
on_fail: zero_exam`. A 6/10 short test makes the effective exam score zero,
even with full raw marks on the main section. Freeze these rules in each drill.
Semester credit requirements are separate MOC data, never inferred student grades.

A MOC may point `study_track` at an existing prerequisite plan. The tutor begins
at the first stage without unaided evidence, independently of exam topic weights.
Unknown clocks/formats require a labelled practice session with a chosen clock.
Practice-quiz questions with unstated points get a generated practice rubric,
never invented official marks. See [drill](skills/drill/SKILL.md) and
[bank](skills/bank/SKILL.md) for the complete contracts.

### Drill result (written by `drill grade`)

Schema example using the historical sample as practice.

```yaml
type: drill-result
course: IZP
attempt_id: 2026-09-15-02
batch_id: null
date: 2026-09-15                 # sitting date if supplied
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
exam_equivalent: false
source_ids: []                  # fill from actual selected items
prepared_mode: practice
graded: 2026-09-16
source: past-paper               # past-paper | synthetic | mixed
mode: practice
raw_score: 41
score: 41
total: 54
exam_format_diagnostic_score: 41
gates_passed: true
gate_results: [{scope: exam, scored: 41, min_points: 23, passed: true}]
cards_added: 0
pending_misconceptions: 1
questions: [{n: 1, topic: pointers, section: final, scored: 2, possible: 4, source_id: IZP:B01, rubric_source: generated}] # abbreviated
```

`stats` reads frontmatter, uses effective scores only for comparable exam curves and raw question marks for diagnosis. Unknown exposure/conditions, different clocks and repeated papers remain separate rows; a batch average cannot hide a failed gate. Practice, legacy and exam modes remain distinct. Topic labels live in the sealed key and result, not on the unanswered paper.

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

- **Question practice throughout the week.** Use focused exercises while learning, then interleave methods. Once prerequisites are ready, use complete papers for rehearsal; one or two consecutively when chosen. There is no monthly or same-day ceiling. Reserve a few untouched FIT variants, using external material for extra volume. Fewer than three comparable results means no score curve.
- **Run an `oral` when a project is submission-ready**, and once more before the real defense — the second one measures whether the first one's cards stuck.
- **Record every real graded event** (midterm, final) as an `exam-result` file the day you get it.
- **Result files and flashcards are append-only, forever.** Never edit a past result; never touch the HTML scheduling comments Spaced Repetition appends to cards.
- Grade in a **fresh session** — the session that generated a drill has the key in context and cannot invigilate it.

## Rules that keep it honest

- **The no-print rule.** A drill you have already read is not a drill. Questions, answers, and topic lists go to disk, never into chat.
- **The key is fixed at creation.** Per-question point breakdowns are written into the sealed key when the drill is built; grading follows them and never re-derives — so the grader can't drift lenient or hostile across a semester.
- **Grade the stated rubric.** Require working where the question or frozen rubric requires it; do not invent explanation penalties after submission.
- **Synthetic drills carry a disclaimer.** Generated-from-topics drills can test recall and application; their style and difficulty are not calibrated against a real paper.
- **No automatic cards from any command.** Rewrite the concept yourself first; approval alone does not pass the gate. The [learning contract](references/learning-contract.md) also covers fitcheck, quizzes and grading.
- **The tutor never states the answer.** This is load-bearing, not style: students practising with an unrestricted GPT tutor scored ~17% *worse* on a later exam with the AI removed, while a never-gives-answers tutor more than doubled classroom learning gains (Bastani et al., PNAS 2025; Kestin et al., Sci. Reports 2025). Hints go up a ladder, one rung per attempt; the student states every answer; sessions end with an unaided check.
- **Hypothesis before diagnosis, diagnosis before fix.** `duck` takes your committed guess before it speaks (calibration you can't skip), explains the mechanism, then stops — the corrected line is yours to find and type.
- **The garden mixes courses on purpose.** Interleaving trains *picking the method*, which blocked practice never tests — 61% vs 38% on a delayed test across 54 classrooms (Rohrer et al.). Consecutive questions from the same course would defeat it.
- **90 minutes is the default, and you may choose longer.** Without an explicit extension, trim the brief to fit. A request for two full papers chooses their combined solving time; show breaks and review separately. Keep real commitments and prerequisite gates. Placeholder slots never block study.
- **Previews prime, they don't teach.** Prequiz questions stay out of the deck; if one still matters after the lecture, it becomes a card through the normal gates — otherwise pretesting would smuggle un-earned cards into the schedule.
- **Factory keys are checked independently.** Use an authorized independent solver or a suitable deterministic check; unresolved items are withheld. No assumed model route or paid fallback.
- **Intel takes reactions, never leaks.** Cohort "that test hit RC hard" is signal; the test's actual questions are contraband — dropped and named, because the drill loop is the only legitimate way to know what tests look like.
- **The ambush stays one question a week.** Random-timing retrieval works at trivial cost; scaled up it becomes noise you learn to ignore, which kills the mechanism it relies on.

## Status

Local v0.2.5 preparation, 12 September 2026: all ten first-year FIT courses have
curated resource guides and private searchable sources. Winter FIT banks retain
400 indexed items, 397 eligible candidates (selected PDF questions still require visual checks). A separate opening collection now has 48 checked external questions and 24 independently checked original C questions, issued as 12 short practice packs. Other external document indexes are not claims of
question-level banking. Multiple same-day papers, whole variants, repeat/exposure
records and chosen longer sessions are specified. See the local
[resource library](/home/tryhardstation/vutsamko/fit-study/resources/README.md).
The [opening practice guide](/home/tryhardstation/vutsamko/fit-study/first-week-2026-09-12/README.md) lists the packs and their prerequisite order. Sealed keys now freeze the hashes of separate diagram assets and permitted tools. A pending or failed tutor check leaves the stage pending without erasing demonstrated progress.
These are agent procedures, not access controls or evidence of student mastery.
No new student sitting or live grading has been demonstrated.

## License

MIT
