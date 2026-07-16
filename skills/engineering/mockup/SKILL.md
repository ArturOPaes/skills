---
name: mockup
description: Build a high-fidelity, promotable mockup of a whole flow in the project's real UI stack, on a dedicated route with mock data, so you can align on it before building. Use when you want to see and validate a flow end-to-end before implementing, or seed the real build from a design.
---

# Mockup

A mockup is **high-fidelity, promotable UI that renders a whole flow** so you can walk it and align on it before building. It is the opposite of a [prototype](../prototype/SKILL.md): a prototype is throwaway code that answers one question and gets deleted; a mockup is real code you keep and grow into the feature.

The defining constraint: **the mockup is promotable, not throwaway.** It's built in the project's actual UI stack, from real components and real design tokens, with mock data behind a clear seam — so shipping it is swapping mock data for real, never a rewrite.

## When to reach for it

Reach for it when a flow is decided enough to draw but expensive to build, and you want to **validate the whole experience cheaply first** — a whole wave's worth of screens, walked end-to-end, aligned on before a line of production logic is written. It is the natural companion to a bigger MVP: mocking the flow is cheaper than building it, so it de-risks the bet.

If instead you have *one* open question — does this state machine feel right, or which of several UI directions wins — that's a throwaway [prototype](../prototype/SKILL.md), not a mockup. Prototype to *decide*; mockup to *align and seed*.

## Draw with taste, not defaults

A mockup is where the project's design taste is on show, so draw it against the [design-taste](../design-taste/SKILL.md) discipline rather than the median SaaS template. Two beats before anything is drawn:

- **Obey `DESIGN.md` if it exists.** If the project has a `DESIGN.md` (from [grill-design](../grill-design/SKILL.md)), it already fixes the dials, tokens, and motion language — build to it. If it doesn't, `design-taste`'s principles and its anti-slop checklist still apply; consider settling the three dials with the user first, and offer to capture them so the mockup seeds the design language rather than guessing it per screen.
- **Ask for references.** Point me at a folder of screenshots, a design system, component-library links (Origin UI, shadcn/ui, MagicUI), or an app to echo. Take structure, spacing rhythm, and accessibility patterns from them — but **bind every colour, radius, and token to the project's own design tokens**, never paste hardcoded styles. If the project has no tokens yet, agree a minimal token set before building.

Run the anti-slop checklist over every screen before calling the mockup done.

## Rules

1. **Promotable, never throwaway.** Real components in the project's real stack (its React framework, router, and styling system), real tokens, mock data isolated behind one clear seam (a `mock/` module or a single data hook). A reader must be able to promote it by replacing that seam, not by rewriting the screens.
2. **A whole flow, one direction.** Mock every screen and state of the flow — happy path, empty, loading, error — so it's walkable end-to-end. One polished direction, not several variations to compare (that's a prototype).
3. **Create a dedicated mockup directory.** Put the mockup in its own directory under the project's existing routing convention (e.g. a `/mockup/<flow>` route), clearly named as a mockup. Don't scatter it through production folders, and don't invent a new top-level structure.
4. **Obey the app shell.** The navigation is part of the flow: render the real sidebar/topbar with the active item, keyboard navigation, and visible focus. A flow mocked without its shell mocks the wrong thing.
5. **Semantic, accessible markup.** Use real roles, labels, and headings so the [e2e](../e2e/SKILL.md) tests written later can target them — the mockup's markup becomes the e2e's selectors. This is what threads the mockup into the traceability spine.
6. **Mock only what was decided.** The ideal input is the decided flow — the tickets or user stories from [to-tickets](../to-tickets/SKILL.md), scoped to one wave. Never invent requirements while drawing; if a screen has no decision behind it, ask before mocking it.

## Output

A **navigable route** plus a short **README** in the mockup directory that says what is mock and what still needs wiring, each item pointing at the ticket / user-story ID it satisfies. Anything the alignment surfaces as a needed change goes back to [to-tickets](../to-tickets/SKILL.md), not patched silently into the mockup — the mockup renders decisions, it doesn't make them.
