# Stripe Design System — Generation Prompt

This file is the canonical prompt for reproducing or extending the Stripe Design System.

## System Identity

Build a complete, production-quality design system called the "Stripe Design System" inside `/path/to/Stripe/`.

This is part of a series of brand-faithful design systems. The reference implementation is at `/path/to/Apple/` — read those files to understand expected quality and depth before building.

## Stripe Brand Aesthetic

- **Personality:** B2B gold standard — financial precision, polished prose, developer-trusted. Stripe's design is warm, approachable, yet serious. It communicates credibility through typography and whitespace, not decoration.
- **Typography:** Sohne (fallback: `"Sohne", "Inter", -apple-system, BlinkMacSystemFont, sans-serif`). Mono: `"Sohne Mono", "JetBrains Mono", "Fira Code", monospace`. Well-spaced body, precise line-length control (65ch max for body).
- **Colors:**
  - Stripe Blurple: `#635BFF`
  - Blurple dark: `#4B44CC`
  - Blurple light: `#8A84FF`
  - Background: `#FFFFFF`
  - Surface 1: `#F6F9FC`
  - Surface 2: `#EBEDF0`
  - Label primary: `#0A2540`
  - Label secondary: `#425466`
  - Label tertiary: `#8898A9`
  - Border: `#E0E7EC`
  - Success green: `#09825D`
  - Warning amber: `#B45309`
  - Error red: `#C0123C`
  - Gradient: `#635BFF` → `#9F7AFF` → `#C4B5FD` (hero gradient)
- **Light-first:** Yes. Light canvas with optional dark code blocks/terminal sections.
- **Motion:** Smooth, confident — 150ms/200ms/300ms/400ms. Easing: `cubic-bezier(0.25, 0.46, 0.45, 0.94)`.
- **Reference:** stripe.com, stripe.com/docs

## File Structure

```
Stripe/
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

## Design Tokens (tokens.css)

`:root` is light. `@media (prefers-color-scheme: dark)` override for dark mode.

Tokens:
- All colors + semantic (background, surface, label, border, accent, success, warning, error)
- Typography: Sohne stack + mono stack, scale 52/40/32/24/20/18/16/15/14/13/12px
- Spacing: 4px grid — 4/8/12/16/20/24/32/40/48/64/80/96px
- Radius: 4px (inputs), 6px (buttons), 8px (cards), 12px (modals), 20px (hero sections)
- Shadows: `0 2px 6px rgba(10,37,64,0.08)`, `0 4px 16px rgba(10,37,64,0.12)`, `0 8px 32px rgba(10,37,64,0.16)`
- Motion: 150/200/300/400ms, standard easing

## Typography (typography.css)

- `.display`: 52px, weight 700, tracking -0.02em, label-primary color
- `.heading-1`: 40px, weight 700, tracking -0.01em
- `.heading-2`: 32px, weight 700
- `.heading-3`: 24px, weight 600
- `.heading-4`: 20px, weight 600
- `.body-lg`: 18px, weight 400, line-height 1.7, max-width 65ch
- `.body`: 16px, weight 400, line-height 1.6
- `.body-sm`: 15px, weight 400
- `.caption`: 13px, label-secondary
- `.label`: 12px, weight 600, uppercase, tracking 0.08em — section labels
- `.mono`: monospace, 14px — code, API keys, amounts
- `.amount`: mono, weight 600, 24px — for financial display
- `.amount-lg`: mono, weight 600, 40px
- Gradient text utility: `.text-gradient` using blurple gradient

## Animations (animations.css)

- `@keyframes fadeIn`, `fadeInUp`, `fadeInDown`, `fadeInLeft`, `fadeInRight`
- `@keyframes slideInUp`, `slideInDown`, `slideOutDown`
- `@keyframes scaleIn`, `scaleOut`
- `@keyframes shimmer` — skeleton loading
- `@keyframes gradientShift` — subtle gradient animation for hero mesh
- `@keyframes meshFloat`, `meshFloat2` — floating orb animation
- `@keyframes countUp` — number ticker reveal
- `@keyframes blurpleGlow` — blurple pulse for CTAs
- `@keyframes statusPulse` — live indicator dot
- Utility classes, `prefers-reduced-motion` support

## Components (components.css)

### Buttons
- `.btn-primary`: blurple `#635BFF` fill, white text, 6px radius, 40px height, weight 600 — hover: blurple-dark, subtle shadow lift
- `.btn-secondary`: white fill, border, label-primary text — hover: surface-1
- `.btn-ghost`: transparent, blurple text — hover: blurple at 8% opacity background
- `.btn-danger`: error red fill
- `.btn-link`: text-only, blurple, underline on hover
- `.btn-dark`: for dark backgrounds — frosted glass
- Size variants: `.btn-sm` (32px), `.btn-md` (40px), `.btn-lg` (48px)

