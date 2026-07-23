---
name: tutu-loop-validate
description: The validation satellite of tutu-loop — proves each system role's complete happy path unattended, walking it in the browser (interim verdict by the agent, not a human), matching the hi-fi reference, running the critical-qa critique, and backing it with e2e. Self-contained; consolidates manual-qa (unattended), critical-qa, and e2e. Invoked only by the tutu-loop coordinator.
disable-model-invocation: true
---

# tutu-loop · validate

The validation step of [tutu-loop](../SKILL.md), run **per role**. It proves each role's **complete happy path** two ways — an unattended manual walk in the browser and passing e2e — which together are the loop's exit test. It is **self-contained**: it consolidates the manual walk, the critical-qa critique, and e2e into one satellite, referencing only its siblings — never the tutu skills.

## Unattended — the agent gives the interim verdict

The source manual-QA discipline never declares a task validated — a human does. **tutu-loop overrides that for the per-role pass:** it runs unattended, so the **agent gives the interim verdict** for each role, screen by screen. The single *human* validation happens once, at the end, at the coordinator's gate — never here. This satellite orchestrates the walk and records findings; the human sees the result at the final gate, not per role.

- **Local only.** Bring the app up on localhost and drive it through Orca's embedded browser. Never touch a real environment; never deploy.
- **From zero, with seeds.** Discover the project's run/seed commands, create deterministic seed data for the role's flow (agree a minimal seed mechanism if none exists — never invent unrealistic data silently), and start from **signup/onboarding**, not a pre-seeded dashboard.

## Match the hi-fi reference

Validating a role includes comparing the shipped FE **against the [design](../design/SKILL.md) reference** — layout, spacing, states, components. The reference is a promise about how the UI looks; **divergence from it is a finding, not taste** (a reference you aligned on and didn't build to was wasted). Where they differ, the built UI is what's wrong — unless the difference is itself a decision, which routes back to [design](../design/SKILL.md) first.

## The critique — find what the criteria never named

Walking the happy path proves what was *asked for* got built; it's blind to **what's missing** and **what's merely weak**. So on every screen run the critical-qa critique — generative probes, kept as a separate pass from conformance:

1. **CRUD-completeness** — for every noun the role manages, can they create/read/update/delete it where they'd expect? A value shown-but-not-editable, an item listed-but-not-removable — a gap.
2. **Action → consequence** — perform each state-changing action and confirm the UI reflects it **everywhere it appears** (counters, badges, quotas, lists). For a third-party handoff you can't complete for real (payment, auth, e-sign): drive it in the provider's **sandbox**, **simulate the success callback** (its test webhook), and verify the downstream consequence landed.
3. **State quality** — for every loading/empty/error/disabled/over-limit state, is it a *designed* state or a raw default (placeholder-as-loading, a browser `alert()`, a blank empty screen)?
4. **Native / unstyled controls** — flag anything the user would recognise as "the browser's," not "the product's."
5. **Shortest path & friction** — count the steps to each outcome; dead ends, detours, and re-entry of what the app already knows are gaps in the *experience*.

Separate **gap** (missing → route as a coverage fix or a new decision) from **improvement** (present but weak → route back through the definition first, never invent product silently). Each finding carries a **recommended fix** and a **trace** to the definition node.

## Journeys and personas — the per-role happy path, in full

The exit test is **every role's complete happy path**, so walk each role end-to-end from zero:

- **From zero** — signup, onboarding, empty states, the first successful action — where the deepest gaps hide.
- **Every role** the definition names (client, provider, admin, member…) — a flow that works for one role and breaks for another is a gap only per-role testing finds. Enumerate the roles from the specs/ADRs before walking them; a defined role never walked is an unfinished pass.
- **Cross-role handoffs** — where one role acts on another (invite, assignment, shared resource), validate **both sides**: the action, *delivery* (did the other role receive it), and the receiver accepting and **getting in with the right access**.
- **Permissions, both directions** — each role can do everything it's allowed *and* is blocked from everything it isn't. Test the negative, not just the happy allow.

## e2e — the machine proof

Back the walk with end-to-end tests: **the acceptance criterion is the test.**

1. **One criterion → one scenario**, driven through the real UI: *Given* arranges state through real entry points (or a named scratch seed), *When* is the user's action, *Then* asserts on what the user observes.
2. **Happy path first** — the role's complete happy path must go green; that's the floor and the exit test.
3. **Semantic selectors** — assert against roles, labels, and accessible names, not brittle CSS; this survives refactors and matches the design's markup.
4. **Tag each test with the ticket / US id** — the traceability link, criterion ↔ test.
5. **Use the project's existing runner** (Playwright/Cypress/whatever is wired); don't introduce a new stack without asking.
6. **Critique for gaps as you write** — the state/permission/persona cases the criteria never mention are raised as **gap findings** that route back to the specs/[build](../build/SKILL.md), not invented as passing tests.

Avoid the anti-patterns: side-channel assertions (checking the DB instead of what the user sees), brittle selectors, duplicating seam tests already covered by [build](../build/SKILL.md)'s TDD, and rubber-stamping thin criteria (a gap left unflagged is a gap shipped).

## Output

Per role: `happy-path: manual-green + e2e-green` (or the findings that keep it red), each finding thin, independent, with a recommended fix and a trace. A gap routes to a [build](../build/SKILL.md) fix; an improvement routes back through the definition first. When **every** role is green both ways, the exit test is met — the coordinator raises the single human validation gate. Findings the loop can't resolve **escalate** (`blocked`), never hang.
