# NVIDIA Design System — Generation Prompt

This document is the canonical prompt for reproducing the NVIDIA Design System from scratch. Use it with Claude Code or any capable LLM that supports file writing tools.

---

## Task

Build a complete, production-quality design system called the "NVIDIA Design System" inside `/path/to/NVIDIA/`.

This is part of a series of brand-faithful design systems. Read an existing design system (e.g., `Apple/tokens.css` and `Apple/components.css`) first to calibrate the expected depth and completeness before writing anything.

---

## NVIDIA Brand Aesthetic

- **Personality:** AI supremacy, raw GPU power, gaming culture meets enterprise AI. NVIDIA's design is dark, dramatic, and authoritative — green energy pulses through everything. Cinematic without being frivolous. The brand has shifted from gaming to "the AI company" — both worlds coexist.
- **Typography:** NVIDIA uses a custom display font. Fallback stack: `"NVIDIA Sans", "DM Sans", "Inter", system-ui, sans-serif`. Mono: `"DM Mono", "JetBrains Mono", "Fira Code", monospace`. Bold headlines, tight tracking.
- **Colors:**
  - NVIDIA Green: `#76B900`
  - Green light: `#8ED400`
  - Green dark: `#5A8C00`
  - Green glow: `rgba(118,185,0,0.4)` — for glow effects
  - Background: `#1A1A1A` (dark, not pure black — warmer)
  - Surface 1: `#222222`
  - Surface 2: `#2D2D2D`
  - Surface 3: `#383838`
  - Pure black: `#000000` — hero sections
  - Label primary: `#FFFFFF`
  - Label secondary: `#A0A0A0`
  - Label tertiary: `#606060`
  - Border subtle: `#333333`
  - Border default: `#444444`
  - Accent blue (secondary): `#00A3E0` — used for links and info
  - Error: `#FF4444`
  - Warning: `#FFB300`
  - Success: `#76B900` (same as brand green)
- **Dark-first:** Yes — black/dark canvas.
- **Motion:** Cinematic — 200ms/350ms/600ms. Easing: `cubic-bezier(0.25, 0.46, 0.45, 0.94)`. Green glows pulse. Particle effects (CSS only). GPU cards reveal on hover.
- **Reference:** nvidia.com

---

## File Structure

```
NVIDIA/
├── index.html
├── tokens.css
├── typography.css
├── components.css
├── animations.css
├── prompt.md
└── components/
    ├── buttons.html
    ├── cards.html
    ├── forms.html
    ├── navigation.html
    └── modals.html
```

---

## Design Tokens (tokens.css)

`:root` is dark. `@media (prefers-color-scheme: light)` override.

All tokens:
- Full color system above + semantic mappings (background, surface, label, border, accent, glow)
- Typography: NVIDIA Sans/DM Sans stack + mono stack, scale 80/64/48/36/28/22/18/16/14/13/12px
- Spacing: 4px grid — 4/8/12/16/20/24/32/40/48/64/80/96/128px
- Radius: 2px (sharp/chips), 4px (buttons), 8px (cards), 12px (modals), 9999px (pills)
- Shadows + Glows: `0 0 20px rgba(118,185,0,0.3)`, `0 0 40px rgba(118,185,0,0.2)`, `0 4px 24px rgba(0,0,0,0.6)`
- Motion: durations 150/200/350/600ms, NVIDIA easing
- Z-index scale
- GPU aesthetic tokens: scanline colors, particle colors, gradient presets

---

## Typography (typography.css)

- `.display-hero`: 80px, weight 800, tracking -0.03em, uppercase — "THE AI COMPANY"
- `.display-large`: 64px, weight 800, tracking -0.02em
- `.display`: 48px, weight 700, tracking -0.01em
- `.heading-1`: 36px, weight 700
- `.heading-2`: 28px, weight 600
- `.heading-3`: 22px, weight 600
- `.subhead`: 18px, weight 500, tracking 0.02em
- `.body-lg`: 18px, weight 400, line-height 1.65
- `.body`: 16px, weight 400, line-height 1.6
- `.body-sm`: 14px
- `.caption`: 13px, label-secondary
- `.label`: 12px, weight 700, uppercase, tracking 0.1em — product labels, nav items
- `.mono`: monospace, 13px — specs, benchmarks
- `.spec-value`: large mono, green — for benchmark numbers
- Gradient text: `.text-green-gradient` (green to white), `.text-ai-gradient` (green to cyan)
- All use `clamp()` for fluid responsive scaling

---

## Animations (animations.css)

