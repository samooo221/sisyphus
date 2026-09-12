---
name: bank
description: Ingest his past-paper PDFs into a per-course question bank that drill draws from. Use when papers land in the corpus dir ("bank the IZP papers").
---

# Bank

Read [the learning contract](../../references/learning-contract.md) and [paper practice](../../references/paper-practice.md) before acting.

**Never print a question, an answer, or a topic list into the chat.** Reply with file paths and counts only. Reading the bank in chat spoils future drills.

## `sisyphus bank <COURSE>`

1. **Resolve the corpus.** Read `exam.corpus` from the course MOC's `exam:` block (no block → stop, point at `sisyphus setup <COURSE>`). The bank lives at `<corpus>/question-bank.md` — **in the corpus dir, never in the vault and never in any repo**: verbatim exam text is copyrighted, and vaults sync and get shared. Papers are the user's own copies; the bank never redistributes them.
2. **Parse each PDF** in the corpus (Read handles PDFs directly). Extract every question, its stated point value, and an official answer only if supplied. Preserve every variant and section: one PDF may hold many complete papers. Keep matrices, diagrams, tables, shared instructions and supplied formulae with the right question. Store page references and, where useful, page images outside the vault. Extracted text is a search aid, not authoritative mathematics: flag `status: pdf-required` until the selected question has been checked visually against the original. Never silently repair an apparent source error; mark it ineligible pending review. A lossless held text capture is usable for text-only practice; flag questions whose missing figures or layout make them incomplete.
3. **Idempotent:** skip unchanged sources already cited in the bank; re-running after adding one source ingests only that source. Preserve IDs and every `used:` date. Store source SHA-256 and a metadata-only `bank-manifest.json` beside the bank if useful. A changed source requires review, not silent replacement. Unknown year or official marks are `null`, never guessed. Lab sheets, practice quizzes, midterms and finals are different source kinds; do not label a practice quiz as a past final.
4. **Tag topics only from `exam.topics`.** Nearest match wins; a question that fits nothing in the list → ask the user whether to add a topic to the `exam:` block, **never coin a name silently** (invented names fragment the per-topic stats).
5. **Append** to `question-bank.md` (create with frontmatter `type: question-bank`, `course`, `updated` — bump `updated` on every run):
   ```markdown
   ## B07
   - points: 4 · topic: pointers · paper: 2024-regular.pdf · year: 2024
   - used:
   - section: final · variant: A · question: 3 · page: 2
   - kind: past-exam · eligible: true · status: pdf-required
   - answer-source: not-provided
   - source-sha256: <digest>
   - source-pdf: [Original question](2024-regular.pdf#page=2)
   What does `sizeof(int *)` evaluate to on... (verbatim)
   ### Answer
   (the paper's solution, or blank if the PDF has none)
   ```
   IDs `B01, B02, ...` continue from the highest existing. The `used:` line stays empty here — `drill new` appends dates to it to avoid repeats.
   An empty Answer section means no official answer was supplied; do not solve the paper during intake. `eligible: false` excludes missing figures, unresolved source errors and other incomplete questions. `points: null` permits practice with an explicitly generated rubric, never invented official marks. The manifest mirrors metadata only; the bank owns `used:` history. Put the per-topic tally on disk, not in chat.
6. **Report** sources ingested/skipped, questions added, withheld entries, and how many lack official answers, plus file paths. No question, answer or topic content.

## External exercises — `bank <COURSE> <collection> [chapter/section]`

The MOC's `resource_guide` and `<corpus>/practice-sources.json` point to the curated
private library. This index describes documents, not verified individual questions.
Bank only the requested, course-aligned selection; do not turn an entire book into
an exam pool. Keep external entries in `<corpus>/external-question-bank.md` and
`external-bank-manifest.json`, with stable `E0001` IDs. Preserve existing FIT bank
IDs and history. Source references include document ID, SHA-256, chapter, original
exercise number and PDF page; record any prerequisites. Check every selected
statement, diagram and matching solution against the original. An answer elsewhere
in the same PDF stays sealed. Unknown marks remain null; label any later practice
rubric generated. Use canonical course topics and `kind: external-practice`.

The same idempotence, exposure, copyright and missing-figure rules apply. Never mine
reserved FIT variants for examples or generated variations. This route feeds
`drill new <COURSE> practice`; MIT papers and textbook exercises do not acquire FIT
exam gates or calibrated difficulty by being banked. No bank entry establishes
student understanding or authorizes a flashcard.
