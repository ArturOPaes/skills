---
name: ask-tutu
description: Ask which skill or flow fits your situation. A router over the skills in this repo.
disable-model-invocation: true
---

# Ask Tutu

You don't remember every skill, so ask.

A **flow** is a path through the skills. Most paths run along one **main flow**, and two **on-ramps** merge onto it. Everything else is standalone, or a vocabulary layer that runs underneath.

## The main flow: idea → ship

The route most work travels. You have an idea and want it built.

1. **`/grill-with-docs`** — sharpen the idea by interview. Start here when you **have a codebase**: it's stateful, retaining what it learns in `CONTEXT.md` and ADRs. (No codebase? Use `/grill-me` — see Standalone. Both run the same `/grilling` primitive; `grill-with-docs` is the one that leaves a paper trail.)
2. **Branch — can you settle every question in conversation?** If a question needs a runnable answer (state, business logic, a UI you have to see), detour through a prototype, bridged by **`/handoff`** in both directions (see Crossing sessions):
   - **`/handoff`** out, then open a fresh session against that file,
   - **`/prototype`** to answer the question with throwaway code,
   - **`/handoff`** back what you learned, and reference it from the original idea thread.
3. **Branch — is this a multi-session build?**
   - **Yes** → **`/to-spec`** (turn the thread into a spec). If the scope is **too big to slice in one pass** — many features, a greenfield build — go up one altitude first with **`/to-waves`**, which partitions it into ordered, validatable **waves** (shippable milestones, each proving something); otherwise skip straight to tickets. Then, **per wave**, optionally settle the project's *visual* language with **`/grill-design`** (the design-side counterpart to step 1's `/grill-with-docs`, leaving a `DESIGN.md` paper trail) and **`/mockup`** the flow to align on it visually before building — and, when adopted, the mockup is the **canonical frontend source** every feature is mocked into and promoted from, so nothing ships on the FE that isn't in it; optionally **`/blueprint`** to draw the whole flow as connected Mermaid diagrams (navigation map, per-screen field/action wireflows, user flow, and a story→screen→ADR→ticket traceability map) so the macro picture is shared before slicing; and **`/to-tickets`** to split *that wave* into tracer-bullet tickets, each declaring its **blocking edges** and a **test level** (`seams` by default, `e2e` for critical user-facing flows). On a local tracker that's one file per ticket under `.scratch/<feature>/issues/`, worked blockers-first by hand; on a real tracker the edges become native blocking links, so any ticket whose blockers are done can be grabbed. Before building the wave, run **`/pre-flight`** — the pre-build gate that confirms the wave's documentation, diagrams, and hi-fi layout are current, cover it, and have been reviewed and adjusted, and only then greenlights the build; it's what makes `/mockup`, `/blueprint`, and `/grill-design` effectively non-optional. Then kick off **`/implement`** per ticket, **clearing context between each one**.
   - **No** → **`/implement`** right here, in the same context window.

   Either way, **`/implement`** builds each issue by driving **`/tdd`** internally — one red-green slice at a time — then closes out by running **`/code-review`**, a two-axis review (Standards + Spec) of the diff, before committing. On a ticket whose test level is **`e2e`**, it also drives **`/e2e`** to prove the flow through the UI. Reach for **`/tdd`** on its own to build a concrete behaviour test-first without a full spec, **`/e2e`** on its own to backfill end-to-end coverage onto work that shipped without it, and **`/code-review`** on its own whenever you want to review a branch or PR against a fixed point. For the **human** pass — validating a built task in the real app before shipping, either locally with self-created seeds or against a credentialed environment — reach for **`/manual-qa`**; it's the manual counterpart to `/e2e`, and the verdict is yours to give. Its **pre-build twin** is **`/pre-flight`** above: where manual-qa is the human gate *after* a task is built, pre-flight is the human gate *before* a wave is built — both hand you the verdict.

### Context hygiene

Keep steps 1–3 in **one unbroken context window** — don't compact or clear until after `/to-tickets` — so the grilling, spec, and tickets all build on the same thinking. Each `/implement` then starts fresh, working from the ticket.

The limit on this is the **[smart zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone)**: the window (~120k tokens on state-of-the-art models) within which the model still reasons sharply. If a session approaches it before `/to-tickets`, don't push on degraded — `/handoff` and continue in a fresh thread.

## On-ramps

A starting situation that generates work, then merges onto the main flow.

- **Bugs and requests piling up** → **`/triage`**. It moves issues through triage roles and produces agent-ready issues, which **`/implement`** later picks up.

  Triage is only for issues **you didn't create** — bug reports, incoming feature requests, anything that arrives raw. Tickets that `/to-tickets` produced are already agent-ready, so **don't triage them**.

- **Something's broken** → **`/diagnosing-bugs`**. For the hard ones: the bug that resists a first glance, the intermittent flake, the regression that crept in between two known-good states. It refuses to theorise until it has a **tight feedback loop** — one command that already goes red on *this* bug — then fixes with a regression test. Its post-mortem hands off to **`/improve-codebase-architecture`** when the real finding is that there's no good seam to lock the bug down.

