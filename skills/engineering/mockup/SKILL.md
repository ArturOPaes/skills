---
name: mockup
description: Build a high-fidelity, promotable mockup in the project's real UI stack with mock data. Optional, but when adopted it becomes the canonical source of the frontend — every feature mocked and promoted in place, covering all user stories, ADRs, diagrams, and design definitions, with nothing on the frontend that isn't in the mockup first. Use to align on the UI before building and to seed the real build.
---

# Mockup

A mockup is **high-fidelity, promotable UI that renders a whole flow** so you can walk it and align on it before building. It is the opposite of a [prototype](../prototype/SKILL.md): a prototype is throwaway code that answers one question and gets deleted; a mockup is real code you keep and grow into the feature.

The defining constraint: **the mockup is promotable, not throwaway.** It's built in the project's actual UI stack, from real components and real design tokens, with mock data behind a clear seam — so shipping it is swapping mock data for real, never a rewrite.

## The canonical frontend source

The mockup is **optional** — but the moment you adopt it, it becomes the **single source of truth for the frontend**. From then on it isn't a per-wave sketch; it's the complete FE canvas that every feature is mocked into and promoted from.

- **It covers everything decided.** Every user story, every ADR with a frontend consequence, the [blueprint](../blueprint/SKILL.md)'s diagrams, and the `DESIGN.md` definitions all resolve to something in the mockup. If it's a frontend decision, it has a home here.
- **Implementation happens *in* it, in place.** "Promotable, not throwaway" is what makes this work: features aren't rebuilt elsewhere — the mock data behind each screen is swapped for real, wave by wave, ticket by ticket. The mockup and the shipped frontend converge into the same code.
- **Waves and tickets slice it, they don't bypass it.** Breaking the layout into incremental tickets is expected — implement a screen, then a section, then a detail. But a ticket promotes a *slice of the mockup*; it never introduces frontend the mockup doesn't already contain.
- **The invariant: nothing on the frontend that isn't in the mockup.** Every FE definition — a field, a screen, an action, a state — must appear in the mockup *before* it's implemented. If implementation needs something the mockup lacks, add it to the mockup first (and trace it back to its owning decision — a user story, an ADR, `DESIGN.md`), never invent it in production code. This is the invariant [pre-flight](../pre-flight/SKILL.md) checks before greenlighting a build.

## When to reach for it

Reach for it when a flow is decided enough to draw but expensive to build, and you want to **validate the whole experience cheaply first** — a whole flow, up to the entire frontend once adopted as the base, walked end-to-end and aligned on before a line of production logic is written. It is the natural companion to a bigger MVP: mocking the flow is cheaper than building it, so it de-risks the bet.

If instead you have *one* open question — does this state machine feel right, or which of several UI directions wins — that's a throwaway [prototype](../prototype/SKILL.md), not a mockup. Prototype to *decide*; mockup to *align and seed*.

## Draw with taste, not defaults

A mockup is where the project's design taste is on show, so draw it against the [design-taste](../design-taste/SKILL.md) discipline rather than the median SaaS template. Two beats before anything is drawn:

- **Obey `DESIGN.md` if it exists.** If the project has a `DESIGN.md` (from [grill-design](../grill-design/SKILL.md)), it already fixes the dials, tokens, and motion language — build to it. If it doesn't, `design-taste`'s principles and its anti-slop checklist still apply; consider settling the three dials with the user first, and offer to capture them so the mockup seeds the design language rather than guessing it per screen.
- **Ask for references.** Point me at a folder of screenshots, a design system, component-library links (Origin UI, shadcn/ui, MagicUI), or an app to echo. Take structure, spacing rhythm, and accessibility patterns from them — but **bind every colour, radius, and token to the project's own design tokens**, never paste hardcoded styles. If the project has no tokens yet, agree a minimal token set before building.

Run the anti-slop checklist over every screen before calling the mockup done.

## Rules

1. **Promotable, never throwaway.** Real components in the project's real stack (its React framework, router, and styling system), real tokens, mock data isolated behind one clear seam (a `mock/` module or a single data hook). A reader must be able to promote it by replacing that seam, not by rewriting the screens.
2. **The whole frontend, one direction.** Mock every screen and state — happy path, empty, loading, error — so each flow is walkable end-to-end; and when the mockup is the adopted base, every decided feature is present, not just one wave's. One polished direction, not several variations to compare (that's a prototype).
3. **Create a dedicated mockup directory.** Put the mockup in its own directory under the project's existing routing convention (e.g. a `/mockup/<flow>` route), clearly named as a mockup. Don't scatter it through production folders, and don't invent a new top-level structure.
4. **Obey the app shell.** The navigation is part of the flow: render the real sidebar/topbar with the active item, keyboard navigation, and visible focus. A flow mocked without its shell mocks the wrong thing.
5. **Semantic, accessible markup.** Use real roles, labels, and headings so the [e2e](../e2e/SKILL.md) tests written later can target them — the mockup's markup becomes the e2e's selectors. This is what threads the mockup into the traceability spine.
6. **Mock only what was decided — but mock all of it.** Every screen traces to a decision — a user story, an ADR, a `DESIGN.md` definition. Never invent requirements while drawing; if a screen has no decision behind it, ask before mocking it. As the adopted base the mockup covers *all* decided features, not one wave — the scope grows with the decisions, never ahead of them.

## Output

A **navigable route** plus a short **README** in the mockup directory that says what is mock and what still needs wiring, each item pointing at the ticket / user-story ID it satisfies. As the canonical source, that README doubles as a **coverage map**: every screen and major element traced to the user story / ADR / `DESIGN.md` definition it satisfies, so a gap — a decided feature with no screen, or a screen with no decision — is visible at a glance. Anything the alignment surfaces as a needed change goes back to [to-tickets](../to-tickets/SKILL.md), not patched silently into the mockup — the mockup renders decisions, it doesn't make them.
