Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=grill-design
```

```bash
npx skills update grill-design
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design)

## What it does

`grill-design` interviews you relentlessly about a project's *visual and interaction* design language — the three dials, the references, the type/colour/motion tokens — one decision at a time, and writes each choice into a `DESIGN.md` as it's settled.

It grills the *design*, not the domain. Where [grill-with-docs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-with-docs) sharpens what the thing *is* and leaves `CONTEXT.md`, this one settles what the thing *looks and feels like* and leaves `DESIGN.md`. Same grilling engine, a different subject and a different paper trail.

## When to reach for it

You invoke this by typing `/grill-design` — the agent won't reach for it on its own.

Reach for it when a project's look is undecided and you want to fix its visual language before drawing screens — so a [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) renders *a* design instead of guessing one per screen. If you only want the taste vocabulary and rules without being interviewed, use [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste) directly; if the thing you need to settle is the *domain*, not the look, use [grill-with-docs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-with-docs).

## Prerequisites

Stateful — it writes a `DESIGN.md` at the repo root as it grills: the dials (variance, motion, density), chosen references, tokens, and the project's anti-slop guardrails. Created lazily, so nothing needs scaffolding up front, but you need to be somewhere it's safe to write the file.

## The grill

The engine is the same **grill** as its siblings: a relentless, one-question-at-a-time walk down the decision tree, a recommended answer offered for every question, facts looked up rather than asked. What makes this variant its own skill is the subject — it walks the three **dials** and the token language rather than domain terms — and where the answers go: into `DESIGN.md`, inline, the moment each choice crystallises. It drives [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste) to do the capturing, exactly as `grill-with-docs` drives `domain-modeling`.

## Where it fits

`grill-design` is the design-side on-ramp to the per-wave design step: settle the visual language here, then [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) renders a flow against it. Its closest neighbours are [grill-with-docs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-with-docs), its domain-side twin, and [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste), the discipline it drives. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
