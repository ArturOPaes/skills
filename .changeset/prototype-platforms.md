---
"mattpocock-skills": minor
---

Make **`prototype`**'s UI branch **platform-aware and recommendation-first** (inspired by `will-ness-ai/grilling-frontend-prototyping`, adapted to stay one-shot).

- **Platform first.** The UI branch now asks the target platform — web / mobile web / native / combination — before drafting. It renders **matching the project's real stack**: React Native/Expo projects prototype native there; web-only projects render mobile/native variants in a phone frame on a web route. For web + mobile-web combinations it produces one **responsive** design toggled between desktop and a phone frame; anything involving native gets **separate variants per platform**.
- **Recommendation-first.** Variant A is the recommended direction (marked, with a one-line rationale); the prototype opens on it. B and C stay genuine alternatives, not strawmen.
- **Platform conventions** land in `design-taste` as a new [PLATFORMS.md](../skills/engineering/design-taste/PLATFORMS.md) (touch targets, safe areas, native navigation idioms, hover/keyboard/density on web), pulled in by the prototype; `DESIGN.md` now records which platforms the project targets.

Stays one-shot (no multi-round convergence) — the prototype keeps its "throwaway that answers one question" nature; refine by re-running on the winning direction. Docs pages, both READMEs updated. Plugin/package version bumped to `1.6.0`.
