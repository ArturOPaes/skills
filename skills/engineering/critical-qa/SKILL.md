---
name: critical-qa
description: Shared discipline for critically interrogating a running product the way grilling interrogates a plan — generative probes and a relentless posture that surface what's missing and what could be better, not just whether the spec was met. Use when QA needs a critical eye rather than a pass/fail checklist, when reviewing a built UI for gaps and improvements, or when another skill (manual-qa, orca-qa-loop) needs the critique method.
---

# Critical QA

QA the way [grilling](../../productivity/grilling/SKILL.md) questions a plan: **relentless, generative, never satisfied.** The default QA pass checks the built thing against the spec — it confirms what was *asked for* and, by construction, is blind to two things the spec never named: **what's missing**, and **what's merely weak**. Critical QA is the discipline of finding those anyway.

Two jobs live here, like the other discipline layers:

- **The probes and the posture** below are the *source of truth* other skills question against — the method [manual-qa](../manual-qa/SKILL.md) and [orca-qa-loop](../../in-progress/orca-qa-loop/SKILL.md) reach for when they need a critical eye, not a checklist.
- **The active discipline** is running that critique on a running product: interrogate each screen *and each persona's journey from zero*, surface findings, attach a recommended fix to each.

The defining move: **a checklist can only find what's on it.** So critical QA doesn't carry a list of symptoms to look for — it carries **generative probes** that *manufacture* candidate findings from whatever app is in front of it, plus a posture that refuses to stop at "it works."

## The posture — grilling, pointed at a built UI

- **Two passes, kept separate.** First **conformance** — does the UI match its definition (the spec, mockup, blueprint). Then **critique** — the generative pass below, which asks what the definition never did. Conformance findings are bugs; critique findings are gaps and improvements. Don't let the first pass' "it matches" end the interrogation.
- **One thing at a time, never satisfied.** Take a screen, exhaust it, move on. "It works" is where the questioning *starts*, not ends: a screen can be fully functional and still be missing an obvious action or wearing a raw default.
- **Every finding carries a recommended fix.** As grilling attaches a recommended answer to each question, each finding attaches the change that would close it — so it's actionable, not just a complaint.
- **Separate *missing* from *weak*.** A **gap** is something the user needs that isn't there (route it as a conformance/coverage fix, or as a new decision). An **improvement** is something present but sub-par (route it back through the definition first — never invent product silently). Both are findings; they're closed differently.

## The probes — generative, not a symptom list

Run each probe on every screen. A probe is a *question that produces findings*; it generalizes, so it works on an app it has never seen.

1. **CRUD-completeness.** For every noun the product manages — every entity, setting, and preference the user can *see* — ask: can they **create, read, update, and delete** it where they'd expect to? A value shown but not editable, an item listed but not removable, a setting displayed but read-only — each is a gap.
2. **Action → consequence.** Perform every state-changing action, then check the UI reflects the new state **everywhere it appears** — counters, badges, quotas, lists, summaries. An action whose effect isn't visible where the user would look is a gap, even when the write succeeded. When the action **hands off to a third-party service** you can't complete for real (payment, auth, e-sign), drive the handoff in the provider's *sandbox*, **simulate the callback** it would send on success (its test webhook), and verify the consequence landed — a checkout that redirects but whose webhook never upgrades the plan or raises the quota is the classic gap.
3. **State quality.** For every transient and edge state — loading, empty, error, disabled, zero-results, over-limit — ask: is this a *designed* state, or a raw default? Placeholder text standing in for a loading state, a browser `alert()`, an unhandled error, a blank empty screen — each is an improvement (or a gap, if the state is simply absent).
4. **Native / unstyled controls.** Flag every control that betrays the design system — native file inputs, default selects, unstyled scrollbars, browser dialogs, system tooltips. Anything the user would recognize as "the browser's," not "the product's," is an improvement.
5. **Shortest path & friction.** For each outcome the user wants, count the steps and look for dead ends, detours, and re-entry of what the app already knows. A flow that costs more than it should, or a navigation node that goes nowhere, is a gap in the *experience* even when every screen individually works.

The probes compose with the design and product lenses — hierarchy, affordance, and consistency (a designer's eye) and outcome, coverage, and flow (a PO's eye). Where a project has a `DESIGN.md` ([design-taste](../design-taste/SKILL.md)), its dials and tokens are the bar the critique measures against; where it's thin, the anti-slop tells still apply.

## Journeys and personas — validate from zero

The probes above interrogate *screens*. The deepest gaps hide in *journeys* and *roles* — and a QA that starts from a seeded dashboard is blind to all of them. So the critique also walks the product **end-to-end, from a clean slate, for every persona the project defines**:

- **From zero.** Start at **signup and onboarding**, not a pre-seeded state. The first run — the empty account, the onboarding path, the first successful action — is where the most gaps live and where seeded QA can't look.
- **Every persona.** Enumerate the persona/role types the project defines (client, provider, admin, member…) and run **each one's journey from zero** through its core jobs. A flow that works for one role and breaks for another is a gap only per-persona testing finds.
- **Cross-persona handoffs.** Where one persona acts on another — an invite, an assignment, a shared resource — validate the **whole handoff**, both sides: the sender's action, *delivery* (did the other persona actually receive it), and the receiver completing it (did they accept and **get into the platform with the right access**). A handoff that half-works — invite sent but never received, accepted but no access — is the classic gap.
- **Permissions, both directions.** For each persona, check that it can do everything its role **allows** *and* is blocked from everything it **doesn't**. Test the negative — a member reaching an owner-only action, one client seeing another's data — not just the happy allow.

Enumerate personas and their journeys from the definition (user stories, roles, the blueprint's flows) before walking them; a persona the project defines but the QA never runs is itself a coverage gap.

## Findings — how the critique comes out

Each finding, written the way durable issues are written — **behaviour in the user's words, not code**:

- **what** — expected vs. observed, as an experience (never a file path or a stack trace, which go stale).
- **class** — `gap` (missing) or `improvement` (weak), and which probe/lens surfaced it.
- **recommended fix** — the change that closes it.
- **trace** — the definition node it touches (a user story, a screen, `DESIGN.md`), so a fix can update the definition rather than the code alone.

Keep findings **thin and independent** — one behaviour each — so they can be fixed and verified in parallel.

## Who drives it

This is the *method*, not the runner:

- [manual-qa](../manual-qa/SKILL.md) runs it **with a human** — a critical pass on a built task, the human giving the verdict.
- [orca-qa-loop](../../in-progress/orca-qa-loop/SKILL.md) runs it **unattended** — the critique that turns its screen sweep from a checklist into an interrogation, dispatching each finding to a worker.

Reach for it directly whenever a QA pass needs to find what a checklist can't.
