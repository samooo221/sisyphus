---
name: garden
description: Weekly interleaved quiz across two or more courses — mixed problem types one at a time, weighted toward the topics where drill results show weakness, graded strictly at the end, misconceptions queued for the student's own explanation. Use for the weekly mixed session ("garden", "sisyphus garden IZP IDM", "quiz me across my courses").
---

# Garden

Read [the learning contract](../../references/learning-contract.md) before acting.

Real FIT exams are single-course, so drills stay single-course. The garden exists because **recognizing *which* method a problem needs is its own skill, and blocked practice never trains it** — you always know the chapter. In a 54-classroom math RCT, interleaved practice beat blocked 61% to 38% on a surprise test a month later (Rohrer et al.). Mixing feels worse and works better; that discomfort is the training signal. Don't "optimize" this skill into a blocked quiz — the mix is the mechanism.

## `sisyphus garden [COURSE ...]`

1. **Resolve every course named** (default: all with an `exam:` block). Pull each course's `exam.topics` and its drills dir.
2. **Target the holes.** Per course, read `questions:` frontmatter from past `*-result.md` files: topics scored below ~50% are priority; `weight: invest` topics come next; a course with no results yet is weighted by `invest` alone — say its targeting is cold. Never reuse an actual past **drill** question: those papers are sealed and may be re-drilled; garden questions are fresh generations from topic names only.
3. **Interleave, one at a time.** 8–12 questions total, rotating between courses so consecutive questions come from different courses and different *types* (recall → "what does this print" → proof step → worked computation → back). Ask one question, **wait for the full answer, no hints while it's live** — same law as oral. Chat is fine: garden questions are ephemeral, not sealed papers.
4. **Grade at the end, not per question.** Hold all answers until the student has answered everything (this is *their* interleaving to sit in), then grade hostilely: unjustified conclusions score zero even when right; partial credit only where a breakdown is obvious. Per-topic tally at the end, weakest first.
5. **Queue misconceptions.** Apply the learning contract: no card until the student rewrites the corrected concept. Group related misses and preserve the existing deck.
6. **Report:** score, per-topic tally, which topics graduate off the priority list next week, cards added. **No result files** — the garden measures, it doesn't archive; the drill curve is the dataset.

## Rules

- **The mix is the point.** Never group questions by course ("IZP block, then IDM block") — consecutive-same-course defeats the mechanism. Rotate.
- No hints, no ladder, no second chances on a live question — this is the measurement end of the loop; teaching belongs to `tutor`.
- Fresh generations only, from topic names; if the student recognizes a past drill question, replace it and note the leak.
- Keep it 15–20 minutes. A garden that takes an evening stops happening; frequency beats depth here.
- A drop on a topic with no concept note yet goes to the weekend queue too (say so) — cards without understanding are decoration.
