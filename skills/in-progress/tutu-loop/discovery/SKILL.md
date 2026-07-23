---
name: tutu-loop-discovery
description: The discovery satellite of tutu-loop — sharpens an idea or design into verifiable specs (user stories + ADRs) and a domain glossary, run unattended: it resolves facts itself and batches genuine decisions into a single needs-decision escalation. Self-contained; consolidates grilling, domain-modeling, research, and the wayfinder decision-map. Invoked only by the tutu-loop coordinator.
disable-model-invocation: true
---

# tutu-loop · discovery

The spec-sharpening step of [tutu-loop](../SKILL.md). It turns an idea or a design into **sharp, verifiable specs** — user stories (`US-<n>`) and frontend/architectural decisions (`ADR-<n>`) — plus a domain glossary, so no worker ever builds on a vague requirement. It is **self-contained**: it consolidates the grilling interview, domain modeling, background research, and the wayfinder decision-map into one satellite, referencing only its siblings — never the tutu skills.

## Run unattended — the loop's rule for a HITL discipline

Grilling is normally human-in-the-loop: facts are looked up, but *decisions are the human's*, put one at a time. `tutu-loop` runs unattended with a **single human gate**, so this satellite adapts the discipline without breaking it:

- **Resolve every fact autonomously.** Anything discoverable from the environment — the design, existing `CONTEXT.md`/ADRs, the codebase, the tracker, or primary sources — is looked up, never asked.
- **Draft a recommended answer for every decision.** Walk the decision tree; for each genuine decision, do the work to recommend one answer with its rationale.
- **Batch the genuine decisions into one `needs-decision` escalation.** A decision is the human's, but the loop doesn't ask them one at a time — it prepares *all* open decisions with recommendations and escalates them together (push-right). The coordinator surfaces that batch; discovery resumes on the answers. A decision the work can't justify is escalated, never invented.

This is where most of the loop's `needs-decision` escalations happen — discovery is the human-decision-heavy phase. Everything downstream should be `continuable`.

## Size the effort first

- **Fits one focused pass** → grill it: walk the decision tree, resolve dependencies one by one, capture as you go.
- **Huge and foggy** (greenfield, sprawling multi-feature) → chart it as a **decision map** rather than charging the destination. Name the **destination** first (what these specs are finding their way to), then map the **frontier** breadth-first: the open decisions and the first takeable steps. The loop's own `/loop` continuation *is* the multi-session mechanism — the ledger holds the decision tickets, the fog (suspected-but-not-yet-sharp questions), and what's out of scope. Resolve the frontier a slice per pass until the way to buildable specs is clear.

## The grilling discipline

Interview relentlessly toward a shared understanding. Walk each branch of the decision tree, resolving dependencies one by one. For every question, attach a **recommended answer**. If a *fact* can be found by exploring the environment, look it up rather than escalating it — only genuine *decisions* go to the human (batched, as above). Don't act on a decision until it's confirmed.

## Domain modeling — capture as you go

Actively sharpen the model while sharpening the specs; write it down the moment it crystallises (don't batch):

- **Challenge against the glossary.** A term that conflicts with `CONTEXT.md` is called out immediately.
- **Sharpen fuzzy language.** Propose a precise canonical term for vague/overloaded ones ("'account' — Customer or User? those are different things").
- **Stress-test with concrete scenarios.** Invent edge-case scenarios that force precision about boundaries between concepts.
- **Cross-reference the code.** If a stated behaviour contradicts the code, surface it.
- **Update `CONTEXT.md` inline** — a pure glossary, devoid of implementation detail. Not a spec, not a scratchpad.
- **Offer an ADR only when all three hold:** hard to reverse, surprising without context, the result of a real trade-off. Miss any one → skip it. Keep frontend-relevant ADRs explicit — the [gate](../verify-design/SKILL.md) checks the design against them.

## Research — for facts outside the working directory

When a decision waits on knowledge outside the repo (a third-party API, a spec, provider behaviour), spin up a **background research agent**: investigate against **primary sources** (official docs, source, first-party APIs — not secondary write-ups), follow every claim to its owning source, and write cited findings to a Markdown file where the repo keeps such notes. Facts resolved this way never become escalations.

## Output

The buildable specs — **user stories** and **frontend/architectural ADRs**, with stable IDs — plus a `CONTEXT.md` glossary and any research notes. This is what the [design](../design/SKILL.md) map is dressed against and what the [gate](../verify-design/SKILL.md) proves the design covers before the [build](../build/SKILL.md) begins. Nothing is done while a genuine decision is unresolved — those ride out as the loop's `needs-decision` batch.
