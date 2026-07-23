---
name: tutu-loop-design
description: The design satellite of tutu-loop — produces the binding hi-fi visual reference a build must match, plus the connective screen/traceability map that the gate checks. Self-contained; consolidates hi-fi design, low-fi structure, design taste, and blueprint. Invoked only by the tutu-loop coordinator.
disable-model-invocation: true
---

# tutu-loop · design

The design step of [tutu-loop](../SKILL.md). It produces the **binding visual reference** the shipped frontend must match, and the **connective map** (screen inventory + traceability) the [gate](../verify-design/SKILL.md) later checks the specs against. It is **self-contained**: it consolidates the substance of hi-fi design, low-fi structure, design taste, and the blueprint into one satellite, and references only its sibling satellites — never the tutu skills.

`tutu-loop` runs **hi-fi-only**: the sole design artifact is the hi-fi reference. A low-fi structure pass is a **bootstrap**, used only when the screen set isn't settled yet.

## What it produces

1. **The hi-fi reference** — the polished look the build is required to match, kept as a **standalone artifact** at `<project>/design/open-design/`, *not* code in the stack. The frontend is built *toward* it (the way a team builds toward a Figma), and [validate](../validate/SKILL.md) checks the shipped UI against it. A change to the look comes back here and re-reviews — it never drifts silently during the build.
2. **`DESIGN.md`** — the brand contract: the three dials, tokens, type, and motion the reference speaks.
3. **The connective map** — a screen inventory + traceability table (`Screen:<Name>` → the `US-<n>` it serves → the `ADR-<n>` that shaped it), the backbone the [gate](../verify-design/SKILL.md) measures coverage against.

## The brand contract comes first

The reference is only as good as its brief. Before generating anything:

- **Settle the three dials** and record them in `DESIGN.md` (most "does this look good" disputes are really disputes about a dial):
  - **Variance** — safe/grid-locked ↔ asymmetric/expressive. Data tools low, marketing high.
  - **Motion** — still ↔ rich hover/scroll choreography. Noise on a dashboard, life on a landing page.
  - **Density** — airy/generous ↔ dense/pro-tool. Neither is better; they serve different jobs.
- **Ask for references** — screenshots, a design system, component-library links, an app to echo. Take *structure, spacing rhythm, and accessible patterns* from them, but **bind every colour/radius to the project's own tokens** — never paste hardcoded styles.

## Taste — the quality bar (anti-slop)

Design **against slop**: the default an untended agent reaches for is the median SaaS template — Inter everywhere, purple→pink gradient, cards-in-cards, bouncy easing, pure-black text. Every choice must be deliberate, on a scale, bound to a token. Pass this checklist over every screen before calling it done:

- **Type** — one or two faces on a modular scale, limited weights; line-height tightens as size grows; measure 45–75ch; tabular numerals in tables; negative letter-spacing on big headings.
- **Spacing** — every gap off one 4/8px scale; proximity groups before borders do; consistent vertical rhythm.
- **Colour** — every colour a semantic token (`bg`/`fg`/`border`/`accent`), never a raw hex at a call site; neutrals tinted toward the brand hue; text near-black, never `#000`; one accent, spent on the single primary action; contrast clears WCAG AA.
- **Layout** — one primary action per view, unmistakably loudest; everything on a grid; structure with space and the type scale before reaching for a card/border.
- **Depth** — pick *one* system (soft layered shadows *or* flat-with-borders) and hold it; shadows tinted, soft, one light source; never a blurry pure-black shadow.
- **Motion** — earns its place, natural easing, interruptible, respects reduced-motion.

`DESIGN.md` is the visual glossary (dials, tokens, type/motion language, the anti-slop tells this project watches for) — not a spec or a component inventory; keep implementation detail out.

## The loop

1. **Settle coverage first.** There must be a screen set to dress. On a settled scope, that's the screens the [discovery](../discovery/SKILL.md) specs and stories name. If the screen set is still foggy, run the **bootstrap**: a low-fi structure pass first (real components, real tokens, mock data behind one seam, every screen/field/action/state present but no polish) to align on *coverage and flow* — then design hi-fi over the settled set. Designing hi-fi before coverage is settled polishes screens that will change.
2. **Assemble the brief** from `DESIGN.md` + the screen/state inventory (happy, empty, loading, error), and generate the hi-fi artifact. You're dressing screens that already exist — never inventing new ones.
3. **Link it in** at `<project>/design/open-design/`, next to the code that must match it.
4. **Draw the connective map** — screen inventory + traceability table with stable IDs (`Screen:<Name>`, `US-<n>`, `ADR-<n>`), Mermaid so it renders and diffs. Every screen traces back to at least one `US-<n>`; a dangling node is a finding, surfaced, not invented over.
5. **Review against `DESIGN.md`.** Divergence from the brand contract is a fix now, not after 20 screens are built to a wrong look.
6. **Hand off.** The reference is fixed; the [build](../build/SKILL.md) matches it, the [gate](../verify-design/SKILL.md) checks coverage against the map.

## Rules

1. **Reference, not promote-in-place.** The hi-fi is a standalone `.html` the build works *toward*; don't paste its raw markup into production expecting it to be the frontend.
2. **Dress decided screens only.** Every screen traces to a `US-<n>`/`ADR-<n>`/`DESIGN.md` definition. No screen with no decision behind it — ask, or route it to [discovery](../discovery/SKILL.md).
3. **No silent drift.** A look change goes through here and re-reviews, so the binding target and the build never disagree.
4. **Bind to tokens.** References seed structure and rhythm; their colours/radii are theirs. Bind to this project's tokens or you've forked someone else's design system by accident.
5. **Synthesise the map, don't decide it.** The connective map renders decisions; a missing decision (a story with no screen, a screen with no story) routes back to [discovery](../discovery/SKILL.md).

## Output

The hi-fi reference at `<project>/design/open-design/`, a `DESIGN.md` brand contract, and the connective screen/traceability map — the three inputs the [gate](../verify-design/SKILL.md) needs to prove the design covers every story and ADR before the build begins.
