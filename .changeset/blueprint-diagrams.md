---
"mattpocock-skills": minor
---

Add **`blueprint`** (new, user-invoked) — a synthesis skill that turns a spec's user stories, the domain model, and the UI into a `BLUEPRINT.md` of Mermaid diagrams giving a macro, *connected* view of a flow before implementation. Like `to-spec`/`to-tickets`, it does not interview — it draws what's already decided.

Eight diagram types, all Mermaid so they render inline on GitHub. Five are the always-drawn connective backbone: **screen inventory** (table), **navigation map**, **screen detail map** (each screen's fields and actions, with actions linked to the screens they lead to — the one to review field-by-field), **user flow**, and the signature **traceability map** (`user story → screen → ADR → ticket`). Three are per-flow: **screen states**, **sequence**, and **data (ER)**. Stable IDs (`US-<n>`, `ADR-<n>`, `#<n>`, `Screen:<Name>`) reused across every diagram are what wire them into one traceable map instead of disconnected drawings.

Sits after `to-spec`/`mockup` and before `to-tickets` in the per-wave flow; `to-tickets` now slices against a `BLUEPRINT.md` when one exists. Routed by `ask-tutu`, listed in the top-level and Engineering READMEs (Engineering, user-invoked), in the plugin manifest, and documented at `docs/engineering/blueprint.md`. Ships in the same `1.5.0` release as the design-taste layer.
