---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Before building a wave, its documentation, diagrams, and hi-fi layout should be current and reviewed — that's the `/pre-flight` gate. If it hasn't been run and the wave has design surface, flag that rather than building against half-designed artifacts.

For frontend work, build by **promoting the hi-fi mockup in place** — the shipped UI must match it (layout, spacing, states, components), not a fresh take on the same screen. Don't restyle or drift from the mockup; if something needs to change, change the mockup first (it's the canonical source). Divergence from the hi-fi mockup is a defect the `/manual-qa` gate will catch.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, use /code-review to review the work.

Commit your work to the current branch.
