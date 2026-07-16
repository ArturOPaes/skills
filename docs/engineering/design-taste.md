Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=design-taste
```

```bash
npx skills update design-taste
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste)

## What it does

`design-taste` is the single source of truth for a project's *visual and interaction* design language — typography, spacing, colour and tokens, layout, depth, and motion — and the discipline of capturing it in a `DESIGN.md`.

It exists to design **against slop**: the median SaaS template — Inter everywhere, a purple gradient, cards nested in cards, bouncy easing, pure-black text — is exactly what an untended agent reaches for, and exactly what this skill refuses. It is the design-side twin of [domain-modeling](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/domain-modeling): where that keeps `CONTEXT.md` a clean *domain* glossary, this keeps `DESIGN.md` a clean *visual* one.

## When to reach for it

Type `/design-taste`, or the agent reaches for it automatically when a UI needs to look considered rather than generic, when a project's visual language needs pinning down, or when [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) or [prototype](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/prototype) needs taste to draw against.

Reach for it when the problem is the *words and rules* of design — "what makes this look machine-default, and what should it be instead?". When you instead want to be *interviewed* to settle those choices for a specific project, that's [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design), which drives this skill.

## Prerequisites

Stateful only when it's *setting* the language: it captures the project's design decisions into a `DESIGN.md` at the repo root — dials, tokens, type and motion language, and the project's anti-slop guardrails. Created lazily, when the first choice crystallises; reading it later is just a habit, not this skill.

## The three dials and the anti-slop tells

Two leading ideas make this skill click:

- **The three dials** — variance, motion, density. Most arguments about "does this look good" are really arguments about where a dial should sit: a data tool wants low variance and high density; a landing page wants the opposite. Settle the dials first, and the rest of the choices fall into place.
- **The anti-slop tells** — a fast pre-flight checklist of the patterns that mark a UI as AI-default (the AI gradient, untinted neutrals, card soup, default bounce). Run it over any drawn screen before calling it done.

Underneath sit the principles by axis and a dedicated motion discipline (the eight things a considered animation gets right). Every principle ultimately resolves to a **token** — the point where taste becomes enforceable rather than a matter of opinion.

## Where it fits

`design-taste` is **vocabulary underneath** — a reference and discipline that runs beneath the other skills rather than a step in the chain, alongside [domain-modeling](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/domain-modeling) and [codebase-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/codebase-design). It is driven by [grill-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/grill-design) (the interview that fills `DESIGN.md`), and drawn against by [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) and [prototype](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/prototype). When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
