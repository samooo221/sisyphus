---
name: stress
description: Adversarial explanation check — he explains a concept closed-book, an attacker seat hunts for what's wrong or misleading in the explanation, he defends, and an auditor seat rules on whether attacks were fair and defenses held. Use on concepts he thinks he already knows ("stress-test my pointers explanation", "sisyphus stress IEL RC transients").
---

# Stress

Read [the learning contract](../../references/learning-contract.md) before acting.

The Dunning zone is where AI study tools fail quietly: fluent explanation *feels* like
knowing. This skill buys an honest verdict on that feeling. Two seats, two jobs:
an **attacker** hunts real holes (grounded in course materials, not style nitpicks), an
**auditor** rules on fairness — so a held defense is real and a broken one can't be
argued away. The user's own vivid note applies here: *the examiner picks the model*;
this skill makes that literal before FIT does it for real.

## `sisyphus stress <COURSE> <topic>`

1. **Explanation first, closed-book.** He writes (or dictates) his explanation of the
   topic — 5–10 minutes, **no materials open**. The explanation is the artifact under
   test; reading first would just move the test to reading comprehension.
2. **Spawn the attacker seat.** `opencode run -m opencode-go/grok-4.6` (neutral temp
   dir) with: the explanation verbatim, the course's MOC topic description and any
   relevant concept notes, and this brief — *produce the 5 sharpest attacks: claims
   that are wrong, incomplete, misleading, or true-but-only-in-a-narrow-regime. Each
   attack is one question the student can be asked. Ground every attack in the course
   materials; no stylistic attacks.* Deliver attacks **one at a time**.
3. **He defends each attack, one at a time.** No hints from the session during a
   defense — same law as oral. Follow up once if a defense is vague, then move on.
4. **Spawn the auditor seat** (a third route, e.g. `opencode-go/kimi-k3`): given the
   explanation, the attacks, and his defenses + course materials, rule per attack —
   *fair or unfair? defense held or broken? one-line why.* Dismiss unfair attacks
   openly; flag lucky-or-vague defenses as broken even when the auditor "mostly agrees".
5. **Broken defenses enter the own-words queue.** Ask him to rewrite the corrected
   mechanism, then apply the learning contract. The auditor's answer cannot become
   his card automatically.
6. **Report:** held X/5, the two most dangerous holes in his own words, cards added.

## Rules

- **Explanation before materials, always.** A stress round on a freshly-read topic
  tests nothing; if he just studied it, wait a day (spacing does the work).
- Attacks must be *course-grounded*; the auditor exists to enforce that as much as the
  verdicts.
- Seats run on flat routes only (ledger law); attacker and auditor must be different
  models — audit independence is the point.
- A clean 5/5 on a first-ever stress = suspicion, not celebration: pick the harder
  sub-topic or raise attack difficulty next time.
