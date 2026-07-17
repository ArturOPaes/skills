---
"mattpocock-skills": minor
---

Make the **hi-fi mockup a binding visual reference** and validate the shipped FE against it at the gates — so a hi-fi mockup you aligned on is actually built to, not wasted.

- **`mockup`** — states that when hi-fi, the mockup is the binding visual reference the final FE must *match* (not just be covered by). Because it's promoted in place, alignment is by construction; the gates verify it held.
- **`implement`** — frontend work promotes the hi-fi mockup **in place** and must match it (layout, spacing, states, components); no restyling or drift — change the mockup first if something must change.
- **`pre-flight`** (pre-build gate) — if the FE is meant to be polished, requires a **hi-fi** mockup as the alignment target; a low-fi mockup passes on coverage but defers visual fidelity as a recorded step (promote low → hi before shipping).
- **`manual-qa`** (post-build gate) — adds an explicit check: when a hi-fi mockup exists, compare the built UI against it; divergence is a **finding**, not a matter of taste.

Docs pages for mockup, pre-flight, and manual-qa updated. Ships in `1.9.0`.
