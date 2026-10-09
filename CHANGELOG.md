# Changelog

## Unreleased (branch `showcase`)

- Added `examples/`: an invented course and a transcript of `drill new` then `drill grade` (hand-written).
- README: added "What this is, and is not", trimmed Status, moved release notes here.

## 0.3.1, 19 September 2026: consistency pass

No new skills. A review of the whole plugin found places where two skills disagreed, or where a skill promised something the repository does not provide. They are fixed in the wording:

- `stress` no longer hardcodes model IDs and applies `factory`'s route rule (available and authorized only, never paid).
- `ambush` no longer promises a Wednesday delivery the plugin does not install, and states that its outcomes are deliberately unrecorded.
- `harvest` retries a failed source instead of treating it as acquired.
- `moonshot` uses `harvest`'s filename scheme and allocates every download name before the checklist is handed over.
- Releasing a reserved paper writes a `released` event rather than rewriting the inventory, so the reserve count stays enforceable and `drill` can tell permission from exposure.
- `oral` and the real-exam record allocate a sequence number like `drill` does, so two events on one day cannot collide.
- `drill grade` distinguishes an interrupted result from a finished one.
- `tutor` now writes the `learning-check` record that `stats` was already reading.
- `lookup` quotes its `*` terms, names all three meanings of exit 1, and stops pointing at one machine's prvak checkout. `prvak` is listed as its requirement.

## 0.3.0, 18 September 2026: `lookup`

A nineteenth skill: the answer layer over `prvak search`, a local keyword index. It answers only from retrieved passages and names them. The index carries no exam-bank material, by design; `bank` and `drill` remain the only route to assessment text.

## 0.2.5 (local preparation), 12 September 2026

Resource guides and practice sources for a first-year course set. Multiple same-day papers, whole variants, repeat and exposure records and chosen longer sessions are specified. Sealed keys freeze the hashes of separate diagram assets and permitted tools. A pending or failed tutor check leaves the stage pending without erasing demonstrated progress.
