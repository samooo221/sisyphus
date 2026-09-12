---
name: daily
description: Plan or run study within a 90-minute default, with longer question or paper sessions when explicitly chosen. Prioritise problem solving, prerequisites and actual deadlines; compose existing sisyphus activities.
---

# Daily

Read [the learning contract](../../references/learning-contract.md) and [paper practice](../../references/paper-practice.md) before acting.

## `sisyphus daily [plan|run] [minutes=N | papers=2 COURSE]`

Natural language works too: “normal 90 minutes”, “three-hour question grind”, or “two full ILG papers”. These are prose skill arguments, not a separate executable.

1. **Load the chosen budget.** Read `<Area>/Free Time Guard.md`. `daily_cap_min` defaults to 90. An explicit longer duration or paper count overrides it for this session only. State solving time plus chosen breaks/review; never squeeze a 120-minute exam into 90 and call it a full sitting. Merely preparing files does not commit the student to sit them now. With `slots_verified: false`, use session-relative timings and ignore example commitments. Protect actual commitments; ask only about a material conflict or an unspecified long-session duration.
2. **Compose the brief.** Read the course `study_track`, deadlines, lecture confusions, pending misconceptions and progress. Do not start C at pointers because its exam weight is high. Use `resource_guide` to select sources.
   - **Normal day, 90 minutes:** a starting split is 10 minutes retrieval from already-owned concepts; 20 minutes on an urgent lecture confusion or prerequisite; 45 minutes solving questions; 15 minutes on the student's error explanation and a fresh unaided check. Adjust to the actual work. With no learned cards, give their time to prerequisites. This is a sample allocation, not four mandatory rituals.
   - **Chosen question grind:** spend most of the selected block solving. Start focused, then mix learnt question types. Use `drill` for sealed timed blocks and `tutor` for discussion between blocks. Reserve visible review time or carry it forward as pending. No quota for cards or notes.
   - **Chosen paper pair:** use `drill new COURSE whole-paper count=2`, or the requested practice/synthetic alternative. State clocks and source availability. Follow the pair procedure in paper practice. Do not bolt a daily card/lecture routine on top; fit urgent work elsewhere in the chosen plan.
   During teaching, rotate question practice across active courses within available time. Full papers become a larger share during revision. Project and semester-credit deadlines are real work, not replaceable by paper counts.
3. **Run the selected activity.** Timed assessment has no AI help while sitting. Tutoring uses one hint per attempt. For new scope during a session, explain remaining time and swap work or use an explicitly changed budget; do not reject it by fiat or silently overrun.
4. **Close with evidence.** Record attempts, actual time when supplied, unfinished review, unaided-check verdict and real card/pending counts. Never infer completion time or mastery. A fresh-session grader handles sealed papers. Keep assessment content outside the vault and repos.

## Retrieval details

Only quiz concepts the student has owned; an old prefilled deck is not evidence. Prefer the installed Spaced Repetition plugin's own due queue. If parsing comments, inspect its installed format first: bidirectional cards can have separate schedules. Do not use the latest date across all directions to hide a direction already due. Never edit scheduling comments. If the due count cannot be read reliably, say it is unknown.

The selected budget is a stopping point, not a permanent ceiling on effort. Carry forward unfinished work when it expires; extend only when the student chooses to. Keep the 90-minute default unchanged.
