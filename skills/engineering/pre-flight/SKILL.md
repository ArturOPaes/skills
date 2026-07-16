---
name: pre-flight
description: Before a wave is implemented, confirm its documentation, diagrams, and hi-fi layout are current and cover it, then walk them with a human to review and adjust — the pre-build gate that greenlights implementation. Use to review everything before any code is written.
disable-model-invocation: true
---

# Pre-flight

Before a wave is built, run a **pre-flight check**: confirm the design and spec artifacts are current and *cover the wave*, walk them with a human to review and adjust, and only then greenlight the build.

The defining constraint: **it never greenlights the build — you do — and it refuses to reach that point until documentation, diagrams, and hi-fi all cover the wave.** It's the pre-build twin of [manual-qa](../manual-qa/SKILL.md): manual-qa gates a *built* task before shipping; pre-flight gates a *planned* wave before building. Both set the stage and capture your verdict; neither asserts the result for you.

## When to reach for it

You invoke this by typing `/pre-flight` — the agent won't reach for it on its own. It's the deliberate "are we ready to build this?" checkpoint, run once per wave, right before [implement](../implement/SKILL.md).

Reach for it to make sure nothing goes into code half-designed: that the docs, the diagrams, and the hi-fi layout are all current, cover the wave, and have been reviewed. It's what makes [mockup](../mockup/SKILL.md), [blueprint](../blueprint/SKILL.md), and [grill-design](../grill-design/SKILL.md) effectively non-optional — the gate won't greenlight a wave they haven't covered.

## What it checks — three artifacts, current and covering the wave

For the wave about to be built, cross-checked against its user stories and tickets:

- **Documentation** — `CONTEXT.md` covers the wave's domain terms, the hard decisions have ADRs, and (if the wave has UI) `DESIGN.md` fixes the dials, tokens, and target platforms. Docs are owned by [grill-with-docs](../grill-with-docs/SKILL.md) / [domain-modeling](../domain-modeling/SKILL.md); `DESIGN.md` by [grill-design](../grill-design/SKILL.md).
- **Diagrams** — `BLUEPRINT.md` exists and its traceability map covers the wave: every user story traces to a screen and to a ticket, with no dangling nodes. Owned by [blueprint](../blueprint/SKILL.md).
- **Hi-fi layout** — when the [mockup](../mockup/SKILL.md) is the project's canonical frontend source, **every FE definition in the wave** (screen, field, action, state) already appears in it, and its screens match the blueprint's inventory. Anything the wave puts on the frontend that the mockup lacks is a **fail** — the mockup is extended first, never bypassed at implementation time.

The gate is **coverage, not just existence**: a `BLUEPRINT.md` that omits half the wave's stories, or a wave that would build frontend absent from the mockup, is a **fail**, not a pass.

## The loop

1. **Identify the wave** — its spec, user stories, and tickets.
2. **Run the readiness check** — the three artifacts × coverage against the wave's stories and tickets. Produce a short report: what's current, what's missing or stale, per story and screen.
3. **Refresh the gaps — route, don't patch.** Send each gap to its owning skill: docs → `grill-with-docs`/`domain-modeling`, `DESIGN.md` → `grill-design`, diagrams → `blueprint`, hi-fi → `mockup`. Re-check after. **The gate never writes these artifacts itself** — it verifies and routes.
4. **Walk it with the human.** Present the consolidated dossier — the docs, the blueprint, the mockup route — and walk it so they can review and adjust before any code. Each requested change routes back to its owner, then re-check.
5. **Greenlight — the verdict is yours.** Only on the human's sign-off, with all three current and covering the wave, hand to [implement](../implement/SKILL.md). A wave with **no UI** needs no hi-fi or `DESIGN.md` — say so and check the rest. A deliberate skip is a **recorded waiver** (which artifact, and why), noted on the wave or spec — never a silent one.

Gate one wave, not the whole project.
