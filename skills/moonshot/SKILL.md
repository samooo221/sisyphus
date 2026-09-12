---
name: moonshot
description: The past-exam acquisition evening — build a click-list of every obtainable past exam for a course (official pages first, then public student archives), run `harvest` for the public ones, and hand HIM a precise checklist for the login-only ones. Use once per course, or when a corpus feels thin ("moonshot IEL", "get every IZP past exam").
---

# Moonshot

Read [the learning contract](../../references/learning-contract.md) before acting.

The loop's quality is capped by corpus reality: a synthetic drill guesses the exam's style, a real paper *is* it. One evening of clicking buys a semester of drills that measure the right thing. This skill maximizes coverage legally — his login, his hands, nothing bypassed.

## `sisyphus moonshot <COURSE>`

1. **Prepare the corpus dir.** `mkdir -p ~/data/fit-exams/<CODE>/` and confirm the MOC's `exam.corpus` points there.
2. **Run `harvest` first** — everything public gets fetched automatically; this skill is for what remains.
3. **Build the click-list.** Search + fetch, in priority order:
   - The course's official pages (fit.vut.cz → course → Materials/Archive) and its e-learning course shell — anything behind the faculty login is **manual**, never bypassed.
   - Known public student archives (GitHub topics, community gists) — note provenance, they're lower trust.
   For each item: URL · what it is (midterm / final / solutions · year) · public-or-login.
4. **Hand over the checklist.** Login-only items become numbered steps for HIM: open URL → download → save as `<CODE>-<year>-<kind>.pdf` in the corpus dir. He does this in his browser, logged in — an agent with his session is not part of this skill.
5. **Verify what landed.** Each PDF: opens, page count sane, not an HTML page saved as `.pdf`, not a duplicate (same content as an existing file). Flag junk and name the gap.
6. **Report:** public-found N · manual-click M · landed K · topics still uncovered (these become the `synthetic` disclaimer on future drills). Then: *"Run `sisyphus bank <CODE>` when you're done clicking."*

## Rules

- **Never bypass a login, paywall, or access control** — not with his session, not with anyone's. The checklist is the boundary; anything gated stays manual.
- The corpus stays in `~/data/` outside the vault and never gets redistributed — exam text is copyrighted; `bank` already keeps it out of the vault.
- A PDF of unknown provenance (random student site) gets a provenance note in the bank entry — trust lower, verify against official materials where they exist.
- Coverage is the metric: after a moonshot, every `exam.topics` name should be either represented in the bank or listed as an explicit gap. No silent holes.
