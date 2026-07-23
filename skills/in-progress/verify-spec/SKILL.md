---
name: verify-spec
description: Post-implementation eval for a GitHub spec-kit feature — verifies the built thing actually satisfies every requirement in spec.md (FR / SC / acceptance scenarios), gathering evidence per item and emitting a traceability matrix, per-requirement verdicts, and a done/not-done gate. Use after /speckit.implement, or to audit whether a shipped spec-kit feature meets its spec.
---

# Verify Spec

Take a [GitHub spec-kit](https://github.com/github/spec-kit) feature and prove, **requirement by requirement, with evidence**, that the built thing satisfies what `spec.md` promised.

The defining constraint mirrors [e2e](../../engineering/e2e/SKILL.md): **the requirement is the test.** You don't invent things to check — you take every `FR-`, `SC-`, and acceptance scenario the spec already committed to and produce a verdict for each, backed by something that actually ran or was actually inspected. A verdict with no evidence is not a verdict.

## Where this sits in the spec-kit flow — and what it is *not*

The pure spec-kit flow is:

```
/speckit.constitution → /speckit.specify → /speckit.clarify → /speckit.plan
  → /speckit.tasks → /speckit.analyze → /speckit.implement → /speckit.converge
```

spec-kit already ships static/authoring checks. `verify-spec` fills the one gap they leave — **evidence-based, post-implementation verification** — so keep the boundaries sharp:

- **vs `/speckit.analyze`** — analyze is *static, pre-implementation, docs-vs-docs*: it cross-checks spec ↔ plan ↔ tasks for consistency and coverage. `verify-spec` is *post-implementation, artifact-vs-reality*: does the running code satisfy the requirement? Don't re-run analyze's consistency pass here.
- **vs `/speckit.checklist`** — checklist *generates* quality checklists at authoring time. `verify-spec` *executes* verification against a built feature.
- **vs `/speckit.converge`** — converge scans broadly for *remaining work*. `verify-spec` issues a *per-requirement pass/fail with evidence* — narrower, sharper, gated.
- **vs [code-review](../../engineering/code-review/SKILL.md) (Spec axis)** — that reads the *diff statically* against the spec. `verify-spec` **runs the thing**. They're complementary: review the diff, then verify the behaviour.

One line: `/speckit.analyze` asks "are the documents consistent with each other?"; `verify-spec` asks "**does the built thing satisfy each requirement?**"

## When to reach for it

Type `/verify-spec`, or reach for it right after `/speckit.implement` finishes a feature, or to audit a spec-kit feature that already shipped. It needs the artifacts a spec-kit feature produces: `specs/NNN-feature/spec.md` (required), plus `tasks.md` and `plan.md` (for traceability) if present.

## The loop

1. **Locate the feature.** Find the target under `specs/` (spec-kit stores each feature as `specs/NNN-feature/`). If there's more than one and the user didn't say which, ask — don't guess. Read `spec.md`; read `tasks.md` and `plan.md` if they exist. If `spec.md` is missing, stop and say so.

2. **Extract the verifiable items** — this is the eval dataset, pulled verbatim from `spec.md`:
   - **Functional Requirements** — `**FR-001**: System MUST …` under `### Functional Requirements`.
   - **Success Criteria** — `**SC-001**: …` under `## Success Criteria`. These are *measurable* (a percentage, a time budget, a throughput). Verifying an SC means hitting its number, not gesturing at it.
   - **Acceptance Scenarios** — the `Given / When / Then` blocks under each `### User Story N (Pn)`. Each scenario is one case.
   - **`[NEEDS CLARIFICATION: …]` markers** — any requirement still carrying one is **unverifiable by definition**; record it as `blocked`, don't try to guess intent.

3. **Build the traceability matrix.** Wire each item forward through the artifacts: `FR / US → task(s)` (tasks tag their story as `[US1]` and carry exact file paths) `→ code/file → test`. Surface both leaks: a **requirement with no task/code** behind it, and **code/tasks with no requirement** in front of it (scope creep). Missing `tasks.md`/`plan.md` just means the middle columns are blank — still map requirement → code directly.

4. **Pick the cheapest sufficient verification per item, and gather real evidence.** Route by the nature of the requirement:
   - **An automated test already covers it** → run it; the result is the evidence.
   - **A user-visible flow with acceptance scenarios** → make it runnable via [e2e](../../engineering/e2e/SKILL.md) (the Given/When/Then *is* the scenario), or exercise it live with [manual-qa](../../engineering/manual-qa/SKILL.md).
   - **A measurable SC** → run the measurement (timing, count, load) and record the number against the target.
   - **Behaviour not observable from outside** (invariants, internal contracts) → inspect the code at `file:line` and cite it; prefer a seam test ([tdd](../../engineering/tdd/SKILL.md)) over prose where one can exist.
   - While walking user-visible flows, run the [critical-qa](../../engineering/critical-qa/SKILL.md) probes: a gap they surface that no requirement covers is a **finding against the spec**, not a verdict you invent.

5. **Assign a verdict per item — never without evidence:**
   - ✅ **met** — evidence exists and passed (name the test / cite the run / attach the observation).
   - ⚠️ **partial** — some paths pass, others don't; say which.
   - ❌ **not met** — no passing evidence, or a check failed.
   - 🚧 **blocked** — carries `[NEEDS CLARIFICATION]`, or can't be verified in this environment; say why.

   Echoing e2e's honesty rule: **a requirement is not "met" on a test that didn't run.** No green without a run or an inspection behind it.

6. **Report, then gate.** Emit:
   - the **traceability matrix** (requirement → task → file → test, with orphans flagged),
   - the **verdict table** (item, method, verdict, evidence),
   - the **gap list** (unmet requirements, scope creep, and critical-qa findings).

   Then the gate: **not done** while any `FR` or `SC` lacks a passing check — unless the user records an explicit waiver. Blocked-on-clarification items route back to `/speckit.clarify`; missing behaviour routes back to `/speckit.implement`; missing criteria route back to `/speckit.specify`.

## Report shape

```
## Verify Spec — specs/NNN-feature

### Traceability
| Requirement | Task(s) | File(s)        | Test / evidence         |
|-------------|---------|----------------|-------------------------|
| FR-001      | T003    | src/auth.ts    | auth.test.ts::login ✅  |
| FR-004      | —       | —              | ⚠️ ORPHAN: no task      |
| —           | T011    | src/export.ts  | ⚠️ SCOPE CREEP          |

### Verdicts
| Item   | Method        | Verdict     | Evidence                          |
|--------|---------------|-------------|-----------------------------------|
| FR-001 | unit test     | ✅ met      | auth.test.ts::login passed        |
| SC-002 | measurement   | ❌ not met  | p95 820ms, target < 500ms         |
| US1-S3 | e2e           | ✅ met      | checkout.spec.ts green            |
| FR-007 | —             | 🚧 blocked  | [NEEDS CLARIFICATION] on limits   |

### Gate: NOT DONE — 1 SC unmet (SC-002), 1 blocked (FR-007), 1 orphan (FR-004)
```

## Anti-patterns

- **Verdict without evidence** — the cardinal sin. "Looks implemented" is not a pass; name the run or cite the line.
- **Inventing requirements** — you verify what `spec.md` says, not what you wish it said. Gaps are *findings routed back to the spec*, never new tests you assert as passing.
- **Re-running analyze** — don't spend the pass on doc-vs-doc consistency; that's `/speckit.analyze`'s job. Stay on artifact-vs-reality.
- **Waving at an SC** — a Success Criterion has a number. "Feels fast" doesn't verify "under 500ms"; take the measurement.
- **Silent gate** — never report all-green while a requirement is unmet or blocked. An unverified requirement is a gap shipped.
