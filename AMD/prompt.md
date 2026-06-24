# AMD Design System — Generation Prompt

This document is the canonical generation prompt for the AMD Design System. Use it to regenerate or extend any file in this system.

---

## Task

Build a complete, production-quality design system called the "AMD Design System" inside `/Users/sscargall/Documents/ClaudeDesignSystems/AMD/`.

This is part of a series of brand-faithful design systems. Read `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/tokens.css` and `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/components.css` first to calibrate the expected depth and completeness.

---

## AMD Brand Aesthetic

- **Personality:** Aggressive challenger brand, gaming heritage, high-performance computing. AMD's design is bold and energetic — red as the war color, dark backgrounds, cinematic product reveals. The brand spans gaming (Ryzen, Radeon) and enterprise (EPYC, Instinct). AMD's redesign under Lisa Su is confident and direct: "Together We Advance."
- **Typography:** AMD uses "AMD Font" custom. Fallback: `"Barlow", "DM Sans", "Inter", system-ui, sans-serif`. Barlow is the closest open-source match — condensed and wide weights both used. Bold, wide, confident.
- **Colors:**
  - AMD Red: `#ED1C24`
  - Red dark: `#C41017`
  - Red light: `#FF3B42`
  - Red glow: `rgba(237,28,36,0.35)`
  - Background: `#0D0D0D` (near-black, dark-first)
  - Surface 1: `#1A1A1A`
  - Surface 2: `#252525`
  - Surface 3: `#303030`
  - Label primary: `#FFFFFF`
  - Label secondary: `#A8A8A8`
  - Label tertiary: `#606060`
  - Border subtle: `#2A2A2A`
  - Border default: `#3D3D3D`
  - AMD Graphite: `#7A7A7A`
  - White: `#FFFFFF`
  - Light bg: `#F5F5F5`
  - Ryzen Orange (sub-brand): `#FF6A00`
  - EPYC teal (sub-brand): `#00B4D8`
  - Instinct purple (sub-brand): `#7B2FBE`
  - Radeon orange-red (sub-brand): `#FF4500`
- **Dark-first:** Yes — AMD's primary web presence is dark.
- **Motion:** Bold, kinetic — 150ms/300ms/500ms. Easing: `cubic-bezier(0.4, 0, 0.2, 1)`. Red glows on hover. Dramatic product reveals.
- **Reference:** amd.com

---

## File Structure

```
AMD/
├── index.html           — Full design system showcase
├── tokens.css           — All design tokens (:root dark, light override)
├── typography.css       — Full type system with Barlow import
├── components.css       — All components
├── animations.css       — Keyframes, utilities, reduced-motion
├── prompt.md            — This file
└── components/
    ├── buttons.html     — All button variants, sizes, states
    ├── cards.html       — Product, spec, feature, family tile cards
    ├── forms.html       — All form controls
    ├── navigation.html  — Nav bar, mega menu, breadcrumb, logo
    └── modals.html      — Modals, toasts, overlays (with live JS)
```

---

## Design Tokens (tokens.css)

- `:root` is dark (AMD dark-first)
- `@media (prefers-color-scheme: light)` overrides backgrounds, labels, shadows
- Full color system: AMD Red, surfaces, labels, borders, sub-brand tokens
- Sub-brand tokens: `--color-ryzen`, `--color-epyc`, `--color-instinct`, `--color-radeon`
- Glow tokens: `--glow-red`, `--glow-red-xl`, `--glow-ryzen`, `--glow-epyc`, `--glow-instinct`, `--glow-radeon`
- Typography: Barlow/DM Sans stack + mono stack, scale 80/64/48/36/28/22/18/16/14/13/12px
- Spacing: 4px grid — 4/8/12/16/20/24/32/40/48/64/80/96/128px
- Radius: 0px (AMD is sharp), 2px, 4px, 8px, 9999px (pills only)
- Shadows + Glows: red glow variants, dark shadows
- Motion: 100/150/300/500/700/1000ms, AMD easing `cubic-bezier(0.4,0,0.2,1)`
- Z-index scale
- Gradient definitions including sub-brand gradients
- CSS reset + base styles

---

## Typography (typography.css)

- Google Fonts import: Barlow 400–900, Barlow Condensed, DM Sans, JetBrains Mono
- `.display-hero`: 80px, 800, uppercase, -0.02em
- `.display-large`: 64px, 800, uppercase, -0.02em
- `.display`: 48px, 700, -0.01em
- `.heading-1`: 36px, 700
- `.heading-2`: 28px, 600
- `.heading-3`: 22px, 600
- `.subhead`: 18px, 500, label-secondary
- `.body-lg`: 18px, 400, 1.65
- `.body`: 16px, 400, 1.60
- `.body-sm`: 14px
- `.caption`: 13px
- `.label`: 12px, 700, uppercase, 0.10em
- `.mono`: JetBrains Mono 13px
- `.spec-value`: 48px, mono, AMD red
- `.product-tagline`: bold italic, 18px, uppercase
- `.eyebrow`: 12px, 700, uppercase, AMD red
- Gradient text: `.text-red-gradient`, `.text-amd-gradient`, `.text-silver-gradient`
- Sub-brand labels: `.label-ryzen`, `.label-epyc`, `.label-instinct`, `.label-radeon`
- Responsive: 1024px and 768px breakpoints
- Utility classes: color, alignment, weight, tracking, leading

---

## Animations (animations.css)