- `@keyframes fadeIn`
- `@keyframes slideInUp`
- `@keyframes greenGlow`: box-shadow pulse with NVIDIA green glow (2.5s infinite)
- `@keyframes greenPulse`: opacity pulse for green elements (2s infinite)
- `@keyframes scanline`: horizontal scan line moving down — GPU aesthetic (6s linear infinite)
- `@keyframes shimmer`: skeleton loading (1.8s linear infinite)
- `@keyframes countUp`: benchmark number reveal (600ms ease-out)
- `@keyframes particleFloat`: small dots floating up — AI/data aesthetic (8 particles via nth-child, 7–12s durations)
- `@keyframes borderGlow`: animated border that glows green (2s infinite)
- `@keyframes springIn`: modal entry with scale spring
- `.particle-field` container + `.particle` elements for CSS-only particles
- `.scanline-overlay` + `.scanline-beam` for GPU terminal aesthetic
- Utility classes for all keyframes, delay classes (0–1000ms), stagger helpers
- `prefers-reduced-motion` support — collapses all durations to 0.01ms, hides decorative particles/scanlines

---

## Components (components.css)

### Layout
- `.container`: max-width 1200px
- `.container-wide`: max-width 1440px

### Buttons
- `.btn-primary`: NVIDIA green `#76B900` fill, black text, 4px radius, 44px height, weight 700, uppercase, tracking 0.1em — hover: green-light, green glow shadow
- `.btn-secondary`: transparent, green border + green text — hover: green fill + black text
- `.btn-outline`: dark surface fill, white border, white text — hover: surface-2
- `.btn-ghost`: transparent, label-secondary — hover: surface-1
- `.btn-cta`: 52px height, full-width green fill — for product CTAs
- `.btn-blue`: accent blue fill for data center / info actions
- `.btn-danger`: error red fill
- Size variants: sm (32px) / md (44px) / lg (52px)
- All: `transition: all 150ms`, active `scale(0.98)`, loading state with spinner

### GPU Product Card — NVIDIA's signature component
- `.card-gpu`: dark surface, 8px radius, overflow hidden
  - `.card-gpu-image`: image area (dark gray placeholder with green corner triangle), aspect-ratio 4/3
  - `.card-gpu-badge`: top-left chip — "RTX 4090", "H100", "GeForce" — green bg + black text
  - `.card-gpu-body`: padding 20px
  - `.card-gpu-name`: heading-2 style, white
  - `.card-gpu-spec`: spec line in mono style — "24GB GDDR6X | 16384 CUDA Cores"
  - `.card-gpu-price`: large, green color, mono
  - `.card-gpu-cta`: full-width green button
- Hover: card lifts 4px, green glow appears around border

### AI/Data Center Card
- `.card-datacenter`: wider card, dark surface, green left-border accent (4px), padding 24px
  - Product name, description, "Learn more →" in green

### Feature Card
- `.card-feature`: gradient bg (black to dark green), large text, full-width or half-width
  - Green top-border accent reveals on hover

### Spec/Benchmark Card
- `.card-spec`: dark surface, centered
  - Large spec value in `.spec-value` style (green, mono, huge, text-shadow glow)
  - Spec label below
  - Optional comparison bar (4px height)

### Event/GTC Card
- `.card-event`: dark surface, gradient border glow effect on hover, green pulse dot on date

### Navigation
- `.nav-global`: pure black, NVIDIA wordmark left, links center (uppercase label style), CTA right
- `.nav-links` items: label-secondary, hover: white, 12px uppercase
- `.nav-dropdown`: mega-menu style, dark surface, green 2px top-border, organized in 3-column grid
- `.nav-breadcrumb`: label style, slash-separated, green current page

### Performance / Benchmark Bar
- `.perf-bar`: comparison bar — label left, green fill bar, value right
- `.perf-bar-fill`: animated green fill (width transition), glow trail on leading edge
- `.perf-bar-fill--competitor`: gray fill for competitor bars
- `.perf-comparison`: stacked bars comparing products

### Product Spec Table
- `.spec-table`: dark, clean — product name + spec rows
- `.spec-row`: 44px height, label left + value right, border-bottom
- `.spec-row--highlight`: green left border for key specs, green value text

### Forms
- `.input`: dark surface-2 bg, border, 4px radius, 44px height, green focus ring — `0 0 0 2px rgba(118,185,0,0.4)`
- `.input-search`: full-width, with search icon
- `.select`: dark custom dropdown
- `.checkbox`: 16px, 2px radius — checked: green fill + black checkmark
- `.radio`: 16px circle — selected: green inner dot
- `.toggle`: 44×24px pill, green track + glow when on

### Modals
- `.modal-overlay`: rgba(0,0,0,0.85), backdrop-filter blur(6px)
- `.modal`: dark surface-2, 12px radius, green top-border accent (2px), shadow-overlay + green-glow-sm
- `.notification-bar`: full-width banner, green bg — "New: NVIDIA H200 now available"

