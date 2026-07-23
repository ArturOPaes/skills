Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=manual-qa
```

```bash
npx skills update manual-qa
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa)

## What it does

`manual-qa` gets a built task into a state where it can be exercised in the real app, then walks its acceptance criteria with a human.

It never declares the task validated — you do. The skill brings the app up, reaches the right state, and lays out what to check; the verdict is yours. That keeps it honest: it orchestrates the validation without asserting the result on your behalf.

## When to reach for it

You invoke this by typing `/manual-qa` — the agent won't reach for it on its own, because bringing up an app and touching an environment must be a deliberate act.

Reach for it to validate a just-built task before shipping — the human pass for what automation can't cheaply judge: whether it feels right, looks right, and holds up on real-shaped data. It is not a manual re-run of [e2e](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e): where a criterion already has a green e2e test, trust it and spend the manual effort on the gaps.

When an [open-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/open-design) **hi-fi reference** exists, that includes checking the built UI **matches it** — layout, spacing, states, components, and design. The reference is a promise about how the UI looks; divergence from it is a finding, not a matter of taste, because a reference you aligned on and then didn't build to was wasted. It closes the loop the [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) and [pre-flight](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/pre-flight) open: pre-flight confirms the open-design reference exists before the build, manual-qa confirms the shipped FE matches it after.

## Prerequisites

A way to reach a validatable state. In **local** mode that's the project's run and seed commands (the skill creates deterministic seeds for the specific flow); if the project has no seed mechanism, you agree a minimal one. In **environment** mode that's credentials for a target environment, supplied at runtime — never from committed files.

## Two modes, and the safety line

The skill asks which mode before doing anything. **Local, with seeds** is self-sufficient and safe. **Environment** reaches a live target and is not — so its rules are hard: credentials come from the runtime and are never printed or committed, the target is a confirmed choice, **never production without explicit confirmation**, and actions are read-only by default. The local seed is always preferred over mutating shared state.

## Where it fits

`manual-qa` is a validation gate you reach for after [implement](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/implement) has built a task — the human counterpart to [e2e](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e), which validates by machine. When a check fails, it hands off to [diagnosing-bugs](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/diagnosing-bugs) or files the finding through [triage](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/triage). When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
