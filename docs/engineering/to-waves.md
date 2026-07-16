Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=to-waves
```

```bash
npx skills update to-waves
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-waves)

## What it does

`to-waves` sequences the **build** into a series of ordered **waves** — shippable, validatable milestones — after the whole-product overview is locked, then slices one wave at a time into tickets.

A wave is a validation milestone, not a batch of work. Each wave is a coherent slice of value you ship and validate together, and it declares what it validates. It sequences *delivery*, not design — the mockup and blueprint already cover the whole product from the overview, so `to-waves` decides only the coarse, ordered milestones the build ships in; [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets) slices one wave into thin tracer bullets.

## When to reach for it

You invoke this by typing `/to-waves` — the agent won't reach for it on its own. It's **optional** and lives in the build phase, after [pre-flight](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight) greenlights the overview and before [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets).

Reach for it when the greenlit scope is big enough that shipping in ordered milestones beats one big drop; a small scope skips it and goes straight to tickets. For a *foggy* effort where the way isn't visible yet, use [wayfinder](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/wayfinder) first: wayfinder resolves unknowns into decisions, `to-waves` phases a known, already-designed scope into delivery milestones.

## Two altitudes that compose

The point that makes `to-waves` click: a wave is **fat at the validation level** (what to prove together — it can be a bigger MVP) but **built in thin tracer-bullet slices** (how to build it safe). You validate a coherent MVP and keep the tight feedback loop, because the wave sets the scope and the tickets keep each step green. A wave with no validation goal is just an arbitrary batch — that's the anti-pattern the skill exists to prevent.

## Where it fits

`to-waves` is an **optional build-phase step**, downstream of the overview gate:

```txt
… → blueprint → pre-flight → [to-waves] → (per wave) to-tickets → implement → manual-qa
```

Upstream it takes the greenlit plan; downstream each wave feeds [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets), whose frontend tickets promote slices of the already-built [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup). Its neighbour to keep straight is [wayfinder](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/wayfinder) — fog vs phasing. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
