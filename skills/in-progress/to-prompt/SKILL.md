---
name: to-prompt
description: Turn a rough goal into a complete, copy-pasteable prompt for a downstream model — draft the whole prompt with recommended defaults (libs, sections, structure, constraints, acceptance criteria), confirm only the genuinely open points one at a time, then emit the finished prompt. Use when the user wants a polished prompt to hand to a model to build or do something (a landing page, a feature, a script), rather than building it here.
---

# To Prompt

Turn a rough goal — "a landing page for my project", "a CLI that does X" — into a **single, finished prompt the user pastes into a model to actually perform the task**. The interview here is cheap (it can run on a smaller model); the prompt it produces is what a stronger model then executes well.

The deliverable is **the prompt, not the built thing.** Do not build the landing page — build the prompt that builds the landing page.

## The core move: draft first, then confirm — don't interrogate

A blank interrogation ("what stack? what sections? what colours?") is slow and dumps every decision on the user. Instead: **propose a complete prompt with sensible defaults filled in, and only ask about the few points where the default is genuinely uncertain or high-leverage.** Most decisions you make and mark as a default the user can override; a handful you confirm. That's what makes this fast and precise.

## Phase 1 — Draft (do this before asking anything)

1. **Restate the goal** in one sentence.
2. **Look up facts** from the environment — existing stack, framework, conventions, design tokens — so your defaults fit the project instead of inventing a new world. Never ask what you can find.
3. **Draft the full prompt with recommended defaults.** The *slots* you fill depend on the task — pick the ones that fit and fill every one with a recommended choice:
   - **UI / landing page** → stack/libs, ordered sections, content outline, design direction or the project's tokens, responsive + accessibility, acceptance criteria.
   - **CLI / script** → language, arguments/flags, input/output, error handling, dependencies, example invocation.
   - **Feature in an existing codebase** → files/modules touched, data model, API surface, tests, migration/rollout.
   - **Data pipeline** → source, transforms, output schema, schedule, failure handling.
   - **Writing / content** → audience, structure, tone, length, sources.

   Whatever the domain, every slot gets a filled-in value marked as a default the user can override: `Stack: Next.js + Tailwind (default)`. If the task doesn't match a shape above, infer its natural slots the same way.
4. **Extract the open points** — the *few* decisions where the default is a real coin-flip or where getting it wrong is expensive. These, and only these, become the confirm queue. If a default is obviously fine, don't ask.

Show the draft and the list of open points, then move to Phase 2.

## Phase 2 — Confirm the open points (one at a time)

Work down the queue. Each turn, output **exactly** this and nothing after it:

```
Locked: <defaults + confirmed choices, one line each — or "drafted, none confirmed yet">
Open: <the points still to confirm>

Q<n>: <a single, concrete question about one open point>
Options:
  a) <option>
  b) <option>
  c) <option>   (only as many as are real; "other" is always allowed)
Recommendation: <the option you'd pick> — <one sentence why>
```

Then **stop and wait.** One question per message — never two. When the user answers: fold it into "Locked", drop or add dependent points, ask the next. Rules that bind every question:

- **Always recommend** — never "up to you"; take a position, the user overrides.
- **Concrete, optioned** — not "any thoughts on the design?".
- **One decision deep** — don't bundle stack + hosting + auth into one question.
- **Never ask a fact** — look it up.

## Phase 3 — Emit the finished prompt

When the queue is empty, assemble everything (defaults + confirmed answers) into **one self-contained prompt in a fenced code block**, ready to paste into a fresh model with no other context. Structure it so a downstream model performs well:

```
# <Task title>

## Context
<project, audience, where this runs>

## Goal
<one-paragraph what and why>

## Requirements
- Stack / libs: ...
- Sections / structure (in order): ...
- Content: ...
- Design: ...

## Constraints
<responsive, accessibility, performance, what to reuse>

## Acceptance criteria
<observable checks the result must pass>

## Deliverable
<what to output and in what form>

## Out of scope
<what NOT to do>
```

Then confirm once: *"This is the prompt — want any changes before you use it?"* Fold in edits and re-emit. **Do not start executing the task yourself** unless the user explicitly asks you to run the prompt here.

## How it relates to other skills

- It reuses the one-question-at-a-time discipline of [grilling](../../productivity/grilling/SKILL.md), but the product is a **prompt artifact**, not shared understanding.
- It's the `to-*` idiom (like [to-spec](../../engineering/to-spec/SKILL.md) / [to-tickets](../../engineering/to-tickets/SKILL.md)): rough input in, a concrete artifact out — here a prompt for a downstream model rather than an internal spec.

## Anti-patterns

- **Interrogating instead of drafting** — starting with questions rather than a defaults-filled draft. The draft is the point; questions are the exception.
- **Asking what a default covers** — only the open points earn a question.
- **Building the thing** — the deliverable is the prompt; don't render the landing page.
- **A prompt that needs your chat context** — the emitted prompt must stand alone; a fresh model with only that text should be able to run it.
- **Two questions in one message**, no recommendation, or asking a fact — the same failures the interview discipline exists to prevent.
