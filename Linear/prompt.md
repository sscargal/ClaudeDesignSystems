# Linear Design System — Generation Prompt

Build a complete, production-quality design system called the "Linear Design System" inside `/path/to/Linear/`.

This is a dark-first, keyboard-centric design system that faithfully reproduces Linear's engineering aesthetic. Read the reference implementation at `/path/to/Apple/` to understand the expected depth and quality before building.

---

## Linear Brand Aesthetic

- **Personality:** Developer cult favorite — ultra-minimal, dark-first, keyboard-centric, precise, calm engineering confidence. Linear is what productivity software looks like when designers care deeply about craft.
- **Typography:** Inter (system fallback: `"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`). Tight tracking on headings. Monospace (`"JetBrains Mono", "Fira Code", "SF Mono", "Consolas", monospace`) for metadata, IDs, shortcuts.
- **Dark-first:** Yes — `:root` is dark. Light mode is secondary, via `@media (prefers-color-scheme: light)`.
- **Motion:** Subtle, purposeful — 150ms/200ms/300ms. Easing: `cubic-bezier(0.16, 1, 0.3, 1)` (spring-like). Never decorative. Only functional feedback. Issue row hover: instant (no transition).
- **Reference:** linear.app

---

## Color System

### Backgrounds & Surfaces (dark default)
| Token | Value |
|---|---|
| `--color-bg` | `#0F0F11` |
| `--color-surface-1` | `#1A1A1F` |
| `--color-surface-2` | `#232329` |
| `--color-surface-3` | `#2E2E36` |
| `--color-surface-4` | `#363640` |

### Borders
| Token | Value |
|---|---|
| `--color-border-subtle` | `#2E2E36` |
| `--color-border-default` | `#3E3E4A` |
| `--color-border-strong` | `#52525E` |
| `--color-border-focus` | `#5E6AD2` |

### Labels / Text
| Token | Value |
|---|---|
| `--color-label-primary` | `#FFFFFF` |
| `--color-label-secondary` | `#8A8A9A` |
| `--color-label-tertiary` | `#55555F` |
| `--color-label-quaternary` | `#3A3A44` |

### Brand Colors
| Token | Value | Usage |
|---|---|---|
| `--color-purple` | `#5E6AD2` | Primary accent |
| `--color-purple-light` | `#7B86E8` | Hover, active text |
| `--color-purple-muted` | `rgba(94,106,210,0.18)` | Command palette hover, focus rings |
| `--color-purple-subtle` | `rgba(94,106,210,0.08)` | Subtle highlight |
| `--color-green` | `#26C486` | Done status |
| `--color-orange` | `#F0A030` | In Progress status |
| `--color-red` | `#E85555` | Cancelled / destructive |
| `--color-yellow` | `#E8B430` | Backlog status |

---

## File Structure

```
Linear/
├── index.html          — Full showcase page
├── tokens.css          — All CSS custom properties
├── typography.css      — Type scale, base reset, utilities
├── components.css      — All component styles
├── animations.css      — Keyframes, utility classes, reduced-motion
├── prompt.md           — This file
└── components/
    ├── buttons.html    — All button variants and states
    ├── cards.html      — Project, cycle, roadmap cards
    ├── forms.html      — Inputs, selects, checkboxes, radio, full form
    ├── navigation.html — Topbar, sidebar, tabs, command palette, popover
    └── modals.html     — Standard, confirm, wide modals; toasts (live demo)
```

---

## tokens.css

CSS custom properties in `:root` (dark). Light mode via `@media (prefers-color-scheme: light)` override.

### Spacing — 4px base grid
`--space-1: 2px` through `--space-14: 96px`

Key values: 2/4/6/8/12/16/20/24/32/40/48/64px

### Typography scale
`--text-32`, `--text-24`, `--text-20`, `--text-16`, `--text-14`, `--text-13`, `--text-12`, `--text-11`

Weights: `--weight-regular: 400`, `--weight-medium: 500`, `--weight-semibold: 600`

### Border radius
`--radius-sm: 4px`, `--radius-md: 6px`, `--radius-lg: 8px`, `--radius-xl: 12px`, `--radius-pill: 9999px`

Semantic: `--radius-btn: 6px`, `--radius-input: 8px`, `--radius-card: 8px`, `--radius-modal: 12px`

### Shadows — dark-calibrated
```css
--shadow-sm:  0 1px 3px rgba(0,0,0,0.40), 0 1px 2px rgba(0,0,0,0.25);
--shadow-md:  0 4px 12px rgba(0,0,0,0.50), 0 2px 4px rgba(0,0,0,0.30);
--shadow-lg:  0 8px 24px rgba(0,0,0,0.55), 0 4px 8px rgba(0,0,0,0.35);
--shadow-xl:  0 16px 40px rgba(0,0,0,0.60), 0 8px 16px rgba(0,0,0,0.40);
--shadow-2xl: 0 24px 64px rgba(0,0,0,0.65), 0 12px 24px rgba(0,0,0,0.45);
```

