---
"mattpocock-skills": minor
---

Make **`mockup`** the **canonical source of the frontend** when adopted. It stays optional, but the moment a project uses one it is no longer a per-wave sketch — it's the single source of truth the whole frontend is mocked into and promoted from.

- **Covers everything decided.** Every user story, every ADR with a frontend consequence, the blueprint's diagrams, and the `DESIGN.md` definitions resolve to something in the mockup.
- **Implemented in place.** Because the mockup is promotable, features aren't rebuilt elsewhere — mock data is swapped for real, wave by wave, ticket by ticket, so the mockup and the shipped frontend converge into the same code.
- **The invariant: nothing on the frontend that isn't in the mockup first.** Waves and tickets slice the mockup incrementally, but a ticket only promotes a slice that already exists; anything new is added to the mockup (traced to its owning decision) before it's built, never invented in production code.

Propagated: `pre-flight` now fails a wave that would build frontend absent from the mockup; `to-tickets` slices frontend tickets as in-place promotions of the mockup; `ask-tutu` and the mockup docs page describe the canonical-source role and the invariant. Version bumped to `1.7.0`.
