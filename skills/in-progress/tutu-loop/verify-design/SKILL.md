---
name: tutu-loop-verify-design
description: The gate satellite of tutu-loop — the convergence point where design and specs are reconciled before any code. Proves, user-story by user-story and ADR by ADR, that the hi-fi design already covers and faithfully expresses every requirement; greenlights the build or escalates the divergence as needs-decision. Self-contained. Invoked only by the tutu-loop coordinator.
disable-model-invocation: true
---

# tutu-loop · verify-design (the gate)

The **convergence gate** of [tutu-loop](../SKILL.md): both on-ramps (design-first and grill-first) land here, and no code is written until it is green. It proves, **user-story by user-story and ADR by ADR, against the design**, that what will be built is already designed — completely and faithfully — *before* a line of implementation.

The defining constraint: **the user story / ADR is the item, and the design is the evidence.** You don't invent checks — you take every user story and every frontend-relevant ADR the [discovery](../discovery/SKILL.md) produced and give a verdict for each, pointing at the screen/element in the [design](../design/SKILL.md) reference that satisfies it. A verdict that points at nothing is not a verdict.

`tutu-loop` is **hi-fi-only**: coverage and fidelity are verified against the hi-fi reference directly (the low-fi bootstrap, if one was drawn, backs structure).

## It arms the loop's reconciliation — it is not a separate human gate

In tutu-loop the divergence path *is* the loop's `needs-decision` escalation:

- **All green** → greenlight; the coordinator enters the [build](../build/SKILL.md).
- **Any gap** → the loop can't pick a winner between design and spec on its own → it **escalates the specific divergence as `needs-decision`** with a recommendation (revise the design, or revise the spec). On the answer, route back to [design](../design/SKILL.md) or [discovery](../discovery/SKILL.md) and re-gate.

## The loop

1. **Gather the inputs** — the hi-fi reference and its connective map; the **user stories**; the **frontend-relevant ADRs** (skip backend-only ones); and the `story → screen → ADR` map if it exists.
2. **Extract the checklist** — every user story, and every ADR with a frontend consequence. Each is one item.
3. **Build the traceability matrix** — wire each item to the design (`US / ADR → screen(s)/element(s)`). Surface both leaks: an item with **no screen** behind it, and a **screen with no owning US/ADR** (scope creep).
4. **Verdict per item, by inspecting the design — four checks:**
   - **Presence** — a screen/element exists for the item. Absent → ❌.
   - **Fidelity** — it doesn't merely exist, it *expresses the intent*: the US's promised action/outcome is actually there, the ADR's decision actually reflected. Present but hollow → ⚠️.
   - **State-completeness** — for every collection or async read a US implies, is there an **empty / loading / error** treatment? The hi-fi reference is *look-only* and usually shows the populated happy state, so silence here is **expected** — flag each missing state as a finding to resolve (extend the design, or record "build state per convention X"), not as a failure.
   - **FE-adherence** — is the look expressible in the component library / patterns the ADRs fixed (in `DESIGN.md`)? A design that ignores the settled stack is a finding.
5. **Assign a verdict per item — never without pointing at the design:**
   - ✅ **present & faithful** — a screen expresses it, states accounted for.
   - ⚠️ **shallow / state-incomplete** — present but hollow, or missing empty/loading/error; say which.
   - ❌ **absent** — no screen/element for it.
   - 🚧 **contradiction** — two ADRs (or an ADR and a US) that can't both hold; name both.
6. **Decide the gate.** All ✅ → greenlight the build. Any ❌/⚠️/🚧 → **escalate as `needs-decision`** with the routed recommendation: absent/shallow → extend the design; missing states → extend the design or record a build-time convention; contradiction → back to the ADR / [discovery](../discovery/SKILL.md). Re-gate after the fix.

## Report shape

```
## Gate — <flow> (hi-fi-only)

### Traceability
| US / ADR | Screen(s)         | Verdict                   |
|----------|-------------------|---------------------------|
| US-1     | Dashboard, Detail | ✅ present & faithful     |
| US-4     | —                 | ❌ absent                 |
| ADR-7    | Settings          | ⚠️ no error/empty state   |
| —        | Pricing           | ⚠️ SCOPE CREEP: no US/ADR |

### Gate result: BLOCKED → needs-decision
1 absent (US-4), 1 state-incomplete (ADR-7), 1 scope-creep (Pricing)
Recommendation: extend design for US-4; record empty/error convention for ADR-7; drop Pricing or add a US.
```

## Anti-patterns

- **Verdict without pointing at the design** — "probably covered" is not present; name the screen or mark it absent.
- **Checking code** — there is no code yet at the gate; the evidence is the design. (Code-vs-spec verification is the [build](../build/SKILL.md)'s two-axis code review and [validate](../validate/SKILL.md), after.)
- **Treating the hi-fi as complete** — it is look-only; missing empty/loading/error states are expected findings to resolve, not proof the design is wrong.
- **Inventing user stories** — you verify the USs/ADRs that exist; a gap is a finding routed back, never a screen you assert as covered.
- **Silently picking a winner** — a design↔spec divergence is the human's call; escalate it as `needs-decision`, don't resolve it by fiat.
