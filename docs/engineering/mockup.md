Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=mockup
```

```bash
npx skills update mockup
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup)

## What it does

`mockup` builds a high-fidelity render of a whole flow — every screen and state — in the project's real UI stack, on a dedicated route with mock data, so you can walk it and align on it before building.

The mockup is promotable, not throwaway. It's real components and real design tokens with mock data isolated behind one clear seam, so shipping it is swapping that seam for real data — never a rewrite. That single fact separates it from a prototype and is the reason it's worth building at production fidelity.

## The canonical frontend source

Using a mockup is optional — but adopt one and it becomes the **single source of truth for the frontend**, not a per-wave sketch. Every feature is mocked into it (covering the user stories, ADRs, diagrams, and `DESIGN.md`) and, because it's promotable, implemented *in* it in place — the mock data is swapped for real, wave by wave, ticket by ticket, so the mockup and the shipped frontend converge into the same code.

That yields one hard invariant: **nothing on the frontend that isn't in the mockup first.** Waves and tickets slice the mockup into incremental work, but a ticket only ever promotes a slice that already exists; anything new gets added to the mockup (and traced to its owning decision) before it's built, never invented in production code. It's the invariant [pre-flight](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight) checks before greenlighting a build.

## When to reach for it

Type `/mockup`, or the agent reaches for it when a flow is decided enough to draw but expensive to build and you want to validate the whole experience cheaply first.

Reach for it to see and align on a flow — a whole wave's worth of screens — before writing production logic. For *one* open question — does this state model feel right, which of several directions wins — use [prototype](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/prototype) instead: prototype to decide and discard, mockup to align and seed.

## Drawn against taste

A mockup is where the project's design taste is on show, so `mockup` draws against the [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste) discipline rather than the median SaaS template. If a `DESIGN.md` exists (from [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design)), it obeys it — dials, tokens, motion language already fixed; if not, the taste principles and the anti-slop checklist still apply, and it's worth settling the language first so the mockup seeds it rather than guessing per screen.

It still asks you for references — screenshots, a design system, component-library links — taking structure and accessibility patterns from them but binding every colour and token to the project's own design tokens, never pasting hardcoded styles. References seed the design; they aren't a source of truth.

## It's working if

- The mockup lives in its own route/directory, clearly marked, in the project's existing routing convention.
- Its data sits behind one seam you could swap for real data without touching the screens.
- Its markup uses real roles and labels, so [e2e](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e) can target it later.
- Any change the alignment surfaces goes back to the tickets — the mockup renders decisions, it doesn't invent them.

## Where it fits

`mockup` is part of the **whole-product overview**, built upfront before implementation — `grill-design → mockup → blueprint → pre-flight` — and when adopted it's the canonical frontend source every feature is mocked into and promoted from, wave by wave. Its closest neighbour is [prototype](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/prototype), the throwaway counterpart it's often confused with, and it feeds [e2e](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e), whose selectors its markup becomes. When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
