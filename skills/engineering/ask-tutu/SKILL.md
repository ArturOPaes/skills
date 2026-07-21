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

1. **`/grill-with-docs`** — sharpen the idea by interview. Start here when you **have a codebase**: it's stateful, retaining what it learns in `CONTEXT.md` and ADRs. It **sizes the effort first** — if the idea turns out too big and foggy for one session, it stops and points you at `/wayfinder` (below) rather than grinding on. (No codebase? Use `/grill-me` — see Standalone; it does the same sizing. Both run the same `/grilling` primitive; `grill-with-docs` is the one that leaves a paper trail.)
2. **Branch — can you settle every question in conversation?** If a question needs a runnable answer (state, business logic, a UI you have to see), detour through a prototype, bridged by **`/handoff`** in both directions (see Crossing sessions):
   - **`/handoff`** out, then open a fresh session against that file,
   - **`/prototype`** to answer the question with throwaway code,
   - **`/handoff`** back what you learned, and reference it from the original idea thread.
3. **Branch — is this a multi-session build?**
   - **Yes** → **`/to-spec`** (turn the thread into a spec — **all** the user stories, upfront). Then build the **whole-product overview before any implementation**: **`/grill-design`** for the *visual* language (`DESIGN.md`, the design-side counterpart to step 1's `/grill-with-docs`); the **design**, on one of two paths recorded in `DESIGN.md` (chosen during `/grill-design`): on **`mockup+hi-fi`**, **`/mockup`** is the **canonical frontend source** at **low-fi** — every feature mocked into it and promoted from it in place, so nothing ships on the FE that isn't in it first (structure and coverage) — plus **`/open-design`** for the look; on **`hi-fi-only`**, **`/open-design`** is the *sole* design artifact and the FE is built toward it directly (no mockup, `/e2e` backfilled). Either way **`/open-design`** is the **hi-fi visual reference** the shipped UI must match (generated from `DESIGN.md` — it replaces the old hi-fi mockup); and **`/blueprint`** to draw the whole thing as connected Mermaid diagrams (navigation map, per-screen field/action wireflows, user flow, a story→screen→ADR→ticket traceability map, and a system-design diagram for bottlenecks). Then **`/pre-flight`** — the **overview gate**: it runs a **pre-build design eval** (a `US / ADR → screen` traceability matrix with per-item verdicts) to confirm the design, diagrams, and open-design reference cover and faithfully express **every** user story and frontend ADR, walks the findings with you to review and adjust, and only then greenlights the build. That gate is what makes `/grill-design`, `/mockup`, `/open-design`, and `/blueprint` effectively non-optional. Now **build**, where **waves only sequence the work**: optionally **`/to-waves`** to break delivery into ordered, shippable milestones (skip it for a small scope), then **per wave** **`/to-tickets`** to slice *that wave* into tracer-bullet tickets — each a **promotion of a slice of the mockup**, declaring its **blocking edges** and a **test level** (`seams` by default, `e2e` for critical user-facing flows). On a local tracker that's one file per ticket under `.scratch/<feature>/issues/`, worked blockers-first by hand; on a real tracker the edges become native blocking links. Kick off **`/implement`** per ticket, **clearing context between each one**, and validate with **`/manual-qa`** — at the end of each wave by default, or skip to a single check at the very end.
   - **No** → **`/implement`** right here, in the same context window.

   Either way, **`/implement`** builds each issue by driving **`/tdd`** internally — one red-green slice at a time — then closes out by running **`/code-review`**, a two-axis review (Standards + Spec) of the diff, before committing. On a ticket whose test level is **`e2e`**, it also drives **`/e2e`** to prove the flow through the UI. Reach for **`/tdd`** on its own to build a concrete behaviour test-first without a full spec, **`/e2e`** on its own to backfill end-to-end coverage onto work that shipped without it (as it writes, it runs the `/critical-qa` critique over the flow — proving the happy path and raising the gaps the criteria never named), and **`/code-review`** on its own whenever you want to review a branch or PR against a fixed point. For the **human** pass — validating a built task in the real app before shipping, either locally with self-created seeds or against a credentialed environment — reach for **`/manual-qa`**; it's the manual counterpart to `/e2e`, and the verdict is yours to give. Its **pre-build twin** is **`/pre-flight`** above: where manual-qa is the human gate *after* the build (per wave, or once at the end), pre-flight is the human gate *before* the build begins — run once on the whole overview — both hand you the verdict.

### Context hygiene

Keep the early thinking — the grilling and `/to-spec` — in **one unbroken context window** so the spec builds on the same thinking. The overview artifacts that follow (`DESIGN.md`, the mockup, `BLUEPRINT.md`) persist to disk, so you can compact or `/handoff` once `/pre-flight` greenlights; each `/to-tickets` and `/implement` in the build phase then starts fresh, working from those artifacts.

The limit on this is the **[smart zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone)**: the window (~120k tokens on state-of-the-art models) within which the model still reasons sharply. If a session approaches it before the overview is settled, don't push on degraded — `/handoff` and continue in a fresh thread.

## On-ramps

A starting situation that generates work, then merges onto the main flow.

- **Bugs and requests piling up** → **`/triage`**. It moves issues through triage roles and produces agent-ready issues, which **`/implement`** later picks up.

  Triage is only for issues **you didn't create** — bug reports, incoming feature requests, anything that arrives raw. Tickets that `/to-tickets` produced are already agent-ready, so **don't triage them**.

- **Something's broken** → **`/diagnosing-bugs`**. For the hard ones: the bug that resists a first glance, the intermittent flake, the regression that crept in between two known-good states. It refuses to theorise until it has a **tight feedback loop** — one command that already goes red on *this* bug — then fixes with a regression test. Its post-mortem hands off to **`/improve-codebase-architecture`** when the real finding is that there's no good seam to lock the bug down.

- **A huge, foggy effort — a greenfield project or a huge feature build, too big for one session** → **`/wayfinder`**, the most cognitively demanding flow here. When the way from here to the destination isn't visible yet, it charts a **shared map** of **decision tickets** on the issue tracker and resolves them one at a time — producing **decisions, not deliverables** — until the fog is pushed back and the way is clear. Where **`/grill-with-docs`** sharpens an idea you can hold in one session, wayfinder is for the idea you can't — and `/grill-with-docs` **escalates you here** the moment its opening sizing shows the effort is this shape (it can't invoke wayfinder — both are user-invoked — so it hands off). It's slower and denser, so save it for exactly that, never a well-scoped feature.

  When the map clears, **it hands off, it doesn't build**: merge onto the main flow at **`/to-spec`**, which collapses the map's linked decisions into a buildable plan, then `/to-waves` (if the scope is still big), `/to-tickets`, and `/implement` as usual. Looping the map straight into `/implement` skips that collapse and throws the linked detail away — go straight to `/implement` only when the effort turned out genuinely small.

## Codebase health

Not feature work — upkeep.

- **`/improve-codebase-architecture`** — run whenever you have a spare moment to keep the codebase good for agents to operate in. It surfaces **deepening opportunities**; picking one _generates an idea_ you can take into the main flow at `/grill-with-docs`. It's the survey that finds the candidates; **`/codebase-design`** (below) is the bench you design the chosen one on.

## Vocabulary underneath

Four model-invoked references that run *beneath* the other skills — each the single source of truth for its vocabulary or method. Reach for them directly when the **words** (or the **critique**), not the process, are the problem; or let the skills above pull them in.

- **`/domain-modeling`** — sharpen the project's *domain* language: challenge a fuzzy term, resolve an overloaded word ("account" doing three jobs), record a hard-to-reverse decision as an ADR. It's the active discipline `/grill-with-docs` drives to keep `CONTEXT.md` a clean glossary.
- **`/codebase-design`** — the deep-module vocabulary (module, interface, depth, seam, adapter, leverage, locality) for designing a module's *shape*: a lot of behaviour behind a small interface at a clean seam. `/tdd` and `/improve-codebase-architecture` both speak it.
- **`/design-taste`** — the *visual and interaction* vocabulary (the three dials — variance, motion, density — plus typography, spacing, tokens, depth, motion, and the anti-slop tells) for making UI look considered rather than machine-default. It's the active discipline `/grill-design` drives to keep a clean `DESIGN.md`, and the taste `/mockup`, `/open-design`, and `/prototype` draw against. The design-side counterpart to `/domain-modeling`.
- **`/critical-qa`** — the *QA critique* method: generative probes (CRUD-completeness, action→consequence, state quality, native controls, shortest-path) and a grilling posture that surface **what's missing and what's weak**, not just whether the spec was met. It's the eye `/manual-qa` runs beyond pass/fail — the validation-side counterpart to `/design-taste`.

## Crossing sessions

- **`/handoff`** — when a thread is full or you need to branch off (e.g. into a `/prototype` session), this compacts the conversation into a markdown file. You don't continue in place — you **open a new session and reference that file** to carry the context across. It's the bridge between context windows, in either direction. Use it when you want a **fresh session** but need the **current conversation preserved**.
- **`/compact`** (built-in) — stay in the **same conversation**, letting the earlier turns be summarized. Use it at **intentional breaks between phases**, when you don't mind losing the verbatim history. Don't compact mid-phase — the agent can lose its way. `/handoff` forks; `/compact` continues.

## Standalone

Off the main flow entirely.

- **`/grill-me`** — the same relentless interview as `/grill-with-docs`, but for when you have **no codebase**. Stateless: it saves nothing locally, builds no `CONTEXT.md`. Reach for it to sharpen any plan or design that doesn't live in a repo.
- **`/prototype`** — a small, throwaway program that answers one design question: does this state model feel right, or what should this UI look like. Throwaway from day one — keep the answer, delete the code. It's the detour in step 2 of the main flow, but reach for it any time a design question is hard to settle on paper.
- **`/mockup`** — a **promotable** low-fi render in the project's real stack, on a `/mockup` route with mock data, built to **align** on coverage and flow before building — then kept and grown into the feature (mock → real), never thrown away. Where `/prototype` is throwaway and answers *one* question with several variations, `/mockup` is promotable and shows *one* direction. It's **optional**, but when adopted it becomes the **canonical source of the frontend's structure**: every feature is mocked into it (covering the user stories, ADRs, diagrams, and `DESIGN.md`) and promoted from it in place, waves and tickets slice it, and the invariant holds — **nothing ships on the frontend that isn't in the mockup first** (which `/pre-flight` enforces). The polished visual look is not its job — that's `/open-design`. Reach for it any time you want to see a flow end-to-end before committing to it.
- **`/open-design`** — generates the flow's **hi-fi visual design** as a **binding reference** the shipped UI must match, from `DESIGN.md` + the mockup's screen inventory, using Open Design (an AI design engine). Unlike `/mockup`, it's **not** code in the project's stack — it's a standalone artifact you build *toward*, the way a team builds toward a Figma. It **replaces the old hi-fi mockup**: `/mockup` owns structure and coverage, `/open-design` owns the look. `/pre-flight` confirms it exists before a polished build; `/manual-qa` checks the shipped FE matches it after.
- **`/research`** — delegate reading legwork to a **background agent**: it investigates a question against **primary sources**, then leaves a cited Markdown file in the repo. Keep working while it reads. The file it produces is something to take *into* the main flow at `/grill-with-docs` — research feeds the thinking, it doesn't replace it.
- **`/teach`** — learn a concept over multiple sessions, using the current directory as a stateful workspace.
- **`/writing-great-skills`** — reference for writing and editing skills well.

## Precondition

**`/setup-tutu-skills`** — run before your first engineering flow to configure the issue tracker, triage labels, and doc layout the other skills assume. Custom issue trackers also work.
