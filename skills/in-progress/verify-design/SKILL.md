---
name: verify-design
description: Pre-implementation eval that verifies a flow's design — the open-design hi-fi reference, plus the low-fi mockup when the project uses one — covers and faithfully expresses every user story and frontend ADR, with state-completeness and component-lib adherence checked, emitting a traceability matrix and per-item verdicts that feed pre-flight. The pre-build mirror of verify-spec. Use in the overview phase, before pre-flight greenlights a build.
---

# Verify Design

Prove, **user-story by user-story and ADR by ADR, against the design**, that what will be built is already designed — completely and faithfully — *before* a line of implementation. It is the pre-build mirror of [verify-spec](../verify-spec/SKILL.md): where verify-spec checks the built code against the spec *after* the build, verify-design checks the **design** against the user stories and frontend decisions *before* it.

The defining constraint mirrors verify-spec: **the user story / ADR is the item, and the design is the evidence.** You don't invent things to check — you take every user story and every frontend-relevant ADR the project already committed to and produce a verdict for each, pointing at the screen or element in the design that satisfies it. A verdict that points at nothing in the design is not a verdict.

## Where it sits — it feeds pre-flight, it is not the gate

In the overview phase (see [ask-tutu](../../engineering/ask-tutu/SKILL.md)): `… → mockup?/open-design → blueprint → verify-design → pre-flight → build`. verify-design is the **eval that arms the human gate**: it produces the matrix and verdicts; [pre-flight](../../engineering/pre-flight/SKILL.md) then walks the *findings* with the user and gives the verdict. It does not greenlight anything itself.

Keep the boundary with verify-spec sharp: verify-spec is *post-build, code-vs-spec, evidence = a test that ran*; verify-design is *pre-build, design-vs-intent, evidence = a screen in the design*. Same discipline, opposite ends of the build.

## Read the design path first

The project records its **design flow** in `DESIGN.md` (set by [grill-design](../../engineering/grill-design/SKILL.md)):

- **`hi-fi-only`** — the [open-design](../../engineering/open-design/SKILL.md) HTML reference is the *sole* design artifact. Coverage and fidelity are verified against it directly.
- **`mockup+hi-fi`** — a low-fi [mockup](../../engineering/mockup/SKILL.md) (structure, in the real stack) *and* the open-design reference (look). Verify structure/coverage against the mockup, look/fidelity against the reference.

Read that field and verify against the right artifacts. If it's absent, ask which path the project uses rather than guessing.

## The loop

1. **Gather the inputs.** The design artifact(s) per the path above; the **user stories** (the spec); the **frontend-relevant ADRs** (decisions with a UI consequence — skip backend-only ones); and [blueprint](../../engineering/blueprint/SKILL.md)'s `story → screen → ADR` map if it exists.

2. **Extract the checklist** — the eval dataset: every **user story**, and every **ADR with a frontend consequence**. Each is one item.

3. **Build the traceability matrix.** Wire each item to the design: `US / ADR → screen(s)/element(s) in the design`. Surface both leaks: an item with **no screen** behind it, and a **screen with no owning US/ADR** (design scope creep).

4. **Verdict per item, by inspecting the design — four checks:**
   - **Presence** — a screen/element exists for the item. Absent → ❌.
   - **Fidelity** — it doesn't merely exist, it *expresses the intent*: the US's promised action/outcome is actually there, the ADR's decision is actually reflected. Present but hollow → ⚠️.
   - **State-completeness** — run [critical-qa](../../engineering/critical-qa/SKILL.md)'s state-quality probes over each item: for every collection or async read a US implies, is there an **empty / loading / error** treatment? The open-design HTML is **look-only** and typically shows the populated happy state, so silence here is *expected* — flag each missing state as a finding to resolve (extend the design, or record "build state per convention X"), not as a failure of the eval.
   - **FE-adherence** — is the look expressible in the **component library / patterns** the ADRs fixed (in `DESIGN.md`)? A design that ignores the settled stack is a finding.

5. **Assign a verdict per item — never without pointing at the design:**
   - ✅ **present & faithful** — a screen expresses it, states accounted for.
   - ⚠️ **shallow / state-incomplete** — present but hollow, or missing empty/loading/error; say which.
   - ❌ **absent** — no screen/element for it.
   - 🚧 **contradiction** — two ADRs (or an ADR and a US) that can't both hold once the whole product is drawn; name both.

6. **Report, then hand to pre-flight.** Emit the matrix, the verdict table, and the gap list. Route findings: absent/shallow → extend `open-design` (or the mockup on `mockup+hi-fi`); missing states → extend the design or record a build-time convention; contradictions → back to the ADR / [domain-modeling](../../engineering/domain-modeling/SKILL.md) or `grill-design`. pre-flight walks these and gives the greenlight — verify-design does not.

## Report shape

```
## Verify Design — <flow> (path: hi-fi-only)

### Traceability
| US / ADR | Screen(s)            | Verdict                     |
|----------|----------------------|-----------------------------|
| US-1     | Dashboard, Detail    | ✅ present & faithful       |
| US-4     | —                    | ❌ absent                   |
| ADR-7    | Settings             | ⚠️ no error/empty state     |
| —        | Pricing              | ⚠️ SCOPE CREEP: no US/ADR   |

### Verdicts
| Item  | Check that failed | Verdict         | Where in the design            |
|-------|-------------------|-----------------|--------------------------------|
| US-1  | —                 | ✅ faithful     | dashboard.html, detail.html    |
| US-4  | presence          | ❌ absent       | no screen                      |
| ADR-7 | state-complete    | ⚠️ incomplete   | settings.html (no empty/error) |
| ADR-3 | —                 | 🚧 contradiction| conflicts with ADR-9 on nav    |

### For pre-flight: 1 absent (US-4), 1 state-incomplete (ADR-7), 1 contradiction (ADR-3↔9), 1 scope-creep
```

## Anti-patterns

- **Verdict without pointing at the design** — the cardinal sin, mirrored from verify-spec. "Probably covered" is not present; name the screen or mark it absent.
- **Checking code** — that's verify-spec, and it runs *after* the build. Here there is no code yet; the evidence is the design.
- **Treating the HTML as complete** — the open-design reference is *look-only*. Missing empty/loading/error states are **expected findings to resolve**, not proof the design is wrong or the eval failed.
- **Inventing user stories** — you verify the USs/ADRs that exist; a gap is a finding routed back, never a screen you assert as covered.
- **Acting as the gate** — verify-design arms pre-flight; it never greenlights the build itself.
