---
name: open-design
description: Generate the hi-fi visual design of a flow as a binding reference, before implementing the tasks, using Open Design (an AI design engine). The design is a standalone artifact the shipped frontend must match — not code in the project's stack. Use once the flow's coverage is settled (low-fi mockup) and you want the polished look fixed before building. Pairs with mockup (structure) and design-taste (DESIGN.md brand contract).
---

# Open Design

Produce the **hi-fi visual design** of a flow as a **binding reference** — the look the shipped frontend is required to match — *before* the implementation tasks are built. The design is generated with [Open Design](https://github.com/nexu-io/open-design) (an AI design engine that turns a brief + a design system into real HTML/CSS artifacts) and kept as a **standalone artifact**, not as code in the project's stack.

The defining constraint, and the trade-off to be honest about: **this is a reference, not promote-in-place code.** Unlike the [mockup](../mockup/SKILL.md) — which is real components in the project's stack that you grow into the shipped feature — an Open Design artifact is a separate `.html` you build *toward*, the way a team builds toward a Figma. You gain a fast, high-polish visual target; you accept that the real frontend is implemented separately and must be checked against it.

## Where it sits — it replaces the hi-fi mockup

In the overview phase of the main flow (see [ask-tutu](../ask-tutu/SKILL.md)), a project picks one of **two design paths** and records it in `DESIGN.md`:

- **`hi-fi-only`** — open-design is the **sole** design artifact. There is no [mockup](../mockup/SKILL.md); the frontend is built in-stack **toward this reference**, coverage is verified against *it*, and [e2e](../e2e/SKILL.md) is backfilled from the built code. The reference to follow is the HTML **plus** `DESIGN.md`/frontend-ADRs — the HTML is *look-only* and won't carry the stack's component decisions or the empty/loading/error states, so those come from the decisions and are checked before the build.
- **`mockup+hi-fi`** — a low-fi [mockup](../mockup/SKILL.md) owns **structure and coverage** (in the real stack, promoted in place, seeding e2e selectors) and open-design owns the **look**. Implementation promotes the mockup in place and styles it to match the reference.

Either way open-design is the **binding visual reference**: the polished look the shipped UI must match. The gates enforce it — [pre-flight](../pre-flight/SKILL.md) confirms the reference exists (and, via the pre-build design eval, that it covers and faithfully expresses every user story and frontend ADR) before greenlighting a polished build, and [manual-qa](../manual-qa/SKILL.md) checks the shipped frontend matches it after.

## Feed it the brand contract

Open Design is only as good as its brief. Before generating:

- **Pass `DESIGN.md` as the brand contract.** If [grill-design](../grill-design/SKILL.md) produced a `DESIGN.md`, it already fixes the dials, tokens, type, and motion — hand it to Open Design so the output speaks the project's language, not a generic template. No `DESIGN.md` yet? Settle the [design-taste](../design-taste/SKILL.md) dials with the user first; a vague brief yields generic design.
- **Give it the coverage.** The low-fi mockup and the blueprint already enumerate every screen and state. The design brief covers the same set — you're dressing screens that already exist, not inventing new ones.

## The loop

1. **Check coverage is settled.** There should be a screen inventory to dress — the low-fi mockup on `mockup+hi-fi`, or at least the blueprint's screens and the user stories on `hi-fi-only`. Designing hi-fi before coverage exists risks polishing screens that will change — settle the set of screens first.
2. **Assemble the brief** from `DESIGN.md` + the screen/state inventory, and generate the artifact with Open Design.
3. **Link it into the project.** Keep the generated artifact in the Open Design workspace and expose it in the project at a stable path — `<project>/design/open-design/` — so the reference lives next to the code that must match it. (The exact link convention is per-setup; see the project's own notes.)
4. **Review it with the user against `DESIGN.md`.** It's a reference others will build to, so divergence from the brand contract is a fix now, not after 20 screens are built to a wrong look.
5. **Hand off to the build.** From here the reference is fixed; implementation matches it. A change to the look goes back through here (regenerate/adjust) and re-review — never drifts silently during implementation.

## Anti-patterns

- **Designing before coverage.** Hi-fi over screens whose existence isn't settled — polish thrown away when the flow changes. Low-fi mockup first.
- **A brief with no brand contract.** Generating without `DESIGN.md` (or settled dials) yields median-SaaS output that ignores the project's language.
- **Treating it as promote-in-place.** It is a reference, not the shipped code; don't paste its raw HTML into production expecting it to be the frontend — the real FE is the promoted mockup, styled to match.
- **Silent drift.** Changing the look during implementation without updating the reference, so the binding target and the build disagree and the [manual-qa](../manual-qa/SKILL.md) match becomes meaningless.
- **Inventing screens.** The design dresses decided screens (user stories, ADRs, `DESIGN.md`); it doesn't add UI no decision called for.
