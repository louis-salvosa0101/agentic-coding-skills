---
name: wayfinder
description: Plan a huge chunk of work (more than one agent session can hold) as a shared map of decision tickets on your issue tracker, and resolve them one at a time until the way to the destination is clear.
disable-model-invocation: true
---

A loose idea has arrived, too big for one agent session, and wrapped in fog: the way from here to the **destination** isn't visible yet. Wayfinding is about finding that way, not charging at the destination. This skill charts the way as a **shared map** on the repo's issue tracker, then works its **decision tickets** (questions whose resolution is a decision, not slices of a build to execute) one at a time until the route is clear.

The destination varies per effort, and naming it is the first act of charting: it shapes every ticket. It might be a spec to hand off and iterate on, a decision to lock before planning starts, or a change made in place like a data-structure migration. The map is domain-agnostic: engineering work, course content, whatever fits the shape.

## Plan, don't do

Wayfinder is **planning** by default: each ticket resolves a decision, and the map is done when the way is clear, with nothing left to decide before someone goes and does the thing. The pull to just do the work is usually the signal you've reached the edge of the map and it's time to hand off. An effort can override this in its **Notes**, carrying execution into the map itself, but absent that, produce decisions, not deliverables.

## Refer by name

Every map and ticket is an issue, so it has a **name**: its title. In everything the human reads (narration, the map's Decisions-so-far), refer to it by that name, never by a bare id, number, or slug. A wall of `#42, #43, #44` is illegible; names read at a glance. The id and URL don't vanish; a name wraps its link, but they ride _inside_ the name, never stand in for it.

## The Map

The map is a single issue on this repo's issue tracker, labelled `wayfinder:map`, the canonical artifact. Its tickets are child issues of the map.

The map is an **index**, not a store. It lists the decisions made and points at the tickets that hold their detail; a decision lives in exactly one place, its ticket, so the map never restates it, only gists it and links.

**Where the map, its child tickets, blocking, and frontier queries physically live is tracker-specific.** The issue tracker should have been provided to you. If not, tell the user to run `/setup-skills`. Consult the tracker doc's "Wayfinding operations" section for how _this_ repo expresses them. If no tracker has been provided, default to the local-markdown tracker.

### The map body

The whole map at low resolution, loaded once per session. Open tickets are **not** listed: they are open child issues, found by query.

```markdown
## Destination

<what reaching the end of this map looks like: the spec, decision, or change this effort is finding its way to. One or two lines; every session orients to it before choosing a ticket.>

## Notes

<domain; skills every session should consult; standing preferences for this effort>

## Decisions so far

<!-- the index: one line per closed ticket, enough to judge relevance, then zoom the link for the detail the ticket holds -->

- [<closed ticket title>](link): <one-line gist of the answer>

## Not yet specified

<!-- see "Fog of war": in-scope fog you can't ticket yet; graduates as the frontier advances -->

## Out of scope

<!-- see "Out of scope": work ruled beyond the destination; closed, never graduates -->
```

### Tickets

Each ticket is a **child issue** of the map; the tracker's issue id is its identity. Its body is the question, sized to one 100K token agent session:

```markdown
## Question

<the decision or investigation this ticket resolves>
```

Each ticket carries a `wayfinder:<type>` label, one of `research`, `prototype`, `grilling`, `task` (see [Ticket Types](#ticket-types)).

A session **claims** a ticket by assigning it to the dev driving the map, **first**, before any work, so concurrent sessions skip it. That assignee _is_ the claim: an open, unassigned ticket is unclaimed.

Blocking uses the tracker's **native** dependency relationship: essential because it renders the frontier _visually_ in the tracker's own UI, so the human sees what's takeable without opening the map. Only a tracker that lacks native blocking falls back to a body convention. A ticket is **unblocked** when every ticket blocking it is closed; the **frontier** is the open, unblocked, unclaimed children, the edge of the known.

The answer isn't part of the body; it's recorded on resolution (see [Work through the map](#work-through-the-map)). Assets created while resolving a ticket are linked from the issue, not pasted in.

## Ticket Types

Every ticket is either **HITL** (human in the loop, worked _with_ a human who speaks for themselves) or **AFK** (agent works alone, human reviews after). The type is recorded in the `wayfinder:<type>` label. Choose the type when you create the ticket:

| Label | Type | Description |
|---|---|---|
| `wayfinder:research` | AFK | Agent investigates a question and documents findings. Use `/research`. |
| `wayfinder:prototype` | AFK | Agent builds a throwaway prototype to answer a design question. Use `/prototype`. |
| `wayfinder:grilling` | HITL | A grilling session to resolve ambiguity, with a human. Use `/grill-with-docs`. |
| `wayfinder:task` | Either | Execution: write code, migrate data, update config. Use `/implement` for AFK tasks. |

## Charting the map

### First session

1. Name the destination. One or two sentences, in the map body.
2. Start ticketing from the frontier: what do you need to know or decide _first_ before the rest can be determined? These are the initial unblocked tickets.
3. Sketch the fog: add a "Not yet specified" section to the map for things you know are in scope but can't ticket yet.
4. Publish the map and its initial tickets to the tracker.

### Subsequent sessions

1. Load the map. Read the Destination and Decisions so far.
2. Query the frontier: open, unblocked, unclaimed tickets.
3. Claim one ticket.
4. Work it (using the skill its label names).
5. Record the answer in the ticket's resolution comment, then close the ticket.
6. Update the map: add a one-line gist to "Decisions so far" linking the closed ticket.
7. Create any new tickets the answer reveals. Promote fog to tickets when they become specific enough to size.
8. Release the claim.

## Work through the map

The map is done when the frontier is empty and the fog section is empty: nothing left to decide.

**Hand off, don't execute.** When the map clears, merge onto the main flow at `/to-spec`, which collapses the linked decisions into a buildable plan, then `/to-tickets` and `/implement`. Looping the map straight into implementation skips the spec and loses the structured handoff; don't do it.

## Fog of war

Fog is in-scope work you know exists but can't ticket yet because the shape depends on something undecided. Fog lives in "Not yet specified." As decisions close, fog graduates into tickets. Fog that turns out to be out of scope moves to "Out of scope," never to tickets.

## Out of scope

Out-of-scope items are things ruled beyond the destination: related work that would be useful but isn't on the way to the current destination. Record them in the map's "Out of scope" section and close them permanently. A future map can pick them up if the destination changes.
