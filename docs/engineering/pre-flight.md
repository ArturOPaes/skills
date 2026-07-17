Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=pre-flight
```

```bash
npx skills update pre-flight
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight)

## What it does

`pre-flight` is the checkpoint run **once, before any implementation begins**: it confirms the whole product's documentation, diagrams, and mockup are current and *cover every user story*, walks them with a human to review and adjust, and only then greenlights the build.

It never greenlights the build — you do — and it refuses to reach that point until documentation, diagrams, and the mockup all cover the whole product. That refusal is the whole value: it's what turns the otherwise-optional design steps into a real gate, so nothing goes into code half-designed.

## When to reach for it

You invoke this by typing `/pre-flight` — the agent won't reach for it on its own. It's the deliberate "is the whole thing designed enough to build?" moment: run once, after the overview is drawn (grill-design → mockup → blueprint) and before implementation begins.

Reach for it to review everything before any code exists. It's the pre-build twin of [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa): where manual-qa is the human gate *after* the build (per wave, or once at the end), pre-flight is the human gate *before* the build begins. If instead you need to *produce* one of the artifacts it checks, reach for that artifact's own skill — pre-flight verifies and routes, it never writes them.

## Prerequisites

It reads, rather than writes, the product's artifacts: `CONTEXT.md` and the ADRs, `DESIGN.md`, the `BLUEPRINT.md`, and the [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) route, cross-checked against **all** the spec's user stories. Those are produced upstream by [grill-with-docs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-with-docs), [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design), [blueprint](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/blueprint), and mockup — a product that reaches pre-flight with none of them will mostly fail the gate, which is the point.

## Coverage, not existence

The check that makes it a gate rather than a checklist is **coverage**. A `BLUEPRINT.md` that omits half the product's user stories, or a mockup missing a screen a story needs, is a **fail** — the artifact exists but doesn't cover the product. Each gap routes back to its owning skill to refresh (docs → grill-with-docs, `DESIGN.md` → grill-design, diagrams → blueprint, mockup → mockup); pre-flight re-checks, never patches. A product with no UI legitimately needs no mockup or `DESIGN.md`; a deliberate skip is a **recorded waiver**, not a silent one.

When the FE is meant to be polished, the gate also requires the mockup to be at **hi-fi** — it's the visual reference the build is required to match, and [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa) checks that match after. A low-fi mockup passes on structure and coverage but defers visual fidelity (promote low → hi before shipping), recorded, never left as an unstated gap.

## It's working if

- It reports readiness per user story and screen, not just "docs: yes / no".
- A missing screen or an untraced story blocks the greenlight instead of sliding through.
- Gaps go back to the owning skill; pre-flight itself writes none of the artifacts.
- The build doesn't start until you sign off — and once it does, the build phase runs without re-gating.

## Where it fits

`pre-flight` is the **gate between the overview and the build** — run once, on the whole product:

```txt
grill-design → mockup → blueprint → pre-flight → (build: [to-waves] → to-tickets → implement)
```

It's the last step of the overview, and the reason [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup), [blueprint](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/blueprint), and [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design) are effectively non-optional — it won't greenlight a product they haven't covered. After it greenlights, the invariant that no frontend exists outside the mockup keeps the overview true as the build proceeds. Its twin is [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa), the human gate on the far side of the build. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
