---
name: manual-qa
description: Bring a task into a validatable state and walk its acceptance criteria with a human — either locally with self-created seeds, or against an environment with defined credentials. Use to manually validate a built task in the real app before shipping.
disable-model-invocation: true
---

# Manual QA

Get a built task into a state where it can be exercised in the **real app**, then walk its acceptance criteria **with a human**.

The defining constraint: **it never declares the task validated — you do.** The skill sets the stage (brings the app up, reaches the right state, lays out what to check) and captures your verdict. It orchestrates the validation; it doesn't assert the result on your behalf.

## When to reach for it

You invoke this by typing `/manual-qa` — the agent won't reach for it on its own, because it can bring up an app and touch an environment, and that must be a deliberate act.

Reach for it to validate a just-built task before shipping — the human pass for what automation can't cheaply judge: does it *feel* right, does it *look* right, does it hold up on real-shaped data. It is not a manual re-run of [e2e](../e2e/SKILL.md): where a criterion already has a green e2e test, trust it and spend the manual effort on the gaps automation doesn't cover.

## Pick a mode — ask the user

Two ways to reach a validatable state. **Ask which one** before doing anything:

- **Local, with seeds.** Self-sufficient: discover the project's run and seed commands, create deterministic seed data for the *specific flow* under test, and bring the app up locally. If the project has no seed mechanism, agree a minimal one for this flow — never invent unrealistic data silently.
- **Environment.** Reach a target environment (preview, staging) using credentials supplied at runtime, and exercise the task there.

## Credentials and safety — hard rules

The local mode is safe; touching a live environment is not. These are rules, not options:

- **Credentials come from the runtime** — an env var, a secrets manager, or pasted by the user. Never read them from committed files, never print them, never write them into the repo.
- **The target environment is a confirmed choice.** **Never production without explicit confirmation** — validating against prod can mutate real data. When in doubt, ask which environment you're pointed at.
- **Read-only by default.** Any write or destructive action against a real environment is confirmed first. Prefer a disposable local seed to mutating shared state.

## The loop

1. **Identify the task and its acceptance criteria** — the ticket or user story under validation.
2. **Ask the mode** — local-with-seeds, or a named environment.
3. **Reach the validatable state** — seed the specific flow and bring the app up locally, or connect to the environment.
4. **Walk each criterion with the user.** Show what to check; capture pass / fail and a note per criterion. Do not mark a criterion passed on the user's behalf.
5. **Record the verdict.** Pass → note the validation on the ticket. Fail → hand the finding to [diagnosing-bugs](../diagnosing-bugs/SKILL.md), or file it through [triage](../triage/SKILL.md).

Validate one task or flow, not the whole app.
