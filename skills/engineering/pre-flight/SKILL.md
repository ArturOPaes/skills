---
name: pre-flight
description: Before any implementation begins, confirm the whole product's documentation, diagrams, and mockup are current and cover every user story, then walk them with a human to review and adjust — the overview gate that greenlights the build. Use to review everything before any code is written.
disable-model-invocation: true
---

# Pre-flight

Before any implementation begins, run a **pre-flight check** on the whole-product overview: confirm the design, diagrams, and mockup are current and *cover every user story*, walk them with a human to review and adjust, and only then greenlight the build.

The defining constraint: **it never greenlights the build — you do — and it refuses to reach that point until documentation, diagrams, and the mockup all cover the whole product.** It's the pre-build twin of [manual-qa](../manual-qa/SKILL.md): manual-qa gates *built* work before shipping (per wave, or once at the end); pre-flight gates the *planned* product before building begins. Both set the stage and capture your verdict; neither asserts the result for you.

## When to reach for it

You invoke this by typing `/pre-flight` — the agent won't reach for it on its own. It's the deliberate "is the whole thing designed enough to build?" checkpoint, run **once** — after the overview is drawn ([grill-design](../grill-design/SKILL.md) → [mockup](../mockup/SKILL.md) → [blueprint](../blueprint/SKILL.md)) and before implementation begins.

Reach for it to make sure nothing goes into code half-designed: that the docs, the diagrams, and the mockup are all current, cover **every** user story, and have been reviewed. It's what makes mockup, blueprint, and grill-design effectively non-optional — the gate won't greenlight a product they haven't covered. Once it greenlights, the build phase (optional [to-waves](../to-waves/SKILL.md) → [to-tickets](../to-tickets/SKILL.md) → [implement](../implement/SKILL.md)) runs without re-gating — the invariant that no frontend exists outside the mockup keeps the overview true as the build proceeds.

## What it checks — three artifacts, current and covering the whole product

Cross-checked against **all** the spec's user stories:

- **Documentation** — `CONTEXT.md` covers the product's domain terms, the hard decisions have ADRs, and (if it has UI) `DESIGN.md` fixes the dials, tokens, and target platforms. Docs are owned by [grill-with-docs](../grill-with-docs/SKILL.md) / [domain-modeling](../domain-modeling/SKILL.md); `DESIGN.md` by [grill-design](../grill-design/SKILL.md).
- **Diagrams** — `BLUEPRINT.md` exists and its traceability map covers the product: every user story traces to a screen, with no dangling nodes (the ticket column fills later, in the build). Owned by [blueprint](../blueprint/SKILL.md).
- **Mockup** — when the [mockup](../mockup/SKILL.md) is the project's canonical frontend source, **every FE definition** (screen, field, action, state) already appears in it, and its screens match the blueprint's inventory. Anything the build would later put on the frontend that the mockup lacks is a **fail** — the mockup is extended first, never bypassed at implementation time. And if the intent is a polished FE, the mockup must be at **hi-fi** here: it's the visual reference the shipped UI is required to match, and [manual-qa](../manual-qa/SKILL.md) checks that match after the build. A low-fi mockup greenlights structure and coverage only — visual fidelity then becomes a **recorded, deferred step** (promote low → hi before shipping), never an unstated gap.

The gate is **coverage, not just existence**: a `BLUEPRINT.md` that omits half the product's stories, or a mockup missing a screen a story needs, is a **fail**, not a pass.

## The loop

1. **Identify the overview scope** — the spec and **all** its user stories.
2. **Run the readiness check** — the three artifacts × coverage against every user story. Produce a short report: what's current, what's missing or stale, per story and screen.
3. **Refresh the gaps — route, don't patch.** Send each gap to its owning skill: docs → `grill-with-docs`/`domain-modeling`, `DESIGN.md` → `grill-design`, diagrams → `blueprint`, mockup → `mockup`. Re-check after. **The gate never writes these artifacts itself** — it verifies and routes.
4. **Walk it with the human.** Present the consolidated dossier — the docs, the blueprint, the mockup route — and walk it so they can review and adjust before any code. Each requested change routes back to its owner, then re-check.
5. **Greenlight — the verdict is yours.** Only on the human's sign-off, with all three current and covering the whole product, greenlight the build. A product with **no UI** needs no mockup or `DESIGN.md` — say so and check the rest. A deliberate skip is a **recorded waiver** (which artifact, and why), noted on the spec — never a silent one.

Gate the overview **once**, before the build begins — not per wave.
