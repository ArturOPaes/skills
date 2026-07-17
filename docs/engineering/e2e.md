Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=e2e
```

```bash
npx skills update e2e
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/e2e)

## What it does

`e2e` turns a ticket's acceptance criteria into end-to-end tests that drive the real UI — each criterion, each Given/When/Then, becomes one scenario walked through the browser from the user's perspective.

The acceptance criterion is the test. You don't invent behaviours to cover; you take the ones the ticket or user story already promised and make them executable, linked back by the ticket ID. The criterion is the spec, the e2e is its runnable form. But writing the test is also where you *read the criteria critically* — validating the happy path while flagging the gaps the criteria never named.

## When to reach for it

Type `/e2e`, or the agent reaches for it when a ticket's test level is `e2e` (set in [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets)) or when you ask to add end-to-end coverage.

Reach for it to prove the whole behaviour a ticket promised, or to **backfill** e2e onto a feature that shipped without it — the common "start without e2e, add it later" path. For fine-grained logic at internal seams, use [tdd](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/tdd) instead: `tdd` is red-green at the seams while you build, `e2e` is the assembled flow through the browser after it exists.

## The loop

One criterion → one scenario: *Given* arranges state through the app's real entry points, *When* is the user's action through the UI, *Then* is an assertion on what the user can observe. Assert against **semantic selectors** — roles, labels, accessible names — not brittle CSS, so the test survives refactors and reuses what a [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) already rendered. Tag each test with its ticket ID: the tag is the traceability link between criterion and test.

## Read the criteria critically

Encoding criteria into tests is the moment you can see what they *miss*. So as it writes, `e2e` runs the [critical-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/critical-qa) critique over the flow — states, actions, permissions, personas — and validates the **happy path** first, then probes around it: the empty/error state no criterion mentions, the action with no criterion behind it, the permission direction left untested, the cross-persona handoff that stops at "sent." Each is raised as a **gap finding** — a missing criterion routed back to the spec — not invented as a passing test. The discipline holds (the criterion is still the test), but thin criteria no longer pass unquestioned. That's what makes it *criterious* rather than a rubber stamp.

## Where it fits

`e2e` is the browser-level companion to [tdd](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/tdd): [implement](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/implement) drives `tdd` at the seams, and reaches for `e2e` on the tickets marked for it. Its markup comes seeded by [mockup](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/mockup) and its criteria come from [to-tickets](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/to-tickets). When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
