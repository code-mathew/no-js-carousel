# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Web developers learning modern CSS. They arrive from a CSS tip/tutorial (blog post, video, or social) wanting to see how a production-looking hero carousel is built with zero JavaScript, then read the source to learn the techniques.

## Product Purpose

A teaching demo: one Vice City–styled hero carousel implemented with two pure-CSS engines, so learners can compare the approaches. Success means the demos look impressive enough to prove CSS can do this, and the source stays readable enough to learn from.

## Positioning

Not a component library — a side-by-side lesson. It demonstrates honestly why two demos exist: CSS cannot both auto-advance and stay user-scrollable, so the project ships one interactive engine (scroll-snap + scroll-driven animations + `::scroll-button` / `::scroll-marker`) and one autoplay engine (a single shared 20s keyframe clock). That "here's the constraint, here are both answers" framing is the differentiator.

## Operating Context

- Three pages: `index.html` (landing/chooser), `scroll-carousel.html`, `autoplay-carousel.html`.
- Static files, no build step; opened directly or via a simple local server (`.claude/launch.json` exists).
- Scroll-snap demo targets Chrome/Edge 135+ (carousel pseudo-elements); autoplay demo targets all modern browsers. Stated on the landing cards — keep those support claims truthful.

## Capabilities and Constraints

- **CSS-only forever (confirmed):** zero JavaScript is the defining rule. Future work must never add scripts, including for enhancement.
- Both demos share tokens and slide anatomy in `shared.css`; engine-specific CSS lives in `scroll-carousel.css` / `autoplay-carousel.css`.
- Autoplay timing is a shared clock: `--slide-duration: 5s` × 4 slides = one 20s keyframe cycle syncing crossfades, content cascade, counter, and countdown; hover pauses.
- `prefers-reduced-motion` support is established (shared kill-switch; each demo restores a safe static state) and must be preserved.
- Mobile art direction via `<picture>` with portrait sources.

## Brand Commitments

- **GTA VI / Vice City theme is binding (confirmed):** this is a fan demo; the official artwork and the pink/orange/violet Vice City palette stay the content of the demos. The artwork is Rockstar's IP used as demo content — do not present it as original or commercial work.
- Established voice: terse, uppercase, cinematic game-marketing register with plain-spoken technical notes (e.g. the landing page's honest constraint footnote).

## Evidence on Hand

- Official GTA VI key art in `Images/` (landscape .webp) with portrait variants in `Images/mobile/` for mobile art direction.
- No testimonials, metrics, or external content exist; none should be invented.

## Product Principles

1. **The code is the product.** Every technique used must be worth a learner reading; prefer the idiomatic modern-CSS way over a clever hack that obscures the lesson.
2. **Never break the no-JS rule** — even where JS would be easier; the constraint is the point.
3. **Look like real game marketing.** The demo teaches best when it looks production-grade, not like a tutorial fixture.
4. **State browser support honestly** wherever a cutting-edge feature gates an experience.
5. **Motion respects the visitor:** autoplay pauses on hover, reduced-motion always has a safe static state.
