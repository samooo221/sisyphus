---
name: lecture
description: Process a messy pass-1 lecture note (plus optional slides PDF) into the vault's pass-2 artifacts — answers to the `> [!question]` cues, atomic concept-note drafts the user confirms in their own words, MOC links, and flashcards appended to the course deck. Use on lecture days ("process my IZP lecture", "sisyphus lecture IDM today's note").
---

# Lecture

The second pass is where lectures become knowledge: same-day processing of the live-captured mess. This skill does the mechanical half — extract, split, link, answer what the slides answer, format cards — and enforces the ownership half: **cards are written only from notes whose one-sentence core the user has rewritten or approved in their own words.** Draft notes the user never confirmed are decoration with a due date.

## `sisyphus lecture <COURSE> <messy-note-path> [slides.pdf]`

1. **Resolve the course** (MOC + `exam:` block), the notes dir (default `<Area>/Notes/`) and the flashcards file (default `<Area>/Flashcards/<code> — flashcards.md`).
2. **Read the inputs.** The messy note stays **read-only** — it remains the raw record of the lecture. Slides PDFs are Read directly; where slides and note disagree, slides win on facts, the user's `> [!question]` cues win on priority.
3. **Triage the cues.** Every `> [!question]` the materials answer gets its answer written into a processed section of the output. Cues they don't answer go under `## Unresolved` at the end — the weekend queue, and prime card candidates once resolved.
4. **Draft atomic concept notes** into the notes dir: one idea per file, titled as the concept (`Pointers in C`, not `IZP week 2`), following the vault's `Concept note` template and the vault `CLAUDE.md` conventions — frontmatter `type: concept`, `course: <CODE>`, tags reusing `university/<CODE>`, a link to the course MOC plus one related note, and the note added to the MOC's concept list in the same edit. **Stop before writing any cards.**
5. **The own-words gate.** Show the user each draft's `## Idea` one-liner and have them rewrite or approve it, one round. If a draft covers something the user couldn't *do* yet, apply the Study Loop rule: the note waits until they can — notes about things you can't do are decoration.
6. **Write cards** from confirmed notes and every answered cue, appended under a `## From lectures` heading in the course deck: `Q::A`, `:::` for bidirectional pairs, `==cloze==` for the term inside a sentence. One fact per card.
7. **Report:** notes drafted / confirmed, cards added, unresolved-cue count, and any place the user's note contradicted the slides.

## Rules

- **The raw note is read-only.** Pass-1 mess stays as captured.
- **Never state a fact the materials don't contain** without marking it inline `[!] verify` — a lecture processor that textbook-splains manufactures confident errors.
- **Append-only** to flashcard files; never touch the HTML scheduling comments the Spaced Repetition plugin appends.
- Full pass-2 is for the sieve courses only — for anything else the Study Loop's 10-minute skim is the right tool, and saying so is part of the skill.
