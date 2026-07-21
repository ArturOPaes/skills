---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Before building a wave, its documentation, diagrams, low-fi mockup, and open-design visual reference should be current and reviewed — that's the `/pre-flight` gate. If it hasn't been run and the wave has design surface, flag that rather than building against half-designed artifacts.

For frontend work, build by **promoting the low-fi mockup in place and styling it to match the [open-design](../open-design/SKILL.md) reference** — the shipped UI takes its structure from the mockup (the canonical source) and its look from the reference (layout, spacing, states, components), not a fresh take on the same screen. Don't drift from either; if the structure needs to change, change the mockup first; if the look needs to change, go back through `/open-design`. Divergence from the reference is a defect the `/manual-qa` gate will catch.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, use /code-review to review the work.

Commit your work to the current branch.
