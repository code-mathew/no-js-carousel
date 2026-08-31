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

Needs Chrome / Edge 135+ (scroll-driven animations and the carousel pseudo-elements).

### 02 — Autoplay ([`autoplay-carousel.html`](autoplay-carousel.html))

Auto-advances every 5 seconds. Every moving part — slide crossfade, background zoom, staggered content cascade, the `01 / 04` counter strip, and the countdown pills — runs off a single shared 20s keyframe clock, so nothing can drift out of sync. Hover the play/pause button to pause (the icon morphs in CSS); move away to resume.

Works in all modern browsers.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Landing page linking the two demos |
| `shared.css` | Design tokens (Vice City palette, Anton/Oswald/Inter type scale), slide layout, buttons, responsive + reduced-motion rules |
| `scroll-carousel.html` / `.css` | Scroll-snap engine |
| `autoplay-carousel.html` / `.css` | Keyframe-clock engine |
| `Images/` | Landscape artwork, with portrait crops in `Images/mobile/` served via `<picture>` + `(orientation: portrait)` |

## Notes

- Responsive down to small phones and short landscape viewports; `prefers-reduced-motion: reduce` disables the animation in both demos.
- Artwork is Rockstar Games' official GTA VI promotional material, used here for a non-commercial CSS demo.
