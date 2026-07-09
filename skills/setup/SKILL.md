---
name: setup
description: Configure a course for drilling — interview the user, then write the `exam:` block into the course's MOC frontmatter (scaffolding the vault folders and a bare MOC first if needed). Use when adding a course to sisyphus ("set up IZP", "sisyphus setup") or when drill/bank report a missing `exam:` block.
---

# Setup

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
   - Final exam total points? Time limit in minutes?
   - Topic list, and which topics deserve `invest` / `skim` weight? (Everything else defaults to `normal`.)
   - A directory of past-paper PDFs, if any? (Point it **outside the vault** — verbatim exam text is copyrighted and vaults sync/share. Skippable; drills fall back to synthetic.)
3. **Write the block** into the MOC frontmatter:
   ```yaml
   exam:
     final_total: 54
     time_min: 90
     corpus: ~/data/exams/IZP        # omit if none
     topics:
       - {name: pointers, weight: invest}
       - {name: control-flow, weight: skim}
       - {name: functions}            # normal
     # drills_dir / flashcards — only when the vault's layout needs an override
   ```
   Topic names are the canonical vocabulary every other skill joins on: short, kebab-case, stable. Omit `drills_dir`/`flashcards` unless the defaults (`<Area>/exam-drill/<code>/`, `<Area>/Flashcards/<code> — flashcards.md`) don't fit the vault.
4. **Warn once:** nested YAML and Obsidian's Properties panel don't mix — edit the `exam:` block in source mode.
5. **Report:** the MOC path, the block as written, and the next step (`sisyphus bank <COURSE>` if a corpus was given, else `drill new <COURSE>`).
