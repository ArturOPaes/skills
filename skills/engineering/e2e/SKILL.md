---
name: e2e
description: Write end-to-end browser tests from a ticket's acceptance criteria or user stories, driving the real UI. Use when a ticket is marked for e2e, or to backfill end-to-end coverage onto work that shipped without it.
---

# E2E

Turn acceptance criteria into **end-to-end tests that drive the real UI**. Each acceptance criterion — each Given/When/Then — becomes one scenario walked through the browser from the user's perspective.

The defining constraint: **the acceptance criterion is the test.** You don't invent behaviours to cover; you take the ones the ticket or user story already promised and make them executable. The criterion is the spec, the e2e is its runnable form, and the two are linked by the ticket ID.

## When to reach for it — and how it differs from tdd

Type `/e2e`, or the agent reaches for it when a ticket's test level is **e2e** (see [to-tickets](../to-tickets/SKILL.md)) or when you ask to add end-to-end coverage.

It is not [tdd](../tdd/SKILL.md). `tdd` tests at internal **seams** — integration and unit, red-green while you build a slice. `e2e` tests the **assembled flow through the browser**, after it exists, from the outside. Reach for `tdd` while building; reach for `e2e` to prove the whole behaviour a ticket promised — or to **backfill** e2e onto a feature that shipped without it, the common "start without e2e, add it later" path.

## The loop

1. **Find the source criteria.** The ticket's acceptance criteria, or the user story's Given/When/Then. If there are none, ask which behaviours to cover — never invent them.
2. **Use the project's existing runner.** Playwright, Cypress, whatever is already wired. Don't introduce a new e2e stack without asking.
3. **One criterion → one scenario.** *Given* arranges state through the app's real entry points (or a clearly-named scratch seed seam), *When* is the user's action through the UI, *Then* is an assertion on what the user can observe.
4. **Target semantic selectors.** Assert against roles, labels, and accessible names — not brittle CSS or test-only hooks where a real role exists. This survives refactors and matches what a [mockup](../mockup/SKILL.md) already rendered, so a mockup-seeded flow is e2e-ready.
5. **Tag each test with the ticket / user-story ID.** The tag is the traceability link — criterion ↔ test — so coverage is checkable against the spec.
6. **Run them, and report honestly.** A criterion isn't covered until its scenario is green. Say which criteria are now covered, and which you skipped and why. Never mark a criterion covered on a test that didn't run.

## Anti-patterns

- **Side-channel assertions** — checking the database instead of what the user sees. e2e verifies the flow through its public surface; if you assert through the back door you've written an integration test wearing an e2e costume.
- **Brittle selectors** — coupling to CSS classes or DOM structure, so the test breaks on a refactor that changed no behaviour.
- **Duplicating seam tests** — re-testing at the browser what a `tdd` seam test already covers. Keep e2e for the assembled, user-visible flow; leave the fine-grained logic to `tdd`.
