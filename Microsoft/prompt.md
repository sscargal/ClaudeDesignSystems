# Microsoft Fluent Design System — Generation Prompt

## Overview

Build a complete, production-quality design system called the "Microsoft Fluent Design System"
inside `/Users/sscargall/Documents/ClaudeDesignSystems/Microsoft/`.

This is part of a series of brand-faithful design systems. The reference implementation is at
`/Users/sscargall/Documents/ClaudeDesignSystems/Apple/` — read those files to understand expected
quality and depth before building.

---

## Microsoft Fluent 2 Brand Aesthetic

- **Personality:** Fluent Design 2 — Windows 11 and Microsoft 365. Acrylic/Mica translucency
  materials, depth layers, connected motion, calm information density. Approachable enterprise —
  Microsoft's post-Metro maturity.
- **Typography:** Segoe UI Variable (`"Segoe UI Variable", "Segoe UI", system-ui, sans-serif`).
  Weight range 300–700. Dense but readable hierarchy.
- **Colors:**
  - Microsoft Blue: `#0078D4`
  - Blue light: `#2899F5`
  - Blue dark: `#005A9E`
  - Communication blue: `#0063B1`
  - Background (light): `#FFFFFF`
  - Surface (light): `#F3F3F3`
  - Surface subtle: `#FAFAFA`
  - Background (dark): `#202020`
  - Surface (dark): `#2C2C2C`
  - Surface subtle (dark): `#383838`
  - Label primary (light): `#242424`
  - Label secondary (light): `#616161`
  - Label tertiary (light): `#A19F9D`
  - Border (light): `#E0E0E0`
  - Border (dark): `#3D3D3D`
  - Success: `#107C10`
  - Warning: `#797500`
  - Error: `#C42B1C`
  - Info: `#0078D4`
  - Acrylic tint (light): `rgba(243,243,243,0.85)` with backdrop-filter blur(30px) saturate(125%)
  - Mica tint (dark): `rgba(32,32,32,0.9)` with backdrop-filter blur(60px) saturate(150%)`
- **Both light and dark:** Yes — Windows respects system preference.
- **Motion:** Connected motion — 150ms/250ms/350ms. Easing: `cubic-bezier(0.1, 0.9, 0.2, 1)` for
  entrances. Reveal highlight effect on hover (mouse-tracking glow border).
- **Reference:** fluent2.microsoft.design, microsoft.com

---

## File Structure

```
Microsoft/
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

`:root` = light. `@media (prefers-color-scheme: dark)` = dark.

Tokens:
- Full color system including Acrylic and Mica material tokens
- Semantic: fill-primary, fill-secondary, fill-accent, fill-subtle, stroke-default, stroke-strong
- Typography: Segoe UI Variable stack, scale 40/32/28/24/20/18/16/14/13/12px
- Spacing: 4px grid — 2/4/6/8/10/12/16/20/24/32/40/48px
- Radius: 4px (default), 6px, 8px (cards), 12px (flyout), 9999px (pills)
- Shadows (called "Depth"): depth-4, depth-8, depth-16, depth-64
- Motion: 83/150/250/350ms durations, Fluent easing curves

---

## Requirements

- Zero external dependencies
- Both light and dark mode via `@media (prefers-color-scheme: dark)`
- Responsive, mobile-first, 768px and 1024px breakpoints
- Semantic HTML5, `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs
