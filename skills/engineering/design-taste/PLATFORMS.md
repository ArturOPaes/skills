# Platform conventions

A design isn't platform-neutral. The same flow drawn for desktop web, mobile web, and native obeys different physical and idiomatic rules — ignore them and a "mobile" screen is just a narrow web page, and a "native" one an uncanny web app. These are the conventions each platform earns; apply them on top of the taste principles, not instead of them.

## Web (desktop)

- **Pointer + keyboard.** Hover states, focus rings, and full keyboard operability are load-bearing, not optional. Every action reachable and visible on `:focus-visible`.
- **Density.** More information per viewport is fine and often wanted — desktop users scan. Denser tables, multi-column layouts, persistent sidebars.
- **Pointer-sized targets.** ~28–32px is enough for a mouse; reserve the big targets for touch.
- **Width discipline.** Content has a max measure even on wide screens — full-bleed text is a tell. Use the extra width for structure (columns, panels), not longer lines.

## Mobile web

- **Touch first.** Minimum **44×44px** touch targets (Apple HIG) / 48dp (Material); space them so thumbs don't mis-tap.
- **Thumb reach.** Primary actions sit in the bottom third, within thumb arc; avoid burying the main CTA at the top.
- **One column, one focus.** Small viewport means a single column and one primary thing per screen; progressive disclosure over dense panels.
- **No hover.** Never gate meaning or affordance on hover — it doesn't exist. State must be visible or tap-driven.
- **Safe areas & chrome.** Respect the browser chrome and notch/home-indicator insets (`env(safe-area-inset-*)`); don't put controls where the OS bars sit.
- **Native input types.** Use the right keyboard (`type=email`, `inputmode=numeric`), large tap-friendly form controls.

## Native (iOS / Android)

- **Platform idioms.** Follow the OS: iOS (Apple HIG) and Android (Material) differ in navigation (tab bar vs bottom nav / nav drawer), back behaviour (swipe/back-gesture vs system back button), typography (SF / Roboto), and controls (switches, action sheets vs dialogs). Don't ship an iOS design on Android unchanged.
- **Real navigation.** Native stacks, tabs, and modals with their transitions — not a web router pretending. Screens push and pop; sheets slide.
- **Gestures & momentum.** Swipe, pull-to-refresh, momentum scrolling, edge-swipe back — motion feels physical (see [MOTION.md](MOTION.md)) and interruptible.
- **Safe areas.** Honour the notch, dynamic island, status bar, and home indicator; content and controls stay inside the safe area.
- **System affordances.** Haptics on commit, native pickers, permission prompts at the moment of need — lean on the platform rather than reinventing it.

## Combination

- **Web + mobile web** → **one responsive design** that reflows across breakpoints; it should feel deliberately composed at each size, not a desktop layout squeezed thin. Judge it at both sizes.
- **Anything with native** → **design per platform.** Share the brand, tokens, and motion language (one design system), but let the layout, navigation, and gestures follow each platform's idiom. A shared token set with platform-specific composition — not one layout forced onto three targets.
