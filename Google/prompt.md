# Google Material You (Material Design 3) — Design System Generation Prompt

## Purpose

This document is the canonical specification for regenerating the complete Google Material You (Material Design 3) design system from scratch. It describes every design decision, token, component, and file in enough detail to produce pixel-faithful, spec-compliant output without referencing any existing files.

---

## Scope

Generate 7 files:

1. `tokens.css` — all design tokens (colors, type scale, spacing, shape, motion, elevation, z-index)
2. `typography.css` — base reset, all 15 M3 type classes, heading defaults, body, links, utilities, responsive overrides
3. `animations.css` — all M3 keyframes, ripple, state layer classes, animation utilities, skeleton loader, reduced-motion
4. `components.css` — all M3 UI components as pure CSS (no JS classes)
5. `index.html` — full showcase page with every component
6. `components/buttons.html` — buttons deep-dive page
7. `components/cards.html` — cards deep-dive page
8. `components/forms.html` — forms deep-dive page
9. `components/navigation.html` — navigation deep-dive page
10. `components/modals.html` — modals/overlays deep-dive page

**Zero external dependencies** except the Google Fonts `@import` in `typography.css`. All files link to the 4 CSS files. Dark mode via `@media (prefers-color-scheme: dark)`. Reduced motion via `@media (prefers-reduced-motion: reduce)`.

---

## Brand Identity

- **System**: Material Design 3 / Material You
- **Spec reference**: m3.material.io
- **Seed color**: Google Blue `#4285F4`
- **Design philosophy**: Adaptive, expressive, personal — dynamic color, tonal palettes, expressive motion
- **Platforms**: Android, Web, Flutter

---

## 1. tokens.css

### Color System — Light Mode (`:root`)

Derived from seed color `#4285F4` using the HCT color space (approximated).

```
/* Primary */
--color-primary:                  #4285F4
--color-on-primary:               #FFFFFF
--color-primary-container:        #D3E4FF
--color-on-primary-container:     #001C3B

/* Secondary */
--color-secondary:                #5A6472
--color-on-secondary:             #FFFFFF
--color-secondary-container:      #DCE4F0
--color-on-secondary-container:   #171E27

/* Tertiary */
--color-tertiary:                 #6D5778
--color-on-tertiary:              #FFFFFF
--color-tertiary-container:       #F4DAFF
--color-on-tertiary-container:    #271632

/* Error */
--color-error:                    #BA1A1A
--color-on-error:                 #FFFFFF
--color-error-container:          #FFDAD6
--color-on-error-container:       #410002

/* Surface (5 container levels) */
--color-surface:                  #F8F9FF
--color-on-surface:               #1A1C22
--color-surface-variant:          #E1E2EC
--color-on-surface-variant:       #44464F
--color-surface-container-lowest: #FFFFFF
--color-surface-container-low:    #F2F3FA
--color-surface-container:        #ECEDF4
--color-surface-container-high:   #E7E8EF
--color-surface-container-highest:#E1E2E9

/* Inverse */
--color-inverse-surface:          #2F3038
--color-inverse-on-surface:       #E3E2EC
--color-inverse-primary:          #A4C8FF

/* Background */
--color-background:               #F8F9FF
--color-on-background:            #1A1C22

/* Outline */
--color-outline:                  #74777F
--color-outline-variant:          #C4C6D0

/* Scrim / Shadow */
--color-scrim:                    #000000
--color-shadow:                   #000000
```

### Color System — Dark Mode (`@media (prefers-color-scheme: dark)`)

