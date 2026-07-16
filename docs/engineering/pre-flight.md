Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=pre-flight
```

```bash
npx skills update pre-flight
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight)

## What it does

`pre-flight` is the checkpoint run once per wave, right before implementation: it confirms the wave's documentation, diagrams, and hi-fi layout are current and *cover* it, walks them with a human to review and adjust, and only then greenlights the build.

It never greenlights the build — you do — and it refuses to reach that point until documentation, diagrams, and hi-fi all cover the wave. That refusal is the whole value: it's what turns the otherwise-optional design steps into a real gate, so nothing goes into code half-designed.

## When to reach for it

You invoke this by typing `/pre-flight` — the agent won't reach for it on its own. It's the deliberate "are we ready to build this?" moment, once per wave, immediately before [implement](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/implement).

Reach for it to review everything before any code exists. It's the pre-build twin of [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa): where manual-qa is the human gate *after* a task is built, pre-flight is the human gate *before* a wave is built. If instead you need to *produce* one of the artifacts it checks, reach for that artifact's own skill — pre-flight verifies and routes, it never writes them.

## Prerequisites

It reads, rather than writes, the wave's artifacts: `CONTEXT.md` and the ADRs, `DESIGN.md`, the `BLUEPRINT.md`, and the [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) route, cross-checked against the wave's user stories and tickets. Those are produced upstream by [grill-with-docs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-with-docs), [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design), [blueprint](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/blueprint), and mockup — a wave that reaches pre-flight with none of them will mostly fail the gate, which is the point.

## Coverage, not existence

The check that makes it a gate rather than a checklist is **coverage**. A `BLUEPRINT.md` that omits half the wave's user stories, or a mockup missing a screen a ticket builds, is a **fail** — the artifact exists but doesn't cover the wave. Each gap routes back to its owning skill to refresh (docs → grill-with-docs, `DESIGN.md` → grill-design, diagrams → blueprint, hi-fi → mockup); pre-flight re-checks, never patches. A wave with no UI legitimately needs no hi-fi or `DESIGN.md`; a deliberate skip is a **recorded waiver**, not a silent one.

## It's working if

- It reports readiness per user story and screen, not just "docs: yes / no".
- A missing screen or an untraced story blocks the greenlight instead of sliding through.
- Gaps go back to the owning skill; pre-flight itself writes none of the artifacts.
- The build doesn't start until you sign off.

## Where it fits

`pre-flight` is the **gate between planning and building**:

```txt
… → blueprint → to-tickets → pre-flight → implement
```

It's the last step before [implement](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/implement), and the reason [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup), [blueprint](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/blueprint), and [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design) are effectively non-optional — it won't greenlight a wave they haven't covered. Its twin is [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa), the human gate on the far side of the build. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