### Motion
```css
--duration-fast:     100ms;   /* borders, color, opacity */
--duration-normal:   150ms;   /* buttons, hover states */
--duration-moderate: 200ms;   /* popovers, fade-in */
--duration-slow:     300ms;   /* modals, slide-in */
--ease-spring:       cubic-bezier(0.16, 1, 0.3, 1);
--ease-standard:     cubic-bezier(0.4, 0, 0.2, 1);
```

### Z-index scale
100 (dropdown) / 200 (sticky) / 300 (overlay) / 400 (modal) / 500 (toast) / 600 (tooltip)

### Component dimensions
```css
--btn-height-sm:    28px;
--btn-height-md:    32px;     /* default */
--btn-height-lg:    36px;
--input-height:     32px;
--row-height:       36px;     /* issue rows */
--row-height-sm:    30px;     /* sidebar items */
--sidebar-width:    240px;
--topbar-height:    48px;
--command-width:    560px;
```

---

## typography.css

### Base reset
- `box-sizing: border-box` + antialiasing on all elements
- `html` base font-size 14px, Inter font stack
- `body` uses `var(--color-bg)` background and `var(--color-label-primary)` text

### Type classes
| Class | Size | Weight | Notes |
|---|---|---|---|
| `.heading-xl` | 32px | 600 | tracking: -0.02em |
| `.heading-lg` | 24px | 600 | tracking: -0.01em |
| `.heading-md` | 20px | 600 | |
| `.heading-sm` | 16px | 600 | |
| `.body-lg` | 16px | 400 | line-height: 1.6 |
| `.body-md` | 14px | 400 | line-height: 1.5 — primary reading size |
| `.body-sm` | 13px | 400 | line-height: 1.5 |
| `.caption` | 12px | 400 | label-secondary color |
| `.label` | 11px | 500 | UPPERCASE, tracking: 0.06em, label-tertiary |
| `.mono` | 13px | 400 | JetBrains Mono, tabular-nums |
| `.code-inline` | 12px | 400 | surface-2 bg + border + padding 1px 5px |

---

## animations.css

### Required keyframes
| Name | Description |
|---|---|
| `fadeIn` | opacity 0→1 |
| `fadeInUp` | opacity 0→1 + translateY(8px→0) |
| `slideInRight` | opacity 0→1 + translateX(8px→0) — command palette items |
| `scaleInCenter` | scale(0.96→1) + opacity 0→1 — modal/popover appear |
| `commandPaletteIn` | translateY(-8px→0) + scale(0.97→1) + opacity |
| `shimmer` | background-position for skeleton loading |
| `progressIndeterminate` | translateX + scaleX for loading bars |
| `spin` | 360deg rotation for spinners |
| `pulse` | opacity 1→0.45→1 for live indicators |
| `toastIn` | translateY(-8px→0) + scale(0.97→1) |

### Utility classes
`.animate-fade-in`, `.animate-slide-right`, `.animate-scale-in`, `.animate-cmd-in`, `.animate-toast-in`, `.animate-spin`, `.animate-pulse`

### Delay utilities
`.delay-50` through `.delay-600`

### Reduced motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## components.css

### Buttons

**Base `.btn`:** `display: inline-flex`, `height: 32px`, `padding: 0 12px`, Inter Medium 14px, `border-radius: 6px`, `outline: none`, no `transform` on hover (Linear does not scale buttons).

| Class | Background | Text | Border |
|---|---|---|---|
| `.btn-primary` | `#5E6AD2` | white | transparent |
| `.btn-secondary` | `surface-2` | label-primary | border-default |
| `.btn-ghost` | transparent | label-secondary | transparent |
| `.btn-danger` | `#E85555` | white | transparent |
| `.btn-icon` | transparent | label-secondary | transparent | 28px square |

**States:** `:disabled` → `opacity: 0.35`. `.loading` → `color: transparent`, spinner via `::after`.

**`.btn-kbd`:** `font-family: mono`, `font-size: 11px`, `background: surface-2`, `border: border-subtle`, `border-radius: 4px`, `pointer-events: none` — display only.

### Issue Row — Linear's most iconic component

