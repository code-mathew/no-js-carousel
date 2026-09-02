# No-JS Carousel

A GTA VI–themed hero carousel built with **zero JavaScript** — two separate pure-CSS engines, because CSS can auto-advance a slider *or* keep it user-scrollable, but not both at once.

**[Live demo →](https://code-mathew.github.io/no-js-carousel/)**

No build step, no dependencies — just static HTML and CSS. To run it locally, open [`index.html`](index.html) and pick a demo.

## The two demos

### 01 — Scroll-Snap ([`scroll-carousel.html`](scroll-carousel.html))

Interactive: swipe, scroll, or use the arrows. Built on:

- `scroll-snap-type: x mandatory` with `scroll-snap-stop: always`
- Scroll-driven animations — a `scroll-timeline` on the track and a `view-timeline` per slide drive the content reveal, background zoom, slide counter, and progress bar
- The native carousel pseudo-elements `::scroll-button()` and `::scroll-marker` / `::scroll-marker-group` for arrows and dots — no markup for either

Best in Chrome / Edge 135+, the only engines that ship the carousel pseudo-elements today. Everything is progressively enhanced — see [Browser support](#browser-support).

### 02 — Autoplay ([`autoplay-carousel.html`](autoplay-carousel.html))

Auto-advances every 5 seconds. Every moving part — slide crossfade, background zoom, staggered content cascade, the `01 / 04` counter strip, and the countdown pills — runs off a single shared 20s keyframe clock, so nothing can drift out of sync. A visually hidden checkbox holds the pause state via `:has(:checked)`, so click, tap and keyboard all work; on mouse pointers, hovering the button also previews the pause.

Works in all modern browsers — plain `@keyframes` plus `:has()`.

## Browser support

Verified against [MDN browser-compat-data](https://github.com/mdn/browser-compat-data), September 2026.

| Feature | Chrome / Edge | Safari | Firefox |
| --- | --- | --- | --- |
| `scroll-snap-type` / `scroll-snap-stop` | ✅ | ✅ | ✅ |
| `:has()` | ✅ 105 | ✅ 15.4 | ✅ 121 |
| Scroll-driven animations (`animation-timeline`, `scroll()`, `view()`) | ✅ 115 | ✅ 26 | 🚩 behind `layout.css.scroll-driven-animations.enabled` |
| Anchor positioning (`anchor-name`, `position-anchor`, `anchor()`) | ✅ 125+ | ✅ 26+ | ✅ 147+ |
| `::scroll-button()` / `::scroll-marker` / `scroll-marker-group` | ✅ 135 | ❌ | ❌ |

**What that means per demo:**

- **Autoplay** works everywhere. Nothing in it is experimental.
- **Scroll-Snap** is fully featured only in Chrome / Edge 135+. Elsewhere it degrades rather than breaks:
  - Every scroll-driven rule sits behind `@supports (animation-timeline: --slide)`. Without it the reveal would run as a 0s animation frozen on its `100%` frame — opacity 0, an art-only page with no text. The fallback instead ships a static, fully readable snap carousel, hides the scroll-linked counter rather than let it lie at `01`, and shows a slim accent scrollbar so the horizontal scroll stays discoverable.
  - The arrows and dot markers are pure pseudo-elements, so browsers without them simply render no controls — swipe, trackpad scroll, and keyboard still navigate.

Firefox is the one to watch: scroll-driven animations are a named Interop 2026 priority and already default-on in Nightly, so Demo 01's reveal and counter should light up there without a code change once it ships in stable.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Landing page linking the two demos |
| `shared.css` | Design tokens (Vice City palette, Anton/Oswald/Inter type scale), slide layout, buttons, responsive + reduced-motion rules |
| `scroll-carousel.html` / `.css` | Scroll-snap engine |
| `autoplay-carousel.html` / `.css` | Keyframe-clock engine |
| `Images/` | Landscape artwork, with portrait crops in `Images/mobile/` served via `<picture>` + `(orientation: portrait)` |

## Notes

- Responsive down to small phones and short landscape viewports; `prefers-reduced-motion: reduce` disables the animation in both demos and each one restores a sensible static first frame.
- Hover rules are gated behind `@media (hover: hover) and (pointer: fine)`. Touch browsers keep a sticky `:hover` on a tapped element, which would otherwise leave the autoplay demo frozen after the pause checkbox is unchecked.
- Artwork is Rockstar Games' official GTA VI promotional material, used here for a non-commercial CSS demo.
