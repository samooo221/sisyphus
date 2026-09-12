---
name: ambush
description: Seal a pool of one-line project questions so the weekly cron ambush can fire one at him at a random-feeling moment — random-timing retrieval on his own submitted code. Use when a project is near submission ("ambush pool for my maze.c", "sisyphus ambush IZP <project-dir>").
---

# Ambush pool

Read [the learning contract](../../references/learning-contract.md) before acting.

Random-timing retrieval is expanding-interval spacing wearing a horror mask: a question
about *your own code*, arriving unannounced, forces re-retrieval without a study cue.
The blast radius is deliberately tiny — **one question a week** — and this skill is
just the armory: a sealed pool the cron session draws from.

## `sisyphus ambush <COURSE> <project-path>`

1. **Read the project** (read-only — same law as oral; `git status` identical after)
   and build **10 one-line questions** with their answers: the reading-comprehension
   and robustness picks from the oral ladder (loop bounds, malloc checks, EOF paths,
   exit codes), each answerable in one sentence. No multi-part questions — the ambush
   has one exchange, not a session.
2. **Write the pool** to `<drills_dir>/ambush-pool.md`:
   ```markdown
   ---
   type: ambush-pool
   course: IZP
   project: <path>
   created: <date>
   ---
   - Q1:: <question> ｜ A: <one-line answer> ｜ used: never
   - Q2:: …
   ```
   One line per entry, `used:` flipped to the date by whoever fires it. Overwrite the
   file only with his say-so — an existing pool may still have live rounds.
3. **Report:** pool path, 10 questions sealed, and the one-liner: the weekly cron fires
   Wednesdays ~17:07 and asks exactly one of these.
4. **Optional second pool** before the real obhajoba: regenerate against the *submitted*
   version — whether the first pool's answers stuck is the same measurement orals use.

## Rules

- **Read-only on the project**, like oral and duck.
- Questions must be answerable from *his own code and the course material* — no trivia
  about C standard paragraph numbers; the ambush tests ownership, not pedantry.
- The cron does the firing; this skill never asks the questions itself in-session
  (surprise is the mechanism, and he has already seen the pool file path — told, not shown).
- Pool exhausted (all `used:`) → the cron says "pool empty, run `sisyphus ambush` again"
  in one line and stops. No improvising questions from nothing.
