---
name: tutu-loop-build
description: The build satellite of tutu-loop — slices a role's scope into tracer-bullet tickets and implements them toward the hi-fi reference, TDD at agreed seams, closing each with a two-axis code review, and escalating hard bugs into a tight feedback loop. Runs unattended. Self-contained; consolidates to-tickets, implement, tdd, code-review, and diagnosing-bugs. Invoked only by the tutu-loop coordinator.
disable-model-invocation: true
---

# tutu-loop · build

The implementation step of [tutu-loop](../SKILL.md), run **per role**. It slices a role's scope into tracer-bullet tickets and builds them toward the [design](../design/SKILL.md) reference, test-first at agreed seams, closing each with a two-axis review. It is **self-contained**: it consolidates ticketing, implementation, TDD, code review, and hard-bug diagnosis into one satellite, referencing only its siblings — never the tutu skills.

It runs **unattended**: no human quiz. Where the source discipline would ask the user (ticket granularity, seam choice), the loop uses a recommended default and escalates only a *genuine* ambiguity as `needs-decision`.

## Slice into tracer bullets — per role

Break the role's scope into **vertical slices**, each cutting a narrow but complete path through every layer (schema → API → UI → tests), demoable on its own, sized to one fresh context window.

- **Blocking edges.** Each ticket declares the tickets that must finish before it starts. Independent tickets fan out; dependent ones are a DAG, worked blockers-first (frontier order).
- **Test level.** Default **seams** (integration/unit at internal boundaries). Mark **e2e** where the value lives in the assembled user-facing flow — a role's critical happy path is always e2e (it *is* the exit test). Not a lock-in; e2e can be backfilled.
- **hi-fi-only discipline.** Frontend tickets build the screen in-stack **toward the reference**, and must not introduce frontend the design doesn't already show. If a ticket would, the design is **extended first** (back to its owning `US-<n>`/`ADR-<n>`) — production frontend never gets ahead of the design.
- **Wide refactors are the exception.** A mechanical change whose blast radius fans across the codebase is sequenced **expand → migrate-in-batches → contract**, each batch a ticket, CI green batch to batch — not forced into one vertical slice.
- **Same screen/file → same worker.** Two tickets touching the same code go to one worker; parallel workers on shared code is a conflict, not speed.

Tickets use the project's **domain glossary** and respect the ADRs in the area. Titles describe the end-to-end behaviour from the user's perspective, not a layer-by-layer list; avoid file paths and code snippets (they go stale).

## Implement each ticket

1. **Promote toward the reference.** For frontend, build the screen's structure and style it to **match the [design](../design/SKILL.md) reference** (layout, spacing, states, components) — not a fresh take. Look drift is a defect [validate](../validate/SKILL.md) will catch; if the look must change, it goes back through [design](../design/SKILL.md) first.
2. **TDD at agreed seams.** Red → green, one slice at a time.
3. **Typecheck and test continuously**; run the full suite once at the end.
4. **Close with a code review** (below), then commit to the **fix branch** (never `main`).

## TDD — the red-green loop

- **A seam is the public boundary you test at** — the interface where behaviour is observable without reaching inside. Tests live at seams, never against internals. Write down the seams under test before writing tests; default them from the ticket rather than asking, and only escalate if the right seam is genuinely unclear.
- **Red before green.** Failing test first, then only enough code to pass it. No speculative features.
- **One slice at a time.** One seam, one test, one minimal implementation per cycle. Refactoring belongs to the review stage, not the loop.
- **A good test reads like a specification** and survives refactors because it verifies behaviour through the public interface. Avoid the anti-patterns: **implementation-coupled** (mocks internals, breaks on refactor with no behaviour change), **tautological** (asserts a value recomputed the way the code computes it — expected values must come from an independent source of truth), **horizontal slicing** (all tests then all code — work vertically, one test → one implementation).

## Code review — two axes, in parallel

Review the ticket's diff along two independent axes, as **parallel sub-agents** so they don't pollute each other's context, then aggregate:

- **Standards** — does the code follow the repo's documented standards (`CODING_STANDARDS.md`, `CONTRIBUTING.md`), **plus** a fixed smell baseline (Fowler ch.3): Mysterious Name, Duplicated Code, Feature Envy, Data Clumps, Primitive Obsession, Repeated Switches, Shotgun Surgery, Divergent Change, Speculative Generality, Message Chains, Middle Man, Refused Bequest. A documented repo standard overrides the baseline; baseline smells are judgement calls; skip anything tooling enforces.
- **Spec** — does the code faithfully implement the ticket/US? Report missing/partial requirements, scope creep, and requirements implemented wrongly, quoting the spec line for each.

Keep the two axes **separate** — don't merge or rerank; a change can pass one and fail the other, and reporting them apart stops one from masking the other.

## Hard bugs — build a tight feedback loop first

When a fix resists (intermittent, mysterious), don't jump to a hypothesis — **build a tight, red-capable feedback loop** that drives the actual bug path and asserts the user's exact symptom (a failing test, a curl, a headless-browser script, a replayed trace). It must be **red-capable, deterministic, fast, and agent-runnable** — run it once and confirm it goes red before theorising. Then: reproduce + **minimise** to the smallest still-red scenario, generate **3–5 ranked falsifiable hypotheses**, **instrument one variable at a time** (tagged `[DEBUG-xxxx]` logs, cleaned up after), then write the regression test **before** the fix at a correct seam (if no correct seam exists, that absence is itself a finding). Done when the original repro no longer reproduces, the regression test passes, and all instrumentation is removed.

## Output

Each ticket built green on the **fix branch** — TDD seams passing, the role's critical happy path e2e-ready, the two-axis code review clean — ready for [validate](../validate/SKILL.md) to prove the role's complete happy path. Nothing merges to `main` here; integration onto the feature branch and the single human gate are the coordinator's job.
