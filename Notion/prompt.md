# Notion Design System — Generation Prompt

## Overview

Build a complete, production-quality design system called the "Notion Design System" inside `/Users/sscargall/Documents/ClaudeDesignSystems/Notion/`.

This is part of a series of brand-faithful design systems. The reference implementation is at `/Users/sscargall/Documents/ClaudeDesignSystems/Apple/` — read those files to understand expected quality and depth before building.

---

## Notion Brand Aesthetic

- **Personality:** Content-first, block editor, almost invisible chrome. Notion's UI gets out of the way — every pixel serves the content, not the app. Soft neutrals, gentle shadows, barely-there borders. Feels like a digital notebook.
- **Typography:** `ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji"`. Medium weight, generous line-height for readability.
- **Colors:**
  - Background: `#FFFFFF`
  - Surface (sidebar): `#F7F6F3` (slightly warm off-white)
  - Surface hover: `#EFEFEC`
  - Notion black: `#191919`
  - Label secondary: `#787774`
  - Label tertiary: `#ACAAA8`
  - Border subtle: `#E3E2E0`
  - Border default: `#D9D9D7`
  - **9 Notion named colors** (bg + text variant each):
    - Gray: bg `#F1F1EF`, text `#787774`
    - Brown: bg `#F4EEEE`, text `#9F6B53`
    - Orange: bg `#FAEBDD`, text `#D9730D`
    - Yellow: bg `#FBF3DB`, text `#CB912F`
    - Green: bg `#EDF3EC`, text `#448361`
    - Blue: bg `#E7F3F8`, text `#337EA9`
    - Purple: bg `#F6F3F8`, text `#9065B0`
    - Pink: bg `#FAF1F5`, text `#C14C8A`
    - Red: bg `#FDEBEC`, text `#D44C47`
  - Dark bg: `#191919`
  - Dark surface: `#202020`
  - Dark surface hover: `#2F2F2F`
  - Dark label primary: `#FFFFFF` at 90% opacity
  - Dark label secondary: `#FFFFFF` at 45% opacity
  - Dark border: `#FFFFFF` at 9% opacity
- **Both light and dark:** Yes — Notion has a polished dark mode
- **Motion:** Minimal, gentle — 80/120/200/300ms. Easing: `cubic-bezier(0.25, 0.1, 0.25, 1)`. Nothing flashy.
- **Reference:** notion.so

---

## File Structure

