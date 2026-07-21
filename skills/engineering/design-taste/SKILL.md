---
name: design-taste
description: Shared vocabulary and principles for visual and interaction design taste — typography, spacing, colour/tokens, layout, depth, motion — plus the active discipline of capturing a project's design language in DESIGN.md. Use when the user wants a UI to look considered rather than generic, wants to pin down a project's visual language, is building or reviewing a mockup or prototype, or when another skill needs the design-taste vocabulary.
---

# Design Taste

Design **against slop**. The default an untended agent reaches for is the median SaaS template — Inter everywhere, a purple→pink gradient, cards nested in cards, bouncy easing, pure-black text. That look is what "AI-generated frontend" has come to mean. Taste is the discipline of not shipping the median: every visual choice is deliberate, on a scale, and bound to the project's own language.

Two jobs live here:

- **The vocabulary and principles** below are the *source of truth* other skills question against — the words and rules `mockup`, `open-design`, `prototype`, and any design review reach for.
- **The active discipline** captures the project's own design language into `DESIGN.md` the moment a choice is made — mirroring how [domain-modeling](../domain-modeling/SKILL.md) captures `CONTEXT.md`. Merely *reading* `DESIGN.md` for tokens is a one-line habit any skill can do; this skill is for when you're *setting* the language, not just consuming it.

## The three dials

Every project sits somewhere on each of three dials. Settle them first — most disagreements about "does this look good" are really disagreements about where a dial should sit. Record the chosen positions in `DESIGN.md`.

- **Variance** — safe/centred/grid-locked ↔ asymmetric/expressive/tension. A marketing site wants high variance; a data tool wants low.
- **Motion** — still ↔ rich hover/scroll choreography. High motion on a dashboard is noise; on a landing page it's life.
- **Density** — airy/generous whitespace ↔ dense/pro-tool/information-rich. Linear is dense; Stripe's marketing is airy. Neither is "better" — they serve different jobs.

## Principles by axis

Use these as the checklist a considered UI passes. Each line names the slop it kills.

**Typography.** One or two typefaces, on a modular scale, with a limited set of weights. Pick a type *with a point of view* — the system stack is a fine body face when it's *chosen*, never a default you fell into. Line-height tightens as size grows (loose ~1.5 for body, tight for display); measure stays 45–75ch; big headings get negative letter-spacing; tables get tabular numerals.

**Spacing & rhythm.** Every gap comes off one scale (a 4px/8px base), never an arbitrary pixel. Space communicates grouping — proximity does the work borders would. Keep a consistent vertical rhythm; generous whitespace beats dividers.

**Colour & tokens.** Bind *every* colour to a semantic token (`bg`, `fg`, `border`, `accent`) — never a raw hex at a call site. Neutrals are *tinted* toward the brand hue, and text is near-black, never `#000`. One accent, spent sparingly on the single primary action. Contrast clears WCAG AA.

**Layout & composition.** One primary action per view, unmistakably the loudest thing. Everything aligns to a grid. Reduce boxes: structure with space and the type scale before you reach for a card or a border. Introduce asymmetry only as high as the variance dial allows.

**Depth & elevation.** Pick *one* system — layered soft shadows, or flat with borders — and hold it. Shadows are tinted and soft with a consistent light source, stepped on a small elevation scale; never a blurry pure-black `0 4px 8px rgba(0,0,0,.5)`.

**Motion.** Motion must earn its place, use natural easing, and stay interruptible and accessible. The full discipline — the eight things a considered animation gets right — is in [MOTION.md](MOTION.md).

**Platform.** A design isn't platform-neutral — desktop web, mobile web, and native each earn their own touch targets, navigation idioms, and safe-area rules. The per-platform conventions are in [PLATFORMS.md](PLATFORMS.md); apply them on top of the principles above, and record which platforms the project targets in `DESIGN.md`.

## The anti-slop tells

The specific patterns that mark a UI as machine-default — overused fonts, the AI gradient, nested cards, dated easing, untinted neutrals — are catalogued as a fast pre-flight checklist in [ANTI-SLOP.md](ANTI-SLOP.md). Run it against any drawn UI before calling it done.

## Capturing DESIGN.md (the active discipline)

When you're *setting* the language, not just applying it:

1. **Ask for references first.** A folder of screenshots, a design system, component-library links, or an app to echo. Take structure, spacing rhythm, and accessibility patterns from them — but bind every colour and token to the project's own tokens; never paste hardcoded styles.
2. **Settle the three dials** with the user, one at a time, recommending a position for each based on what the project *is*.
3. **Write it down inline.** The moment a choice crystallises — a typeface, an accent, a motion duration, a dial position — record it in `DESIGN.md`. Don't batch. Use the format in [DESIGN-FORMAT.md](DESIGN-FORMAT.md).

`DESIGN.md` is the project's visual glossary: dials, tokens, type and motion language, and the anti-slop guardrails this project specifically watches for. It is *not* a spec or a component inventory — keep implementation detail out, exactly as `CONTEXT.md` stays a pure glossary.

## Relationships

- The **dials** set the ceiling for the **principles**: how much variance, motion, and density is *in taste* for this project.
- **Tokens** are where taste becomes enforceable — every principle above ultimately resolves to a token in `DESIGN.md`.
- **`mockup`** renders a whole flow *against* this vocabulary and `DESIGN.md`; **`open-design`** generates the hi-fi visual reference *from* it; **`prototype`**'s UI branch varies *within* it; a design review audits *against* it.
- **`grill-design`** is this discipline driven by a grilling — the interview that fills `DESIGN.md` in the first place.

## Rejected framings

- **"Make it look modern/clean."** Undefined, and the median of "modern" *is* the slop. Name the dial and the token instead.
- **Taste as a coat of paint at the end.** Taste is set before drawing (dials, tokens) and checked continuously (anti-slop), not sprinkled on afterward.
- **Copying a reference's styles.** References seed structure and rhythm; their colours and radii are *theirs*. Bind to this project's tokens or you've forked someone else's design system by accident.