- `@keyframes fadeIn`, `fadeOut`
- `@keyframes slideInUp`, `slideInDown`, `slideInLeft`, `slideInRight`
- `@keyframes revealLeft`: clip-path reveal (dramatic product reveal)
- `@keyframes revealUp`
- `@keyframes redGlow`: AMD signature box-shadow pulse
- `@keyframes redPulse`: color pulse
- `@keyframes borderFlare`: red border glow sweep
- `@keyframes scanline`: horizontal scan line (hero sections)
- `@keyframes shimmer`: skeleton loading
- `@keyframes countUp`: benchmark number reveal
- `@keyframes spin`, `scaleIn`, `diagonalWipe`, `barFill`, `flicker`, `pulseScale`, `gradientShift`
- Utility classes: `.animate-fade-in`, `.animate-slide-up`, `.animate-reveal-left`, `.animate-red-glow`, `.animate-scanline`, `.animate-shimmer`, `.skeleton`, etc.
- Delay utilities: `.delay-100` through `.delay-1200`
- Scroll-triggered: `.on-scroll`, `.on-scroll-left` with `.visible` state
- Hover effects: `.hover-red-glow`, `.hover-lift`, `.hover-red-border`
- `@media (prefers-reduced-motion: reduce)` — disables all animations

---

## Components (components.css)

### Layout
- `.container` (1280px max), `.container-wide` (1440px), `.container-content` (1024px)
- Grid utilities: `.grid-2`, `.grid-3`, `.grid-4` with responsive breakpoints
- Section spacing: `.section`, `.section-lg`, `.section-sm`

### Buttons
- Base: `.btn` — sharp corners (0px radius), 44px height, uppercase 12px 700, 0.10em tracking
- Variants: `.btn-primary` (AMD Red), `.btn-secondary` (outlined red), `.btn-outline`, `.btn-ghost`, `.btn-cta` (large hero), `.btn-white`
- Sub-brand: `.btn-ryzen`, `.btn-epyc`, `.btn-instinct`, `.btn-radeon`
- Sizes: `.btn-sm` (32px), `.btn-md` (44px), `.btn-lg` (52px), `.btn-xl` (64px)
- States: focus (red glow), active (scale 0.98), disabled (opacity 0.40), loading

### Navigation
- `.nav-amd`: fixed, 64px, near-black, logo + links + actions
- `.nav-dropdown-amd`: mega menu, 4-column product family layout
- `.nav-product-column-header`: sub-brand colored (`.ryzen`, `.epyc`, `.instinct`, `.radeon`)
- `.breadcrumb`, `.breadcrumb-item`

### Product Cards
- `.card-product-amd` + modifier classes: `.ryzen`, `.epyc`, `.instinct`, `.radeon`
- Structure: header stripe → image area with corner triangle → body (arch, name, spec, score, CTA)
- Hover: sub-brand glow border, translateY(-4px)

### Sub-brand Tiles
- `.product-family-tile` + `.product-family-ryzen/epyc/instinct/radeon`
- CSS custom property inheritance: `--family-color`, `--family-glow`, `--family-gradient`

### Feature Cards
- `.card-feature-amd`: min-height 360px, red gradient overlay, full content stack

### Spec Cards
- `.card-spec-amd`: centered, large `.card-spec-value` in AMD red, `.card-spec-bar`

### Performance Bars
- `.perf-bar-amd`, `.perf-bar-track`, `.perf-bar-fill` (red = AMD, gray = competitor)
- `.perf-winner`: "AMD WINS" inline badge
- `.benchmark-chart-amd`: vertical CSS bar chart

### Spec Table
- `.spec-table-amd`: red header row, `.spec-category-row`, `.spec-row` alternating

### Forms
- `.input`, `.textarea`, `.select`: sharp corners, dark surface-2, red focus state
- `.checkbox`, `.radio`, `.toggle`: all with AMD red checked/on state
- `.form-label` (uppercase bold), `.form-hint`, `.form-error`, `.form-success`

### Modals
- `.modal-overlay`: rgba(0,0,0,0.90), flex centered
- `.modal-amd`: sharp corners, surface-2, 3px red left border, scale animation
- `.modal-header`, `.modal-body`, `.modal-footer`, `.modal-close`

### Badges
- `.badge-red`, `.badge-ryzen`, `.badge-epyc`, `.badge-instinct`, `.badge-radeon`
- `.badge-new`, `.badge-sale`, `.badge-winner` (gold border), `.badge-award`
- `.badge-outline`, `.badge-outline-red`, `.badge-lg`

### Campaign Block
- `.campaign-block`: full-width, dark, diagonal red CSS accent via pseudo-elements
- `.campaign-headline` with `<em>` for red accent word

### Footer
- `.footer-amd`: 5-column grid, brand col + 4 link columns
- `.footer-bottom`: copyright + legal links

### Brand Logo
- `.brand-logo` + size variants: `.brand-logo-sm/md/lg/xl`

---

## Logo SVG (CSS Approximation)

```html
<a href="#" class="nav-brand" aria-label="AMD Home">
  <svg width="80" height="24" viewBox="0 0 80 24" fill="none" aria-hidden="true">
    <!-- AMD arrow/chevron mark approximation -->
    <polygon points="0,0 14,0 20,12 14,24 0,24 6,12" fill="#ED1C24"/>
    <!-- AMD wordmark -->
    <text x="26" y="17" font-family="Barlow, DM Sans, Inter, sans-serif" font-size="16" font-weight="800" fill="white" letter-spacing="1">AMD</text>
  </svg>
</a>
```

Replace with licensed AMD SVG asset in production.

---

## Requirements

- Zero external dependencies (Google Fonts via @import is acceptable)
- Dark-first (`:root` is dark), light via `@media (prefers-color-scheme: light)`
- Responsive: mobile-first, breakpoints at 768px and 1024px
- Semantic HTML5, `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs
- Write all files to disk
