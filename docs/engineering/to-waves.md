Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=to-waves
```

```bash
npx skills update to-waves
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-waves)

## What it does

`to-waves` partitions a large scope into a sequence of **waves** — shippable, validatable increments — before any of them is sliced into tickets.

A wave is a validation milestone, not a batch of work. Each wave is a coherent slice of value you ship and validate together, and it declares what it validates. That's the altitude above tickets: `to-waves` decides the coarse, ordered milestones; [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets) slices one wave into thin tracer bullets.

## When to reach for it

You invoke this by typing `/to-waves` — the agent won't reach for it on its own. It sits between [to-spec](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-spec) and [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets).

Reach for it when a scope is too big to slice into tickets in one pass — many features, a greenfield build — and you want to ship it in phases that each earn their keep. For a *foggy* effort where the way isn't visible yet, use [wayfinder](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/wayfinder) first: wayfinder resolves unknowns into decisions, `to-waves` phases a known scope into delivery milestones.

## Two altitudes that compose

The point that makes `to-waves` click: a wave is **fat at the validation level** (what to prove together — it can be a bigger MVP) but **built in thin tracer-bullet slices** (how to build it safe). You validate a coherent MVP and keep the tight feedback loop, because the wave sets the scope and the tickets keep each step green. A wave with no validation goal is just an arbitrary batch — that's the anti-pattern the skill exists to prevent.

## Where it fits

`to-waves` is a chain step: `grill-with-docs → to-spec → to-waves → (per wave) mockup → to-tickets → implement`. Upstream it takes the plan from [to-spec](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-spec); downstream each wave feeds [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) and [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets). Its neighbour to keep straight is [wayfinder](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/wayfinder) — fog vs phasing. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