- **A huge, foggy effort — a greenfield project or a huge feature build, too big for one session** → **`/wayfinder`**, the most cognitively demanding flow here. When the way from here to the destination isn't visible yet, it charts a **shared map** of **decision tickets** on the issue tracker and resolves them one at a time — producing **decisions, not deliverables** — until the fog is pushed back and the way is clear. Where **`/grill-with-docs`** sharpens an idea you can hold in one session, wayfinder is for the idea you can't — and it's slower and denser, so save it for exactly that, never a well-scoped feature.

  When the map clears, **it hands off, it doesn't build**: merge onto the main flow at **`/to-spec`**, which collapses the map's linked decisions into a buildable plan, then `/to-waves` (if the scope is still big), `/to-tickets`, and `/implement` as usual. Looping the map straight into `/implement` skips that collapse and throws the linked detail away — go straight to `/implement` only when the effort turned out genuinely small.

## Codebase health

Not feature work — upkeep.

- **`/improve-codebase-architecture`** — run whenever you have a spare moment to keep the codebase good for agents to operate in. It surfaces **deepening opportunities**; picking one _generates an idea_ you can take into the main flow at `/grill-with-docs`. It's the survey that finds the candidates; **`/codebase-design`** (below) is the bench you design the chosen one on.

## Vocabulary underneath

Three model-invoked references that run *beneath* the other skills — each the single source of truth for its vocabulary. Reach for them directly when the **words**, not the process, are the problem; or let the skills above pull them in.

- **`/domain-modeling`** — sharpen the project's *domain* language: challenge a fuzzy term, resolve an overloaded word ("account" doing three jobs), record a hard-to-reverse decision as an ADR. It's the active discipline `/grill-with-docs` drives to keep `CONTEXT.md` a clean glossary.
- **`/codebase-design`** — the deep-module vocabulary (module, interface, depth, seam, adapter, leverage, locality) for designing a module's *shape*: a lot of behaviour behind a small interface at a clean seam. `/tdd` and `/improve-codebase-architecture` both speak it.
- **`/design-taste`** — the *visual and interaction* vocabulary (the three dials — variance, motion, density — plus typography, spacing, tokens, depth, motion, and the anti-slop tells) for making UI look considered rather than machine-default. It's the active discipline `/grill-design` drives to keep a clean `DESIGN.md`, and the taste `/mockup` and `/prototype` draw against. The design-side counterpart to `/domain-modeling`.

## Crossing sessions

- **`/handoff`** — when a thread is full or you need to branch off (e.g. into a `/prototype` session), this compacts the conversation into a markdown file. You don't continue in place — you **open a new session and reference that file** to carry the context across. It's the bridge between context windows, in either direction. Use it when you want a **fresh session** but need the **current conversation preserved**.
- **`/compact`** (built-in) — stay in the **same conversation**, letting the earlier turns be summarized. Use it at **intentional breaks between phases**, when you don't mind losing the verbatim history. Don't compact mid-phase — the agent can lose its way. `/handoff` forks; `/compact` continues.

## Standalone

Off the main flow entirely.

- **`/grill-me`** — the same relentless interview as `/grill-with-docs`, but for when you have **no codebase**. Stateless: it saves nothing locally, builds no `CONTEXT.md`. Reach for it to sharpen any plan or design that doesn't live in a repo.
- **`/prototype`** — a small, throwaway program that answers one design question: does this state model feel right, or what should this UI look like. Throwaway from day one — keep the answer, delete the code. It's the detour in step 2 of the main flow, but reach for it any time a design question is hard to settle on paper.
- **`/mockup`** — a **promotable** high-fidelity render in the project's real stack, on a `/mockup` route with mock data, built to **align** on the UI before building — then kept and grown into the feature (mock → real), never thrown away. Where `/prototype` is throwaway and answers *one* question with several variations, `/mockup` is promotable and shows *one* direction. It's **optional**, but when adopted it becomes the **canonical source of the frontend**: every feature is mocked into it (covering the user stories, ADRs, diagrams, and `DESIGN.md`) and promoted from it in place, waves and tickets slice it, and the invariant holds — **nothing ships on the frontend that isn't in the mockup first** (which `/pre-flight` enforces). Reach for it any time you want to see a flow end-to-end before committing to it.
- **`/research`** — delegate reading legwork to a **background agent**: it investigates a question against **primary sources**, then leaves a cited Markdown file in the repo. Keep working while it reads. The file it produces is something to take *into* the main flow at `/grill-with-docs` — research feeds the thinking, it doesn't replace it.
- **`/teach`** — learn a concept over multiple sessions, using the current directory as a stateful workspace.
- **`/writing-great-skills`** — reference for writing and editing skills well.

## Precondition

**`/setup-tutu-skills`** — run before your first engineering flow to configure the issue tracker, triage labels, and doc layout the other skills assume. Custom issue trackers also work.
