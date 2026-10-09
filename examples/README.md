# Examples

A made-up course, `LOG101`, to show what sisyphus reads and writes. Nothing here comes from a real course or a real student.

**Read this first: these files were written by hand to show the formats and the shape of the replies. They are not the recorded output of a run.** The plugin has no automated tests, so nothing checks that the files match what a live session would produce. The one thing I did check is arithmetic: the drill's answers, the point split and the SHA-256 digests (drill digest inside the key, key digest inside the answer sheet) were recomputed.

| Path | What it shows |
|---|---|
| [`transcript-drill-new-and-grade.md`](transcript-drill-new-and-grade.md) | The two sessions: `drill new`, then `drill grade` in a fresh session |
| `sample-vault/University/MOCs/` | A course note with the `exam:` block that `setup` writes |
| `sample-vault/University/Flashcards/` | The course deck, still empty after grading (no automatic cards) |
| `sample-corpus/LOG101/drills/` | The four files of one attempt: drill, sealed key, answers, result |
| `sample-corpus/LOG101/pending-learning.md` | Two misconceptions waiting for the student's own explanation |

In real use the corpus folder lives outside the vault and outside every repository. Here it sits next to the vault only so you can read it.
