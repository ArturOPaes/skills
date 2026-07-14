---
name: to-waves
description: Partition a large spec into ordered waves — shippable, validatable increments (milestones), each with a validation goal — before slicing any of them into tickets. Use when a scope is too big to break into tickets in one pass, or you want to ship and validate a bigger MVP in phases.
disable-model-invocation: true
---

# To Waves

Partition a large scope into a sequence of **waves** — shippable, validatable increments, each proving something on its own — before any of them is sliced into tickets.

The defining constraint: **a wave is a validation milestone, not a batch of work.** Each wave is a coherent slice of value you ship and validate together — it can be a bigger MVP — and it declares *what it validates*. This is the altitude above [to-tickets](../to-tickets/SKILL.md): to-waves decides the coarse, ordered milestones; to-tickets slices *one* wave into thin tracer bullets.

Two altitudes compose. A wave is fat at the **validation** level (what to prove together, a product bet) but built in thin tracer-bullet slices (how to build it safe, an engineering concern). You validate a bigger MVP *and* keep the tight feedback loop.

## When to reach for it

Reach for it when the scope is too big to slice into tickets in one pass — many features, a greenfield build — and you want to ship it in phases that each earn their keep. It sits between [to-spec](../to-spec/SKILL.md) and [to-tickets](../to-tickets/SKILL.md).

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
- A wave is **bigger than a ticket, smaller than the whole product** — small enough to mock as one flow and break into a handful of tracer bullets.

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

Per wave, run the flow and **ship before starting the next**:

1. **[mockup](../mockup/SKILL.md)** the wave's flow and align on it.
2. **[to-tickets](../to-tickets/SKILL.md)** to slice *that wave* into tracer bullets.
3. **[implement](../implement/SKILL.md)** the frontier, then ship and check the wave's validation goal.

Do not slice every wave into tickets up front — that throws away what shipping wave 1 teaches you. Slice the wave you're on.
