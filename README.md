# Agentic Coding Skills

A focused, highly opinionated collection of agent skills implementing a complete end-to-end engineering workflow.

This repository provides a coherent software-development methodology built for coding agents (Claude Code, Codex, Cursor, Antigravity, etc.). It brings the core Engineering capabilities of Matt Pocock's skills repository to full functional parity while maintaining a clean, project-neutral architecture and strict engineering focus.

---

## Architecture & Concepts

Skills fall into two distinct execution tiers:

1. **User-Invoked Orchestration**: Slash commands (`/workflow-router`, `/grill-with-docs`, `/to-spec`, etc.) typed directly by the human operator to initiate and orchestrate multi-step engineering workflows.
2. **Model-Invoked Discipline**: Reusable primitive skills (`tdd`, `code-review`, `diagnosing-bugs`, `domain-modeling`, `codebase-design`, `prototype`, etc.) automatically reached for by the agent or invoked to enforce rigorous technical standards.

---

## Canonical Engineering Workflow

```
                    USER REQUEST
                         │
                         ▼
                  workflow-router
                         │
            ┌────────────┼────────────┐
            │            │            │
           NEW          BUG       EXISTING CODE
            │            │            │
            ▼            ▼            ▼
       grill-with-docs  diagnosing   improve-codebase-
            │             bugs         architecture
            ▼            │            │
         to-spec          │            │
            │              │            │
            ▼              │            │
       to-tickets          │            │
            │              │            │
            └──────────────┼────────────┘
                           ▼
                       implement
                           │
                           ▼
                          tdd
                           │
                           ▼
                      code-review
                           │
                           ▼
                         done
```

### Specialized Pathways

- **v0 UI Prompting**: Idea / `to-spec` / Screenshot → `v0-app-prompt` → v0 generation → inspect / `prototype` → `implement`
- **Large / Foggy Projects**: `wayfinder` → `research` / `domain-modeling` / `codebase-design` → `to-spec` → `to-tickets` → `implement`
- **UI / Logic Uncertainty**: `prototype` → learn & observe → `grill-with-docs` / `to-spec`
- **Merge & Rebase Conflicts**: `resolving-merge-conflicts` → intent analysis → resolution → `tdd` test verification
- **Human-Only Operational Steps**: `wizard` → interactive bash script → human execution → agent verification

---

## The Complete Engineering Skill Map

| Skill | Category | Type | Purpose |
|---|---|---|---|
| [`workflow-router`](./skills/engineering/workflow-router/SKILL.md) | Routing | User-invoked | Route arbitrary engineering requests to the appropriate skill flow |
| [`setup-skills`](./skills/engineering/setup-skills/SKILL.md) | Setup | User-invoked | Configure project issue tracker, triage labels, and domain doc layout |
| [`grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) | Specification | User-invoked | Sharpen an idea by interview while capturing domain terms & ADRs |
| [`to-spec`](./skills/engineering/to-spec/SKILL.md) | Specification | User-invoked | Synthesize conversation context into a formal spec published to tracker |
| [`to-tickets`](./skills/engineering/to-tickets/SKILL.md) | Slicing | User-invoked | Break spec into tracer-bullet vertical slices with explicit blocking edges |
| [`implement`](./skills/engineering/implement/SKILL.md) | Execution | User-invoked | Build tickets using TDD at testing seams and close out with code review |
| [`triage`](./skills/engineering/triage/SKILL.md) | Triage | User-invoked | Move incoming issues and PRs through a state machine of triage roles |
| [`wayfinder`](./skills/engineering/wayfinder/SKILL.md) | Planning | User-invoked | Chart multi-session large projects as decision maps on issue tracker |
| [`improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) | Refactoring | User-invoked | Surface deepening opportunities and present visual HTML candidate reports |
| [`v0-app-prompt`](./skills/engineering/v0-app-prompt/SKILL.md) | UI Generation | User-invoked | Generate optimized implementation prompts for v0 by Vercel |
| [`grilling`](./skills/productivity/grilling/SKILL.md) | Primitive | Model-invoked | Relentless interview primitive for stress-testing decisions and ideas |
| [`domain-modeling`](./skills/engineering/domain-modeling/SKILL.md) | Domain | Model-invoked | Build and sharpen project domain glossary (`CONTEXT.md`) and ADRs |
| [`codebase-design`](./skills/engineering/codebase-design/SKILL.md) | Design | Model-invoked | Vocabulary and principles for designing deep modules and seams |
| [`research`](./skills/engineering/research/SKILL.md) | Research | Model-invoked | Investigate questions against primary sources and capture cited findings |
| [`tdd`](./skills/engineering/tdd/SKILL.md) | Quality | Model-invoked | Red-green-refactor loop at defined integration and testing seams |
| [`diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md) | Debugging | Model-invoked | Gated, evidence-driven bug diagnosis loop with tight feedback loops |
| [`prototype`](./skills/engineering/prototype/SKILL.md) | Experiment | Model-invoked | Disposable prototyping (logic state-machines or UI variants) |
| [`code-review`](./skills/engineering/code-review/SKILL.md) | Quality | Model-invoked | Two-axis code review (Standards + Specification) for diffs |
| [`resolving-merge-conflicts`](./skills/engineering/resolving-merge-conflicts/SKILL.md) | Git | Model-invoked | Intent-preserving git merge/rebase conflict resolution |
| [`wizard`](./skills/engineering/wizard/SKILL.md) | Operations | Model-invoked | Generate interactive bash scripts for manual human operations |

---

## Setup & Installation

```bash
npx skills@latest add louis-salvosa0101/agentic-coding-skills
```

After installation, run `/setup-skills` once per repository to configure your issue tracker (GitHub, GitLab, or Local Markdown) and domain documentation paths.

---

## Key Differences from Upstream (`mattpocock/skills`)

1. **Strict Engineering Scope**: Excludes non-engineering productivity, social media, writing beats, framework-specific ecosystems, or personal workflow skills.
2. **Project-Neutral Naming**: Replaces author-specific skill names (`ask-matt` → `workflow-router`, `setup-matt-pocock-skills` → `setup-skills`).
3. **Decoupled Architecture**: All skills reference generic project configuration pointers (`/setup-skills`, `.scratch/` or tracker configs) rather than hardcoded personal defaults.
