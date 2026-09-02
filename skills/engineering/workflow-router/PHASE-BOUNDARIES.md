# Phase Boundaries

Context hygiene for the main flow: when to compact or clear between phases.

## Why phase boundaries matter

The model reasons sharply within a **smart zone**: roughly the first 100-150k tokens of a context window. Past that, it still produces output but at reduced quality. Phase boundaries are the planned points where you act on this, rather than letting quality silently degrade.

## Boundary rules

### Between grilling and to-spec

Stay in **one unbroken context window**. The spec synthesises what the grilling produced. Clearing here throws that away.

### Between to-spec and to-tickets

Stay in **one unbroken context window**. The tickets are slices of the spec; they need to know the spec.

### Between to-tickets and implement

**Clear context here.** Each ticket's `/implement` run starts fresh, working only from the ticket. This is intentional: the ticket is self-contained and the implement context should not be polluted by the grilling thread.

### During a multi-session wayfinder effort

Each decision ticket is its own session: claim, work, resolve, clear. The map on the issue tracker is the shared state between sessions; keep it current.

## Compacting vs clearing

**Compact** (Claude Code: `/compact`) when you want to continue in the same session but have passed the smart zone. It summarises the history and frees headroom. Use it between phases when you're still in the same broad flow.

**Clear** (Claude Code: `/clear`) when the current task is done and the next task is genuinely independent. Use it between `/implement` sessions.

If you're unsure which to use: compact within a flow, clear between flows.