Override all color tokens. Key differences:
- Primary becomes the light tone (#A4C8FF) for legibility on dark
- Containers invert: primary-container #004785 (dark)
- Surfaces: #111318 base, container-low #1A1C22, container #1E2027, container-high #282A31, container-highest #333540
- Error becomes #FFB4AB
- Outlines: #8E9099 / #44464F

### Elevation — Surface Tint (M3 model)

M3 uses primary-color tinting instead of just shadows.

```css
--elevation-0: var(--color-surface)
--elevation-1: color-mix(in srgb, var(--color-primary)  5%, var(--color-surface))
--elevation-2: color-mix(in srgb, var(--color-primary)  8%, var(--color-surface))
--elevation-3: color-mix(in srgb, var(--color-primary) 11%, var(--color-surface))
--elevation-4: color-mix(in srgb, var(--color-primary) 12%, var(--color-surface))
--elevation-5: color-mix(in srgb, var(--color-primary) 14%, var(--color-surface))
```

Also provide `--shadow-elevation-1` through `--shadow-elevation-5` as drop shadows (used together with tint, not instead of it).

### Tonal Palette — Primary (13 stops)

```
--palette-primary-0:   #000000
--palette-primary-10:  #001C3B
--palette-primary-20:  #003062
--palette-primary-30:  #00468C
--palette-primary-40:  #4285F4   ← seed
--palette-primary-50:  #4A90F5
--palette-primary-60:  #6BA3F7
--palette-primary-70:  #8DB7F8
--palette-primary-80:  #A4C8FF
--palette-primary-90:  #D3E4FF
--palette-primary-95:  #EAF1FF
--palette-primary-99:  #FDFCFF
--palette-primary-100: #FFFFFF
```

### Typography

```
--font-brand: "Google Sans", "Product Sans", Roboto, system-ui, sans-serif
--font-body:  "Roboto", system-ui, -apple-system, sans-serif
--font-mono:  "Roboto Mono", "Google Sans Mono", ui-monospace, monospace
```

M3 Type Scale — 15 entries, each with `-size`, `-weight`, `-tracking`, `-leading`:

| Token name              | Size | Weight | Tracking | Leading |
|-------------------------|------|--------|----------|---------|
| display-large           | 57px | 400    | -0.25px  | 64px    |
| display-medium          | 45px | 400    | 0px      | 52px    |
| display-small           | 36px | 400    | 0px      | 44px    |
| headline-large          | 32px | 400    | 0px      | 40px    |
| headline-medium         | 28px | 400    | 0px      | 36px    |
| headline-small          | 24px | 400    | 0px      | 32px    |
| title-large             | 22px | 400    | 0px      | 28px    |
| title-medium            | 16px | 500    | 0.15px   | 24px    |
| title-small             | 14px | 500    | 0.1px    | 20px    |
| label-large             | 14px | 500    | 0.1px    | 20px    |
| label-medium            | 12px | 500    | 0.5px    | 16px    |
| label-small             | 11px | 500    | 0.5px    | 16px    |
| body-large              | 16px | 400    | 0.5px    | 24px    |
| body-medium             | 14px | 400    | 0.25px   | 20px    |
| body-small              | 12px | 400    | 0.4px    | 16px    |

### Spacing — 4px Grid

`--space-1: 4px` through `--space-32: 128px` (steps: 1,2,3,4,5,6,7,8,10,12,14,16,20,24,32).

### Shape Scale

```
--shape-none:        0px
--shape-extra-small: 4px
--shape-small:       8px
--shape-medium:      12px
--shape-large:       16px
--shape-extra-large: 28px
--shape-full:        9999px
```

Component shape mappings:
- button → full
- chip → small (8px)
- card → medium (12px)
- dialog → extra-large (28px)
- bottom-sheet → extra-large top corners, 0 bottom
- menu → extra-small (4px)
- snackbar → extra-small
- textfield-filled → extra-small extra-small 0 0 (top rounded only)
- fab → large (16px)
- fab-small → medium (12px)
- fab-large → extra-large (28px)
- nav-indicator → full

### Motion

Easing curves:
- `--motion-easing-standard`: `cubic-bezier(0.2, 0, 0, 1)`
- `--motion-easing-emphasized`: `cubic-bezier(0.2, 0, 0, 1)`
- `--motion-easing-emphasized-decelerate`: `cubic-bezier(0.05, 0.7, 0.1, 1)` — for entering elements
- `--motion-easing-emphasized-accelerate`: `cubic-bezier(0.3, 0, 0.8, 0.15)` — for exiting elements
- `--motion-easing-standard-decelerate`: `cubic-bezier(0, 0, 0, 1)`
- `--motion-easing-standard-accelerate`: `cubic-bezier(0.3, 0, 1, 1)`
- `--motion-easing-legacy`: `cubic-bezier(0.4, 0, 0.2, 1)`

Durations (16 tokens): short-1 (50ms) → extra-long-4 (1000ms).

### State Layers

```
--state-hover-opacity:    0.08
--state-focus-opacity:    0.12
--state-pressed-opacity:  0.12
--state-dragged-opacity:  0.16
--state-disabled-opacity: 0.38
```

### Component Dimensions

```
--btn-height:         40px
--btn-height-sm:      32px
--fab-size:           56px
--fab-size-small:     40px
--fab-size-large:     96px
--chip-height:        32px
--textfield-height:   56px
--nav-bar-height:     80px
--nav-rail-width:     80px
--nav-drawer-width:   360px
--app-bar-height:     64px
--list-item-height-1: 56px   (one-line)
--list-item-height-2: 72px   (two-line)
--list-item-height-3: 88px   (three-line)
--dialog-max-width:   560px
```

### Z-Index Scale

base(0) → raised(10) → nav(100) → app-bar(200) → drawer(300) → modal-scrim(400) → modal(500) → snackbar(600) → tooltip(700).

---

## 2. typography.css

- Google Fonts `@import` for Roboto (100–900), Google Sans (400/500/700), Google Sans Display (400), Roboto Mono (400/500)
- `*, *::before, *::after { box-sizing: border-box; -webkit-font-smoothing: antialiased }`
- `body`: font-body, body-large size, color-on-background, background-color-background, margin/padding 0
- 15 type utility classes (`.display-large`, `.display-medium`, … `.label-small`): each sets font-family, font-size, font-weight, line-height, letter-spacing, color, margin:0
  - Display/Headline/Title → `--font-brand`
  - Label/Body → `--font-body`
- `h1`–`h6` defaults mapped to M3 scale
- `p { font-body, body-large }` with 1em bottom margin
- `code/pre/kbd`: font-mono, surface-container-high background
- `a`: color-primary, no underline by default, underline on hover
- Text utilities: `.text-primary`, `.text-secondary`, `.text-on-primary`, `.text-error`, `.text-primary-color`, `.text-gradient-m3` (primary→tertiary gradient clip)
- Responsive: at 768px reduce display-large/medium/small and headline-large; at 480px further reduce
- `prefers-reduced-motion: reduce` → `scroll-behavior: auto`

---

## 3. animations.css

### Keyframes

- `fadeIn / fadeOut` — opacity 0↔1
- `m3SlideUp` — from `opacity:0, translateY(100%)` to `opacity:1, translateY(0)` — for bottom sheets, snackbars
- `m3SlideDown` — reverse
- `m3ScaleIn` — from `opacity:0, scale(0.8)` to `opacity:1, scale(1)` — for dialogs, menus
- `m3ScaleOut` — reverse
- `m3Ripple` — scale 0→4, opacity pressed→0, 600ms
- `fabExtend / fabLabelReveal` — extended FAB enter
- `shimmer` — background-position for skeleton loader
- `m3LinearIndeterminate1 / m3LinearIndeterminate2` — two-segment linear indeterminate
- `m3CircularSpin` — rotate 0→360deg
- `m3CircularDash` — stroke-dashoffset oscillation for circular indeterminate
- `m3SnackbarIn / m3SnackbarOut` — translateY + scale for snackbar
- `m3NavIndicator` — pill scale-in
- `m3CheckmarkIn` — chip checkmark scale + rotate
- `spin, pulse, bounce, float, gradientFlow, glowPulse, shake` — general utilities

### Ripple

`.ripple-container { position: relative; overflow: hidden }` with JS-injected `.ripple-wave` spans that use `m3Ripple` keyframe.

### State Layer

`.state-layer { position: relative; overflow: hidden }` with `::before { background: --color-on-surface; opacity: 0 }` that rises to 0.08 on hover, 0.12 on focus/active. Variant `.state-layer-primary` uses `--color-primary`.

### Utility Classes

`.animate-fade-in`, `.animate-slide-up`, `.animate-scale-in`, `.animate-spin`, `.animate-pulse`, `.animate-bounce`, `.animate-float`, `.animate-glow-pulse`, `.animate-snackbar-in`, `.animate-gradient`, `.animate-shake`.

Delay utilities: `.delay-50` through `.delay-1000`.

Transition utilities: `.transition-standard/emphasized/decelerate/accelerate`.

Hover effects: `.hover-lift` (translateY -2px + shadow), `.hover-scale` (scale 1.02 hover, 0.98 active).

### Skeleton

`.skeleton` — gradient shimmer, 200% wide background animated.
`.skeleton-text` with `.short` (40%), `.medium` (65%), `.long` (90%).
`.skeleton-circle`, `.skeleton-rect`.

### Reduced Motion

`@media (prefers-reduced-motion: reduce)` — all animations 0.01ms, no iterations, scroll auto. Skeleton becomes static, gradient stops.

---

## 4. components.css

### Layout Utilities

`.container { max-width: 1200px; margin-inline: auto; padding-inline: 24px }`
`.container-compact { max-width: 600px }`, `.container-medium { max-width: 840px }`.

### Buttons (`.btn-m3`)

Base: `display: inline-flex; align-items: center; height: 40px; padding: 0 24px; border-radius: 9999px; font: label-large; position: relative; overflow: hidden`. State layer via `::before { background: currentColor; opacity: 0 }` on `:hover` (0.08), `:focus` (0.12), `:active` (0.12). Disabled: opacity 0.38, pointer-events none.

5 variants:
1. **`.btn-filled`** — bg: primary, color: on-primary. Hover: shadow-elevation-1.
2. **`.btn-filled-tonal`** — bg: secondary-container, color: on-secondary-container. Hover: shadow-elevation-1.
3. **`.btn-elevated`** — bg: elevation-1, color: primary, shadow-elevation-1. Hover: shadow-elevation-2.
4. **`.btn-outlined`** — bg: transparent, color: primary, border: 1px outline. Focus: border becomes primary.
5. **`.btn-text`** — bg: transparent, color: primary, padding: 0 12px.

`.btn-icon { width: 18px; height: 18px }` for leading icons.

### Icon Buttons (`.btn-icon-m3`)

40×40px circle. 4 variants: `.btn-icon-standard` (transparent), `.btn-icon-filled` (primary), `.btn-icon-tonal` (secondary-container), `.btn-icon-outlined` (border + outline). All have ::before state layers. Icons: 24×24px.

### FAB (`.fab`)

56×56px default, shape-large (16px) radius, bg: tertiary-container, shadow-elevation-3. Hover: shadow-elevation-4 + 8% state layer. Size variants: `.fab--small` (40px, shape-medium), `.fab--large` (96px, shape-extra-large). Color variants: `.fab--primary`, `.fab--secondary`. Extended: `.fab--extended` — auto width, 20px horizontal padding, pill shape, label-large text.

### Chips (`.chip`)

32px height, shape-small (8px) radius, label-large typography. 4 types:
- **`.chip-assist`** — surface bg, outline-variant border. Hover: shadow-elevation-1.
- **`.chip-filter`** — surface bg, outline-variant border. Selected (`.selected` / `[aria-selected="true"]`): secondary-container bg, no border. Shows `.chip-filter-check` SVG on selection via `display:block` + `m3CheckmarkIn` animation.
- **`.chip-input`** — secondary-container bg, includes `.chip-input-close` button (18×18px with 14×14px X icon).
- **`.chip-suggestion`** — same as assist but no icon slot expected.

### Cards (`.card-m3`)

shape-medium (12px) radius, overflow: hidden, `::before` state layer for interactive variants. 3 types:
- **`.card-elevated`** — elevation-1 bg, shadow-elevation-1. Hover (tabindex/role=button): shadow-elevation-2.
- **`.card-filled`** — surface-container-highest bg, no shadow.
- **`.card-outlined`** — surface bg, 1px outline-variant border. Hover: shadow-elevation-1.

Anatomy: `.card-media` (16:9 aspect ratio), `.card-header` (flex row, 16px padding), `.card-avatar` (40px circle), `.card-title-group`, `.card-title` (title-medium), `.card-subtitle` (body-medium, on-surface-variant), `.card-content` (16px padding), `.card-body` (body-medium, on-surface-variant), `.card-actions` (flex row, 12px 16px 16px padding).

### Navigation Bar (`.nav-bar`)

`position: fixed; bottom: 0; height: 80px; background: surface-container`. Items: `.nav-bar-item` — flex column, 1fr flex, color: on-surface-variant. Active: color: on-surface. Indicator: `.nav-bar-indicator` — 64×32px pill, transparent → secondary-container when active. State layer via `::before`. Labels: label-medium. 3–5 items.

### Navigation Rail (`.nav-rail`)

`position: fixed; left: 0; width: 80px; min-height: 100vh; background: surface-container-low`. Items: `.nav-rail-item` — flex column, full width. Indicator: 56×32px pill. Otherwise same pattern as nav-bar.

### Navigation Drawer (`.nav-drawer`)

`position: fixed; left: 0; width: 360px; background: surface-container-low`. `.nav-drawer-headline` (title-large), `.nav-drawer-section-header` (title-small, on-surface-variant), `.nav-drawer-item` (56px height, full pill, active: secondary-container bg). Badge and icon slots.

### Tabs (`.tabs-m3`)

`display: flex; background: surface; border-bottom: 1px surface-variant`. `.tab-item` (48px height, title-small typography, on-surface-variant color). Active: `::after` (3px bottom bar, primary color, scaleX 1). Inactive: scaleX 0. State layer via `::before`. Secondary variant `.tabs-m3--secondary`: no bg, 2px indicator in on-surface.

### Text Fields

Two variants. Both: `.textfield-m3 { position: relative; width: 100% }`.

**Filled** (`.textfield-filled`): `.field-container` bg: surface-container-highest, border-radius: extra-small extra-small 0 0. Bottom line via `::after` (1px on-surface-variant → 2px primary on `:focus-within`). Floating label: `position: absolute; left: 16px; top: 50%; transform: translateY(-50%)`. On focus or `.has-value`: `top: 8px; transform: translateY(0) scale(0.75)`. Label color: on-surface-variant → primary on focus → error on `.error`.

**Outlined** (`.textfield-outlined`): `.field-container` border: 1px outline. Focus: 2px primary. Label notches into border by floating with `background: --color-background`. On focus or `.has-value`: `top: 0; transform: translateY(-50%) scale(0.75)`.

Both: `.field-leading-icon / .field-trailing-icon` (24px SVG), `.field-supporting-text` (body-small, on-surface-variant), `.field-supporting-text.error` (error color), `.field-counter` (right-aligned body-small). Disabled: `.disabled .field-container { opacity: 0.38 }`.

### Selection Controls

**Checkbox** (`.checkbox-m3`): Hidden `<input>`, custom `.checkbox-box` (18×18px, 2px border, 2px radius). State layer via `::before { inset: -11px; border-radius: full }`. On `:checked`: primary bg + border, checkmark SVG (12×12) animates in (scale 0.6→1). Disabled: 0.38 opacity.

**Radio** (`.radio-m3`): Hidden `<input>`, custom `.radio-circle` (20×20px, 2px border, full radius). `.radio-dot` (10×10px primary, scale 0→1 on checked). State layer same pattern.

**Switch** (`.switch-m3`): Track 52×32px, border: 2px outline, bg: surface-container-highest. Thumb: 16px circle (on outline color), left: 6px. On `:checked`: track bg primary + border primary; thumb 24px, white, left 2px, translateX(20px). Hover: thumb expands to 24px. Icon in thumb: 12×12 checkmark, opacity 0→1 on checked.

### Sliders (`.slider-m3`)

44px height wrapper. `input[type="range"]` custom: 4px track, full radius. Webkit track: linear-gradient from primary (0% to `--slider-value`) then secondary-container (to 100%). Thumb: 20×20px primary circle, no border. Hover: 24×24px.

### Progress

**Linear** (`.progress-linear`): 4px height, secondary-container bg, full radius. `.progress-linear-fill` — primary color, transition width. Indeterminate (`.progress-linear--indeterminate`): fill animates `m3LinearIndeterminate1`; `::after` animates `m3LinearIndeterminate2`.

**Circular** (`.progress-circular`): 48px wrapper. SVG with `transform: rotate(-90deg)`. `.progress-circular-track` (secondary-container stroke). `.progress-circular-fill` (primary stroke, stroke-linecap: round, stroke-dasharray: 125.66, stroke-dashoffset: `125.66 * (1 - --progress-value)`). Indeterminate: container spins via `m3CircularSpin`, fill uses `m3CircularDash`. Sizes: `--sm` (24px), `--lg` (72px).

### Lists (`.list-m3`)

`flex-direction: column; background: surface; border-radius: medium`. `.list-item-m3` — flex row, min-height 56px, 8px 16px padding. Interactive items: cursor pointer, state layer `::before`. Two-line: min-height 72px. Three-line: min-height 88px, align-items flex-start. `.list-item-leading/trailing { flex-shrink: 0 }`. `.list-item-content { flex: 1; min-width: 0 }`. `.list-item-headline` (body-large, on-surface), `.list-item-supporting` (body-medium, on-surface-variant). `.list-item-avatar` (40px circle), `.list-item-icon` (24px, on-surface-variant), `.list-item-thumbnail` (56px, shape-extra-small). `.divider-m3` (1px, outline-variant). `.divider-m3--inset` (left margin: 16 + 24 + 16 = 56px), `--inset-with-avatar` (16 + 40 + 16 = 72px).

### Dialogs (`.dialog-m3`)

`background: elevation-3; border-radius: 28px; max-width: 560px; box-shadow: shadow-elevation-3; animation: m3ScaleIn`. Scrim: `rgba(0,0,0,0.32); fixed; inset 0`. `.dialog-icon` (center, secondary color SVG). `.dialog-headline` (headline-small, font-brand, center). `.dialog-headline--left` (left-aligned). `.dialog-body` (body-medium, on-surface-variant, max-height 40vh scroll). `.dialog-actions` (flex row, justify-end, 12px 24px padding).

### Bottom Sheets (`.bottom-sheet`)

`position: fixed; bottom: 0; left: 0; right: 0; background: surface-container-low; border-radius: 28px 28px 0 0; animation: m3SlideUp; max-height: 90vh`. Handle: `.bottom-sheet-handle::before` (32×4px pill, on-surface-variant 40% opacity). `.bottom-sheet-headline` (title-large, font-brand). `.bottom-sheet-content { overflow-y: auto; flex: 1 }`.

### Snackbar (`.snackbar-m3`)

`display: flex; min-height: 48px; background: inverse-surface; color: inverse-on-surface; border-radius: 4px; box-shadow: shadow-elevation-3; animation: m3SnackbarIn`. Container: `position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%); max-width: 600px; min-width: 288px`. `.snackbar-text { flex: 1; body-medium }`. `.snackbar-action { inverse-primary color; label-large; no bg/border }`. `.snackbar-close { 40px circle; icon button }`.

### Menus (`.menu-m3`)

`background: elevation-2; border-radius: 4px; box-shadow: shadow-elevation-2; padding: 8px 0; min-width: 112px; animation: m3ScaleIn; transform-origin: top left`. `.menu-item-m3` (48px height, body-large, on-surface, hover state layer). `.menu-item-icon` (24px, on-surface-variant). `.menu-item-label { flex: 1 }`. `.menu-item-trailing` (body-medium, on-surface-variant). `.menu-divider` (1px outline-variant). `.menu-label` (label-small, on-surface-variant, section header).

### Badges (`.badge-m3`)

`display: inline-flex; min-width: 16px; height: 16px; background: error; color: on-error; border-radius: full; label-small`. `.badge-m3--dot` (6px × 6px). `.badge-m3--lg` (24px height, label-medium). `.badge-wrapper { position: relative; display: inline-flex }` with badge `position: absolute; top: -4px; right: -4px`.

### Top App Bar (`.app-bar-m3`)

`display: flex; align-items: center; height: 64px; padding: 0 4px; background: elevation-2; position: sticky; top: 0; z-index: 200`. `.app-bar-title { flex: 1; title-large; font-brand; truncate }`. `.app-bar-nav, .app-bar-actions { flex-shrink: 0 }`. Scrolled: `.app-bar-m3--scrolled` adds shadow-elevation-2. Center: `.app-bar-m3--center .app-bar-title { text-align: center }`. Medium/Large: `.app-bar-m3--medium { flex-direction: column }` with `.app-bar-row` (64px) + `.app-bar-headline` (headline-small, 16px/20px padding).

### Tooltips (`.tooltip-m3`)

`position: relative; display: inline-flex`. `::after { content: attr(data-tooltip); position: absolute; bottom: calc(100% + 4px); left: 50%; transform: translateX(-50%); background: inverse-surface; color: inverse-on-surface; body-small; padding: 4px 8px; border-radius: 4px; opacity: 0; transition standard }`. Hover: opacity 1. Rich: `.tooltip-rich-m3 { background: elevation-2; border-radius: medium; padding 12px 16px; shadow-elevation-2; max-width: 280px }`.

### Surface Utilities

`.surface-0` through `.surface-5` set `background: var(--elevation-N)`. `.surface-container`, `.surface-container-low`, `.surface-container-high`, `.surface-container-highest`.

### Grid & Flex Utilities

`.grid { display: grid; gap: 16px }`. `.grid-2/3/4` (repeat N, 1fr). `.grid-auto { repeat(auto-fill, minmax(280px,1fr)) }`. `.flex, .flex-col, .flex-wrap, .items-center/start/end, .justify-center/between/end, .gap-1` through `.gap-8`, `.flex-1`. Responsive: grid-4 → 2col at 1024px, → 1col at 768px; grid-3 → 2col at 768px; grid-2 → 1col at 480px.

### Spacing Utilities

`.p-0/2/3/4/6/8`, `.pt/pb/px/py-*`, `.m-0`, `.mt/mb-2/4/6/8`.

### Color Utilities

`.bg-primary`, `.bg-primary-container`, `.bg-secondary`, `.bg-secondary-container`, `.bg-tertiary`, `.bg-tertiary-container`, `.bg-error`, `.bg-error-container`, `.bg-surface`, `.bg-surface-variant`.

### Border Utilities

`.rounded-none/xs/sm/md/lg/xl/full` mapping to shape scale.

---

## 5. index.html — Showcase Page

### Structure

```html
<head>
  <!-- 4 CSS links: tokens, typography, animations, components -->
  <!-- Inline <style> for page-specific layout -->
</head>
<body>
  <header class="app-bar-m3"><!-- nav icon, title, actions + badge --></header>
  <nav class="container"><!-- component quick-nav pill links --></nav>
  <main>
    <section class="hero-section">
      <!-- gradient bg from primary/tertiary/secondary containers -->
      <!-- display-large headline, body-large subtitle -->
      <!-- filled + tonal CTA buttons -->
      <!-- tonal palette strip (13 stops) -->
    </section>
    <!-- #colors: color role swatches grid + elevation cards -->
    <!-- #typography: all 15 type scale rows -->
    <!-- #buttons: all 5 + FAB + icon buttons -->
    <!-- #chips: all 4 types + selected states -->
    <!-- #fields: filled + outlined, all states -->
    <!-- #selection: checkboxes, radios, switches -->
    <!-- #navigation: nav bar + nav rail (static) + tabs -->
    <!-- #cards: all 3 card types with content -->
    <!-- #lists: 1-line, 2-line items -->
    <!-- #sliders: 3 examples -->
    <!-- #progress: linear det/indet + circular sizes -->
    <!-- #dialogs: 2 static dialogs -->
    <!-- #overlays: bottom sheet + menu + snackbars + badges -->
    <!-- #motion: state layers + ripple + easing cards + skeleton -->
  </main>
  <nav class="nav-bar"><!-- fixed bottom nav, 4 destinations --></nav>
  <footer class="site-footer"><!-- dark #202124 bg, grid, links --></footer>
  <script><!-- ripple, app-bar scroll, has-value sync --></script>
</body>
```

Key rules:
- All nav-bar / nav-rail / drawer demos must be `position: static` (override fixed positioning) for inline showcase
- Dialog demos: static divs styled like `.dialog-m3`
- Bottom sheet: static, no animation
- Snackbars: `position: static; animation: none`
- JS: ripple injection from click position, app-bar scrolled class toggle, input→has-value sync

---

## 6–10. Component Pages

Each file in `components/`:
- Links to `../tokens.css`, `../typography.css`, `../animations.css`, `../components.css`
- Sticky `page-header` with back link + `<h1>` title
- Uses `.container` for content
- Sections with `.section-title`, `.section-desc`, `.demo-label`
- All variants shown with clear labels
- No TODOs, no placeholders

**buttons.html**: Overview token chips, variant grid table (5 cols × default/disabled), detailed sections per variant, FAB all sizes/colors/extended, icon buttons all variants, tooltip examples, badge examples, common patterns (dialog, form, destructive, toolbar).

**cards.html**: Overview, elevated cards (3 examples with realistic content), filled cards (3 examples), outlined cards (3 examples), anatomy breakdown, interaction states (interactive vs static).

**forms.html**: Filled fields all states (default/value/helper/icon/error/disabled), outlined fields all states, textarea, select dropdown, checkboxes (all states, in-list, agreement), radios (all states, frequency group, styled tier selector), switches (all states, settings panel), sliders (4 examples with live label), complete form (account creation).

**navigation.html**: Top App Bar (small/center/medium variants), nav bars (3/4/5 destinations with badges), nav rails (with/without FAB), nav drawer (full example with sections), primary tabs (icon+label, text-only), secondary tabs, breadcrumb navigation.

**modals.html**: Dialogs (4 variants: icon-centered, left-aligned, selection list, warning icon), bottom sheet (full anatomy), snackbars (5 variants), menus (simple, with icons/shortcuts/disabled), badges (all sizes, on nav icons), progress indicators (linear det/indet, circular det/indet all sizes), tooltips (plain CSS, rich).

---

## Implementation Notes

### HTML Patterns

All interactive elements use `position: relative; overflow: hidden` for state layers.

The `::before` pseudo-element pattern:
```css
.component::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: <state-color>;
  opacity: 0;
  transition: opacity var(--motion-duration-short-4) var(--motion-easing-standard);
  pointer-events: none;
}
.component:hover::before  { opacity: var(--state-hover-opacity);   }
.component:focus::before  { opacity: var(--state-focus-opacity);   }
.component:active::before { opacity: var(--state-pressed-opacity); }
```

### SVGs

All icons are inline SVG. No icon fonts, no external icon libraries. Common viewBox: `0 0 24 24`. Fill: `currentColor`. Size: 18px for button icons, 24px for most others.

### Accessibility

- `aria-label` on all icon-only buttons
- `role="button"` or `tabindex="0"` on interactive non-button elements
- `aria-selected` on nav items and tabs
- `aria-valuenow/min/max` on progress indicators and sliders
- `role="dialog" aria-modal="true" aria-labelledby` on dialogs
- `role="menu" / role="menuitem"` on menus
- `role="tablist" / role="tab"` on tab bars
- `role="radiogroup"` on radio button groups
- `.sr-only` for screen-reader-only text

### Dark Mode

All component colors reference CSS custom properties. The dark mode block in `tokens.css` overrides the color tokens under `@media (prefers-color-scheme: dark)`. No additional class or JS is required.

### Responsive Breakpoints

- 1024px: 4-column grid → 2-column; hide desktop-only elements
- 768px: 3-column → 2-column; nav rail/drawer hidden; reduced display type sizes
- 480px: 2-column → 1-column; hide mobile-targeted elements; further type size reduction

---

## Quality Checklist

- [ ] No external CSS/JS dependencies (except Google Fonts @import)
- [ ] All 15 type scale classes present with correct values
- [ ] Dark mode overrides all color tokens
- [ ] `prefers-reduced-motion` collapses all animations to 0.01ms
- [ ] All 5 button variants + FAB sizes + 4 icon button variants
- [ ] All 4 chip types with selected/disabled states
- [ ] Both text field variants with all 5 states (default/focus/filled/error/disabled)
- [ ] Checkboxes, radios, switches with all states
- [ ] Navigation bar, rail, drawer, tabs all present
- [ ] All 3 card types with realistic content
- [ ] Progress: linear + circular, determinate + indeterminate
- [ ] Dialog: icon + no-icon variants
- [ ] Bottom sheet with drag handle
- [ ] Snackbar with text / action / close variants
- [ ] Menus with icons, dividers, disabled items
- [ ] Badges: dot, numbered, large
- [ ] Tooltips: plain CSS + rich
- [ ] Ripple JS works from click position
- [ ] `has-value` class synced to input state via JS
- [ ] Fixed nav-bar/rail/drawer reset to `position: static` in showcase contexts
- [ ] Semantic HTML5 throughout
- [ ] All files complete, no placeholders, no TODOs
