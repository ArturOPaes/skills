---
name: blueprint
description: Synthesize a spec's user stories, the domain model, and the UI into a BLUEPRINT.md — a set of Mermaid diagrams (screen inventory, navigation map, user flow, traceability, states, sequence, data) that give a macro, connected view of a flow before implementation. No interview — it draws what's already decided.
disable-model-invocation: true
---

# Blueprint

Draw a **blueprint** of a flow: one `BLUEPRINT.md` of Mermaid diagrams that give a macro, *connected* view — how user stories, screens, decisions, and tickets fit together — before a line is implemented. Like [to-spec](../to-spec/SKILL.md) and [to-tickets](../to-tickets/SKILL.md), this does **not** interview you. It synthesises what's already decided into a picture; it never invents requirements.

The blueprint's job is connection. A spec lists user stories, a mockup shows screens, ADRs record decisions, tickets slice the work — but each lives apart. The blueprint is the one artifact that **wires them into a single traceable map**, so a developer can see the whole flow at a glance and trace any story to the screen that serves it, the decision that shaped it, and the ticket that builds it.

## What it reads

Gather from whatever already exists — the more sources present, the richer the blueprint:

- **User stories & implementation decisions** — the spec from [to-spec](../to-spec/SKILL.md) (`## User Stories`, `## Implementation Decisions`).
- **Domain & decisions** — `CONTEXT.md` and the ADRs under `docs/adr/` (the vocabulary and hard choices from [domain-modeling](../domain-modeling/SKILL.md)).
- **Screens & UI** — the [mockup](../mockup/SKILL.md)'s routes/screens and `DESIGN.md` from [grill-design](../grill-design/SKILL.md); if no mockup exists yet, infer the screens from the user stories and mark them provisional.
- **Tickets** — the tickets from [to-tickets](../to-tickets/SKILL.md), if they exist yet. If they don't, draw everything else and leave the ticket column of the traceability map to be filled once tickets are sliced.

**Draw only what a source backs.** Where a source is missing, draw what you can and mark the gap explicitly (`%% TODO: no mockup yet — screens provisional`) rather than inventing. A blueprint that invents screens or stories has stopped synthesising and started deciding — that work belongs back in the owning skill.

## The artifact

A single **`BLUEPRINT.md`** beside the spec — `.scratch/<feature-slug>/blueprint.md` on a local tracker, or the configured docs area — holding **all** the diagrams. Everything is **Mermaid** so it renders inline on GitHub and in any markdown viewer, and stays diffable in git.

The whole thing hangs on **stable, cross-referable IDs** used identically in every diagram:

- `US-<n>` — user story _n_ from the spec.
- `ADR-<n>` — architectural decision record _n_.
- `#<n>` — ticket _n_.
- `Screen:<Name>` — a screen, named exactly as the mockup/navigation map names it.

Reuse of these IDs across diagrams is what lets the **traceability map** close the loop instead of being a fresh, disconnected drawing.

## Process

1. **Gather the sources** above. Read the spec's user stories and decisions, the ADRs, the mockup's screens, and any tickets.
2. **Build the screen inventory first** — the backbone table (screen → features → the `US-<n>` each satisfies). Every other diagram hangs off it, so getting the screens and their IDs right here makes the rest fall out.
3. **Draw each diagram** into `BLUEPRINT.md`, in the order in [DIAGRAMS.md](DIAGRAMS.md), reusing the IDs from step 2.
4. **Close the loop.** The traceability map must connect real IDs on every edge — every screen traces back to at least one `US-<n>`, and forward to the `#<n>` that builds it (or a marked gap). A dangling node is a finding: surface it.
5. **Present it and route the gaps.** Show the blueprint. Anything it surfaces as a *missing decision* (a story with no screen, a screen with no story, an untraced ADR) goes back to the owning skill — [to-spec](../to-spec/SKILL.md) for scope, [grill-design](../grill-design/SKILL.md) for UI — never patched silently into the blueprint.

## Rules

- **Synthesise, don't decide.** Same discipline as `to-spec`: draw what's known, route what isn't. The blueprint renders decisions; it doesn't make them.
- **One file, stable IDs, real cross-references.** The value is the connection — IDs that match across diagrams and back to the spec/tickets.
- **A view, not a source.** The blueprint is cheap to regenerate as the spec and tickets evolve; keep it regenerable rather than hand-maintaining it. When the spec changes, redraw — don't patch.
- **Mark every gap.** A `%%` comment on a provisional node beats a confident invention.

## The diagrams

The full catalogue — what each answers, when to include it, and a Mermaid skeleton — is in [DIAGRAMS.md](DIAGRAMS.md): the **screen inventory**, **navigation map**, **screen detail map / wireflow** (each screen's fields and actions, with actions linked to the screens they lead to), **user flow**, **traceability map**, **screen states**, **sequence**, **data (ER)**, and **system design** (topology + bottlenecks) diagrams. The first five are the connective backbone and are always drawn; the last four are drawn per-flow when the flow's complexity earns them.

The **screen detail map** (a wireflow — a wireframe's content joined to the flow) is the one to walk field-by-field with the user before slicing tickets — it shows every field and action on a screen, so a missing field or an undefined action surfaces as a question here rather than mid-implementation.

## Where it fits

`blueprint` is part of the **whole-product overview**, drawn upfront before any implementation — after the spec and the mockup, and before the pre-flight gate:

```txt
to-spec → grill-design → mockup → blueprint → pre-flight → (build)
```

It reads the spec's stories, the mockup's screens, and the domain's ADRs, and hands the developer a connected macro view of the whole product before the build begins; the tickets that `to-tickets` cuts later fill its traceability map's ticket column. It extends the same **traceability spine** that [mockup](../mockup/SKILL.md) (semantic markup) and [e2e](../e2e/SKILL.md) (selectors) build — the blueprint is the story-to-screen-to-ticket layer of it. Reach for it standalone any time you want to visualise an existing spec. When you're unsure which skill or flow fits, [ask-tutu](../ask-tutu/SKILL.md) routes you.
