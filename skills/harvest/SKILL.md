---
name: harvest
description: Collect a course's public past exams and practice material into its corpus dir so bank can ingest them. Use when a corpus is empty or thin ("harvest IZP").
---

# Harvest

Read [the learning contract](../../references/learning-contract.md) before acting.

Fills the course's `exam.corpus` with the user's own copies of publicly available past papers, before `sisyphus bank` runs. Harvest finds and fetches; bank ingests. **Never print a question, an answer, or a topic list into the chat** — harvested text is future drill material; the reply is file paths and counts only.

## `sisyphus harvest <COURSE>`

1. **Resolve the corpus** from the course MOC's `exam:` block (no block → stop, point at `sisyphus setup <COURSE>`). Create the dir if missing.
2. **Read the MOC `resource_guide` and existing acquisition records first.** Reuse verified held resources; avoid duplicate downloads. Broader textbook/tutorial requests use the guide and `~/data/fit-library/` (or the user's private library), while assessment selection uses `practice-sources.json`. Keep author, URL, access date, licence, hash, local path, text extraction and limitations. For past exams, collect sources best trust first:
   - **Official:** the course's `fit.vut.cz` page and anything it links that is publicly reachable (archived exams, sample tests, public e-learning material).
   - **Student archives:** e.g. `github.com/ondryaso/leoAtFit` (whole-bachelor notes and exam sheets), `osyrion.github.io/FIT-VUT-Projects/`, GitHub topics `vut` and `<lowercase course code>`, community gists of test cases.
   - **Czech student sites** (studentino and friends) only after the content checks out — label them `unverified` in SOURCES.md.
3. **Fetch rules:**
   - Public, unauthenticated pages only. Anything behind a login (campus e-learning, Studis) becomes a `- [ ] manual:` line in SOURCES.md and a mention in the report — the user downloads it from a campus session. **Never bypass authentication.**
   - Respect robots.txt and each source's license; a few requests per host, not a flood.
   - Do not collect student solutions to current FIT graded projects as study fuel. Released instructor practice solutions and openly licensed reference examples may be kept privately with provenance; do not call community answers official. No credential use or access to instructor-only answer manuals.
4. **File naming:** `YYYY-<short-desc>.pdf` (year from the paper or its URL), `undated-<short-desc>.pdf` when unknown. Non-PDF text (gists, web tests) becomes `.md` with its source URL on the first line. If `pdftotext` (poppler) is installed, also emit `.txt` beside each PDF — `bank` reads PDFs, but text greps faster.
5. **Idempotent:** skip a source only when SOURCES.md records it as **successfully fetched** — a line with a local file behind it. A `- [ ] manual:` line, an unreachable source and any other failure note are the opposite of acquired, so they are retry candidates, not skips; a failed download must never be mistaken for a held paper. Append one bullet per fetch: file · origin URL · date · license note.
6. **Report** counts only: files added per source, how many manual/logged-in TODOs remain, next step (`sisyphus bank <COURSE>` once the user has what they need).

## Rules

- The corpus never enters the vault or any repo — verbatim exam text is copyrighted, and vaults sync and get shared.
- An empty harvest is not a failure. Report what exists, list the manual TODOs, and remind that `drill new` falls back to synthetic until a corpus is banked.
- Never fabricate a paper. If a source can't be reached, record it in SOURCES.md — don't reconstruct exam questions from memory or training data.
