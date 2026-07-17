Quickstart:

```bash
npx skills add ArturOPaes/skills --skill=critical-qa
```

```bash
npx skills update critical-qa
```

[Source](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/critical-qa)

## What it does

`critical-qa` is the single source of truth for QA *critique* — the method for interrogating a running product the way [grilling](https://github.com/ArturOPaes/skills/tree/main/skills/productivity/grilling) interrogates a plan, so a pass finds what's missing and what's weak, not just whether the spec was met.

It carries generative probes rather than a list of symptoms, because a checklist can only find what's on it. The probes *manufacture* candidate findings from any app the critique has never seen — so the method generalises instead of enumerating the bugs of one project.

## When to reach for it

Type `/critical-qa`, or the agent reaches for it automatically when a QA pass needs a critical eye rather than a pass/fail checklist, when a built UI needs reviewing for gaps and improvements, or when [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa) needs the critique method.

Reach for it when the problem is *finding what a checklist can't* — the missing action, the state change that doesn't reflect, the raw default where the design language wants a real state. When you instead want to walk a task's acceptance criteria with a human giving the verdict, that's [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa), which now runs this critique beyond pass/fail.

## The probes, the journeys, and the posture

Three things make this skill click:

- **The generative probes** — CRUD-completeness, action→consequence, state quality, native/unstyled controls, and shortest-path/friction. Each is a *question that produces findings*, run on every screen, so it works on an unfamiliar app.
- **Journeys and personas, from zero** — the deepest gaps hide in flows and roles, not single screens. So the critique also walks the product end-to-end from a clean slate for **every persona the project defines**: signup and onboarding, cross-persona handoffs (invite → received → accepted → in the platform with the right access), and permissions in both directions (allowed *and* blocked).
- **The grilling posture** — two passes kept separate (conformance, then critique), one thing at a time, never satisfied with "it works", every finding carrying a recommended fix, and *missing* (a gap) separated from *weak* (an improvement) because they're closed differently.

Where a project has a `DESIGN.md` ([design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste)), its dials and tokens are the bar the critique measures against; where it's thin, the anti-slop tells still apply.

## Where it fits

`critical-qa` is **vocabulary underneath** — a discipline that runs beneath the other skills rather than a step in the chain, alongside [domain-modeling](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/domain-modeling), [codebase-design](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/codebase-design), and [design-taste](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/design-taste). It's the validation-side counterpart to `design-taste`: where that keeps a UI from looking machine-default, this keeps a QA pass from being a rubber stamp. It's driven by [manual-qa](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/manual-qa) (a human running the critique beyond the acceptance criteria). When you're unsure which skill or flow fits, [ask-tutu](https://github.com/ArturOPaes/skills/tree/main/skills/engineering/ask-tutu) routes you.
