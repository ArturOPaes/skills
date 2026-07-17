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

## Read the criteria critically — find the gaps as you write

Encoding criteria into tests is also the moment you can see what the criteria *miss*. So as you write, run the [critical-qa](../critical-qa/SKILL.md) critique over the flow — its probes (state quality, CRUD-completeness, action→consequence, permissions, personas) — and treat whatever fires as a **gap in the criteria, not a test to invent**:

- **Validate the happy path first.** The primary Given/When/Then must go green — that's the floor, and the scenario every criterion earns.
- **Then probe around it.** The empty / error / over-limit state the criteria never mention; the action on screen with no criterion behind it; the permission direction (allowed vs. **blocked**) left untested; the cross-persona handoff that stops at "sent" instead of "received and in with the right access." Each is a gap.
- **Surface gaps — don't silently cover them, don't ignore them.** e2e still doesn't invent behaviours: a gap is raised as a **finding** (a missing criterion) that routes back to the spec / [to-tickets](../to-tickets/SKILL.md) / [manual-qa](../manual-qa/SKILL.md), and once the criterion exists, e2e covers it. The discipline holds — the criterion is still the test — but thin criteria no longer pass unquestioned.

This is what makes e2e *criterious* rather than a rubber stamp: it proves the happy path **and** reports where the happy path is all the criteria actually cover.

## The loop

1. **Find the source criteria.** The ticket's acceptance criteria, or the user story's Given/When/Then. If there are none, ask which behaviours to cover — never invent them.
2. **Use the project's existing runner.** Playwright, Cypress, whatever is already wired. Don't introduce a new e2e stack without asking.
3. **One criterion → one scenario.** *Given* arranges state through the app's real entry points (or a clearly-named scratch seed seam), *When* is the user's action through the UI, *Then* is an assertion on what the user can observe.
4. **Target semantic selectors.** Assert against roles, labels, and accessible names — not brittle CSS or test-only hooks where a real role exists. This survives refactors and matches what a [mockup](../mockup/SKILL.md) already rendered, so a mockup-seeded flow is e2e-ready.
5. **Tag each test with the ticket / user-story ID.** The tag is the traceability link — criterion ↔ test — so coverage is checkable against the spec.
6. **Critique for gaps.** Run the [critical-qa](../critical-qa/SKILL.md) probes over the flow you just encoded — states, actions, permissions, personas. Each thing they surface that no criterion covers is a **gap finding**, raised (not invented as a passing test), so it routes back to the spec (see *Read the criteria critically*).
7. **Run them, and report honestly.** A criterion isn't covered until its scenario is green. Say which criteria are now covered, which you skipped and why, **and which gaps you found** — never mark a criterion covered on a test that didn't run.

## Anti-patterns

- **Side-channel assertions** — checking the database instead of what the user sees. e2e verifies the flow through its public surface; if you assert through the back door you've written an integration test wearing an e2e costume.
- **Brittle selectors** — coupling to CSS classes or DOM structure, so the test breaks on a refactor that changed no behaviour.
- **Duplicating seam tests** — re-testing at the browser what a `tdd` seam test already covers. Keep e2e for the assembled, user-visible flow; leave the fine-grained logic to `tdd`.
- **Rubber-stamping thin criteria** — writing only the happy-path scenario the criteria list and never noting the missing edge, error, permission, or persona cases. Covering is not the same as complete; a gap left unflagged is a gap shipped.
