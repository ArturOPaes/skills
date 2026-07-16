Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=blueprint
```

```bash
npx skills update blueprint
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/blueprint)

## What it does

`blueprint` synthesises a spec's user stories, the domain model, and the UI into a single `BLUEPRINT.md` of Mermaid diagrams — a macro, connected view of a flow you can read before implementing it.

It does not interview you. Like [to-spec](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-spec) and [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets), it only draws what's already decided — and its defining value is *connection*: the spec lists stories, the mockup shows screens, ADRs record decisions, tickets slice work, but each lives apart, and the blueprint is the one artifact that wires them into a single traceable map.

## When to reach for it

You invoke this by typing `/blueprint` — the agent won't reach for it on its own.

Reach for it once a flow is specced (and ideally mocked) and you want the whole thing visible before slicing tickets — the menus, the user's path, and the story→screen→ADR→ticket web on one page. It's also the way to **backfill** diagrams onto a spec that already shipped without them. If what you need is the *spec itself*, use [to-spec](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-spec); if you need a *built, walkable* UI rather than a diagram of it, use [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup).

## Prerequisites

Stateful — it writes a `BLUEPRINT.md` beside the spec (`.scratch/<feature-slug>/blueprint.md` locally, or the configured docs area). It reads whatever exists — the spec's user stories, `CONTEXT.md` and the ADRs, the mockup's screens and `DESIGN.md`, and the tickets — and draws only what a source backs, marking the gaps. The richer those inputs, the richer the blueprint; with just a spec it still draws the backbone.

## The diagrams, and the IDs that connect them

Eight diagram types, all Mermaid so they render inline on GitHub. Five are the **connective backbone**, always drawn — the screen inventory, the navigation map, the **screen detail map** (each screen's fields and actions, with actions linked to where they lead — the one to review field-by-field), the user flow, and the **traceability map** (the diagram the skill exists for). Three are **per-flow**, drawn when complexity earns them — screen states, a sequence diagram, and a data/ER diagram.

What makes them a *blueprint* rather than seven unrelated drawings is a set of **stable IDs** — `US-<n>`, `ADR-<n>`, `#<n>`, `Screen:<Name>` — reused identically across every diagram and back to the spec and tickets. That shared vocabulary is what lets the traceability map close the loop: every screen traces back to a story and forward to the ticket that builds it, and any node that doesn't is a finding routed back to the owning skill.

## It's working if

- Every diagram is Mermaid in one `BLUEPRINT.md`, rendering inline.
- The same `US-<n>` / `Screen:<Name>` / `#<n>` IDs appear across diagrams and match the spec and tickets.
- The traceability map has no dangling nodes — or the dangling ones are surfaced as gaps, not hidden.
- Nothing is invented: screens or stories with no source are marked provisional, not asserted.

## Where it fits

`blueprint` is a **per-wave visual synthesis step**, sitting between the spec/mockup and the tickets:

```txt
to-spec → [mockup] → blueprint → to-tickets → implement
```

It hands the developer a connected macro view to slice [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets) against, and extends the same traceability spine that [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) and [e2e](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e) build. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