```html
<a class="issue-row" role="listitem">
  <div class="issue-priority">   <!-- priority icon slot -->
    <div class="priority-icon priority-urgent">
      <span></span><span></span><span></span><span></span>
    </div>
  </div>
  <div class="issue-status">     <!-- status icon slot -->
    <div class="status-icon status-in-progress"></div>
  </div>
  <span class="issue-id">ENG-2847</span>   <!-- mono, tertiary -->
  <span class="issue-title">Title text</span>
  <div class="issue-meta">
    <!-- label chips, due date, assignee avatar, cycle indicator -->
  </div>
</a>
```

**`.issue-row`:** `height: 36px`, `border-bottom: border-subtle`, `transition: none` (hover is instant).
**`.issue-row:hover`:** `background: surface-2` — no transition.

**Priority icons:** CSS-drawn 4-bar charts using `<span>` elements:
- Urgent: all 4 bars, red
- High: 3 bars active, orange
- Medium: 2 bars active, yellow
- Low: 1 bar, dim

**Status icons:** CSS-drawn circles via pseudo-elements:
- Backlog: `border: 2px dashed label-tertiary`
- Todo: `border: 2px solid border-default`
- In Progress: `border: 2px solid orange`, half-filled via `::before`
- Done: `background: green`, checkmark via `::after`
- Cancelled: `background: surface-3`, X via `::before` + `::after`

### Command Palette

```html
<div class="command-overlay">          <!-- fixed, rgba(0,0,0,0.6) backdrop -->
  <div class="command-palette">        <!-- 560px, surface-2, border, 12px radius -->
    <div class="command-input-wrap">   <!-- 52px height, search icon + input + ESC kbd -->
      <input class="command-input">   <!-- borderless, 16px, caret-color: purple -->
    </div>
    <div class="command-results">
      <div class="command-section-label">...</div>
      <a class="command-item active">  <!-- 36px height, purple-muted hover bg -->
        <div class="command-item-icon">...</div>
        <span class="command-item-label">...</span>
        <span class="command-item-meta mono">ENG-2847</span>
      </a>
    </div>
    <div class="command-footer">...</div>
  </div>
</div>
```

Command items animate with `slideInRight` at 50ms staggered delays.

### Sidebar

240px wide, `surface-1` background, `border-right: border-subtle`.

```html
<nav class="sidebar">
  <div class="sidebar-workspace">          <!-- workspace selector -->
  <div class="sidebar-section">
    <div class="sidebar-section-label">Teams</div>
    <a class="sidebar-item sidebar-item--active">  <!-- purple text + surface-2 bg -->
      <span class="sidebar-item-dot" style="background:#5E6AD2;"></span>
      <span class="sidebar-item-label">Engineering</span>
      <span class="sidebar-item-count mono">84</span>
    </a>
  </div>
</nav>
```

Sidebar item height: `30px`, `border-radius: 6px`, hover: `surface-2`. Active: `surface-2 + purple text`.

### Cards

**`.card`:** `surface-1`, `border-subtle`, `8px radius`, `padding: 16px`. Hover: `border-default`.

**`.card-project`:** Icon (32px colored square) + name + team label + progress bar + avatar stack.

**`.card-cycle`:** Cycle number + date range + CSS progress ring + linear progress bar.

**Progress ring:** Pure CSS SVG with `stroke-dasharray` / `stroke-dashoffset` technique:
```html
<div class="progress-ring">
  <svg viewBox="0 0 36 36">
    <circle class="progress-ring-track" cx="18" cy="18" r="15.5"/>
    <circle class="progress-ring-fill" cx="18" cy="18" r="15.5"
      stroke-dasharray="97.4"
      stroke-dashoffset="27.3"/>   <!-- 97.4 * (1 - 0.72) = 27.3 for 72% -->
  </svg>
  <div class="progress-ring-label">72%</div>
</div>
```

**`.card-roadmap`:** Initiative title + status badge + progress bar + due date + team avatars.

### Forms

All form elements use `surface-2` background, `border-default` border, `border-radius: 8px`, `height: 32px`.

**Focus state:** `border-color: purple`, `box-shadow: 0 0 0 3px purple-muted`.

**`.checkbox`:** 14px square, `border-radius: 4px`. Checked: purple fill + white checkmark via CSS `::after`.

**`.radio`:** 14px circle. Checked: purple `::after` dot.

### Status & Priority Chips

**`.status-chip`:** 24px height, pill, bordered, icon + label.
- `.status-chip-todo`: border-default
- `.status-chip-in-progress`: orange tint
- `.status-chip-done`: green tint
- `.status-chip-cancelled`: red tint + `text-decoration: line-through`
- `.status-chip-backlog`: yellow tint

**`.priority-chip`:** 24px height, pill, colored dot + label.

### Label Chips

`.label-chip`: pill, `border: border-subtle`, `padding: 2px 7px`, colored dot variant:
- `.label-chip-bug` → red dot
- `.label-chip-feature` → purple dot
- `.label-chip-improvement` → blue dot
- `.label-chip-design` → pink dot
- `.label-chip-docs` → teal dot
- `.label-chip-backend` → orange dot

