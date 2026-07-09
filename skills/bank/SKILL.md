---
name: bank
description: Ingest the user's own past-paper PDFs into a per-course question bank that `drill new` draws from — topic-tagged questions with point values and answers, stored in the corpus directory outside the vault. Use when past papers land in the corpus dir ("bank the IZP papers", "sisyphus bank IZP").
---

# Bank

**Never print a question, an answer, or a topic list into the chat. Everything goes to disk; the reply is file paths only.** Reading the bank in chat spoils every future drill drawn from it.

## `sisyphus bank <COURSE>`

1. **Resolve the corpus.** Read `exam.corpus` from the course MOC's `exam:` block (no block → stop, point at `sisyphus setup <COURSE>`). The bank lives at `<corpus>/question-bank.md` — **in the corpus dir, never in the vault and never in any repo**: verbatim exam text is copyrighted, and vaults sync and get shared. Papers are the user's own copies; the bank never redistributes them.
2. **Parse each PDF** in the corpus (Read handles PDFs directly). Extract every question: verbatim text, point value, and the paper's model answer if the PDF includes solutions.
3. **Idempotent:** skip papers already cited in the bank; re-running after adding one PDF ingests only that one.
4. **Tag topics only from `exam.topics`.** Nearest match wins; a question that fits nothing in the list → ask the user whether to add a topic to the `exam:` block, **never coin a name silently** (invented names fragment the per-topic stats).
5. **Append** to `question-bank.md` (create with frontmatter `type: question-bank`, `course`, `updated` — bump `updated` on every run):
   ```markdown
   ## B07
   - points: 4 · topic: pointers · paper: 2024-regular.pdf · year: 2024
   - used:
   What does `sizeof(int *)` evaluate to on... (verbatim)
   ### Answer
   (the paper's solution, or blank if the PDF has none)
   ```
   IDs `B01, B02, ...` continue from the highest existing. The `used:` line stays empty here — `drill new` appends dates to it to avoid repeats.
6. **Report** counts only: papers ingested/skipped, questions added, per-topic tally, and how many lack answers. No content.
