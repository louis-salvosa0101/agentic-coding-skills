---
name: prototype
description: Build a throwaway prototype to answer a design question. Use when the user wants to sanity-check whether a state model or logic feels right, or explore what a UI should look like.
---

# Prototype

A prototype is **throwaway code that answers a question**. The question decides the shape.

## Pick a branch

Identify which question is being answered, using the user's prompt, the surrounding code, or by asking if the user is around:

- **"Does this logic / state model feel right?"** → [LOGIC.md](LOGIC.md). Build a single shareable HTML file (free-play buttons plus tabbed guided walkthroughs) that pushes the state machine through cases that are hard to reason about on paper, and that a non-developer can drive.
- **"What should this look like?"** → [UI.md](UI.md). Generate several radically different UI variations on a single route, switchable via a URL search param and a floating bottom bar.

The two branches produce very different artifacts, so getting this wrong wastes the whole prototype. If the question is genuinely ambiguous and the user isn't reachable, default to whichever branch better matches the surrounding code (a backend module → logic; a page or component → UI) and state the assumption at the top of the prototype.

## Rules that apply to both

1. **Throwaway from day one, and clearly marked as such.** Locate the prototype code close to where it will actually be used (next to the module or page it's prototyping for) so context is obvious, but name it unmistakably (e.g. include the word `prototype` in the filename or directory). Add a prominent comment at the top of every file: `// PROTOTYPE: throwaway code. Do not ship.`

2. **The question lives at the top.** Before writing any code, write down what question this prototype is answering. One sentence, visible in the UI (not just in a comment). A prototype that answers the wrong question is pure waste.

3. **No production dependencies.** A prototype must not touch the production database, call real third-party services, or modify shared state. Use local stubs, fixtures, or in-memory state only.

4. **The prototype ends with a decision.** After the user has seen and used the prototype, document the decision it produced: what was learned, what was confirmed, what was ruled out. This feeds into `/to-spec` or the grilling thread. The prototype code is then deleted or clearly marked archived.

## Integration with the main flow

```
unknown / design question
    ↓
prototype
    ↓
observe & evaluate
    ↓
decision documented
    ↓
grill-with-docs / to-spec
```

A prototype is not a ticket. It's not something to implement. It's an experiment that produces a decision, and that decision enters the spec.
