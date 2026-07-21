---
name: to-waves
description: Sequence the build into ordered, shippable, validatable milestones (waves) after the whole-product overview is locked, each with a validation goal — then slice one wave at a time into tickets. Optional; a small scope skips it. Use in the implementation phase to phase delivery, not to partition the design.
disable-model-invocation: true
---

# To Waves

Partition a large scope into a sequence of **waves** — shippable, validatable increments, each proving something on its own — before any of them is sliced into tickets.

The defining constraint: **a wave is a validation milestone, not a batch of work.** Each wave is a coherent slice of value you ship and validate together — it can be a bigger MVP — and it declares *what it validates*. This is the altitude above [to-tickets](../to-tickets/SKILL.md): to-waves decides the coarse, ordered milestones; to-tickets slices *one* wave into thin tracer bullets.

Two altitudes compose. A wave is fat at the **validation** level (what to prove together, a product bet) but built in thin tracer-bullet slices (how to build it safe, an engineering concern). You validate a bigger MVP *and* keep the tight feedback loop.

## When to reach for it

Reach for it in the **implementation phase**, after the whole-product overview (design, mockup, open-design, blueprint) is locked and [pre-flight](../pre-flight/SKILL.md) has greenlit the build, when the scope is big enough that shipping in ordered milestones beats one big drop. It's **optional** — a small scope goes straight to [to-tickets](../to-tickets/SKILL.md). It doesn't partition the *design* (the mockup and blueprint already cover the whole product); it phases the *delivery*.

This is **not** [wayfinder](../wayfinder/SKILL.md). Wayfinder dissolves *fog* — it resolves unknowns into decisions when the way isn't visible yet. to-waves phases a *known* scope into delivery milestones. If the effort is still foggy, wayfinder first; then to-spec; then to-waves.

## Process

### 1. Gather the spec

Work from the spec or plan already in context (from [to-spec](../to-spec/SKILL.md)), or a reference passed as an argument. Explore the codebase enough to name the waves in the project's domain vocabulary.

### 2. Draft the waves

Break the scope into a short, ordered list of waves.

<wave-rules>

- Each wave is **shippable and validatable on its own** — a coherent chunk of value, not a horizontal layer.
- Each wave declares a **validation goal**: the hypothesis, aha-moment, or activation metric it proves. A wave with no validation goal is just an arbitrary batch — split or merge it until it has one.
- Waves are **ordered so each builds on the last** — a wave never depends on a later one. Wave 1 is the smallest thing that proves the core.
- A wave is **bigger than a ticket, smaller than the whole product** — small enough to build and validate as one milestone and break into a handful of tracer bullets.

</wave-rules>

### 3. Quiz the user

Present the waves as an ordered list. For each: **Title**, **Validates** (the goal), **What ships**. Ask:

- Do the boundaries feel right — does each wave validate something on its own?
- Is wave 1 the smallest thing that proves the core?
- Is the order honest — does each wave stand on the ones before it?

Iterate until the user approves.

### 4. Record the waves

Write the approved waves where the project keeps its plan — a `waves.md` under the feature's scratch/plan folder, or milestones on the tracker — each with its validation goal and position in the order. Do not slice them into tickets yet.

## Then work one wave at a time

Per wave, run the build and **ship before starting the next**:

1. **[to-tickets](../to-tickets/SKILL.md)** to slice *that wave* into tracer bullets — each promoting a slice of the already-built [mockup](../mockup/SKILL.md), never inventing frontend outside it.
2. **[implement](../implement/SKILL.md)** the frontier.
3. Validate the wave's goal with **[manual-qa](../manual-qa/SKILL.md)** (or skip to a single check at the very end), then ship before starting the next.

Do not slice every wave into tickets up front — that throws away what shipping wave 1 teaches you. Slice the wave you're on. The design, mockup, and diagrams are already whole-product from the overview — waves sequence the *build*, not the design.
