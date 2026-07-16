---
"mattpocock-skills": minor
---

Add a **design-taste layer** to the design flow, distilled from the frontend-taste skills community (impeccable, taste-skill, ibelick/ui-skills, emilkowalski/skills, Vercel's web-design-guidelines).

- **`design-taste`** (new, model-invoked) — the single source of truth for *visual and interaction* design taste: the three dials (variance, motion, density), principles by axis (typography, spacing, colour/tokens, layout, depth), an anti-slop pre-flight checklist ([ANTI-SLOP.md](../skills/engineering/design-taste/ANTI-SLOP.md)), and a motion discipline ([MOTION.md](../skills/engineering/design-taste/MOTION.md)). It also owns the active discipline of capturing a project's design language into `DESIGN.md`. The design-side counterpart to `domain-modeling`, sitting in "Vocabulary underneath".
- **`grill-design`** (new, user-invoked) — a grilling session that settles a project's design language and writes `DESIGN.md` inline. The design-side counterpart to `grill-with-docs`; drives `design-taste` the way `grill-with-docs` drives `domain-modeling`.
- **`mockup`** and **`prototype`** now draw *against* `design-taste`: `mockup` obeys `DESIGN.md` when it exists and runs the anti-slop checklist; `prototype`'s UI variants stay structurally different but each passes the taste tells.
- `ask-tutu`, the top-level and Engineering READMEs, the plugin manifest, and docs pages updated to route and describe both new skills. Plugin/package version bumped to `1.5.0`.
