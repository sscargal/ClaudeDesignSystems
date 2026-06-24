# Vercel Design System — Generation Prompt

## Purpose

This document is the canonical generation prompt for the Vercel Design System.
Re-run it to regenerate or update any part of the system.

---

## Brand Identity

**Vercel** is a platform for frontend developers.
The brand communicates speed, reliability, and engineering excellence.

**Personality:** Minimal, dark-first, developer-focused. Extreme whitespace precision.
No decoration — everything earns its place. The brand is built on contrast:
pure black + pure white, with very selective use of accent color.

**Reference:** vercel.com

---

## Design Principles

1. **Dark-first**: Black (`#000000`) is the canvas. Light mode is an override via `@media (prefers-color-scheme: light)`.
2. **No decoration**: No gradients for decoration, no shadows for style. Every visual element communicates something.
3. **Precision spacing**: 4px grid. Every space token is a multiple of 4.
4. **Speed**: Transitions are 100/150/200ms. Nothing lingers.
5. **Mono for technical content**: Paths, hashes, env var keys, commands — always `Geist Mono`.
6. **White border = active**: Focus state is a 1px + 1px ring white border — maximum contrast.

---

## Typography

- **Sans:** `"Geist", "Inter", -apple-system, BlinkMacSystemFont, sans-serif`
- **Mono:** `"Geist Mono", "JetBrains Mono", "Fira Code", monospace`

| Class       | Size | Weight | Tracking | Use                    |
|-------------|------|--------|----------|------------------------|
| `.heading-1`| 48px | 700    | -0.03em  | Hero, landing page     |
| `.heading-2`| 36px | 700    | -0.02em  | Section titles         |
| `.heading-3`| 28px | 700    | -0.01em  | Subsections            |
| `.heading-4`| 24px | 600    | -0.01em  | Card titles            |
| `.heading-5`| 20px | 600    | 0        | Component headers      |
| `.body-lg`  | 18px | 400    | 0        | Long-form reading      |
| `.body`     | 16px | 400    | 0        | Primary body text      |
| `.body-sm`  | 14px | 400    | 0        | Secondary body         |
| `.caption`  | 13px | 400    | 0        | Meta, timestamps       |
| `.label`    | 11px | 600    | 0.10em   | Section markers, CAPS  |
| `.mono`     | 13px | 400    | 0        | Code, paths, hashes    |

---

## Color System

### Dark Mode (`:root` default)

| Token                    | Value     | Purpose                    |
|--------------------------|-----------|----------------------------|
| `--color-bg`             | `#000000` | Page background            |
| `--color-surface-1`      | `#111111` | Cards, sidebars            |
| `--color-surface-2`      | `#1A1A1A` | Inputs, secondary surfaces |
| `--color-surface-3`      | `#222222` | Hover states, borders      |
| `--color-border-subtle`  | `#222222` | Hairline separators        |
| `--color-border-default` | `#333333` | Default borders            |
| `--color-border-strong`  | `#444444` | Hover/active borders       |
| `--color-label-primary`  | `#FFFFFF` | Primary text               |
| `--color-label-secondary`| `#888888` | Secondary text, nav links  |
| `--color-label-tertiary` | `#555555` | Placeholders, meta         |
| `--color-accent-teal`    | `#50E3C2` | Brand accent               |
| `--color-accent-blue`    | `#0070F3` | Links, info                |
| `--color-error`          | `#FF4444` | Errors, danger             |
| `--color-warning`        | `#F5A623` | Warnings, building state   |
| `--color-success`        | `#0DBA58` | Ready, success             |

### Light Mode (`@media (prefers-color-scheme: light)`)

| Token                    | Value     |
|--------------------------|-----------|
| `--color-bg`             | `#FFFFFF` |
| `--color-surface-1`      | `#FAFAFA` |
| `--color-surface-2`      | `#F5F5F5` |
| `--color-border-default` | `#EAEAEA` |
| `--color-label-primary`  | `#000000` |
| `--color-label-secondary`| `#666666` |

---

## Spacing (4px Grid)

| Token        | Value |
|--------------|-------|
| `--space-1`  | 4px   |
| `--space-2`  | 8px   |
| `--space-3`  | 12px  |
| `--space-4`  | 16px  |
| `--space-5`  | 20px  |
| `--space-6`  | 24px  |
| `--space-8`  | 32px  |
| `--space-10` | 40px  |
| `--space-12` | 48px  |
| `--space-16` | 64px  |
| `--space-20` | 80px  |
| `--space-24` | 96px  |

---

## Border Radius

| Token           | Value   | Use                   |
|-----------------|---------|-----------------------|
| `--radius-xs`   | 4px     | Inline code, tiny     |
| `--radius-sm`   | 6px     | Buttons, inputs       |
| `--radius-md`   | 8px     | Cards                 |
| `--radius-lg`   | 12px    | Modals                |
| `--radius-pill` | 9999px  | Badges, pills         |

