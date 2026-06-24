# Nike Design System — Generation Prompt

This is the canonical prompt for generating the Nike Design System from scratch. It is part of a series of brand-faithful design systems, each following the same file structure and approach.

---

## Overview

Build a complete, production-quality design system called the "Nike Design System" inside `/path/to/Nike/`.

Before building, read the Apple Design System reference at `/path/to/Apple/` — specifically `tokens.css` and `components.css` — to calibrate the expected quality, depth, and completeness. The Nike system should match that depth while being maximally differentiated in aesthetic direction.

---

## Nike Brand Aesthetic

- **Personality:** Kinetic, aggressive, bold, aspirational, athletic. Maximum contrast to Apple's soft minimalism.
- **Typography:** Futura Bold / Trade Gothic condensed (system fallbacks: `"Futura", "Century Gothic", "Trebuchet MS", Arial, sans-serif` for display; `"Trade Gothic", "Franklin Gothic Medium", Arial Narrow, Arial, sans-serif` for condensed). Extreme weight contrast — heavy display type (weight 900) alongside light body text (weight 300 for prices).
- **Colors:**
  - Black: `#111111` (primary canvas)
  - White: `#FFFFFF`
  - Nike Volt: `#CFFC03` (electric yellow-green accent — the signature color)
  - Sport Red: `#FA3433`
  - Mid Gray: `#757575`
  - Light Gray: `#E5E5E5`
  - Surface Gray: `#F5F5F5`
- **Dark-first:** Yes — black canvas is the default. Light mode is a secondary variant via `@media (prefers-color-scheme: light)`.
- **Motion:** Fast, snappy — shorter durations than Apple (100ms / 150ms / 250ms / 350ms). Easing: `cubic-bezier(0.4, 0, 0.2, 1)`. Hover states should feel kinetic and instant.
- **Border radius:** Zero everywhere except search inputs (pill). Nike uses sharp corners as a core design principle.
- **Reference:** nike.com

---

## File Structure

