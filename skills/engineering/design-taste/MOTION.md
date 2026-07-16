# Motion

Agents have the worst taste in motion: they reach for bounce, animate the wrong properties, and animate things that should stay still. A considered animation gets eight things right. Judge every animation — and every *decision to animate* — against them.

## The eight axes

1. **Purpose.** Motion earns its place or it's cut. Valid jobs: orient (where did this come from / go), give feedback (the tap registered), or show a relationship (this expanded from that). Decoration is not a job. The first question is always *should this animate at all* — half of good motion is the things left still.

2. **Easing.** Natural curves, never linear and never default bounce. Enters and moves use **ease-out** (fast start, gentle settle); exits can be quicker. Reach for a **spring** when something should feel physical. Overshoot/elastic is a rare, deliberate accent — never the reflex.

3. **Physicality.** Things move like they have mass and momentum: they don't teleport, they don't stop dead. Related elements move together; a menu grows *from* the button that opened it, not into existence at screen centre.

4. **Interruptibility.** A user acting mid-animation is never blocked or made to wait for it to finish. Animations are cancellable and reversible — close while opening should reverse smoothly, not queue.

5. **Performance.** Animate **transform** and **opacity** only; never `width`, `height`, `top`, `left`, or other layout-triggering properties. Hold 60fps. Layout-animating jank reads as cheap even when the design is good.

6. **Accessibility.** Honour `prefers-reduced-motion`: replace movement with an instant or simple opacity change. Never gate meaning on motion alone.

7. **Cohesion.** One motion language across the app — a shared, small set of duration and easing tokens, reused. Ten bespoke timings read as ten different apps.

8. **Duration.** Most UI transitions live in **150–300ms**. Under ~100ms reads as a jump; over ~400ms feels sluggish and makes the app wait on itself. Larger surfaces (a full-screen sheet) can run a touch longer than a small toggle.

## Finding the opportunities

Motion is as much about *where* as *how*. Good candidates: state changes (open/close, expand/collapse), items entering or leaving a list, focus and selection, and confirming a destructive or committing action. Leave still: dense data tables, anything the user reads, and anything that would animate on every keystroke or scroll tick.

## The Apple lens

When the target is fluid, deferential motion (à la `apple-design`): content leads, chrome defers; depth comes from layering, not drop shadows; interactions feel like *direct manipulation* — the thing tracks your finger/cursor 1:1 and settles with a spring when released. Motion should feel continuous, not like a sequence of discrete keyframes.