```
Notion/
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
- All colors above including all 9 Notion named colors × 2 (bg/text)
- Typography: system font stack, emoji font stack, mono stack, scale 40/32/24/20/18/16/14/13/12/11px
- Spacing: 4px grid — 2/4/6/8/10/12/16/20/24/32/40/48px
- Radius: 3px (default/button), 4px (input), 6px (popover), 8px (modal), 9999px (pills)
- Shadows: very gentle — `0 1px 2px rgba(15,15,15,0.04)`, `0 3px 8px rgba(15,15,15,0.07)`, `0 6px 24px rgba(15,15,15,0.10)`
- Motion: 80/120/200/300ms, `cubic-bezier(0.25, 0.1, 0.25, 1)` easing

---

## Typography (typography.css)

- `.title-lg`: 40px, weight 700, line-height 1.2 — page title
- `.title`: 32px, weight 700
- `.heading-1`: 24px, weight 600 (H1 in block editor)
- `.heading-2`: 20px, weight 600 (H2)
- `.heading-3`: 18px, weight 600 (H3)
- `.body`: 16px, weight 400, line-height 1.65 — main reading text
- `.ui-body`: 14px, weight 400, line-height 1.5 — UI chrome text
- `.caption`: 13px, label-secondary
- `.label`: 12px, weight 500, uppercase, tracking 0.06em
- `.overline`: 11px, weight 500, uppercase
- `.mono`: monospace, 14px
- Color utilities: `.text-gray`, `.text-brown`, `.text-orange`, `.text-yellow`, `.text-green`, `.text-blue`, `.text-purple`, `.text-pink`, `.text-red`
- Background utilities: `.bg-gray`, `.bg-brown`, etc.

---

## Animations (animations.css)

- `@keyframes fadeIn`
- `@keyframes slideInLeft` — sidebar appear
- `@keyframes scaleInCenter` — modal/popover appear (from scale 0.96)
- `@keyframes shimmer` — skeleton loading
- `@keyframes checkmark` — checkbox check animation
- `@keyframes toggleExpand` — toggle block open
- `@keyframes menuAppear` — slash menu, popovers
- `@keyframes toastIn` / `toastOut`
- Utility classes (`.animate-fade-in`, `.animate-scale-in`, etc.)
- `prefers-reduced-motion` support

---

## Components (components.css)

### Block Editor
- `.block-editor`: padding 180px horizontal, 96px top — Notion's wide body margin
- `.block-row`: flex row, 100% width, min-height 30px
  - `.block-drag-handle`: appears on hover (6-dot drag icon in CSS)
  - `.block-type-switcher`: appears on hover
  - `.block-content`: flex:1, actual content

Block types:
- `.block-text`, `.block-h1`, `.block-h2`, `.block-h3`
- `.block-bulleted-list`, `.block-numbered-list`
- `.block-todo` — checkbox + text, checked state with strikethrough
- `.block-toggle` — triangle + text, expands children
- `.block-quote` — left gray border, italic
- `.block-callout` — emoji + colored background (all 9 colors via `.block-callout--{color}`)
- `.block-code-wrapper` — language label, copy button, dark background
- `.block-divider` — thin horizontal rule
- `.block-image-wrapper` — image placeholder + caption
- `.block-bookmark` — URL card with title/description/domain/favicon

### Inline Database (Table view)
- `.database-wrapper`, `.database-table`, `.database-header-row`, `.database-row`, `.database-cell`
- `.database-cell--title` — bold first column
- `.property-select-tag` with all 9 color variants

### Page Header
- `.page-cover` — 120px tall, full-width
- `.page-icon` — 72px emoji/icon
- `.page-title` — contenteditable-style title input
- `.page-header-controls` — appear on hover (add icon, add cover)

### Sidebar / Page Tree
- `.sidebar` — 240px, warm off-white, border-right
- `.workspace-switcher` — top area with avatar + name + chevron
- `.sidebar-section`, `.sidebar-section-header`, `.sidebar-section-label`
- `.sidebar-item` — 28px height, toggle + icon + title + actions
- `.sidebar-item--active`, `.sidebar-item--expanded`
- `.sidebar-children` — indented children

### Navigation
- `.topbar` — 45px, breadcrumb + actions
- `.breadcrumb`, `.breadcrumb-item`, `.breadcrumb-separator`
- `.tabs`, `.tab`, `.tab--active`

### Selection Toolbar
- `.selection-toolbar` — dark floating pill
- `.selection-toolbar-btn`, `.selection-toolbar-divider`

### Slash Menu
- `.slash-menu` — 280px, surface bg, shadow, floating
- `.slash-menu-section`, `.slash-menu-item` — icon + title + description

### Page Mention / Backlinks
- `.page-mention` — inline blue underlined link with icon
- `.mention-chip` — @name chip with avatar

### Buttons
- `.btn` + variants: `.btn-primary`, `.btn-secondary`, `.btn-ghost`, `.btn-blue`, `.btn-danger`
- Sizes: `.btn-sm`, default, `.btn-lg`
- `.btn-icon` for square icon-only buttons

### Forms
- `.input`, `.select`, `.textarea`
- `.checkbox`, `.checkbox-wrapper`, `.checkbox-label`
- `.toggle-switch` with track/thumb CSS animation
- `.form-group`, `.form-label`, `.form-hint`, `.form-error`

### Modals & Panels
- `.modal-overlay`, `.modal`, `.modal-header`, `.modal-body`, `.modal-footer`
- `.popover`, `.popover-item`, `.popover-divider`, `.popover-section-label`
- `.peek-modal` — right-side slide-in at 50% width
- `.settings-layout`, `.settings-sidebar`, `.settings-content`
- `.settings-row` — label-left/control-right pattern

### Feedback
- `.toast`, `.toast-container`, `.toast--success`, `.toast--warning`, `.toast--error`
- `.comment-thread`, `.comment-bubble`, `.comment-avatar`, `.comment-body`
- `.badge` with color variants
- `.empty-state`
- `.skeleton`, `.skeleton-text`, `.skeleton-block`

---

## Main index.html

Notion-faithful showcase:
1. Top navigation bar
2. Full Notion page simulation (sidebar + topbar + page header + block editor)
3. Color system (swatches + 9 named color blocks)
4. Typography scale
5. Block types catalog (all 12 types)
6. Inline database (5 rows, 6 columns, all select tag colors)
7. Sidebar demo
8. Buttons (all variants, sizes, states)
9. Forms (inputs, select, textarea, checkbox, toggle)
10. Menus (slash menu, selection toolbar, popover, breadcrumb)
11. Modals (dialog, settings, peek)
12. Feedback (comments, toasts, badges, empty state, skeleton)
13. Motion demos
14. Footer

---

## Component Showcase Pages

Self-contained pages using warm off-white backgrounds:
- `components/buttons.html` — all variants, sizes, states, groups
- `components/cards.html` — standard card, gallery cards, bookmark blocks, callout blocks
- `components/forms.html` — inputs, select, textarea, checkbox, toggle, settings row pattern
- `components/navigation.html` — topbar, breadcrumb, full sidebar, tabs, workspace switcher
- `components/modals.html` — dialog, popovers, peek modal, settings modal, toasts

---

## Requirements

- Zero external dependencies (no CDN fonts, no icon libraries, no frameworks)
- Both light and dark mode equally polished
- Responsive: mobile-first, 768px and 1024px breakpoints
- Semantic HTML5, ARIA attributes, `prefers-reduced-motion` respected
- All files complete — no placeholders, no TODOs, no lorem ipsum (real Notion-flavored content)
