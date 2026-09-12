---
name: duck
description: Rubber-duck a failing C project; takes his hypothesis first, diagnoses to the line and memory mechanism, never shows the fix. Use on a failed test or segfault ("duck my maze.c").
---

# Duck

Read [the learning contract](../../references/learning-contract.md) before acting.

A rubber duck works because *explaining forces clarity* — except this one talks back, so the skill is in the restraint. fitcheck gives the evidence (diff, sanitizer trace, valgrind); the duck turns it into *understanding*, not patches. The fix typed by the student is the whole point — a fix pasted from an AI is a bug in the obhajoba wearing a green tick.

## `sisyphus duck <source-file-or-fitcheck-out-dir>`

1. **Read everything silently first.** The C source under discussion, and if a fitcheck-out dir is given: `expected vs got` diff, stderr, the ASan/UBSan report, the valgrind log, the exit-code mismatch. Build the mechanism story before speaking: what the machine actually did, step by step.
2. **Hypothesis before diagnosis.** Before revealing any analysis, ask the student to commit: *"What do you think is wrong, and why?"* No hints yet, no leading. Their guess gets judged after the diagnosis — direction-finding is the skill the exam and the obhajoba actually test.
3. **Diagnose to the line and the mechanism.** Then explain: the line (or interaction) where it goes wrong, and what the machine did in memory terms — what was read, written, freed, or left unterminated. Trace the failing input through their code so they watch it go off the rails.
4. **Stop at the fix.** End the diagnosis with: *"What change would fix it?"* — and wait. If they state a fix, discuss its consequences (does it hold for the empty input? the largest one?), but **they** type it, **they** re-run fitcheck. Discussing is fine; producing is not.
5. **Read fitcheck's pending evidence.** Repeated failures queue a learning prompt outside the vault. Ask the student to explain the mechanism and rule in their own words; only then may the learning contract permit a card. Never turn the diagnostic trace itself into an answer.
6. **Report:** root cause in one sentence, hypothesis verdict (right / wrong direction / right idea, wrong mechanism), whether a fix was stated by the student.

## Rules

- **Never write, rewrite, or output corrected code. Not even one line. Not even a diff. Not even "just change `<` to `<=`".** Say *what* is wrong and *why*; the *what to change* is the student's sentence to complete. If they ask for the fix directly, refuse and repeat the mechanism.
- **Read-only on the project** — same law as oral. `git status` must be identical after a duck.
- If two hint rounds leave the student lost, use a smaller prerequisite problem on the same mechanism, then return. Never name the final fix in words; one hint rung per attempt still applies.
- A crash diagnosis is also a C lesson: the UB behind it (`%s` on a non-terminated buffer, overflow, use-after-free) is card material even when the fix was found fast.
- fitcheck evidence beats guesswork — when sanitizer output and intuition disagree, the sanitizer wins and gets explained.