---

## Shadows

```css
--shadow-border: 0 0 0 1px rgba(255, 255, 255, 0.06);
--shadow-sm:     0 4px 12px rgba(0, 0, 0, 0.50);
--shadow-md:     0 8px 24px rgba(0, 0, 0, 0.60);
--shadow-lg:     0 8px 40px rgba(0, 0, 0, 0.70);
--shadow-xl:     0 16px 64px rgba(0, 0, 0, 0.80);
```

---

## Motion

```css
--duration-instant:  100ms;   /* buttons, hovers */
--duration-fast:     150ms;   /* dropdowns, tooltips */
--duration-normal:   200ms;   /* modals, menus */
--duration-moderate: 300ms;   /* page transitions */

--ease-vercel: cubic-bezier(0.4, 0, 0.2, 1);
```

**Rules:**
- No bounce/spring easing — Vercel is precise, not playful
- Active states: `scale(0.98)` — physical press feel
- Hover: immediate, no delay
- Respect `prefers-reduced-motion: reduce`

---

## Key Animations

| Name          | Duration | Use                              |
|---------------|----------|----------------------------------|
| `fadeIn`      | 200ms    | Page elements, overlays          |
| `slideInDown` | 150ms    | Dropdown menus                   |
| `fadeSlideUp` | 200ms    | Modals, tooltips                 |
| `shimmer`     | 1600ms   | Skeleton loading                 |
| `pulse`       | 2000ms   | Live status dots                 |
| `spin`        | 750ms    | Loading spinners                 |
| `gridFade`    | 1000ms   | Hero background grid appearance  |
| `blink`       | 1000ms   | Terminal cursor                  |

---

## Components

### Buttons
`.btn` + variant class. Heights: 28/36/44px. Radius: 6px. Font: 14px/600.

| Class          | Background  | Text    | Use                    |
|----------------|-------------|---------|------------------------|
| `.btn-primary` | `#FFFFFF`   | `#000`  | Primary CTA on dark    |
| `.btn-secondary`| surface-2  | white   | Secondary actions      |
| `.btn-ghost`   | transparent | white   | Tertiary actions       |
| `.btn-danger`  | `#FF4444`   | white   | Destructive only       |

### Deployment Row (Signature Component)
`.deployment-row` — 52px height, border-bottom separator.
- Status dot: 8px circle, colored by state
- Branch: mono, secondary
- Commit: 7-char hash, mono, tertiary
- Domain: primary, truncated
- Time: caption, tertiary, right-aligned
- Actions: icon buttons, reveal on hover

### Project Card
`.project-card` — surface-1, border, 8px radius, 20px padding.
Preview area (16:9), project name, mono domain link, meta row with status badge.

### Terminal / CLI Output
`.terminal` — pure black, border, 8px radius.
Prompt `▲ ~` in secondary. Commands in white. Output in secondary. Blinking cursor.

### Forms
`.input` — surface-2 bg, 1px border, 6px radius, 36px height.
Focus: white border + 1px white shadow ring.
`.input-mono` — monospace variant for technical values.

### Environment Variable Row
`.env-row` — key (mono, primary) + value (mono, redacted or revealed) + env badges + actions.

### Badges
`.badge` — 20px height, pill radius, 11px text.
Variants: `--success`, `--error`, `--warning`, `--info`.
Status: `.status-badge` with deployment state (ready/building/error/queued/cancelled).
Region: `.region-badge` — mono, gray.

### Modals
`.modal` — surface-2, border, 12px radius, shadow-xl, 480px max-width.
Backdrop: rgba(0,0,0,0.8) + blur(4px).
`.dialog-danger` — red-accented destructive confirmation.

---

## File Structure

```
Vercel/
├── index.html           — Complete showcase page
├── tokens.css           — All design tokens
├── typography.css       — Type scale + utilities
├── components.css       — All component styles
├── animations.css       — Keyframes + utility classes
├── prompt.md            — This file
└── components/
    ├── buttons.html     — Button component showcase
    ├── cards.html       — Card component showcase
    ├── forms.html       — Form component showcase
    ├── navigation.html  — Navigation showcase
    └── modals.html      — Modal & overlay showcase
```

---

## Regeneration Instructions

To regenerate this design system:

1. Read this prompt.md for specifications
2. Reference vercel.com for visual accuracy
3. Maintain dark-first (`:root` = dark, light override via media query)
4. Keep zero external dependencies — pure CSS + HTML
5. All files must be complete — no placeholders or TODOs
6. Respect `prefers-reduced-motion` in all animations
7. Use semantic HTML5 with proper ARIA attributes
8. Mobile-first, responsive at 768px and 1024px breakpoints

---

*Vercel Design System v1.0.0 — Built on Vercel's design language*