### Cards
- `.card`: white background, border, 8px radius, shadow-sm, padding 24px
- `.card-feature`: gradient mesh background (blurple→purple gradient with noise texture via CSS), rounded 20px, white text
- `.card-pricing`: white, prominent price display, feature list with checkmarks, CTA at bottom
- `.card-product`: icon + title + description — the feature explanation card pattern from stripe.com
- `.card-stat`: large number (amount style) + label + trend indicator (up/down arrow + percentage)
- `.card-testimonial`: quote mark, body text, avatar + name + title

### Code Block — Stripe's signature developer component
- `.code-block`: dark background `#0A2540`, border-radius 12px, padding 24px
- `.code-block-tabs`: multi-language selector (Node/Python/Ruby/PHP tabs)
- `.code-block-header`: filename/language label + copy button
- `.code-block-body`: monospace, syntax-colored
- Syntax tokens: `.token-keyword` (blurple), `.token-string` (green), `.token-comment` (gray), `.token-number` (orange), `.token-function` (cyan), `.token-property` (light blue)
- `.terminal`: dark block, green prompt text, monospace

### Data Table
- `.data-table`: full width, clean, no heavy borders — just row separators
- `.data-table-header`: label style, border-bottom
- `.data-table-row`: 52px height, hover: surface-1 background
- `.status-pill`: inline pill — Succeeded (green), Pending (amber), Failed (red), Refunded (gray)
- `.amount-cell`: mono, right-aligned, label-primary
- `.id-cell`: mono, label-tertiary, truncated

### Dashboard/Metrics
- `.metric-card`: stat value + label + sparkline area
- `.sparkline`: CSS flex bar chart at the bottom of metric cards
- `.chart-placeholder`: CSS-drawn bar chart demo (pure CSS bars at different heights)
- `.chart-label`: x-axis label row
- `.activity-feed`: timeline list with dots + event descriptions

### Navigation
- `.nav-global`: white, logo left, links center, CTA right — links: label-secondary, hover: label-primary
- `.nav-global.is-scrolled`: blur backdrop and border+shadow on scroll
- `.nav-docs`: sidebar nav for documentation — section headers + nested links
- `.breadcrumb`: slash-separated, label-tertiary
- `.tabs`: underline style, blurple active indicator

### Forms
- `.input`: white background, 1px border, 4px radius, 40px height, 16px — focus: blurple border + blurple glow
- `.input-group`: label + input + help text + error message stack
- `.input.is-error`: red border + red error text
- `.input.is-success`: green border
- `.select`: custom dropdown with chevron SVG
- `.checkbox`: 16px square, 4px radius — checked: blurple
- `.radio`: circle — selected: blurple center dot
- `.toggle`: pill, blurple when on
- `.field-card`: payment card field style (card number, expiry, CVC in a bordered container)

### Modals & Overlays
- `.modal-overlay`: rgba(10,37,64,0.5) backdrop + blur(4px)
- `.modal`: white, 12px radius, shadow-xl, max-width 480px, slide-in up
- `.alert-banner`: full-width, info/success/warning/error variants with left-side colored border

### Badges
- `.badge`: pill, 20px height, 12px font, surface-2 background
- `.badge--success`, `.badge--warning`, `.badge--error`, `.badge--blurple`, `.badge--new`: semantic variants

## Main index.html

Stripe-faithful showcase:

1. **Nav**: white, logo + links + "Start now" CTA button, scroll-aware with backdrop blur
2. **Hero**: large display headline with gradient text, body text, two CTAs, background gradient mesh (CSS radial gradients, blurple→purple→lavender), floating orb animations
3. **Trusted by logos**: row of placeholder brand names in label style
4. **Color Palette**: all token swatches with names and hex values
5. **Typography Scale**: all classes rendered with metadata
6. **Buttons**: all variants and sizes with dark-context strip
7. **Code Block demo**: a realistic Stripe API code snippet with language tabs and terminal block
8. **Data Table**: 6 rows of realistic transaction data with status pills
9. **Dashboard Metrics**: 3 metric cards + CSS bar chart + activity feed
10. **Cards**: feature, product (3), pricing (3), stat (4), testimonial (3) cards
11. **Forms**: payment form demo (card number + expiry + CVC field group + submit) + all controls
12. **Navigation patterns**: global nav, docs sidebar, breadcrumbs, tabs
13. **Modals**: alert dialog + 4 alert banner variants
14. **Badges**: all variants
15. **Animations**: skeleton loading + motion token table
16. **Footer**: multi-column, dark `#0A2540` background

## Component showcase pages

Each `components/*.html`: self-contained, links to 4 CSS files from `../`, shows all variants with metadata.

## Requirements

- Zero external dependencies
- Light-first, dark mode via `@media (prefers-color-scheme: dark)`
- Responsive, mobile-first, 768px and 1024px breakpoints
- Semantic HTML5, ARIA attributes where needed
- `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs
- Write all files to disk

## Calibration

Before building, read the reference Apple design system tokens.css to understand expected depth, token naming convention, comment structure, and documentation quality.
