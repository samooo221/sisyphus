---
name: setup
description: Configure a course for drilling — interview the user, then write the `exam:` block into the course's MOC frontmatter (scaffolding the vault folders and a bare MOC first if needed). Use when adding a course to sisyphus ("set up IZP", "sisyphus setup") or when drill/bank report a missing `exam:` block.
---

# Setup

Read [the learning contract](../../references/learning-contract.md) before acting.

Turns a course into something `drill`, `bank`, and `stats` can operate on. The only artifact is the `exam:` frontmatter block in the course's MOC — no config files anywhere else.

## `sisyphus setup <COURSE>`

1. **Find or create the MOC.**
   - Search the vault for a note with `type: moc` frontmatter whose `code:` matches (fall back to filename match). If the vault has a `CLAUDE.md`, follow its conventions for anything you create.
   - **Existing MOC: frontmatter-only edit.** Never rewrite, reorder, or "improve" the MOC's prose — add/update the `exam:` block (and `code:` if missing) and touch nothing else.
   - **No MOC:** scaffold the minimum. An area folder (ask which, e.g. `University/`) with `MOCs/`, `Notes/`, `Flashcards/` subfolders if absent, an empty `Flashcards/<code> — flashcards.md`, and a MOC from this template:
     ```markdown
     ---
     type: moc
     code: IZP
     course: Introduction to Programming
     tags: [university, moc]
     created: <today>
     ---
     # 🗺️ IZP — Introduction to Programming

     ## 🎯 Topics
     <one line per topic — mirror the exam: block>

     ## 🎴 Flashcards
     - [[IZP — flashcards]]
     ```
2. **Interview — but mine first.** If the MOC already lists topics, priorities, or grading facts, propose the `exam:` block from them and ask only for what's missing. Otherwise ask, one round, exactly:
   - Final exam total points, time limit, section point patterns, and any minimum-score gates? Check held official evidence first. Record unknown clock/format as unknown, not a plausible guess.
   - Topic list, and which topics deserve `invest` / `skim` weight? (Everything else defaults to `normal`.)
   - A private corpus directory outside the vault and every repo? It can initially be empty; synthetic assessment files need the same protection. Default drills to `<corpus>/drills`.
3. **Write the block** into the MOC frontmatter:
   ```yaml
   exam:
     # Historical sample schema example only; populate from current evidence.
     final_total: 54
     time_min: 90
     time_status: verified           # null time_min + unverified if no evidence
     corpus: ~/data/fit-exams/IZP
     drills_dir: ~/data/fit-exams/IZP/drills
     sections:
       - {id: final, total: 54, questions: 8, question_points: [6, 8, 6, 8, 10, 6, 4, 6]}
     gates:
       - {scope: exam, min_points: 23, on_fail: zero_exam}
     topics:
       - {name: pointers, weight: invest}
       - {name: control-flow, weight: skim}
       - {name: functions}            # normal
     # flashcards: override only if the existing course deck is elsewhere
   ```
   Topic names are the canonical vocabulary every other skill joins on: short, kebab-case, stable. See `drill` for the two-section short-test gate schema. Preserve evidence dates, `format_basis`, source pointers and separate `semester_requirements` when known. Semester credit thresholds are not exam gates. Never mark a student eligible without their actual grades. Resolve symlinks to ensure the corpus and drills are outside vault/repo boundaries.
4. **Warn once:** nested YAML and Obsidian's Properties panel don't mix — edit the `exam:` block in source mode.
5. **Report:** the MOC path, the block as written, and the next step (`sisyphus bank <COURSE>` if a corpus was given, else `drill new <COURSE>`).

## Existing resource guides

Preserve a MOC’s existing `resource_guide`, `study_track`, corpus paths, canonical topics and dated assessment evidence. The resource guide is a top-level path to curated reading and practice, not another exam configuration. Existing `practice-sources.json` is a document index; selected external exercises must be checked and banked before a drill uses them. Unknown summer clocks and question patterns stay unknown until verified. Minimum passing scores do not imply score cancellation unless the source says so.
