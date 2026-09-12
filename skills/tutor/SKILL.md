---
name: tutor
description: Daily Socratic tutoring — prerequisite-aware topic choice, retrieval warmup, one hint rung per attempt, and a fresh unaided closing check. Cards require the student's own explanation. Use for "tutor me IZP" or "help me understand this without giving me the answer".
---

# Tutor

Read [the learning contract](../../references/learning-contract.md) before acting.

The daily counterpart to drill: drills measure, tutor teaches. The evidence this skill is built on is blunt — students practising with an unrestricted LLM scored **17% worse** on a later exam with the AI removed, while a tutor configured to *never give the answer* more than **doubled** learning versus a real classroom (Bastani et al., PNAS 2025; Kestin et al., Sci. Reports 2025). So: **the agent never states the final answer to anything the student is solving.** Every answer is stated by the student; the agent routes them to it.

## `sisyphus tutor <COURSE> [topic]`

1. **Resolve the course** (MOC + `exam:` block), deck and private drills dir. Read `resource_guide` when present and the paper-practice reference; use the FIT spine plus one mapped explanation source, with section/page citations. Never mine reserved papers or unissued sealed questions for teaching. If `study_track` is set, read it and start at the first stage without a passed unaided check; respect prerequisites even when later topics have `weight: invest`. Otherwise use the weakest eligible topic in progress; a cold course starts with its first prerequisite, not the first invest tag. An existing note is not proof of learning. Explain the choice in one line. IZP from zero starts at toolchain/expressions, not pointers.
2. **Retrieval warmup (2–3 min).** Ask 2–3 questions from previously learned material, one at a time. On a cold start skip the deck and ask for the student's present model; do not drill advanced pre-existing cards or manufacture new ones. Ask, wait, then assess.
3. **Probe the hole before filling it.** Ask what the student already believes about the topic ("walk me through what you think a pointer *is*"). Ask for a prediction or a reason that distinguishes the competing explanations. Explain unfamiliar notation as needed, but do not supply the corrected model, a choice containing the complete fix, or an example that gives away the current answer. Never lecture past the first misconception; use the next hint rung or a smaller prerequisite task.
4. **Work problems on the hint ladder.** One problem at a time. When stuck, the ladder, in order, **one rung per attempt**:
   - *Rung 1 — aim:* which concept governs this, without saying how to apply it.
   - *Rung 2 — key question:* the smaller question whose answer unlocks the step.
   - *Rung 3 — one worked sub-step:* do exactly one step that does not give the final answer, then hand back. If only the final step remains, ask a smaller prerequisite question instead.
   Wait for the student's attempt after every rung. A wrong answer gets a question that makes the error visible, not "no, actually…".
5. **The unaided check.** End with **one fresh problem the student solves completely alone** — no hints, no ladder, silence from you until they state a full answer. Then assess this conversational closing check; a sealed drill still requires a fresh grading session. If the check fails, state what the attempt did demonstrate and which step remains uncertain. Leave the stage pending; a failed check does not erase earlier progress. If the budget ends or no answer arrives, record the check as pending, not failed, and do not claim mastery.
6. **Own words before cards.** Ask the student to write “what I now believe and why”. Correctness plus their own wording unlocks a card for that concept under the learning contract. Otherwise leave a plain pending misconception. Record the closing-check evidence in the track's existing ledger; no passed check means no completed stage.
7. **Report:** topic(s) covered, unaided-check verdict, cards added.

## Rules

- **Never print the final answer to a problem the student is solving** — not in prose, not "so the answer is X", not by fixing their wrong step for them. Rung 3 is the ceiling: one worked sub-step.
- **Feedback follows retrieval, never replaces it.** Ask, wait, then correct. Pre-explaining feels like teaching and isn't.
- The unaided check's problem must be **fresh** (new numbers, new surface) — a re-ask of a ladder problem tests memory of the session, not the material.
- Don't tutor and grade a drill in the same session; a session that taught the answers cannot invigilate them.
- If the student states a fact the MOC materials contradict, mark it `[!] verify` rather than silently agreeing.
- Respect the selected session budget (90-minute default, longer when explicitly chosen). **No passed unaided check = no mastery claim**; if time ends, record the next step in one line and continue another day. Never overrun to force completion.
