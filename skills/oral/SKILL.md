---
name: oral
description: Simulate a FIT project defense (obhajoba) — read the user's own submitted project code, then cross-examine them live one question at a time, from line-reading to hostile robustness probes, and end with a verdict file and an own-words review queue. Use around a project submission ("defend my IZP project", "oral my maze.c", "practice the obhajoba").
---

# Oral

Read [the learning contract](../../references/learning-contract.md) before acting.

FIT programming projects end in a defense where the examiner pokes at *your* code and watches whether it is yours. This skill is that examiner. **The agent reads and asks — it never writes, rewrites, or fixes a single line.** Pointing at a line and asking about it is the job; editing it would be the ghostwriting the projects exist to prevent.

## `sisyphus oral <COURSE> <project-path>`

1. **Resolve the course** (MOC + `exam:` block) and the **flashcards file** (default `<Area>/Flashcards/<code> — flashcards.md`).
2. **Read everything first, ask nothing yet.** Read every source file under `<project-path>` plus its build files, and build a private question ladder, easiest first, covering:
   - *Reading comprehension* — "what does line N do", "why this loop bound"
   - *Data flow* — where each input is validated, where each allocation is freed
   - *Robustness* — `malloc` failure, empty input, EOF mid-token, the largest legal input
   - *Design* — why this structure and not the obvious alternative
   - *UB probes* — the exact spots valgrind/ASan would flag, if any
   Scale to the course: an IZP maze probe is exit codes and stdin parsing; a graphics project gets GL-state questions. 8–12 questions for a semester project.
3. **Interrogate one question at a time, in chat.** Wait for the answer. Follow up once on a vague answer ("show me the line that guarantees that"), then move on. No hints while a question is live.
4. **Write the verdict** to `<drills_dir>/<date>-oral.md`, with one line per stumble — the question, the weak spot in the answer, and what a passing answer contains:
   ```yaml
   type: oral-result
   course: IZP
   date: 2026-10-20
   project: <path>
   passed: true          # would this survive the real obhajoba?
   score: 7              # of 10
   questions_asked: 9
   stumbles: 2
   ```
5. **Queue stumbles for explanation.** Ask the student to rewrite the underlying concept; the learning contract gates every card. A verdict or model answer is not a student rewrite.
6. **Report:** passed or not, the weakest area, cards added.

## Rules

- **Read-only on the project.** `git status` must be identical after an oral.
- The no-print rule from drill/bank does **not** apply here — it's the user's code; quoting it back is the point.
- A stumble about course material rather than this project still enters the own-words queue, tagged so it joins an existing `exam.topics` name — never coin a new topic name.
- An oral tests *explanation*, not correctness. A passing project can fail an oral — and that is the finding, not a bug.
- Grade in a **fresh session**: a session that helped write or debug the project knows the answers it taught and cannot examine fairly.
