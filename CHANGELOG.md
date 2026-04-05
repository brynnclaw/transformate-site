# Transformate Site — Changelog

## 2026-04-03 — Session 3: Logo + Production Readiness

### Added
- **Logo.astro component** — Inline SVG amber squircle (rx 14, 1.5px stroke) with weighted T (crossbar 5.5px, stem 4px, both stroke-linecap round) + "TRANSFORMATE" in Instrument Serif at letter-spacing 0.08em
- **OG & Twitter meta tags** in Layout.astro — og:title, og:description, og:image, twitter:card (summary_large_image), canonical URL
- **Skip-to-content link** — hidden until Tab focus, amber-bordered, z-9999
- **Focus-visible styles** — 2px amber outline on all interactive elements
- **`prefers-reduced-motion` support** — disables particles canvas, marquee, shimmer, collapses all animations to instant
- **404.astro** — Branded error page with Logo, copy, and HudButton back to home
- **robots.txt** — Allow all, points to sitemap
- **@astrojs/sitemap** integration — auto-generates sitemap-index.xml on build

### Changed
- **Header.astro** — text wordmark replaced with `<Logo />` component
- **Footer.astro** — text wordmark replaced with `<Logo />` component
- **favicon.svg** — updated to match logo mark (squircle + weighted T on void bg)
- **Layout.astro** — accepts `description` and `ogImage` props, canonical URL

---

## 2026-04-03 — Session 2: HUD Button System

### Added
- **HudButton.astro component** — Reusable SVG-based button with chamfered corners (style2), adapted from Arkon's GlowingEffect/HudButton React component to vanilla JS for Astro
  - Props: `text`, `href`, `variant` (primary/secondary), `compact`, `class`, `id`
  - SVG uses `preserveAspectRatio="none"` + `vector-effect="non-scaling-stroke"` for responsive width with consistent 1px border
  - Separate fill path (gradient) + stroke path (for GSAP draw-in animation)
  - Primary variant: amber gradient fill (#E5A100 → #D4920A → transparent), #D4920A stroke, shimmer sweep
  - Secondary variant: subtle fill (8% opacity), dimmer stroke (35% opacity), no shimmer
  - Compact mode for header (44px height vs 52px default)
- **HUD button CSS** in global.css:
  - Hover: `scale(1.03) translateY(-2px)` + amber `drop-shadow` glow
  - Active press: `scale(0.97)` with fast transition
  - Corner dots (4, top-right 2×2 grid) via `::before` + `box-shadow`
  - Side dots (2, left vertical) via `::after` + `box-shadow`
  - `@keyframes hud-shimmer` — CSS shimmer sweep using `translateX` (GPU-accelerated)
- **GSAP animations** in Layout.astro:
  - Header button: stroke path draws in on page load (0.5s delay)
  - CTA section button: stroke path draws in on scroll via ScrollTrigger
  - All HUD buttons: text scramble on hover (uppercase chars only, cancellable via `cancelAnimationFrame`)

### Changed
- **Hero.astro** — Replaced pill-style CTAs with `<HudButton>` (primary + secondary)
- **CTA.astro** — Replaced pill-style CTA with `<HudButton>` (preserved `id="calendly-trigger"`)
- **Header.astro** — Replaced desktop pill CTA and mobile menu pill CTA with `<HudButton>` (desktop uses secondary compact variant wrapped in `hidden lg:contents` for responsive visibility)
- **Layout.astro** — Replaced old `.btn-primary` spring entrance animation with HUD button draw-in system

### Removed
- `.btn-text-wrap` CSS (was used for header button text-swap animation, no longer needed)
- Old CTA button spring entrance GSAP animation (replaced by HUD button draw-in)

---

## 2026-04-03 — Session 1: Cinematic Components + Service Card Overhaul

### Added
- **5 cinematic motion components:**
  1. Rotating Glow Border Cards (Services) — cursor-following amber conic gradient border with lift + box-shadow hover
  2. Odometer Counter (Proof) — rolling digit strips for stats (14 days, 100%)
  3. Text Scramble (Hero) — "works." decodes from random characters on load
  4. Kinetic Marquee — two rows of tech/capability pills between Services and Proof, scroll-velocity-responsive
  5. SVG Draw (HowItWorks) — amber gradient line draws between step circles on scroll
- Service card `.service-glow` div with rotating conic-gradient border (mask-composite technique)
- Service card hover: `translateY(-4px)` + amber glow `box-shadow`
- GSAP stagger entrance for service cards
- GSAP cursor-following angle animation for glow border (`expo.out` easing)

### Changed
- Services section: replaced spotlight border card grid (`gap-[1px] bg-border`) with individual cards (`gap-6`, rounded-[16px])
- Service card CTA "Book a call" link: added `self-center` for centering

### Removed
- Spotlight card system (CSS `.service-spotlight`, JS mousemove handler, overlay divs)

---

## Initial Build — Site Foundation

### Stack
- Astro 6.1.3, Tailwind CSS 4.2, GSAP 3.14 + ScrollTrigger, Lenis 1.3
- Fonts: Instrument Serif (headings), Inter (body), JetBrains Mono (accents)
- "Amber Forge" design system: Forge Amber (#D4920A), Bright Amber (#E5A100), Deep Amber (#A67208), Void (#0A0A10)

### Components
- Layout.astro (central GSAP animation hub)
- Header.astro (fixed, scroll-aware, mobile menu, active section detection)
- Hero.astro (split-text word reveal, scroll hint)
- Problem.astro, Promise.astro
- HowItWorks.astro (3-step cards with connector)
- Services.astro (3-tier pricing cards: Signal, Sprint, Overhaul)
- Marquee.astro (tech capabilities ticker)
- Proof.astro (stats with odometer counters)
- Founder.astro
- FAQ.astro (accordion)
- CTA.astro (Calendly-ready)
- Footer.astro
- ParticleField.astro (background canvas)
