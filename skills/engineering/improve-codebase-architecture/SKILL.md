---
name: improve-codebase-architecture
description: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
disable-model-invocation: true
---

# Improve Codebase Architecture

Surface architectural friction and propose **deepening opportunities**: refactors that turn shallow modules into deep ones. The aim is testability and AI-navigability.

This command is _informed_ by the project's domain model and built on a shared design vocabulary:

- Call the Skill tool with "codebase-design" for the architecture vocabulary (**module**, **interface**, **depth**, **seam**, **adapter**, **leverage**, **locality**) and its principles (the deletion test, "the interface is the test surface", "one adapter = hypothetical seam, two = real"). Use these terms exactly in every suggestion, and don't drift into "component," "service," "API," or "boundary."
- The domain language in `CONTEXT.md` gives names to good seams; ADRs in `docs/adr/` record decisions this command should not re-litigate.

## Process

### 1. Explore

**Scope before you scan: YAGNI.** Deepening a module pays off by making future changes to it easier, so put extra weight on the parts of the codebase that have recently changed. Decide *where* to look before you look:

- If the user named a direction (a module, a subsystem, a pain point), take it, and skip the inference below.
- Otherwise, walk back a good stretch of the commit history (`git log --oneline`) to find the codebase's hot spots, the files and areas that keep coming up, and let those paths pull your attention first. If the changes are scattered with no clear hot spot, widen the net.

Read the project's domain glossary (`CONTEXT.md`) and any ADRs in the area you're touching first.

Then spawn a sub-agent to walk the codebase. Don't follow rigid heuristics; explore organically and note where you experience friction:

- Where does understanding one concept require bouncing between many small modules?
- Where are modules **shallow**, with an interface nearly as complex as the implementation?
- Where have pure functions been extracted just for testability, but the real bugs hide in how they're called (no **locality**)?
- Where do tightly-coupled modules leak across their seams?
- Which parts of the codebase are untested, or hard to test through their current interface?

Apply the **deletion test** to anything you suspect is shallow: would deleting it concentrate complexity, or just move it? A "yes, concentrates" is the signal you want.

### 2. Present candidates as an HTML report

Write a self-contained HTML file to the OS temp directory so nothing lands in the repo. Resolve the temp dir from `$TMPDIR`, falling back to `/tmp` (or `%TEMP%` on Windows), and write to `<tmpdir>/architecture-review-<timestamp>.html` so each run gets a fresh file. Open it for the user (`xdg-open <path>` on Linux, `open <path>` on macOS, `start <path>` on Windows; try all three in order until one succeeds).

See [HTML-REPORT.md](HTML-REPORT.md) for the exact format.

Each candidate in the report gets:
- A before/after diagram.
- A one-sentence problem statement.
- A one-sentence solution statement.
- A short list of wins (what gets easier once done).
- A recommendation strength badge: **Strong**, **Worth exploring**, or **Speculative**.

Sort by recommendation strength, strongest first. Cap at 8 candidates; quality over quantity.

### 3. Pick a candidate and grill

After the report is open, ask which candidate to pursue. Then:

- Load the `/grilling` skill.
- Run a grilling session focused on this specific candidate: design, approach, risks, integration points, seams.
- The goal of the grilling is an actionable architectural decision, not a comprehensive refactor plan.
- When the grilling settles, recommend handing off to `/to-spec` to capture the decision.

## Scope rules

This is a **survey**, not a rescue. On a genuinely old codebase it will find real candidates, but it won't untangle the mud for you. Each candidate should be a targeted improvement, not a "rewrite everything" proposal.

Preserve existing behaviour: a deepening opportunity is identified, not executed here. The execution happens through the normal flow (spec → tickets → implement).
