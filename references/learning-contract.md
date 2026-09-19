# Learning contract

Read the user's instructions and the vault's `CLAUDE.md` first. They outrank skill defaults.

## Ownership before cards

No flashcard exists until the student has rewritten the concept in their own words and the explanation is correct. Approval, copying a suggested sentence, a correct multiple-choice choice, or an agent-authored summary does not pass this gate. Ask for “what I now believe and why”; question the weak step before formatting anything.

Before that gate, log only a plain misconception, evidence pointer and next question in `<exam.corpus>/pending-learning.md` (or a user-chosen private directory outside the vault and repos), each entry opening with a stable id — `<CODE>-YYYY-MM-DD-NN`, the next free NN that day — so a later resolution can name the entry it closed. No flashcard syntax, answer draft, cloze, or scheduling comments in the pending queue. Do not quote exam questions or keys into concept notes or decks. Abstract the underlying concept in the student's words after the attempt.

After the gate, append one atomic card per distinct misconception to the existing course deck's `## 🎴 Flashcards` section, optionally under `### From <activity>`. Preserve every existing card and scheduling comment byte-for-byte. Reuse existing vocabulary and check for duplicates. Report cards actually added separately from pending misconceptions. Zero new cards is a valid outcome. Never mark learning complete just because a note or card exists.

`fitcheck` queues repeated failures in `${FITCHECK_PENDING:-${XDG_STATE_HOME:-~/.local/state}/fitcheck/pending-learning.tsv}`. Read this evidence during `duck` or `tutor`; only the student's explanation can turn it into a card. Do not treat an old auto-written card as proof of understanding.

## Teaching and assessment

During tutoring, never state the final answer to the student's problem, including a code fix in words. Use the hint ladder, one rung per attempt; a worked substep must not complete the problem. If the student is lost, use a smaller prerequisite problem and return later. End with a fresh problem solved unaided. If time runs out, record the next step as pending; respect the selected session budget and claim no mastery.

The student authors all submitted C. Read, explain, review and debug; never write graded code, a patch, or a complete algorithm that does the assignment for them. Instructor lab solutions may be inspected only after an independent attempt on that exercise, and must not be copied into submissions.

Generate a drill and seal its key in one session; grade in a fresh session that neither generated it nor taught its answers. While the student sits it, no AI help. A generated rubric is labelled as such, never called an official solution. Keep assessment text, keys, source images, answers and results outside the vault and every repository. Resolve paths and symlinks before writing. The default drills directory is `<exam.corpus>/drills`; without a safe corpus or explicit safe directory, stop and request one.

## Course priorities and time

Exam weights choose assessment coverage, not prerequisite order. If a MOC has `study_track`, read that file for the first stage without unaided evidence. Note existence and Python experience do not establish C mastery. Do not draw a sealed bank question for conversational tutoring.

`daily_cap_min` is the **default budget**, 90 minutes for Samuel, not a ban on longer chosen sessions. A request such as “two full papers” or “I have three hours” explicitly selects a longer session; state its duration and use that budget without asking permission again. Never silently extend it or permanently raise the default. State breaks and review separately from paper clocks. `slots_verified: false` means example slots are not calendar facts: offer a session-relative plan, never book an assumed evening. Protect actual commitments; resolve a specific conflict with the student when necessary. No automatic changes to enrolments or electives.

Read [paper practice](paper-practice.md) for long sessions, exposure, reserved papers and library use. The student's preference is substantial problem solving, including consecutive full papers. Cards support that work; they do not take automatic priority over an explicitly chosen paper session.

Never submit university forms, enter credentials, bypass a login, or write to a read-only research archive. Use held copies or public downloads; record missing sources honestly.
