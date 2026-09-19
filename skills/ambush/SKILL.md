---
name: ambush
description: Seal a pool of one-line questions on his submitted project code for the weekly random-timing ambush. Use near a project submission ("ambush pool for my maze.c").
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
3. **Report:** pool path, 10 questions sealed, and **whether anything is actually set up
   to fire them.** The plugin installs no scheduler; the weekly round comes from the
   user's own cron or timer, outside sisyphus. Check for one and say what you found:
   "your weekly job will draw one of these" if it exists, or "no scheduler found — the
   pool is armed but nothing will fire it until you add one" if it does not. Never
   promise a Wednesday delivery the repo does not provide.
4. **Optional second pool** before the real obhajoba: regenerate against the *submitted*
   version — whether the first pool's answers stuck is the same measurement orals use.

## Rules

- **Read-only on the project**, like oral and duck.
- Questions must be answerable from *his own code and the course material* — no trivia
  about C standard paragraph numbers; the ambush tests ownership, not pedantry.
- The scheduled round does the firing; this skill never asks the questions itself in-session
  (surprise is the mechanism, and he has already seen the pool file path — told, not shown).
- Pool exhausted (all `used:`) → the round says "pool empty, run `sisyphus ambush` again"
  in one line and stops. No improvising questions from nothing.
- **A fired round creates no card.** It may mark the entry `used:` and tell him where his
  answer was thin; the own-words gate in the [learning contract](../../references/learning-contract.md)
  applies here exactly as everywhere else, and "no automatic cards from any command" has no
  ambush exception. Any external script that cards a stumble directly is breaking this rule,
  not implementing it.
- **Ambush outcomes are deliberately not recorded.** There is no result file and no schema:
  one question a week is meant to be ignorable, and `stats` does not see it. If you want it
  measured, that is a design change, not a missing feature — the pool file's `used:` dates
  are the only trace by choice.
