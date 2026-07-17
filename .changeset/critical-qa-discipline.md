---
"mattpocock-skills": minor
---

Add `/critical-qa` — a shared QA-critique discipline, and wire it into the validation flow.

QA that only walks acceptance criteria is blind to what the spec never named. `critical-qa` is the method for interrogating a running product the way `/grilling` interrogates a plan — relentless, generative, never satisfied — to surface **what's missing and what's weak**.

- **Generative probes**, not a symptom list: CRUD-completeness, action→consequence, state quality, native/unstyled controls, shortest-path/friction — each a question that manufactures findings from any app.
- **Journeys and personas, from zero**: walk the product end-to-end from a clean slate for every persona the project defines — signup/onboarding, cross-persona handoffs (invite → received → accepted → in the platform with access), and permissions in both directions.
- **The grilling posture**: conformance then critique, one thing at a time, every finding with a recommended fix, *missing* separated from *weak*.

It's the validation-side counterpart to `/design-taste`, driven by `/manual-qa` (which now runs the critique beyond pass/fail) and by the in-progress unattended `/orca-qa-loop`.