### Badges

`.badge`: 20px height, pill, `surface-3 + border-subtle + label-secondary`.

Variants: `.badge--purple`, `.badge--green`, `.badge--orange`, `.badge--red`, `.badge--yellow`, `.badge--blue`

### Progress

- `.progress-bar`: 4px height, `surface-3` track, pill shape
- `.progress-bar-fill`: purple default; `.done` = green; `.in-progress` = orange
- `.loading-bar`: 2px, indeterminate animation via `::after` pseudo-element
- `.progress-ring`: SVG-based circle with stroke-dashoffset technique

### Modals

**`.modal-overlay`:** `position: fixed; inset: 0; background: rgba(0,0,0,0.6)`, flex centered.
**`.modal`:** `surface-2`, `border-default`, `12px radius`, `shadow-2xl`, `max-width: 480px`.
- `.modal-sm`: 360px — confirmation dialogs
- `.modal-lg`: 640px — settings panels
- Animated with `scaleInCenter` (0.96→1 scale)

### Toasts

Fixed position, top-right, `max-width: 360px`. `surface-2 + border-default + shadow-xl`. Four semantic variants: success/error/warning/info with colored icons.

---

## index.html — Showcase Structure

A polished, dark-background showcase demonstrating the full system:

1. **Sticky topbar** — Linear logo (SVG mark + wordmark), nav links, search icon, ⌘K kbd, avatar
2. **Hero** — gradient headline "Move at the speed of thought", two CTAs, mesh gradient background
3. **Color palette** — token swatches organized by group (backgrounds, brand, status, labels)
4. **Typography scale** — all classes with metadata (class name, size/weight spec, example text)
5. **Issue list** — 8 realistic rows across groups (In Progress × 3, Todo × 3, Done, Cancelled) with all priority/status icons, label chips, assignee avatars, due dates
6. **Command palette** — shown open with search results, section labels, keyboard shortcuts
7. **Sidebar** — full sidebar + adjacent content area preview
8. **Buttons** — all variants, sizes, states, icon buttons, kbd display
9. **Status & Priority chips** — all variants in flex rows
10. **Cards** — project, cycle, roadmap (3-up grid)
11. **Forms** — inputs, textarea, select, checkboxes, radios (2-column grid)
12. **Badges & Labels** — all badge variants + label chips
13. **Progress** — bars (purple/orange/green/indeterminate), rings, spinners
14. **Navigation tabs** — with counts
15. **Motion** — 6-item grid showing each animation with description
16. **Footer** — minimal, links to component pages

---

## Component Showcase Pages

Each `components/*.html` is self-contained and links to all 4 CSS files from `../`.

**Common structure:**
- Breadcrumb: `Linear DS / [Component]`
- Page heading + description
- Sections with `.component-section-title` (uppercase, tertiary, border-bottom)
- Demo items with monospace label column (`.demo-label`, width 120px)

**buttons.html:** All variants, all states (default, disabled, loading), icon buttons (7 icons), kbd shortcut display (single + combos), button groups, toolbar composition.

**cards.html:** Base card (3 variants), project cards (3 — active, behind, on track), cycle cards (3 — active, completed, upcoming), roadmap cards (3).

**forms.html:** All input states, textarea, select, checkboxes (unchecked/checked/disabled/group), radio group, full "Create Issue" form example.

**navigation.html:** Topbar, sidebar + content area (460px demo), tabs, command palette, popover/dropdown (status picker + issue actions).

**modals.html:** Live interactive modals (triggered by buttons, closable by ESC + overlay click), standard modal preview, confirm modal preview, wide settings modal preview, all 4 toast variants.

---

## Design Principles to Maintain

1. **Dark-first**: `:root` is always dark. Never assume light.
2. **Dense but comfortable**: 36px issue rows, 30px sidebar items, 32px inputs. Not cramped.
3. **Instant hover**: Issue rows use `transition: none`. No lag on list interactions.
4. **Purple is singular**: Only one accent color. Never use it decoratively.
5. **Mono for metadata**: Issue IDs, shortcuts, percentages, timestamps in JetBrains Mono.
6. **No external dependencies**: All CSS, all custom properties, no frameworks.
7. **Semantic HTML**: Proper ARIA labels, roles, landmarks, keyboard navigation.
8. **Reduced motion support**: All animations disabled for `prefers-reduced-motion: reduce` users.
9. **Light mode is real**: Not an afterthought — all tokens have meaningful light equivalents.
10. **Responsive**: 768px and 1024px breakpoints. Grid collapses. Sidebar can hide on mobile.
