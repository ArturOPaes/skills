---
"mattpocock-skills": minor
---

Make `/e2e` criterious, not a rubber stamp — it now reads the acceptance criteria critically as it writes.

Encoding criteria into tests is the moment you can see what they miss. `/e2e` now runs the `/critical-qa` critique over the flow — states, actions, permissions, personas — validating the happy path first, then probing around it for the empty/error state no criterion mentions, the action with no criterion behind it, the permission direction left untested, the cross-persona handoff that stops at "sent."

Each is raised as a **gap finding** (a missing criterion routed back to the spec / `/to-tickets` / `/manual-qa`), never invented as a passing test — the discipline holds (the criterion is still the test), but thin criteria no longer pass unquestioned.
