---
name: preview
description: Pre-lecture primer — turn published slides (or the next course topic) into a 10-question prequiz with folded answers plus a short "watch for" list, so the lecture is second contact instead of first. Use the evening before a lecture ("preview IEL", "sisyphus preview IMA1 limits", "preview tomorrow's slides").
---

# Preview

Read [the learning contract](../../references/learning-contract.md) before acting.

Pretesting is a desirable difficulty: making half-wrong guesses *before* instruction makes the real encoding stick better. The lecture then lands as review instead of first contact, and pass-2 gets cheaper. The product is **questions, not notes** — slides-to-notes is the `lecture` skill's job.

## `sisyphus preview <COURSE> [slides.pdf | topic]`

1. **Resolve the course** (MOC + `exam:` block). If a slides PDF is given, Read it; otherwise take the next un-covered topic from the MOC's "Core topics (learning order)" list and say this is a guess at lecture content.
2. **Write `<Area>/Notes/previews/YYYY-MM-DD-<CODE>-preview.md`** — frontmatter `type: preview`, `course: <CODE>`, `tags: [university, university/<CODE>]`, `created`. Two sections:
   - **Watch for** — 3–5 one-line bullets: the ideas the lecture will build on, phrased as open questions ("how does the diode decide it's 'forward'?"), so there's a reason to listen for each.
   - **Prequiz** — 10 questions mixing recall and application, each immediately followed by a **folded callout** (`> [!question]- answer`) holding the answer from the material. Folded = he must commit a guess before peeking — same mechanism as lecture cues.
3. **Answers come only from the given material** — anything the material doesn't pin down gets `[!] verify`, never a confident guess.
4. **Report:** the file path, the watch-for list, and a reminder: attempt the prequiz *before* walking in, it's 10 minutes.

## Rules

- **Preview questions never enter the flashcards deck.** They prime; the lecture and pass-2 decide what's worth keeping. A question that still matters after the lecture becomes a card *then*, through the normal gates.
- Max 10 minutes of his time — a preview that becomes a study session is a leak in the Dawn Raid.
- Slides from a previous year? Say so explicitly and lean on the MOC topic list for ordering — topics move between years.
- If nothing is published and the topic is a guess, cap the prequiz at 5 questions and mark the file `guess: true` in frontmatter.
