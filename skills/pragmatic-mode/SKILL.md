---
name: pragmatic-mode
description: Work in pragmatic mode on any code change. Close functional requirements with the user, prototype UI choices, build the smallest extension of existing systems, prove it with visual QA evidence and a compact E2E suite, self-review for complexity, and finish with a PR. Use for /pragmatic-mode, $pragmatic-mode, or when repository instructions ask for this workflow.
---

# Pragmatic mode

Once invoked, this mode governs every task for the rest of the session, not
only the current message. Reread this file when a new task starts or after
context is compacted.

## Route the task

- **Feature**: new or changed user-facing behavior. Run steps 1 to 6.
- **Other code change**: bug fix, refactor, backend-only work, configuration.
  Run steps 3 to 6.
- **Read-only question**: answer it. No flow.

Copy the steps that apply into the todo list before doing anything else. With
no todo tool, keep the list in your reply and update it at each step.

## Gates

Align with the user at the start, deliver to them at the end, and work
autonomously in between. The start has two hard stops, both before production
code: the requirements answers (step 1) and the prototype pick (step 2). The
end is the PR.

- Skip step 1 when the request already closes the functional requirements. Ask
  only what is still open.
- Skip step 2 when the change has no UI or UX surface.
- After the gates, run to the PR without asking. Actions the agreed
  requirements call for proceed, irreversible ones included. Make every other
  implementation choice yourself and report it in the final reply.
- Stop only when the work needs a functional decision that the request and the
  agreed requirements do not settle. Ask it as in step 1, then continue.

## Flow

1. **Requirements.** Read the code the feature touches first, so you never ask
   what the code already answers. Ask at most five questions, the ones that
   close the functional requirements: who acts, what outcome they get, which
   rules decide edge cases, and what must stay unchanged. Stop and wait.
2. **Prototypes.** Build up to three variants that reflect the answers. Ground
   them in the real frontend code (its components, styles, and routes) with
   minimal implementation and no complete backend integration. For each
   variant, attach screenshots and the interaction sequence to the chat, so
   the user can pick without running the app. Stop and wait for the pick. The
   picked variant seeds step 3. Delete the others.
3. **Implement.** Read [references/design.md](references/design.md) before
   writing code. Make the smallest change that meets the requirements, by
   extending what exists.
4. **Verify.** Read [references/testing.md](references/testing.md) before adding,
   changing, or running tests. Do a visual QA pass over the real app with
   browser use, or computer use when browser use is unavailable, and attach
   the captures to the chat. Delivery is not done without them.
5. **Self-review.** Read `../pragmatic-review/SKILL.md` from this file's folder
   and apply it to your own diff. Favor findings that trim the change or remove
   complexity. Apply each simplification that preserves the outcome, then
   rerun the verification it affects.
6. **PR.** Follow [references/pr.md](references/pr.md).

## Delegation

A subagent does not inherit this skill. Start every subagent brief with:
`Read <absolute path of this file> and follow its policies as a delegate. Skip
the gates and the PR; do only the task below.` Then give the goal and the task.
You own the delegate's work: review its diff before building on it.

## Final reply

Lead with the goal. Then give the functional change, the QA captures, each
added test and the completed outcome it proves, what the self-review trimmed,
the PR link, and any material limits on what was verified.
