---
name: v0-app-prompt
description: Generate a high-quality, structured implementation prompt for v0 by Vercel from user requirements, specs, screenshots, or code context.
disable-model-invocation: true
---

# v0 App Prompt

Transform application requirements, specifications, screenshots, existing UI, or rough ideas into an **optimized, implementation-ready prompt for v0 by Vercel**.

This skill does NOT build the application itself; it produces a structured prompt that can be directly pasted into v0.

## Workflow & Composition

```
                    User Input (Idea / Spec / Screenshot / Code)
                                        │
                                        ▼
                             Ambiguity Check
                     ┌──────────────────┴──────────────────┐
                     │ (Ambiguous)                         │ (Clear)
                     ▼                                     ▼
           /grill-with-docs or /to-spec             Analyze Requirements
                     │                                     │
                     └──────────────────┬──────────────────┘
                                        ▼
                             Inspect Context & Tech
                                        │
                                        ▼
                             v0-app-prompt Synthesis
                                        │
                                        ▼
                               Copyable v0 Prompt
```

If inputs are severely ambiguous (e.g. "make a dashboard"), route to `/grill-with-docs` or `/to-spec` first before generating the v0 prompt.

If UI logic or state machine design is uncertain, route to `/prototype` first.

## Process

### 1. Analyze Requirements & Context

Identify the input level:
- **Level 1 — Rough Idea**: Infer safe visual/structural defaults; ask brief clarifying questions if critical product logic is missing.
- **Level 2 — Requirements**: Synthesize user stories and feature lists into layout sections.
- **Level 3 — Specification**: Extract pages, components, layout hierarchy, and state rules from the spec.
- **Level 4 — Existing Codebase**: Inspect existing UI framework (e.g., Next.js App Router, Tailwind CSS, shadcn/ui, Lucide icons), color tokens, and layout patterns to enforce continuity.
- **Level 5 — Screenshot / Image**: Define what to preserve (layout, hierarchy, visual style, spacing) versus tech stack adaptation.
- **Level 6 — Existing v0 App Modification**: Explicitly separate **Preserve** (existing navigation, color palette, data flow) from **Change** (new components, altered layouts).

### 2. Formulate Structured v0 Prompt

Select only relevant sections from the v0 Prompt Specification:

- **Goal & Purpose**: What the UI/app does and who uses it.
- **Layout & Hierarchy**: Page structure, navigation bar/sidebar, container max-widths, card grid layouts.
- **Visual Design & Design System**: Modern administrative/consumer interface aesthetic, typography scale, color roles, spacing scale, border radius, elevation/shadows.
- **Component Breakdown**: Key UI components, tables, forms, cards, modals.
- **Interactions & Behavior**: Form submissions, modal triggers, tab switches, filter operations.
- **UI States**: Initial, loading, empty, error, active/selected, disabled, hover, focus.
- **Responsive Behavior**: Specific desktop, tablet, and mobile layouts (e.g., desktop 3-column grid → mobile 1-column stack with drawer navigation).
- **Accessibility**: Semantic HTML elements, ARIA labels, keyboard focus rings, color contrast.
- **Technical & Data Constraints**: Next.js App Router, TypeScript, Tailwind CSS, shadcn/ui, Lucide icons, mock data structures.
- **Preservation Rules** (for modifications): Explicit lists of components and designs v0 must NOT alter.
- **Acceptance Criteria**: Concrete, observable conditions to check in v0's generated preview.

### 3. Review & Output Format

Return output formatted into three clear sections:

1. **Analysis Summary**: Short summary of target intent and detected context.
2. **Assumptions & Open Questions** (optional): Any safe inferences made or unresolved questions.
3. **v0 Prompt**: A markdown code block clearly fenced for copy-pasting directly into v0.

```markdown
Build/modify [APPLICATION / PAGE / COMPONENT].

## Goal
[Purpose and target user]

## Layout & Hierarchy
[Detailed structural layout]

## Visual Design
[Design language, colors, spacing, radius]

## Components
[List of UI components and their specifications]

## Interactions & Behavior
[Expected user interactions]

## UI States
[Loading, empty, error, success, active states]

## Responsive Behavior
[Desktop, tablet, mobile layouts]

## Accessibility
[Semantic HTML, focus states, contrast]

## Technical & Data Constraints
[Framework, libraries, mock data schemas]

## Preservation (if modifying)
[What NOT to change]

## Acceptance Criteria
[Verifiable criteria]
```

## Rules & Anti-Patterns

1. **No Vague Prompts**: Avoid generic instructions like "make a modern dashboard". Be explicit about visual hierarchy, spacing, density, and component structure.
2. **Do Not Dictate Implementation Mechanics**: Provide specifications and API contracts, but let v0 handle internal React JSX rendering.
3. **Protect Existing Code**: For modification prompts, explicitly list preserved components so v0 does not rewrite unrelated parts of the app.
4. **Scale to Task**: Simple component requests get concise prompts; full application requests get complete structured prompts.
