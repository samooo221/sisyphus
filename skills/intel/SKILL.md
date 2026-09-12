---
name: intel
description: Cohort intel sweep — public-only scan of a course's official pages, faculty news, and student spaces for assignment clarifications, deadline changes, and post-test reactions, reported as ≤10 dated bullets. Use weekly or before a test week ("intel IEL", "sisyphus intel", "what's new at FIT").
---

# Intel

Read [the learning contract](../../references/learning-contract.md) before acting.

Half of first-year friction is information that was public but not seen: a project
spec clarification, a moved deadline, "the IEL test hit RC transients hard". This
skill sweeps the public surface once a week so the daily brief never has to guess.

## `sisyphus intel [COURSE ...]`

1. **Sweep, newest-first, public-only:**
   - the course's official fit.vut.cz page (news/announcements section) for each named
     course — or all first-year courses if none named;
   - faculty-level news and the official calendar (deadline changes, test terms);
   - public student spaces that resolve without a login (faculty forum threads,
     startatfit/SU pages).
   Use WebSearch/WebFetch; last 7 days is the window.
2. **Report ≤10 bullets, each with:** date · source URL · one line of what changed or
   what was said. Sort by impact on him (his courses, then deadlines, then noise).
3. **The line, enforced:** *reactions and clarifications are intel; actual leaked test
   content is not.* Any item that looks like exam questions or project solutions from a
   live assessment gets **dropped and named as dropped** — one line, no details. The
   drill loop is the legitimate way to know what tests look like.
4. **Nothing is archived.** Intel is ephemeral chat output; what's durable (a moved
   deadline, a new test term) goes into the MOC's `exam:` block only if he confirms it.

## Rules

- Public surface only — no login scraping, no Discord/API tokens, no impersonation;
  gated spaces stay manual (his own scrolling, like moonshot's clicking).
- No archive, no vault writes without confirmation — intel decays fast and vault clutter
  is a tax on the loop.
- Zero findings is a valid report ("all quiet") — don't pad with stale items.
- If a course page announces something that contradicts his `exam:` block (totals,
  terms), flag it as a config drift for `sisyphus setup`, and don't silently edit.