### Badges / Tags
- `.badge-green`: green bg, black text — primary product badge
- `.badge-new`: bright green, "NEW" — animated greenGlow
- `.badge-ai`: dark surface, green border, "AI" label
- `.badge-rtx`: dark surface, white text, "RTX" — product family
- `.badge`: standard gray pill
- All 2px radius (sharp), uppercase, bold, tight tracking

### Toast / Notifications
- `.toast`: dark surface-2, 2px top-border colored by state (green/red/warning/blue)
- Four states: success, error, warning, info
- `toastIn` animation: slide down from -16px

### Footer
- `.footer`: pure black, multi-column link grid (2fr + 4× 1fr)
- Green brand mark, tertiary color links

---

## Logo Mark

```html
<!-- NVIDIA logo approximation — Replace with licensed NVIDIA logo -->
<a href="#" class="nav-brand" aria-label="NVIDIA Home">
  <svg width="108" height="22" viewBox="0 0 108 22" aria-hidden="true">
    <!-- Eye/eye-box logomark approximation -->
    <rect x="0" y="1" width="20" height="20" rx="2" fill="#76B900"/>
    <path d="M10 5 C6.5 5 3.5 7.5 3.5 11 C3.5 14.5 6.5 17 10 17 C13.5 17 16.5 14.5 16.5 11 C16.5 7.5 13.5 5 10 5Z" fill="black"/>
    <circle cx="10" cy="11" r="3.2" fill="#76B900"/>
    <!-- NVIDIA wordmark -->
    <text x="27" y="16" font-family="DM Sans, Inter, sans-serif" font-size="15" font-weight="800" fill="white" letter-spacing="1">NVIDIA</text>
    <text x="97" y="10" font-family="DM Sans, Inter, sans-serif" font-size="8" font-weight="400" fill="white" opacity="0.6">®</text>
  </svg>
</a>
```

`.brand-logo` component with sm/md/lg/xl size variants, icon-only, wordmark-only, and placeholder modes.

---

## Main index.html Sections

1. **Notification bar**: green, "NVIDIA Blackwell B200 — Learn More"
2. **Nav**: pure black, NVIDIA logo mark + wordmark left, nav links center (uppercase 12px), "Shop" CTA green button right, Products dropdown with mega-menu
3. **Hero**: full-viewport, black bg, massive "THE AI COMPANY" headline in display-hero (white), green gradient subtitle, two CTAs, animated green particle dots + scanline overlay
4. **Green glowing separator line** (1px green line with glow box-shadow)
5. **Color Palette**: all token swatches with hex values
6. **Typography Scale**: all type classes, spec-value demo, gradient text demos
7. **Buttons**: all 6 variants + sizes + CTA
8. **GPU Product Cards**: 4-column grid — RTX 4090, RTX 4080, H100, L40S
9. **AI Datacenter Cards**: 3 horizontal cards
10. **Benchmark/Performance Bars**: 6 comparison bars (3 NVIDIA green + 3 competitor gray) + 4 spec-value cards
11. **Spec Table**: RTX 4090 full spec table with highlighted rows
12. **Navigation patterns**: breadcrumb + brand logo variants
13. **Forms**: all inputs, select, search, checkboxes, radios, toggles
14. **Feature Cards**: 2-column feature cards + GTC event card
15. **Badges & Tags**: all variants
16. **Motion section**: glow pulse, scanline, particle float, shimmer, countUp, borderGlow, springIn demos
17. **Modals**: inline modal preview + toast notifications
18. **Full-width hero callout banner** with particles
19. **Footer**: dark `#000000`, NVIDIA logo, 5-column links, copyright

---

## Component Showcase Pages

Each `components/*.html`: self-contained, dark-themed, links to `../tokens.css ../typography.css ../animations.css ../components.css`, breadcrumb navigation, all variants with labels and section headers.

- `buttons.html`: variants, sizes, CTA, states (disabled/loading), groups, icon buttons
- `cards.html`: GPU product cards (4), data center cards (3), feature cards (2), spec cards (4), event cards (3)
- `forms.html`: text inputs, search, select, checkboxes, radios, toggles, complete form example
- `navigation.html`: live global nav, notification bar, mega-menu anatomy, breadcrumbs, brand logo variants, footer nav
- `modals.html`: standard modal, destructive modal, product quick-view modal, toast notifications (4 states), notification bars (3 variants), live interactive modal triggers

---

## Requirements

- Zero external dependencies — system fonts only
- Dark-first (`:root` is dark), light via `@media (prefers-color-scheme: light)`
- Responsive, mobile-first, 768px and 1024px breakpoints
- Semantic HTML5, ARIA labels on interactive elements, `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs
- Write all files to disk using the Write tool
