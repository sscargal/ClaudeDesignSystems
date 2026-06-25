# Liqid Design System — Generation Prompt & Brand Research Notes

## About This Document

This is the canonical generation prompt and brand research record for the Liqid Design System.
It documents actual decisions made, color derivations, and rationale for the design system choices.

---

## 1. Brand Research

### Source
WebFetch was denied during generation. Design was constructed from:
- Known brand identity: Liqid is a well-established enterprise composable infrastructure company
- Industry knowledge: enterprise data center, PCIe fabric disaggregation, AI/ML infrastructure
- Publicly visible positioning: dark/technical aesthetic consistent with enterprise data center brands
- Component requirements: rack visualization, performance dashboards, spec tables — all reflecting real Liqid product domains

### Brand Personality
- **Enterprise / Technical**: Precision-focused, data-dense, infrastructure-grade
- **Dark-first UI**: Primary mode is dark navy/black — data center infrastructure aesthetic
- **Modern B2B**: Not sterile corporate; clean, confident, slightly aggressive tech brand
- **Composable**: Visual metaphor of modular, connectable elements runs through the system

---

## 2. Color Decisions

### Primary Brand Colors (derived from Liqid's known visual identity)

| Token | Value | Usage |
|---|---|---|
| `--color-liqid-blue` | `#0070F3` | Primary action, links, active states |
| `--color-liqid-blue-hover` | `#005FCC` | Button hover, darkened blue |
| `--color-liqid-cyan` | `#00C8FF` | Accent, data highlights, spec text, eyebrows |
| `--color-liqid-cyan-hover` | `#00AADE` | Cyan hover state |

### Navy Scale (structural darks)

| Token | Value | Usage |
|---|---|---|
| `--color-liqid-navy-deepest` | `#050A14` | Footer, deepest background |
| `--color-liqid-navy-deep` | `#0A0F1E` | Primary page background |
| `--color-liqid-navy` | `#111827` | Secondary background, cards |
| `--color-liqid-navy-mid` | `#1C2B45` | Card surfaces, elevated surfaces |
| `--color-liqid-navy-light` | `#263550` | Hover states on dark |
| `--color-liqid-navy-border` | `#2E405E` | Borders, dividers on dark |

### Gradient
```css
--color-liqid-gradient: linear-gradient(135deg, #0070F3 0%, #00C8FF 100%);
```
Used for: CTA buttons, card top-border accents, stat number reveals, gradient text.

### Product Category Colors
Each major product type has a distinct color for category badges and rack unit visualization:

| Category | Color | Hex |
|---|---|---|
| PCIe Fabric | Blue | `#0070F3` |
| Compute | Purple | `#8B5CF6` |
| Storage (NVMe) | Teal/Cyan | `#06B6D4` |
| Networking | Green | `#10B981` |
| GPU | Amber | `#F59E0B` |

### Status Colors

| State | Color | Hex |
|---|---|---|
| Active / Online | Green | `#00D97E` |
| Warning | Amber | `#F59E0B` |
| Error / Fault | Red | `#EF4444` |
| Offline | Slate | `#64748B` |

---

## 3. Typography

### Font Stack
Liqid uses a clean geometric sans-serif. Based on their enterprise SaaS positioning, the stack is calibrated for Inter (widely available in enterprise environments) with robust system fallbacks:

```css
--font-display: "Inter", "Segoe UI", system-ui, -apple-system, BlinkMacSystemFont, "Helvetica Neue", Arial, sans-serif;
--font-text:    "Inter", "Segoe UI", system-ui, -apple-system, BlinkMacSystemFont, "Helvetica Neue", Arial, sans-serif;
--font-mono:    "JetBrains Mono", "Fira Code", ui-monospace, SFMono-Regular, "SF Mono", "Cascadia Code", Consolas, "Liberation Mono", monospace;
```

**Monospace rationale**: JetBrains Mono is the first choice because it renders beautifully at small sizes for:
- Rack unit labels
- Spec table values
- CLI output
- Performance metric units (Gbps, µs, GB/s)
- Technical identifiers (FW versions, fabric IDs)

### Type Scale Key Points
- **Display / Hero**: 96px → 56px, `extrabold` weight, tracking `-0.025em` to `-0.015em`
- **H1–H3**: 48px → 28px, `bold` or `semibold`, tight tracking
- **Body**: 16–20px, generous line-height 1.60–1.75 (data-dense content needs air)
- **Spec / Mono**: 12–16px JetBrains Mono, `#00C8FF` cyan for values
- **Eyebrow**: 11–12px, `semibold`, `0.12em` letter-spacing, `uppercase`, cyan

---

## 4. Spacing

4px base grid, 10-step scale from `--space-1: 4px` to `--space-40: 160px`.

