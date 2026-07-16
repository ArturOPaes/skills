---
"mattpocock-skills": minor
---

Restructure the flow so the **whole-product overview is designed and reviewed before any implementation**, and waves only sequence the build.

- **Overview upfront, waves in the build phase.** `grill-design` → `mockup` → `blueprint` now run for the **whole product** before a line is built, not per wave. `to-waves` is reframed as an **optional build-phase step** that sequences delivery into milestones after the overview is greenlit — it no longer partitions the design.
- **`pre-flight` is now the overview gate.** It runs **once**, before the build begins, checking that docs, diagrams, and mockup cover **every** user story (not per wave). After it greenlights, the invariant that no frontend exists outside the mockup keeps the overview true as the build proceeds.
- **Mockup gets a low-/hi-fi choice.** Two fidelities of the *same* canonical mockup: low-fi = real components + structure + every field/action, no polish (validates coverage/flow fast); hi-fi = the design-taste polish promoted in place on the same code. The coverage invariant holds from low-fi.
- **Blueprint gains a 9th diagram — system design.** A per-flow runtime-topology diagram (client → API → services → stores → queues → external) with **bottleneck candidates flagged** (hot paths, N+1, synchronous coupling, single points of failure).
- **Wave validation is a choice** — `manual-qa` at the end of each wave by default, or skip to a single check at the very end.

Updated: `ask-tutu` (the flow), `mockup`, `pre-flight`, `to-waves`, `blueprint` (SKILL + DIAGRAMS), and their docs pages. Version bumped to `1.8.0`.
