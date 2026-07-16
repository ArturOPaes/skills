# Engineering

Skills I use daily for code work.

## User-invoked

Reachable only when you type them (Claude Code: `disable-model-invocation: true`; Codex: `policy.allow_implicit_invocation: false` in `agents/openai.yaml`).

- **[ask-tutu](./ask-tutu/SKILL.md)** — Ask which skill or flow fits your situation. A router over the user-invoked skills in this repo.
- **[grill-with-docs](./grill-with-docs/SKILL.md)** — Grilling session that also builds your project's domain model, sharpening terminology and updating `CONTEXT.md` and ADRs inline.
- **[grill-design](./grill-design/SKILL.md)** — Grilling session that settles your project's visual and interaction design language — dials, references, tokens — and captures it in `DESIGN.md` inline. The design-side counterpart to `grill-with-docs`.
- **[triage](./triage/SKILL.md)** — Move issues through a state machine of triage roles.
- **[improve-codebase-architecture](./improve-codebase-architecture/SKILL.md)** — Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
- **[setup-tutu-skills](./setup-tutu-skills/SKILL.md)** — Configure this repo for the engineering skills (issue tracker, triage labels, domain doc layout). Run once per repo.
- **[to-spec](./to-spec/SKILL.md)** — Turn the current conversation into a spec and publish it to the issue tracker.
- **[to-waves](./to-waves/SKILL.md)** — Partition a large scope into ordered, validatable waves (milestones) before slicing any of them into tickets — for work too big to slice in one pass.
- **[blueprint](./blueprint/SKILL.md)** — Synthesize a spec's user stories, the domain model, and the UI into a `BLUEPRINT.md` of Mermaid diagrams (screen inventory, navigation map, per-screen field/action maps, user flow, traceability, states, sequence, data) for a macro visual view before implementation. No interview.
- **[to-tickets](./to-tickets/SKILL.md)** — Break any plan, spec, or conversation into a set of tracer-bullet tickets, each declaring its blocking edges — text in a local file, or native blocking links on a real tracker.
- **[implement](./implement/SKILL.md)** — Build the work described by a spec or set of tickets, driving `/tdd` at pre-agreed seams and closing out with `/code-review` before committing.
- **[manual-qa](./manual-qa/SKILL.md)** — Bring a built task into a validatable state — locally with self-created seeds, or against an environment with defined credentials — and walk its acceptance criteria with a human. The manual counterpart to `/e2e`.
- **[wayfinder](./wayfinder/SKILL.md)** — Plan a huge chunk of work — more than one agent session can hold — as a shared map of decision tickets on the issue tracker, resolved one at a time until the way to the destination is clear.

## Model-invoked

Model- or user-reachable (rich trigger phrasing so the model can reach for them).

- **[prototype](./prototype/SKILL.md)** — Build a throwaway prototype to answer a design question: a runnable terminal app for state/logic, or several toggleable UI variations.
- **[mockup](./mockup/SKILL.md)** — Build a high-fidelity, promotable mockup of a whole flow in the project's real UI stack, on a dedicated route with mock data, to align on it before building — the opposite of a throwaway prototype.
- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)** — Disciplined diagnosis loop for hard bugs and performance regressions: reproduce → minimise → hypothesise → instrument → fix → regression-test.
- **[research](./research/SKILL.md)** — Investigate a question against high-trust primary sources and capture the findings as a cited Markdown file in the repo, run as a background agent.
- **[tdd](./tdd/SKILL.md)** — Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **[e2e](./e2e/SKILL.md)** — Write end-to-end browser tests from a ticket's acceptance criteria or user stories, or backfill e2e onto work that shipped without it.
- **[domain-modeling](./domain-modeling/SKILL.md)** — Actively build and sharpen a project's domain model — challenge terms, stress-test with scenarios, update `CONTEXT.md` and ADRs inline.
- **[codebase-design](./codebase-design/SKILL.md)** — Shared discipline and vocabulary for designing deep modules: small interfaces, clean seams, testable through the interface.
- **[design-taste](./design-taste/SKILL.md)** — Shared vocabulary and principles for visual and interaction design taste — the three dials, typography, spacing, tokens, depth, motion, anti-slop tells — plus the `DESIGN.md` discipline.
- **[code-review](./code-review/SKILL.md)** — Two-axis review of the diff since a fixed point: **Standards** (does it follow the repo's coding standards, plus a Fowler smell baseline?) and **Spec** (does it faithfully implement the originating issue/PRD?), run as parallel sub-agents.
- **[resolving-merge-conflicts](./resolving-merge-conflicts/SKILL.md)** — Work through an in-progress git merge or rebase conflict hunk by hunk, resolving by intent traced to each side's primary source, then finish the operation — never `--abort`.