```
Nike/
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

## Design Tokens (`tokens.css`)

CSS custom properties only. Two root blocks: `:root` (dark, since Nike is dark-first) and `@media (prefers-color-scheme: light)` override.

Tokens to define:

**Colors:** All brand swatches above, plus semantic tokens:
- Background hierarchy: `--color-bg-primary` (#111111), secondary, tertiary, elevated
- Surface colors for cards, modals, overlays
- Label colors: primary, secondary, tertiary, quaternary (white with opacity in dark mode)
- Separator colors (opaque and transparent)
- Fill colors (for interactive states)
- Volt variants: dim (15% opacity), glow (35%), subtle (8%)
- Red variants: dim, glow

**Typography:**
- `--font-display`: `"Futura", "Century Gothic", "Trebuchet MS", Arial, sans-serif`
- `--font-condensed`: `"Trade Gothic", "Franklin Gothic Medium", Arial Narrow, Arial, sans-serif`
- `--font-body`: `"Helvetica Neue", Helvetica, Arial, sans-serif`
- `--font-mono`: system monospace stack
- Type scale: 88 / 72 / 56 / 44 / 36 / 28 / 22 / 18 / 16 / 14 / 12 / 10px
- Weights: 300 (light) / 400 (regular) / 700 (bold) / 900 (black)
- Letter spacing: -0.02em (display), -0.01em (headline), 0 (body), 0.05em (subhead), 0.10em (labels/uppercase)
- Line heights: 0.95 (display), 1.05 (headline), 1.15 (subhead), 1.60 (body), 1.20 (label)

**Spacing:** 4px base grid — 4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64 / 80 / 96 / 128px

**Radius:** 0 (default everywhere), 2px (xs), 4px (sm), 9999px (pill — search only)

**Shadows:** Minimal — Nike relies on contrast not shadow. `shadow-sm`, `shadow-md`, `shadow-lg`, `shadow-xl`. Plus `shadow-volt` (glow) and `shadow-red` (glow).

**Motion:**
- Durations: 100ms (instant) / 150ms (fast) / 250ms (normal) / 350ms (moderate) / 500ms (slow)
- Easing: `--ease-nike: cubic-bezier(0.4, 0, 0.2, 1)` — sharp deceleration, assertive
- Transition shorthands: fast, normal, moderate

**Z-index:** base(0) / raised(10) / dropdown(100) / sticky(200) / overlay(300) / modal(400) / toast(500) / tooltip(600)

**Component dimensions:** button heights (40/48/56px), input heights, nav height (60px), max-widths (1200/1440px)

---

## Typography (`typography.css`)

Include base reset (`box-sizing`, font-smoothing), `html`/`body` defaults, then:

**Display classes:**
- `.display-hero`: 88px, weight 900, uppercase, tracking -0.02em, line-height 0.95
- `.display-large`: 72px, weight 900, uppercase
- `.display`: 56px, weight 900, uppercase

**Headlines:**
- `.headline-1` / `h1`: 44px, weight 900, uppercase
- `.headline-2` / `h2`: 36px, weight 700, uppercase
- `.headline-3` / `h3`: 28px, weight 700, uppercase

**Body:**
- `.subhead`: 22px, weight 700, uppercase, tracking 0.05em
- `.body` / `p`: 18px, weight 400, line-height 1.6
- `.body-small`: 16px, secondary color
- `.body-large`: 22px, weight 300 (light) — contrasts with display weight

**Special:**
- `.label`: 12px, weight 700, uppercase, tracking 0.10em — nav items, product tags
- `.price` / `.price-small` / `.price-large`: weight 300, `font-variant-numeric: tabular-nums`
- `.price-original`: strikethrough, tertiary color
- `.price-sale`: sport red color

**Condensed:**
- `.condensed-hero`: 88px, condensed font stack, weight 900
- `.condensed-large`: 56px
- `.condensed`: 36px

**Gradient text utilities:**
- `.text-volt`: solid volt color
- `.text-gradient`: volt → white, 135deg
- `.text-gradient-volt`: volt → 40% volt, 90deg (fading)
- `.text-gradient-white`: white → 50% white (vertical fade)

Include full responsive downsizing at 1024px, 768px, 480px breakpoints. Include `prefers-reduced-motion` support.

---

## Animations (`animations.css`)

**Keyframes to define:**
- `fadeIn` / `fadeOut`: opacity only
- `slideInLeft`: translate(-40px, 0) → (0, 0) — hero text entrance
- `slideInUp`: translate(0, 40px) → (0, 0) — content reveals
- `slideInDown`: for nav dropdowns
- `slideInRight`: for alternate entrances
- `drawerSlideIn` / `drawerSlideOut`: translateX(-100%) → 0 — full drawer animation
- `sheetSlideIn`: translateY(100%) → 0 — modal from bottom
- `scaleIn` / `scaleOut`: scale(0.95) ↔ scale(1), with opacity
- `scaleUp`: scale(0.80) → 1, more dramatic reveal
- `marqueeScroll`: translateX(0) → translateX(-50%), infinite
- `voltPulse`: box-shadow glow using volt color, 2.5s infinite
- `voltGlowText`: text-shadow glow, infinite
- `pulse`: opacity 1 → 0.5, infinite
- `spin`: 0 → 360deg, continuous
- `shake`: horizontal ±8px, for error states
- `ripple`: scale 0 → 4, opacity 0.5 → 0
- `shimmer`: for skeleton loading
- `underlineDraw`: scaleX(0) → 1 for link underlines

**Utility classes:**
- `.animate-fade-in`, `.animate-slide-left`, `.animate-slide-up`, `.animate-slide-right`
- `.animate-slide-down`, `.animate-scale-in`, `.animate-scale-up`
- `.animate-drawer-in`, `.animate-sheet-in`
- `.animate-pulse`, `.animate-spin`, `.animate-volt-pulse`, `.animate-volt-glow`, `.animate-marquee`, `.animate-shake`

**Stagger delays:** `.delay-50` through `.delay-1000`

**Hover effects:**
- `.hover-zoom`: image zooms to scale(1.05) on card hover — use with nested `img` or `.card-image`
- `.hover-underline`: volt underline draws from left on hover
- `.hover-lift`: translateY(-4px) + shadow
- `.hover-scale`: scale(1.03) on hover, scale(0.97) on active
- `.hover-volt-border`: border reveals volt on hover

**Marquee component classes:**
- `.marquee-container`: overflow hidden, full width, volt background
- `.marquee-track`: flex row, `animation: marqueeScroll 22s linear infinite`, `width: max-content`
- `.marquee-item`: label-style text
- `.marquee-dot`: small decorative separator

**Scroll reveal:** `.reveal` and `.reveal-left` — opacity/translate start states. JS adds `.is-visible` class.

**Skeleton/shimmer:** `.skeleton`, `.skeleton-text`, `.skeleton-block`

**Reduced motion:** `@media (prefers-reduced-motion: reduce)` collapses all animation durations to 0.01ms, stops marquee, flattens skeletons, makes reveal elements immediately visible.

---

## Components (`components.css`)

### Layout
- `.container` (max-width: 1200px), `.container-wide` (1440px), `.container-text` (760px)
- `.section` (padding 80px 0), `.section-sm`, `.section-lg`
- `.section-overline`: volt colored 12px uppercase label

### Buttons
All buttons: `border-radius: 0`, uppercase, `letter-spacing: 0.10em`, `font-weight: 900`, height 48px default.

- `.btn-primary`: black fill + white text. Hover: volt bg + black text. 150ms transition.
- `.btn-primary--volt`: volt fill + black text. Hover: white bg + black text. Primary CTA.
- `.btn-secondary`: transparent + 1px white border + white text. Hover: white fill + black text.
- `.btn-secondary--dark`: for light backgrounds — black border → black fill on hover.
- `.btn-ghost`: no border, white text, underline on hover (transparent → white).
- `.btn-ghost--volt`: same but volt colored.
- `.btn-destructive`: sport red fill.
- `.btn-icon`: circular 48px, fill secondary, border separator. `.btn-icon--volt`: volt fill.
- `.add-to-cart`: full-width 56px, volt → white on hover. Primary product CTA.
- Sizes: `.btn-sm` (40px), `.btn-lg` (56px)
- States: `:disabled` (0.35 opacity), `.loading` (spinner via `::after`)
- Focus: 2px volt outline at 2px offset

### Cards

**`.card-product`**: dark surface card for product grid.
- Image area with `hover-zoom` image scale
- Absolute badge (top-left) and wishlist button (top-right)
- Wishlist hover: volt bg + black icon
- Body: category label, product name, color count, price

**`.card-feature`**: full-bleed editorial card.
- Position relative, min-height 480px
- Absolute background image
- `::after` gradient overlay (black 90% → transparent over 75% from bottom)
- Content: overline in volt, display-class headline, CTA button
- Image zooms to scale(1.03) on hover

**`.card-collection`**: horizontal grid, image left / content right.
- Grid 1fr 1fr. Stacks on mobile.
- Image side with hover zoom
- Content side: volt overline, display headline, description, CTA

**`.card-editorial`**: text-only card.
- 3px volt left border
- Date, large headline (display class), excerpt, "Read More →" link
- Link arrow gap animates wider on hover
- Background darkens slightly on hover

**`.card-stat`**: volt top border.
- Volt number (72px, weight 900, line-height 0.90)
- Label (12px uppercase)
- Description text

### Navigation

**`.nav-global`**: sticky, 60px height, black bg.
- Three-column grid: brand left / links center / actions right
- Links: `.nav-links` list, 12px bold uppercase, 0.10em tracking
- Active and hover: color → white
- Action buttons: 40px, icon only, hover → volt
- Action badge: volt bg, black text, 16px pill

**`.nav-mobile`**: position fixed, full viewport, black.
- Slides from left via CSS transform. `.is-open` class triggers.
- Links use display-class type (28px, weight 900, uppercase)
- Hover: volt color

**`.nav-breadcrumb`**: flex list, slash separator, label-style text, 12px uppercase.

**`.tabs`**: flex row, `border-bottom: 1px solid separator`.
- Each `.tab-item`: 12px bold uppercase, no background.
- `::after` pseudo-element: 2px volt underline, `transform: scaleX(0)` → `scaleX(1)` on active.
- Hover: 50% width underline preview.

**`.drawer-nav`**: full-screen overlay. Panel is `min(400px, 90vw)`.
- Backdrop: 70% black, fadeIn.
- Panel: drawerSlideIn animation.
- Items: uppercase, border-bottom separator, hover → volt color.

### Forms

**`.input`**: sharp corners, dark bg (`--color-bg-secondary`), 1px separator border.
- Focus: volt border + 2px volt dim box-shadow.
- Error: red border + red dim shadow.
- Success: green border.
- Disabled: 40% opacity.

**`.input-search`**: ONLY component with `border-radius: var(--radius-search)` (pill).
- Pill shape, search icon in padding-left, clear button on right.
- Clear button hover: volt bg + black text.

**`.textarea`**: same as input, resizable.

**`.select`**: custom `▼` arrow, dark styled, sharp corners.

**`.checkbox`**: 20×20px sharp square. Volt fill + black checkmark on checked. `transform: scale(0) → scale(1)` checkmark animation.

**`.radio`**: 20×20px circle. Volt inner dot on checked.

**`.toggle`**: 48×26px pill track. Volt bg on checked. White thumb, 22px translate.

### Product Components

**`.product-grid`**: 4-column responsive grid (→ 3 → 2 at breakpoints).

**`.size-selector`**: label row with "Size Guide" link, then `.size-grid`.
- `.size-grid`: 4-column grid of `.size-btn`
- `.size-btn`: 48px height, sharp, border separator. Selected: volt bg + black text. Unavailable: 25% opacity, strikethrough, not interactive.

**`.color-selector`**: label + `.color-swatches` row.
- `.color-swatch`: 28px circle. Selected: volt outline ring.

**`.add-to-cart`**: full-width 56px volt button. Hover: white. Disabled: fill-secondary bg.

**`.product-badge`**: 10px black uppercase, sharp, no padding rounding.
- `--new`: volt bg, black text
- `--best-seller`: white bg, black text
- `--sale`: sport red bg, white text
- `--member`: dark outline style

### Marquee/Ticker

**`.marquee-container`**: overflow hidden, volt bg, padding 12px 0.
**`.marquee-track`**: flex row, `width: max-content`, `animation: marqueeScroll 22s linear infinite`.
- Pause on container hover: `animation-play-state: paused`.
**`.marquee-item`**: 12px bold uppercase label, black text (for volt bg).
**`.marquee-dot`**: 4px black circle separator.

### Modals

**`.modal-overlay`**: position fixed inset 0, `background: rgba(0, 0, 0, 0.90)`, z-index modal.
- Center variant: `align-items: center; padding: 24px`.

**`.modal-dialog`**: max-width 560px, dark bg (`--color-bg-secondary`), 2px volt top border, no radius.
- Header: title (display class 22px) + close button (circle, hover → volt).
- Body: scrollable, 16px body text.
- Footer: flex row buttons, right-aligned.
- Animation: `sheetSlideIn` from bottom. Center variant: `scaleIn`.

**`.drawer-nav-panel`**: `min(400px, 90vw)`, full height, black bg, `drawerSlideIn` animation.

### Utility classes

Grids: `.grid-2`, `.grid-3`, `.grid-4`, `.grid-auto`
Flex: `.flex`, `.flex-col`, `.flex-center`, `.flex-between`, `.flex-wrap`, gap utilities
Spacing: `.mt-*`, `.mb-*` in 4px grid increments
Accessibility: `.sr-only`
Badges: `.badge` with volt/white/black/red/outline variants

---

## Main `index.html`

A polished showcase demonstrating the complete Nike design language. Structure:

1. **Sticky header** — `.nav-global` with wordmark, nav links, bag/search/favorites icons with badge
2. **Mobile nav** — hidden drawer, toggled by hamburger button
3. **Hero section** — 100svh, black canvas, `.display-hero` "Just Do It." headline with `animate-slide-left`, volt rule accent, subhead, two CTAs (volt primary + white secondary)
4. **Marquee ticker** — volt background, scrolling "New Arrivals · Air Max · Just Do It · Free Shipping · Nike App ·"
5. **Color palette** — swatch grid with all brand tokens
6. **Typography scale** — all classes rendered from display-hero down to price
7. **Buttons section** — all variants: primary, volt, secondary, ghost, destructive, icon, sizes, states
8. **Product cards** — 3-column grid of `.card-product` with different badges
9. **Stat cards** — 4-column `.card-stat` grid
10. **Feature card** — full-bleed `.card-feature`
11. **Collection card** — `.card-collection` horizontal layout
12. **Editorial cards** — 3-column `.card-editorial` grid
13. **Forms section** — inputs, search, textarea, select, checkboxes, radio, toggles, progress bars
14. **Navigation demo** — breadcrumb, tabs, badges, dividers
15. **Product detail** — side-by-side image + `.size-selector`, `.color-selector`, `.add-to-cart`
16. **Motion section** — animated demos (marquee, volt pulse, spinners, slide/scale demos, timing reference, easing reference)
17. **Modals preview** — static inline previews + live modal launch buttons
18. **Footer** — dark, 4-column link grid, copyright, legal links

Include JavaScript for: mobile nav toggle, size/tab/swatch selection, scroll reveal observer.

---

## Component Showcase Pages

Each `components/*.html` is self-contained, links to all 4 CSS files, shows all variants with code-style labels (monospace, small, label-secondary color). Includes the sticky nav and a back link to the main system index.

Pages:
- `buttons.html` — All button variants, sizes, states, groups
- `cards.html` — Product cards (6 variants), feature, collection, editorial, stat
- `forms.html` — All inputs, search, textarea, select, checkbox, radio, toggle, size selector, color swatches, progress bars, complete form example
- `navigation.html` — Global nav preview, mobile nav preview, breadcrumbs, tabs, drawer preview, badges, dividers, tooltips
- `modals.html` — Static previews + fully interactive live modals (sheet, center dialog, size guide, confirm dialog, drawer) with JS open/close/backdrop/escape behavior

---

## Requirements

- Zero external dependencies — no CDN, no Google Fonts, system fonts only
- Dark-first (`:root` is dark), light mode via `@media (prefers-color-scheme: light)`
- Fully responsive, mobile-first, breakpoints 768px and 1024px
- Semantic HTML5 with proper ARIA attributes
- `prefers-reduced-motion` respected in all animation files
- All files complete — no placeholders, no TODOs
- All files written to disk using Write tool
