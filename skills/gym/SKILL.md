---
name: gym
description: Rest-interval recall round for the gym; 6–8 short voice-friendly questions from due cards and the weakest topic. Use before or during a workout ("gym round IZP").
---

# Gym

Read [the learning contract](../../references/learning-contract.md) before acting.

Dead air between sets is the cheapest study time you own — and acute exercise around
practice measurably helps consolidation, so this is stacking, not compromise. The
constraint that makes it work is **voice format**: short questions, one-line answers,
no walls of text. Voice mode loses the thread in long sessions, so this round is hard-capped.

## `sisyphus gym [COURSE]`

1. **Build the round (before the first set).** 6–8 questions, drawn first from due cards
   (same scheduling-comment parsing as the `daily` skill) and topped up from the weakest
   topic of the named course (or from `stats` if none named). Prefer one-word/one-line
   recall over computation — nobody derives Karnaugh maps between sets.
2. **Ask one question, wait, grade in three characters.** "✓" or "✗ + one-line
   correction" — no essay feedback mid-workout. Then wait for "next" (or a rest interval)
   before the next question. If he's mid-set, the question waits; there is no hurry law
   here — the gym outranks the round.
3. **Log drops, don't bank them yet.** Keep an in-chat list of missed questions.
4. **Review after the last set (up to 2 min).** Ask for the corrected concept in his own
   words. Only then may a card be appended under the learning contract. If he is leaving,
   queue a plain misconception for a later `daily`; do not promise automatic cards.
5. **Report in one line:** X/8, weakest miss, banked now-or-later.

## Rules

- **Hard cap 8 questions.** A longer round is how voice mode derails and how gym rounds die.
- One-line answers expected; a question needing more than one sentence moves to the next `daily`.
- If voice mode is unavailable or derailing, the same list works as a text sprint — format is the requirement, not the medium.
- Commute slot: audio overviews of his own notes (NotebookLM) serve the same dead time;
  that's a manual setup outside this skill — point at the research report §4.2 if asked.
