# Transcript: `drill new`, then `drill grade`

Illustrative, not a recording. It shows the shape of the two sessions on the invented course LOG101 (see [README](README.md)). Files are in `sample-corpus/LOG101/drills/`.

## Session 1: build the paper

```text
> /sisyphus:drill new LOG101 practice minutes=60

Paper ready. Nothing about its content is printed here, on purpose.
  attempt id:  2026-03-10-01
  paper:       drills/2026-03-10-01-drill.md
  key:         drills/2026-03-10-01-key.md   (sealed, do not open)
  answers:     drills/2026-03-10-01-answers.md
  clock:       60 minutes, closed book, pen and paper only
  limits:      synthetic paper (made from the topic list), practice mode,
               not exam-equivalent. Pass mark 16 of 40.
Grade in a NEW chat session. This session wrote the key and cannot invigilate.
```

What happened on disk: three files were written with the point split fixed in the key, the SHA-256 of the drill stored in the key, and the digest of the key stored in the answer sheet. The chat reply held paths and limits only, never a question.

## The sitting (no AI involved)

The student opens the drill file, starts a real clock, answers on paper and types the answers into the answer sheet. The student also fills in the conditions (`closed-book-timed-unaided`, 52 minutes). The plugin never infers them.

## Session 2: grade it (fresh chat)

```text
> /sisyphus:drill grade LOG101 2026-03-10-01

Checks passed: this is a new session, the drill and key hashes match, the answer
sheet is filled in, there is no earlier result.
  attempt:    2026-03-10-01 (practice, synthetic, closed-book-timed-unaided)
  score:      30 / 40   (raw 30, effective 30)
  gate:       passed (needs 16, scored 30)
  by topic:   number-systems 8/8, flip-flops 8/10, karnaugh-maps 8/12,
              boolean-algebra 6/10  (weakest)
  cards:      0 added, 2 pending
  result:     drills/2026-03-10-01-result.md
Both pending items wait for your own explanation. No card exists until you give it.
Next: /sisyphus:tutor LOG101 boolean-algebra
```

What the grader did: scored against the fixed rubric without re-deriving points, wrote the result file, and queued the two misconceptions in `pending-learning.md`. It did not write a card, because the student had not yet explained the concept in their own words. The question and answer text stayed in the files, never in the chat.
