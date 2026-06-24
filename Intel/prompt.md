# Intel Design System — Generation Prompt

This file documents the canonical prompt used to generate the Intel Design System.

---

## Prompt

Build a complete, production-quality design system called the "Intel Design System" inside `/Users/sscargall/Documents/ClaudeDesignSystems/Intel/`.

This is part of a series of brand-faithful design systems. Read `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/tokens.css` and `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/components.css` first to calibrate the expected depth and completeness.

### Intel Brand Aesthetic
- **Personality:** Precision engineering, enterprise trust, innovation leadership. Intel's design is clean, professional, and data-forward. Light-first with Intel's distinctive cobalt blue. The brand spans consumer (Core Ultra) and enterprise (Xeon, Gaudi). Post-2020 rebrand is bold and modern — "Intel Inside" meets AI era.
- **Typography:** Intel uses "Intel One" display font. Fallback: `"Intel One", "Clear Sans", "Inter", system-ui, sans-serif`. Mono: `"Fira Code", "JetBrains Mono", monospace`. Clean hierarchy, enterprise-readable.
- **Colors:**
  - Intel Blue: `#0071C5`
  - Blue dark: `#00438A`
  - Blue light: `#1E9BE8`
  - Blue pale: `#E8F4FB`
  - Background: `#FFFFFF`
  - Surface 1: `#F5F5F5`
  - Surface 2: `#EBEBEB`
  - Surface dark (hero): `#0B0B0F`
  - Surface dark 2: `#1A1A2E`
  - Label primary: `#1A1A1A`
  - Label secondary: `#555555`
  - Label tertiary: `#888888`
  - Border: `#D0D0D0`
  - Border dark: `#E0E0E0`
  - Intel Teal (secondary): `#00C7B1`
  - Intel Purple (accent): `#7B2FBE`
  - Error: `#C0392B`
  - Warning: `#E67E22`
  - Success: `#27AE60`
- **Light-first:** Yes — white/light-gray canvas for enterprise credibility.
- **Motion:** Precise, purposeful — 150ms/250ms/400ms. Easing: `cubic-bezier(0.4, 0, 0.2, 1)`. No decoration — every animation earns its place.
- **Reference:** intel.com

### File Structure

```
Intel/
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

### Design Tokens (tokens.css)
`:root` is light. `@media (prefers-color-scheme: dark)` override.

All tokens:
- Full color system above + semantic mappings
- Typography: Intel One/Inter stack + mono stack, scale 72/56/44/36/28/22/18/16/15/14/13/12px
- Spacing: 4px grid — 4/8/12/16/20/24/32/40/48/64/80/96px
- Radius: 0px (Intel uses sharp/minimal radius), 2px, 4px, 8px (cards), 9999px (pills)
- Shadows: `0 1px 4px rgba(0,0,0,0.08)`, `0 4px 16px rgba(0,0,0,0.12)`, `0 8px 32px rgba(0,0,0,0.16)`
- Motion: 100/150/250/400ms, Intel easing
- Z-index scale

### Typography (typography.css)
- `.display-hero`: 72px, weight 800, tracking -0.02em
- `.display-large`: 56px, weight 700, tracking -0.015em
- `.display`: 44px, weight 700
- `.heading-1`: 36px, weight 700
- `.heading-2`: 28px, weight 600
- `.heading-3`: 22px, weight 600
- `.subhead`: 18px, weight 500
- `.body-lg`: 18px, weight 400, line-height 1.65, max-width 68ch
- `.body`: 16px, weight 400, line-height 1.6
- `.body-sm`: 15px
- `.caption`: 13px, label-secondary
- `.label`: 12px, weight 700, uppercase, tracking 0.08em
- `.mono`: monospace, 14px
- `.spec-value`: large, weight 700, Intel Blue
- `.eyebrow`: 13px, weight 600, uppercase, Intel Blue, tracking 0.12em
- Gradient text: `.text-blue-gradient`, `.text-ai-gradient`

### Animations (animations.css)
- `@keyframes fadeIn`, `slideInUp`, `slideInLeft`, `scaleIn`
- `@keyframes blueGlow`: Intel Blue box-shadow pulse
- `@keyframes shimmer`: skeleton loading
- `@keyframes progressFill` / `benchmarkFill`: benchmark bar fills
- `@keyframes spin`: loading spinner
- `@keyframes countUp`: stat number reveal
- Utility classes, stagger helpers, delays, `prefers-reduced-motion`

### Components (components.css)

**Buttons:** `.btn-primary`, `.btn-secondary`, `.btn-outline`, `.btn-ghost`, `.btn-cta`, `.btn-dark`, `.btn-dark-outline`, `.btn-teal`. Sizes: sm/md/lg. 0px radius, 44px default height.

**Product Cards:** `.card-product` with badge, generation eyebrow, image placeholder, 2-col spec grid, benchmark score, CTA. Blue left-border on hover.

**Comparison Card:** `.card-comparison` two-column Intel vs competitor.

**Feature Card:** `.card-feature` dark gradient (blue-teal, AI purple, dark).

**Stat Card:** `.card-stat` Intel Blue large number.

**Navigation:** `.nav-utility` (dark blue top bar) + `.nav-global` + `.nav-mega-menu` 4-column product family grid.

**Performance Bars:** `.perf-bar-intel` (blue) vs `.perf-bar-competitor` (gray), `.benchmark-chart`.

**Spec Table:** `.spec-table-intel` with blue header, `.spec-category` rows, alternating tints.

**Forms:** `.input` (sharp, 44px, blue focus), `.input-search`, `.select`, `.checkbox` (2px radius, blue fill), `.radio`, `.toggle` (blue on).

**Alerts:** `.alert-info`, `.alert-success`, `.alert-warning`, `.alert-error` — blue left-border pattern.

**Modals:** `.modal-overlay` + `.modal` (0px radius, 3px blue top border, shadow-xl, max-w 560px).

**Badges:** `.badge-blue`, `.badge-new` (teal), `.badge-ai` (purple), `.badge-pro` (dark), `.badge-xeon`, `.badge-gray`.

**Intel Inside:** `.intel-inside` — circular blue badge, inner ring, "intel® inside" text.

**Brand Logo:** `.brand-logo` component with size variants.

### Main index.html Sections
1. Utility nav (dark blue bar)
2. Main nav with open mega-menu demo
3. Hero (dark, grid pattern, display-hero headline, two CTAs)
4. Trusted by banner
5. Color palette swatches
6. Typography scale (all classes)
7. Buttons (light + dark context)
8. CPU Product Cards (4-col: Core Ultra 9 285K, Core Ultra 7 265K, Xeon w9-3595X, Gaudi 3)
9. Benchmark bars (6 comparisons, illustrative data)
10. Full spec table (Core Ultra 9 285K)
11. Feature Cards (AI row)
12. Stat Cards
13. Comparison Card
14. Forms (all input types)
15. Alerts (all 4 variants)
16. Badges and tags
17. Intel Inside badge component
18. Modal (inline preview)
19. Motion/animation demos
20. Brand logo component
21. Component page links
22. Dark footer

### Component Showcase Pages
Each `components/*.html`: self-contained, links to all 4 CSS files, all variants with labels, breadcrumb navigation.

### Requirements
- Zero external dependencies (except Google Fonts for Inter fallback)
- Light-first, dark via `@media (prefers-color-scheme: dark)`
- Responsive: mobile-first, 768px and 1024px breakpoints
- Semantic HTML5, `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs

---

## Generated

Date: 2026-06-24
Model: Claude Sonnet 4.6
Design System Series: ClaudeDesignSystems
Brand Reference: intel.com (post-2020 rebrand)