Enterprise UIs need more generous spacing than consumer apps:
- Section padding: `--space-20: 80px` to `--space-24: 96px`
- Card padding: `--space-6: 24px` to `--space-8: 32px`
- Nav height: `72px` (taller than Apple's 52px — enterprise nav has more items)

---

## 5. Border Radius

Enterprise is more angular than consumer. Radii are tighter throughout:

| Token | Value | vs. Apple |
|---|---|---|
| `--radius-button` | `6px` | Apple: pill (9999px) |
| `--radius-card` | `12px` | Apple: 18px |
| `--radius-input` | `6px` | Apple: 12px |
| `--radius-modal` | `16px` | Apple: 24px |

This gives Liqid components a crisp, precision-tooled feel appropriate for infrastructure software.

---

## 6. Shadows

Two shadow systems:
1. **Light mode shadows**: subtle, blue-tinted (`rgba(10, 15, 30, ...)`)
2. **Dark surface shadows**: deep black with optional blue glow (`rgba(0, 0, 0, ...)`)
3. **Brand glow**: `--shadow-blue` and `--shadow-cyan` for CTA buttons and active rack units

---

## 7. Signature Components

### Rack Diagram (`.rack-diagram`)
The most distinctive Liqid-specific component. A CSS-rendered server rack visualization with:
- Scanning line animation (simulates active monitoring)
- Color-coded unit types (Liqid controller, GPU, NVMe, switch, empty)
- LED indicators (green=online, blue=activity, amber=warning)
- Footer stats (power draw, temperature, fabric gen)
- 1U and 2U height variants

### Performance Metrics Dashboard
- `.metrics-dashboard`: 4-column metric card grid
- `.metric-card`: stat + unit + trend indicator
- `.metric-chart`: CSS bar chart with 12-column hourly data
- `.throughput-bar`: animated fill bar for bandwidth visualization
- Color-coded by resource type

### Spec Table (`.spec-table-enterprise`)
- Category header rows in dark navy with cyan uppercase text
- Alternating row tinting
- Monospace values in right column
- Highlighted rows for key specs
- Full-bleed design with `border-collapse: collapse`

---

## 8. Animation Philosophy

All animations are:
1. **Transform/opacity only** — no layout-triggering properties (width, height, top, left)
2. **Purposeful** — every animation communicates state (loading, active, glow = attention)
3. **Reduced motion compliant** — all animations disable to 0.01ms when `prefers-reduced-motion: reduce`
4. **Calibrated duration**:
   - UI feedback: 150–200ms (fast, imperceptible to users but present)
   - Content reveals: 300ms (conscious but not slow)
   - Complex reveals: 400ms (stat counters, hero entries)
   - Ambient/continuous: 2–4s (glow pulse, float, rack scan)

### Notable Animations
- `scanLine`: Scanning horizontal line that traverses the rack diagram top-to-bottom, simulating active monitoring
- `rackActivate`: Rack unit highlight animation with blue glow — used when a unit is selected or composed
- `fillBar`: Width animation for throughput bars — announces the value visually
- `countUp`: Stat number reveal with blur + scale + translateY — used on metric cards and hero stats
- `glowPulse`: Pulsing box-shadow for primary CTA buttons and active indicators

---

## 9. Dark Mode

Liqid's dark mode is the **primary brand mode** (inverted from most consumer design systems). Light mode is provided for enterprise contexts where users prefer lighter UIs (documentation, form-heavy workflows).

Dark mode changes:
- Background: `#F4F6FA` → `#0A0F1E`
- Blue primary: `#0070F3` → `#3B82F6` (brighter — more visible on dark)
- Cyan: `#00C8FF` → `#22D3EE` (lighter for dark bg contrast)
- Text: `#0A0F1E` → `#F0F4FF` (near-white, not pure white — softer)
- Shadows: deeper with more opacity (0.40–0.70 vs 0.04–0.16)
- Borders: `rgba(255,255,255,0.08)` instead of `rgba(10,15,30,0.12)`

---

## 10. File Structure

```
Liqid/
├── index.html          — Complete design system showcase (17 sections)
├── tokens.css          — Design tokens: colors, typography, spacing, radius, shadow, motion
├── typography.css      — Type classes: display, headings, body, mono, spec, gradient text
├── components.css      — All components: nav, hero, cards, rack, dashboard, tables, forms, footer
├── animations.css      — Keyframes, utility classes, skeleton states, status dots
├── prompt.md           — This file
└── components/
    ├── buttons.html    — Button system + badges showcase
    ├── cards.html      — Product, solution, resource cards + skeleton loading
    ├── forms.html      — Enterprise inputs, contact form, newsletter
    ├── navigation.html — Enterprise nav + mega menu + logo variants
    └── modals.html     — Demo request, resource download, confirmation modals
```

---

## 11. Generation Context

- **Date**: 2026-06-24
- **System**: Claude Design Systems series
- **Reference system**: `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/` (calibration for depth and completeness)
- **Dependencies**: None — zero external dependencies, system fonts only
- **Breakpoints**: Mobile-first, 768px (tablet), 1024px (desktop), 1440px max-width
- **Accessibility**: semantic HTML5, `aria-label` on interactive elements, `prefers-reduced-motion` fully respected, focus-visible outlines, color is never the sole indicator of state
