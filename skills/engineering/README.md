# Engineering

A complete, opinionated engineering workflow for agentic software development.

## User-invoked orchestration

Skills reachable only when explicitly invoked by the user to orchestrate a workflow:

- [workflow-router](./workflow-router/SKILL.md): Ask which skill or flow fits your situation. A router over the engineering skills in this repository.
- [setup-skills](./setup-skills/SKILL.md): Configure the project issue tracker, triage labels, and domain-doc layout. Run once per repository.
- [grill-with-docs](./grill-with-docs/SKILL.md): Clarify a change while updating the domain model (`CONTEXT.md` and ADRs).
- [to-spec](./to-spec/SKILL.md): Turn the current conversation into a specification and publish it to the issue tracker.
- [to-tickets](./to-tickets/SKILL.md): Split a plan or specification into tracer-bullet tickets with explicit blocking edges.
- [implement](./implement/SKILL.md): Build a specification or set of tickets using TDD at pre-agreed seams and code review.
- [triage](./triage/SKILL.md): Move incoming issues and PRs through a state machine of triage roles.
- [wayfinder](./wayfinder/SKILL.md): Plan a huge, multi-session effort as a shared map of decision tickets on the issue tracker.
- [improve-codebase-architecture](./improve-codebase-architecture/SKILL.md): Scan a codebase for deepening opportunities, present a visual HTML report, and grill through chosen candidates.
- [v0-app-prompt](./v0-app-prompt/SKILL.md): Generate a structured, implementation-ready prompt for v0 by Vercel from requirements, specs, screenshots, or code context.

## Model-invoked engineering discipline

Composable supporting skills invoked by the model or user when specific technical discipline is needed:

- [grilling](../productivity/grilling/SKILL.md): Relentless interview primitive to stress-test plans, decisions, or ideas.
- [domain-modeling](./domain-modeling/SKILL.md): Build and sharpen the domain glossary (`CONTEXT.md`) and Architectural Decision Records (ADRs).
- [codebase-design](./codebase-design/SKILL.md): Shared vocabulary for designing deep modules, interfaces, seams, and adapters.
- [research](./research/SKILL.md): Research against primary sources and record cited findings.
- [tdd](./tdd/SKILL.md): Build vertical slices test-first through a red-green-refactor loop.
- [diagnosing-bugs](./diagnosing-bugs/SKILL.md): Evidence-driven debugging loop with tight feedback loops.
- [prototype](./prototype/SKILL.md): Build throwaway prototypes (logic state-machines or UI variations) to answer design questions.
- [code-review](./code-review/SKILL.md): Two-axis review (Standards + Specification) of a diff.
- [resolving-merge-conflicts](./resolving-merge-conflicts/SKILL.md): Intent-preserving git merge and rebase conflict resolution.
- [wizard](./wizard/SKILL.md): Generate interactive bash wizards for steps only humans can perform.
