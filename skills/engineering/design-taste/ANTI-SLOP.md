# Anti-slop checklist

The tells that mark a UI as machine-default. Run this against any drawn screen before calling it done — each is a fast, near-deterministic yes/no, the kind a detector could catch. A hit isn't automatically wrong, but it must be a *choice* you can defend against `DESIGN.md`, not a default you drifted into.

## Typography

- [ ] **Default statement font.** Inter, Arial, or the raw system stack used as the *brand/display* face because nothing else was chosen. (System stack as a deliberate body face is fine.)
- [ ] **Too many typefaces or weights.** More than two families, or a ladder of five+ weights doing the job of a scale.
- [ ] **No type scale.** Sizes picked ad hoc rather than stepped off a modular scale.
- [ ] **Runaway measure.** Body text wider than ~75ch — no line-length discipline.

## Colour

- [ ] **The AI gradient.** Purple→pink / blue→purple gradients, or any over-saturated hero gradient reached for as a default.
- [ ] **Pure black.** `#000` text or `#000` shadows. Use a near-black tinted toward the brand hue.
- [ ] **Untinted neutrals.** Grays straight off `gray-500` with no hue relationship to the palette.
- [ ] **Grey text on a coloured fill.** Muddy, low-contrast; and usually fails WCAG AA.
- [ ] **Accent everywhere.** The accent colour spent on many elements, so nothing reads as *the* primary action.
- [ ] **Hardcoded colour.** Any raw hex/rgb at a call site instead of a semantic token.

## Layout & structure

- [ ] **Card soup.** A card inside a card inside a card; every group boxed and bordered when whitespace would separate them.
- [ ] **Flat hierarchy.** Everything at one visual weight — no single loudest primary action.
- [ ] **Off-scale spacing.** Gaps that aren't on the 4/8px scale; or uniform spacing with no rhythm or grouping.
- [ ] **Radius roulette.** Inconsistent border-radii, or a huge radius slapped on everything.
- [ ] **Centre-everything.** Vertically-and-horizontally centred blocks with no tension, when the variance dial wanted structure.

## Depth

- [ ] **Blurry black shadow.** `0 4px 8px rgba(0,0,0,.5)` and friends — untinted, unlayered, one-size elevation.
- [ ] **Mixed depth systems.** Shadows *and* heavy borders *and* flat fills competing, with no single elevation language.

## Motion

- [ ] **Default bounce.** Elastic/overshoot easing as the reflex, or `ease`/`ease-in-out` on everything.
- [ ] **Decorative-only motion.** Animation that neither orients, gives feedback, nor shows a relationship.
- [ ] **No reduced-motion path.** `prefers-reduced-motion` unhandled.
- [ ] (Full motion discipline: [MOTION.md](MOTION.md).)

## Iconography & detail

- [ ] **Emoji as icons**, or icons mixed from two different sets.
- [ ] **Placeholder polish.** Lorem ipsum, default avatars, and stock-grey empty states left in a screen presented as "done".
