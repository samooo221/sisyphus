---
name: harvest
description: Collect a course's past exams and practice material from public web sources into the course's corpus directory (outside the vault), so `bank` has something to ingest — official FIT pages, student archives, GitHub topic repos. Use when a corpus dir is empty or thin ("harvest IZP", "get past papers for IEL") — normally once, in week 1 of term.
---

# Harvest

Fills the course's `exam.corpus` with the user's own copies of publicly available past papers, before `sisyphus bank` runs. Harvest finds and fetches; bank ingests. **Never print a question, an answer, or a topic list into the chat** — harvested text is future drill material; the reply is file paths and counts only.

## `sisyphus harvest <COURSE>`

1. **Resolve the corpus** from the course MOC's `exam:` block (no block → stop, point at `sisyphus setup <COURSE>`). Create the dir if missing.
2. **Collect candidate sources, best trust first:**
   - **Official:** the course's `fit.vut.cz` page and anything it links that is publicly reachable (archived exams, sample tests, public e-learning material).
   - **Student archives:** e.g. `github.com/ondryaso/leoAtFit` (whole-bachelor notes and exam sheets), `osyrion.github.io/FIT-VUT-Projects/`, GitHub topics `vut` and `<lowercase course code>`, community gists of test cases.
   - **Czech student sites** (studentino and friends) only after the content checks out — label them `unverified` in SOURCES.md.
3. **Fetch rules:**
   - Public, unauthenticated pages only. Anything behind a login (campus e-learning, Studis) becomes a `- [ ] manual:` line in SOURCES.md and a mention in the report — the user downloads it from a campus session. **Never bypass authentication.**
   - Respect robots.txt and each source's license; a few requests per host, not a flood.
   - Repos of assignment *solutions* are fine to archive under `<corpus>/solutions-reference/` — they feed `bank`'s answer fields — but they **never leave the corpus dir** (no vault, no repo, no chat).
4. **File naming:** `YYYY-<short-desc>.pdf` (year from the paper or its URL), `undated-<short-desc>.pdf` when unknown. Non-PDF text (gists, web tests) becomes `.md` with its source URL on the first line. If `pdftotext` (poppler) is installed, also emit `.txt` beside each PDF — `bank` reads PDFs, but text greps faster.
5. **Idempotent:** skip a source already cited in `<corpus>/SOURCES.md`; append one bullet per fetch: file · origin URL · date · license note.
6. **Report** counts only: files added per source, how many manual/logged-in TODOs remain, next step (`sisyphus bank <COURSE>` once the user has what they need).

## Rules

- The corpus never enters the vault or any repo — verbatim exam text is copyrighted, and vaults sync and get shared.
- An empty harvest is not a failure. Report what exists, list the manual TODOs, and remind that `drill new` falls back to synthetic until a corpus is banked.
- Never fabricate a paper. If a source can't be reached, record it in SOURCES.md — don't reconstruct exam questions from memory or training data.
