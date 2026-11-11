---
name: pragmatic-review
description: Explain functional changes, assess complexity file by file, challenge unnecessary machinery, and evaluate architectural fit with evidence.
disable-model-invocation: true
---

# Pragmatic review

Invoking this skill requests the complete review below, including the functional
explanation and complexity assessment when there are no actionable findings.
Resolve the PR, branch, diff, or merge conflict from the invocation and current
conversation; ask only when the target is ambiguous. Keep the work to analysis
unless implementation or publishing a review is also requested.

## 1. Establish actual behavior

Pin the reviewed head and base. Read the request, applicable `AGENTS.md` or
`CLAUDE.md`, architectural guidance, and connected code. Trace materially changed
operations through their callers and owners, including related repositories and
feature branches where needed. Use the implementation to establish behavior;
treat the PR description as intent to verify.

Establish what users, operators, and other clients experience before and after.
Include relevant state, failure/recovery paths, compatibility, configuration,
and deployment effects. Separate required outcomes from implementation choices,
and merged source from deployed or physically verified behavior. For merge
conflicts, establish both sides' intent and what the resolution must preserve.

**Complete when:** every changed operation has a supported before/after account;
remaining gaps require a product decision or unavailable evidence.

## 2. Account for and challenge complexity

Inspect every changed file, including tests, documentation, configuration, and
generated files. Identify its contribution to the functional outcome and the
complexity added or removed: branches, state, abstractions, dependencies,
coupling, duplication, and operating or maintenance work. Use diff counts as
context, not as a substitute for this assessment.

For each added mechanism, inspect the closest existing owner, operation, library,
or framework capability. Compare reuse or extension with the proposed structure
through writers, consumers, synchronization, and recovery. Distinguish necessary
behavior from avoidable implementation. Make simpler alternatives concrete:
what to remove, inline, consolidate, or delegate, and why the same outcome holds.
Justify retained complexity rather than recommending deletion for its own sake.

Judge tests by the meaningful regression they catch, its likelihood and
consequence, and whether existing coverage already protects the outcome.
Include fixtures, mocks, and production parameters or abstractions added solely
for testing in their cost. For trivial rendering or formatting, prefer an
assertion in an existing integration scenario; recommend removing standalone
tests that merely exercise framework states or mirror the implementation,
along with any unnecessary test-only production seams. Justify keeping extra
coverage by the application risk it protects, not by passing tests or a list
of success, failure, and pending cases.

Distinguish documentation that explains a non-obvious operating constraint
from restating the code. Follow the repository's own testing and documentation
policies.

Assess ownership, boundaries, dependencies, public contracts, and existing
patterns against documented architectural rules. Cite the rule and concrete
location for a violation; label inferred conventions and personal design
preferences separately. Distinguish introduced problems from inherited debt,
and honor accepted product tradeoffs.

**Complete when:** every changed file is accounted for, and each material
mechanism has a justified keep/simplify/remove assessment and an architectural
basis, or a specific unresolved question.

## 3. Validate and prioritize

For candidate findings, establish the reachable trigger, independently supported
expectation, concrete consequence, and attribution to the change. Try to disprove
them using actual guards, constraints, and recovery. When one issue reveals a
pattern, check the rest of the change and its consumers for the same pattern.

Use focused checks under project guidance to settle material uncertainty.
Distinguish source inspection, automated results, runtime observations, and
physical or production acceptance. Weigh credible occurrence, severity, recovery,
and scope against correction cost. Separate functional defects, worthwhile
simplifications, and architectural violations; keep merge-blocking status
distinct from urgency. Revise conclusions when evidence or clarified intent
changes their basis.

**Complete when:** findings and simplifications are supported and worth acting
on, or narrowed to the exact evidence or decision needed. Keep discarded
candidates and routine investigation internal.

## 4. Deliver the complete review

Lead with a short overall verdict, then provide these five parts in order.
Scale detail to the change and the user's requested brevity; a findings list
alone does not satisfy this skill.

1. **Functional explanation.** Explain the changes in plain language, primarily
   from the user's or operator's perspective: what happens today, what happens
   afterward, and practical consequences. Introduce internal mechanics only
   where they explain the behavior, a tradeoff, or an operating requirement.
2. **File-by-file complexity.** Use a table with file, functional contribution,
   complexity added/removed, and keep/simplify/remove assessment with a reason.
   Include additions/deletions when available. Account for every changed file;
   group only equivalent mechanical or generated changes, naming the files.
3. **Pushback.** Identify which complexity earns its cost and which can be
   reduced while preserving the outcome. Give the smallest coherent alternative
   and its tradeoff. Include useful simplifications even when they are not bugs;
   refer to the table rather than repeating it.
4. **Architectural fit.** State whether the changes respect and contribute to
   this codebase's established architecture. Support concrete violations or
   improvements with rules and locations. If documentation is absent, say what
   evidence supports an inferred convention instead of inventing a standard.
5. **Recommendation and evidence.** State whether to merge, simplify, or fix
   first. Prioritize actionable findings with location, trigger, consequence,
   justified severity, and smallest correction. Separate blocking findings from
   optional improvements. Report meaningful verification and material limits;
   state plainly when there are no actionable findings.

**Complete when:** the user can understand the feature, account for its cost,
judge its architectural fit, and decide what should happen next without asking
for these explanations separately.
