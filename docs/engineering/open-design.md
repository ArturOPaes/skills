Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=open-design
```

```bash
npx skills update open-design
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/open-design)

## What it does

`open-design` generates the **hi-fi visual design** of a flow — the polished look, from the `DESIGN.md` brand contract and the mockup's screen inventory — using [Open Design](https://github.com/nexu-io/open-design), an AI design engine that turns a brief and a design system into real HTML/CSS artifacts. The output is a **binding reference**: the shipped frontend is required to match it.

It is a reference, not promote-in-place code. Unlike a [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) — real components in the project's stack that you grow into the shipped feature — an open-design artifact is a standalone file you build *toward*, the way a team builds toward a Figma. That is the trade it makes: a fast, high-polish visual target, at the cost of the real frontend being implemented separately and checked against it.

## When to reach for it

Type `/open-design`, or the agent reaches for it in the overview phase once a flow's screens are settled — the low-fi mockup on the `mockup+hi-fi` path, or the blueprint's screens and the user stories on `hi-fi-only`. Reach for it when you want the polished look fixed before building.

It **replaces the old hi-fi mockup**, and a project picks its design path in `DESIGN.md` (during [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design)): **`mockup+hi-fi`** splits the job — [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) owns **structure and coverage** (low-fi, in the stack), `open-design` owns the **look**; **`hi-fi-only`** drops the mockup and makes `open-design` the sole design artifact the frontend is built toward. For *one* throwaway visual question — which of several directions wins — use [prototype](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/prototype) instead.

## Prerequisites

Open Design set up and running locally (the AI design engine that produces the artifact), and a settled `DESIGN.md` (from [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design)) plus the mockup's screen inventory to feed the brief. Without a brand contract the output drifts to a generic template.

## Structure here, look there

The leading idea is the **binding reference**. The mockup gives the structure that ships; open-design gives the look that ships; implementation converges the two by promoting the mockup in place and styling it to match the reference. Because the reference lives outside the stack, the discipline is to keep it and the build in sync: a change to the look goes back through `/open-design` and re-review, never a silent restyle during implementation — otherwise the target and the build disagree and the [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa) match check becomes meaningless.

## It's working if

- A hi-fi artifact exists covering the same screens the blueprint (and the mockup, on `mockup+hi-fi`) enumerate, reachable at the project's stable design path.
- It was generated from `DESIGN.md`, not a generic template — it speaks the project's dials, tokens, and motion.
- [pre-flight](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight) can point to it as the visual target before greenlighting a polished build.
- The shipped UI is checked against it, not against a fresh take on the screen.

## Where it fits

`open-design` is part of the **whole-product overview**, drawn upfront before implementation — `grill-design → mockup → open-design → blueprint → pre-flight`. Its closest neighbour is [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup): they split the design job (structure vs. look) and it consumes the mockup's screens; it draws against the [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste) vocabulary, and [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa) checks the shipped FE against it. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
