---
"mattpocock-skills": minor
---

Add **`pre-flight`** (new, user-invoked) — a pre-implementation readiness gate, the pre-build twin of `manual-qa`. Run once per wave, right before `implement`, it confirms the wave's **documentation, diagrams, and hi-fi layout** are current and *cover* it, walks them with a human to review and adjust, and only then greenlights the build.

- **Coverage, not existence.** Cross-checks the three artifacts against the wave's user stories and tickets: a `BLUEPRINT.md` missing half the stories, or a mockup missing a screen a ticket builds, is a fail.
- **Routes, never patches.** Each gap goes back to its owning skill to refresh (docs → `grill-with-docs`/`domain-modeling`, `DESIGN.md` → `grill-design`, diagrams → `blueprint`, hi-fi → `mockup`); pre-flight re-checks. A no-UI wave needs no hi-fi/`DESIGN.md`; a deliberate skip is a recorded waiver.
- **Verdict is the human's** — it never greenlights on your behalf.

This makes `mockup`, `blueprint`, and `grill-design` effectively non-optional (the gate won't greenlight a wave they haven't covered). Wired into `ask-tutu` (the step before `implement`, twinned with `manual-qa`), `implement` (flag if the gate hasn't run), the top-level and Engineering READMEs, the plugin manifest, and `docs/engineering/pre-flight.md`. Ships in the same `1.6.0` release as the prototype platform work.
