# Claude.ai Design System — Generation Prompt

This is the canonical prompt for regenerating the complete Claude.ai design system (CSS + HTML showcase) from scratch using Claude Code.

---

## Instructions for Claude Code

You are building the complete Claude.ai design system for Anthropic. This is a production-quality CSS design system with a fully self-contained HTML showcase. No external dependencies — no CDN, no npm, no Google Fonts, nothing. All files are written to disk.

**Working directory:** set to the project root (e.g. `/path/to/ClaudeDesignSystems/Claude/`).

**Output files:**
- `tokens.css`
- `typography.css`
- `animations.css`
- `components.css`
- `index.html`
- `components/buttons.html`
- `components/cards.html`
- `components/forms.html`
- `components/navigation.html`
- `components/modals.html`

---

## Brand Identity

**Product:** Claude.ai by Anthropic  
**Character:** Warm, intelligent, conversation-first. Calm, honest, capable. Never cold, never clinical.

**Design language keywords:** warm cream, deep brown-black, coral accent, serif display, unhurried motion, conversation-native.

---

## Design Tokens (`tokens.css`)

Define all tokens as CSS custom properties on `:root`.

### Brand Colors

```css
--color-coral:         #DA7756;   /* Primary brand accent */
--color-coral-dark:    #C0624A;
--color-coral-light:   rgba(218, 119, 86, 0.15);
--color-coral-subtle:  rgba(218, 119, 86, 0.08);
--color-coral-glow:    0 0 0 3px rgba(218, 119, 86, 0.18);
```

### Backgrounds (Light Mode)

```css
--color-bg-primary:   #FAF9F5;   /* Warm cream — main page */
--color-bg-secondary: #FFFFFF;   /* Surface white */
--color-bg-warm:      #F3F1EB;   /* Sidebar, input areas */
--color-bg-muted:     #E8E5DC;   /* Hover states, chips */
--color-bg-border:    #E0DDD5;   /* Subtle warm border */
```

### Dark Mode Backgrounds

```css
--color-dark-bg-primary:  #1A1310;   /* Deep brown-black — never pure #000 */
--color-dark-surface-1:   #231F1C;
--color-dark-surface-2:   #2D2825;
--color-dark-border:      #3A3530;
```

### Label Colors (Light)

```css
--color-label-primary:   #1A1310;
--color-label-secondary: #6B6560;
--color-label-tertiary:  #9E9890;
--color-label-quaternary: rgba(26, 19, 16, 0.18);
```

### Semantic Aliases

Define these semantic aliases that remap automatically in dark mode:

```css
--color-bg, --color-surface, --color-surface-raised, --color-surface-overlay,
--color-border, --color-text, --color-text-secondary, --color-text-tertiary,
--color-accent, --color-accent-hover, --color-accent-light
```

### Conversation Bubble Colors

```css
--color-bubble-human-bg:     #FFFFFF;           /* Human bubble — white card */
--color-bubble-human-border: var(--color-bg-border);
--color-bubble-assistant-bg: transparent;       /* No bubble — text flows free */
```

### Semantic System Colors

```css
--color-success: #3D9970;   --color-success-light: rgba(61, 153, 112, 0.12);
--color-warning: #D4A017;   --color-warning-light: rgba(212, 160, 23, 0.12);
--color-error:   #C0392B;   --color-error-light:   rgba(192, 57, 43, 0.12);
--color-info:    #2C7BE5;   --color-info-light:    rgba(44, 123, 229, 0.12);
```

### Typography

```css
--font-display: "Styrene A", "Söhne", Georgia, "Times New Roman", serif;
--font-text:    system-ui, -apple-system, "Segoe UI", "Helvetica Neue", Arial, sans-serif;
--font-mono:    ui-monospace, "SFMono-Regular", "SF Mono", Menlo, Consolas, monospace;
```

Type scale: `--text-48`, `--text-36`, `--text-28`, `--text-22`, `--text-18`, `--text-17`, `--text-15`, `--text-14`, `--text-13`, `--text-11`.

Weights: `--weight-regular:400`, `--weight-medium:500`, `--weight-semibold:600`, `--weight-bold:700`.

Line heights: `--leading-display:1.08`, `--leading-heading:1.15`, `--leading-subhead:1.30`, `--leading-body:1.65`, `--leading-conversation:1.70`, `--leading-caption:1.40`.

Letter spacing: `--tracking-display:-0.02em`, `--tracking-heading:-0.01em`, `--tracking-body:0em`, `--tracking-caps:0.08em`.

### Spacing (4px base grid)

`--space-1:4px` through `--space-24:96px`. Include: 1, 2, 3, 4, 5, 6, 8, 10, 12, 16, 20, 24.

### Border Radius

```css
--radius-xs: 4px;   --radius-sm: 8px;    --radius-md: 12px;  --radius-lg: 16px;
--radius-xl: 20px;  --radius-2xl: 24px;  --radius-pill: 9999px;
```

Aliases: `--radius-input: var(--radius-sm)`, `--radius-card: var(--radius-md)`, `--radius-modal: var(--radius-lg)`, `--radius-bubble: var(--radius-xl)`, `--radius-button: var(--radius-pill)`, `--radius-chip: var(--radius-pill)`.

### Shadows (warm-tinted, never cold blue)

```css
--shadow-xs: 0 1px 2px rgba(26, 19, 16, 0.06);
--shadow-sm: 0 1px 4px rgba(26, 19, 16, 0.08);
--shadow-md: 0 4px 16px rgba(26, 19, 16, 0.10);
--shadow-lg: 0 8px 24px rgba(26, 19, 16, 0.12);
--shadow-xl: 0 16px 48px rgba(26, 19, 16, 0.14), 0 4px 12px rgba(26, 19, 16, 0.08);
--shadow-2xl: 0 24px 64px rgba(26, 19, 16, 0.18), 0 8px 24px rgba(26, 19, 16, 0.10);
--shadow-coral: 0 8px 24px rgba(218, 119, 86, 0.28);
--shadow-inset: inset 0 1px 3px rgba(26, 19, 16, 0.06);
```

Dark mode shadows use pure black RGBA (0, 0, 0) at higher opacity.

### Motion

```css
--duration-instant: 100ms;   --duration-fast: 150ms;    --duration-normal: 200ms;
--duration-moderate: 350ms;  --duration-slow: 500ms;    --duration-blink: 530ms;

--ease-standard:   cubic-bezier(0.25, 0.46, 0.45, 0.94);
--ease-decelerate: cubic-bezier(0.00, 0.00, 0.20, 1.00);
--ease-accelerate: cubic-bezier(0.40, 0.00, 1.00, 1.00);
--ease-spring:     cubic-bezier(0.34, 1.40, 0.64, 1.00);
```

Shorthand transition tokens: `--transition-fast`, `--transition-normal`, `--transition-moderate`, `--transition-spring`.

### Z-Index Scale

```css
--z-base:0  --z-raised:10  --z-dropdown:100  --z-sticky:200
--z-overlay:300  --z-modal:400  --z-toast:500  --z-tooltip:600
```

### Component Dimensions

```css
--btn-height-sm:32px  --btn-height-md:40px  --btn-height-lg:48px
--input-height-sm:36px  --input-height-md:40px  --input-height-lg:48px
--nav-height:56px  --sidebar-width:260px  --thread-max-width:680px
--max-width-site:980px  --max-width-wide:1200px
--avatar-size-sm:24px  --avatar-size-md:32px  --avatar-size-lg:40px  --avatar-size-xl:56px
--blur-sm:blur(8px)  --blur-md:blur(16px)  --blur-lg:blur(24px)
```

### Dark Mode Override

All dark mode overrides live in `@media (prefers-color-scheme: dark)` on `:root`. Override backgrounds, labels, semantic aliases, bubble colors, and shadows. Coral stays `#DA7756` — brand consistency across modes.

---

## Typography (`typography.css`)

### Base Reset

- `box-sizing: border-box` on everything
- `-webkit-font-smoothing: antialiased`
- `html { font-size: 17px; scroll-behavior: smooth; }`
- `body` uses `--font-text`, `--text-17`, `--leading-body`, `--color-text`, `--color-bg`

### Type Classes

| Class | Size | Font | Weight | Use |
|---|---|---|---|---|
| `.display` | clamp(28px, 5vw, 48px) | display/serif | bold | Hero headlines |
| `.heading-1` | clamp(22px, 4vw, 36px) | display/serif | bold | Page titles |
| `.heading-2` | clamp(22px, 3vw, 28px) | display/serif | semibold | Section titles |
| `.heading-3` | 22px | text/sans | semibold | Subsections |
| `.subhead` | 18px | text/sans | medium | Card headers |
| `.body` | 17px | text/sans | regular | Reading body |
| `.body-sm` | 15px | text/sans | regular | Secondary content |
| `.conversation-body` | 17px | text/sans | regular | leading 1.70 — conversation reading |
| `.caption` | 13px | text/sans | regular | Timestamps, meta |
| `.label` | 11px | text/sans | semibold | UPPERCASE CAPS labels |
| `.mono` | 14px | mono | regular | Inline code |

### Gradient Text

```css
.text-gradient-coral {
  background: linear-gradient(135deg, var(--color-coral) 0%, var(--color-coral-dark) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.text-gradient-warm { /* three-stop: #DA7756 → #C0624A → #8B4C3E */ }
```

### `.conversation-body` Rich Content

Style all child elements: `p`, `ul`, `ol`, `li`, `strong`, `em`, `code` (coral-dark tint on bg-muted), `pre`, `blockquote` (coral left border + coral-subtle bg), `h1`–`h4`.

### Utilities

Color: `.text-primary`, `.text-secondary`, `.text-tertiary`, `.text-coral`, `.text-success`, `.text-warning`, `.text-error`

Weight: `.font-regular`, `.font-medium`, `.font-semibold`, `.font-bold`

Alignment: `.text-left`, `.text-center`, `.text-right`

Truncation: `.truncate`, `.line-clamp-2`, `.line-clamp-3`

---

## Animations (`animations.css`)

### Required Keyframes

| Name | Purpose |
|---|---|
| `fadeIn` / `fadeOut` | Opacity 0→1 / 1→0 |
| `fadeInUp` / `fadeInDown` | Opacity + 12px Y translate |
| `slideInUp` / `slideInRight` | 20px / 24px slide + fade |
| `slideOutRight` / `slideOutDown` | Exit animations |
| `messageIn` | 10px Y + fade — signature conversation entrance |
| `typing` | 530ms step-end blink (50% on/off) |
| `thinkingDot` | scale(1)→scale(1.3)→scale(1) + opacity 0.35→1→0.35, 1.4s loop |
| `coralPulse` | Box-shadow ripple 0→10px, coral color |
| `shimmer` | background-position -200%→200% for skeleton loading |
| `scaleIn` | scale(0.90)→scale(1) + fade |
| `springIn` | scale(0.88)→scale(1.02)→scale(0.99)→scale(1), bouncy |
| `toastIn` / `toastOut` | translateY(-100%) scale(0.95) ↔ normal |
| `panelSlideIn` | translateX(100%)→0 |
| `pulse` | opacity 1→0.5→1, generic |
| `spin` | 360° rotation for spinners |
| `float` | translateY 0→-6px→0, decorative |
| `gradientShift` | background-position 0%→100%→0%, ambient hero |
| `shake` | ±5px X for error states |

### Claude-Specific Components

**Typing cursor** (`.typing-cursor`): 2px × 18px, coral, `border-radius:1px`, `vertical-align:text-bottom`, uses `typing` keyframe at `--duration-blink` step-end infinite.

**Thinking indicator** (`.thinking-indicator` + `.thinking-dot`): inline-flex, 3 × 8px coral circles, each dot uses `thinkingDot` animation, dots 2 and 3 have `animation-delay: 160ms` and `320ms` respectively.

**Thinking area** (`.thinking-area`): flex row, centers dots + label text, 15px secondary color.

### Animation Utility Classes

Prefix all with `.animate-*`:
- Fade: `fade-in`, `fade-out`, `fade-in-up`, `fade-in-down`
- Slide: `slide-in-up`, `slide-in-right`, `slide-out-down`
- Special: `message-in`, `scale-in`, `spring-in`
- Ongoing: `pulse`, `spin`, `float`, `coral-pulse`, `gradient` (includes `background-size: 300% 300%`)
- Toast: `toast-in`, `toast-out`
- Panel: `panel-in`

### Delay Utilities

`.delay-50` through `.delay-800` (50, 100, 150, 200, 300, 400, 500, 600, 800ms).

### Hover Utilities

`.hover-lift`: translateY(-2px) + shadow-lg on hover, spring transition.
`.hover-scale`: scale(1.02) on hover, scale(0.98) on active.

### Skeleton Loading

`.skeleton`: shimmer gradient animation on warm colors.  
`.skeleton-text` with `.short` (38%), `.medium` (62%), `.long` (88%) width variants.  
`.skeleton-message` + `.skeleton-avatar` + `.skeleton-content` for conversation-shaped loading states.

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
  /* Reset skeleton, thinking-dot, typing-cursor, animate-gradient */
}
```

---

## Components (`components.css`)

### Layout

- `.container` — max-width 980px, centered, 24px inline padding
- `.container-wide` — max-width 1200px
- `.container-thread` — max-width 680px
- All containers reduce to 16px padding at ≤768px

### Buttons

Base class `.btn` — inline-flex, pill radius, 40px height, 15px semibold text, spring transition on transform, coral focus-visible outline.

States: `:hover` → scale(1.02); `:active` → scale(0.97); `disabled` → opacity 0.40.

| Class | Style |
|---|---|
| `.btn-primary` | Coral fill, white text, coral shadow |
| `.btn-secondary` | Warm surface, border, xs shadow |
| `.btn-ghost` | Transparent, label-secondary text, no shadow |
| `.btn-danger` | Error red fill, white text |

Sizes: `.btn-sm` (32px, 13px text), `.btn-lg` (48px, 17px text).

Icon button: `.btn-icon` — square (width = height).

Loading: `.is-loading` — adds a 14px spinning border pseudo-element via `::after`.

Send button: `.btn-send` — 36px circle, coral, white arrow SVG, disabled state uses bg-muted.

Button group: `.btn-group` — inline-flex with 8px gap.

### Conversation Thread

`.conversation-thread` — flex column, 24px gap, max-width thread, centered.

`.message` — flex row, 12px gap, `messageIn` animation.

`.message--human` — `flex-direction: row-reverse` (bubble + avatar right-aligned).

`.message--assistant` — avatar left, content fills remaining width.

`.message-bubble--human` — white bg, border, `--radius-bubble --radius-bubble 4px --radius-bubble` (flat bottom-right corner).

`.message-avatar` — 32px circle, flex-centered. `.message-avatar--claude` coral bg white text. `.message-avatar--human` muted bg.

`.message-timestamp` — 11px, tertiary color.

`.message-thinking` / `.message-thinking-label` — thinking dots in message context.

### Input Area

`.conversation-input-area` — sticky bottom, warm bg, border-top, z-index sticky.

`.conversation-input-inner` — max-width thread, centered, flex column, 12px gap.

`.conversation-input-box` — white bg, border, rounded-md, focus-within: coral border + glow.

`.conversation-input` — transparent, no border/outline, 17px, leading-body, min-height 28px, max-height 200px.

`.input-toolbar` — space-between flex row.

`.input-toolbar-btn` — 32px square, ghost, tertiary color, hover shows muted bg.

### Prompt Suggestion Chips

`.prompt-chips-row` — horizontal scroll, no scrollbar, flex row, 8px gap.

`.prompt-suggestion-chip` — 36px pill, 13px medium, white bg, border. Hover: warm bg, coral border and text, scale(1.02).

### Model Selector

`.model-selector` — 32px pill, warm bg, border, 13px medium. Hover: muted bg, coral border.

`.model-selector-name` — semibold, primary text color.

`.model-dropdown` — white bg, border, md radius, xl shadow, min-width 280px, `scaleIn` animation, `transform-origin: top left`.

`.model-dropdown-header` — 11px uppercase caps label.

`.model-option` — flex row with indicator + info + optional badge. Hover: warm bg. `.is-selected` has coral-subtle bg.

`.model-option-indicator` — 18px circle, border. When selected: coral bg with white 6px inner dot.

`.model-option-badge` — coral-light bg, coral-dark text, pill.

### Artifact Panel

`.artifact-panel` — fixed right, top=nav-height, width 50%, flex column, panelSlideIn animation.

`.artifact-header` — flex row, warm bg, border-bottom, filename (mono) + lang badge + actions.

`.artifact-tabs` + `.artifact-tab` — underline tabs with `.is-active` → coral border-bottom.

`.artifact-inline` — bordered, rounded-md inline artifact inside message.

### File Attachment Pills

`.attachment-pill` — flex row, warm bg, pill border-radius, 13px. Contains icon zone (coral-light bg), truncated name, size, remove button.

`.attachment-pill-icon` — 20px, coral-light bg, coral color.

`.attachment-pill-remove` — 16px circle button, muted bg. Hover: error-light bg, error color.

`.attachment-row` — flex-wrap, 8px gap.

### Sidebar

`.sidebar` — 260px width, warm bg, right border, flex column.

`.sidebar-section-label` — 11px CAPS, tertiary, 8px tracking.

`.sidebar-item` — 36px flex row, 8px radius, 15px text. `.is-active`: coral-light bg, coral-dark text, medium weight.

`.sidebar-item--new` — coral text, coral-subtle hover.

`.conversation-list-item` — flex column (title + date), auto height, same hover/active as sidebar-item.

### Settings Panel

`.settings-section` → `.settings-group` → `.settings-row` anatomy.

`.settings-group` — white surface, border, rounded-md, overflow hidden.

`.settings-row` — 48px min-height, flex row. Separator via `::after` pseudo-element on all but last child.

`.settings-row-icon` — 28px rounded-xs colored square (emoji or icon).

`.settings-toggle` — 51×31px iOS-style toggle. Hidden native input drives state. `.toggle-track` transitions coral when `:checked`. `.toggle-thumb` white circle translates 20px on checked via sibling selector.

### Cards

`.card` — white surface, border, rounded-md, sm shadow. Hover: translateY(-2px), md shadow.

`.card-body`, `.card-header`, `.card-footer` — 20px padding anatomy.

`.card-title` — 17px semibold. `.card-subtitle` — 15px secondary.

`.card-feature` — min-height 280px, coral gradient overlay (::before pseudo), white text, content at flex-end.

`.card-capability` — surface bg, border, rounded-md, 20px padding. Hover: translateY(-2px) + coral-light border.

`.card-capability-icon` — 44px, rounded-sm, coral-subtle bg, 22px emoji/icon.

`.card-plan` — flex column, surface bg, border, rounded-lg.

`.card-plan.is-featured` — coral bg, coral-dark border, white text.

`.card-plan-price` — 36px display font, bold. `.card-plan-features` — list with check circles.

`.card-plan-check` — 18px circle, success-light bg, success text.

`.card-grid` — `grid-template-columns: repeat(auto-fill, minmax(260px, 1fr))`, 20px gap.

### Forms

`.form-group` — flex column, 8px gap. `.form-label` — 15px medium. `.form-label.is-required::after` — " *" in error color. `.form-helper` — 13px secondary. `.form-error` — 13px error color, flex row with icon.

`.input` — full width, 40px, 17px, surface bg, 1.5px border, 8px radius. Focus: coral border + glow. Error: `.is-error` — error border + red glow. Disabled: 50% opacity. Hover: coral-light border.

`.textarea` — same as input, min-height 120px, resize vertical.

`.select-wrapper` + `.select` — position relative wrapper with custom `.select-chevron` (pointer-events:none positioned right).

`.checkbox-wrapper` — inline-flex label, cursor pointer.

`.checkbox` — 20px relative container. Hidden input. `.checkbox-box` — absolute fill, border, rounded-xs. Checked: coral bg + border. `::after` — white checkmark via border trick, spring-scales in.

`.radio-wrapper` / `.radio` / `.radio-circle` — same pattern, circle shape. `::after` — inner dot in coral, spring-scales in.

### Token Usage Meter

`.token-meter` — flex column, 8px gap. `.token-meter-bar` — 4px height, rounded-pill, muted bg. `.token-meter-fill` — coral by default. `.token-meter--warning .token-meter-fill` → warning color. `.token-meter--critical .token-meter-fill` → error color.

### Modal / Overlay

`.modal-overlay` — fixed inset, dark overlay, `backdrop-filter:blur(8px)`, `fadeIn` animation, flex-centered.

`.modal` — max-width 480px, white surface, rounded-lg, 2xl shadow, `springIn` animation.

`.modal-header`, `.modal-body`, `.modal-footer` — header/footer have borders, footer has `justify-content:flex-end` button row.

`.modal-close` — 28px circle, muted bg.

### Toast

`.toast-container` — fixed top-center, 380px max-width, flex column.

`.toast` — pill shape, `--color-label-primary` bg (dark), primary-bg text, `toastIn` spring animation.

Status variants override background with `--color-success`, `--color-error`, `--color-warning`.

### Navbar

`.navbar` — sticky top, 56px, warm bg, bottom border, z-index sticky.

`.navbar-inner` — max-width wide, space-between flex.

`.navbar-brand` — display font, 17px bold, flex row with logo.

`.navbar-nav` — centered flex list, 2px gap between items.

`.navbar-nav-item a` — 15px medium, secondary color, pill hover bg.

`.nav-avatar` — 32px circle, coral-light bg, coral text. Hover: coral border.

### Badges

`.badge` — 11px semibold, pill, inline-flex.

Variants: `.badge-coral`, `.badge-success`, `.badge-warning`, `.badge-error`, `.badge-neutral`.

`.badge-dot` — 6px circle in `currentColor`.

### Avatar

`.avatar` — 40px circle (default), coral-light bg. Sizes: `.avatar-sm` (24px), `.avatar-md` (32px), `.avatar-xl` (56px).

### Progress / Spinner

`.progress-bar` / `.progress-fill` — 4px bar, coral default. State modifiers: `.is-success`, `.is-warning`, `.is-error`.

`.spinner` — 24px, 2.5px border, coral top-color, spin 0.8s linear. `.spinner-sm` (16px), `.spinner-lg` (36px).

### Color Swatch (showcase only)

`.color-swatch` — aspect-ratio 1, rounded-sm, warm inset border.

`.color-swatch-name` — 13px medium primary. `.color-swatch-value` — 11px secondary mono.

### Hero Section

`.hero` — min-height 100svh, flex-centered, overflow hidden.

`.hero-bg` — absolute inset, three radial coral gradients at low opacity (ambient warmth).

`.hero-badge` — pill with pulsing coral dot and secondary text.

`.hero-title` — display font, clamp(36px, 7vw, 48px), display leading, negative tracking.

`.hero-subtitle` — 17px–18px clamp, secondary color, max-width 540px, centered.

### Section Layout

`.section` — 80px vertical padding. `.section-sm` — 48px.

`.section-overline` — 11px coral caps.

`.section-title` — display font, clamp(28px, 4vw, 36px), bold.

`.section-subtitle` — 17px secondary, max-width 580px.

### Grid / Flex Utilities

`.grid-2`, `.grid-3`, `.grid-4`, `.grid-auto` — CSS grid with 20px gap.

Responsive: grid-4 → 2 cols at ≤1024px. All grids → 1 col at ≤768px.

Flex utilities: `.flex`, `.flex-col`, `.flex-center`, `.flex-between`, `.flex-wrap`, `.items-center`, `.items-start`, `.flex-1`.

Gap utilities: `.gap-1` through `.gap-8`.

---

## `index.html` — Main Showcase Page

Link all four CSS files. Structure:

1. **Sticky navbar** — wordmark + centered nav links + model selector + user avatar
2. **Hero section** — `.hero` + `.hero-bg` + badge + gradient headline "Talk to Claude" + subtitle + two CTAs
3. **Component page nav** — pill links to all component pages
4. **Conversation demo** — realistic 3–4 exchange thread inside `.demo-conversation` chrome frame with model selector in header; includes attachment pill, input area with toolbar and send button, prompt suggestion chips, thinking indicator in last message
5. **Color palette** — `.swatch-grid` with all token colors, names, hex values
6. **Typography scale** — one `.type-row` per style showing the class rendered
7. **Buttons** — all variants, sizes, states, icon buttons, send button, button groups
8. **Model selector** — trigger variants + open dropdown
9. **Cards** — capability cards (grid-3), plan cards (grid-3), feature card, standard cards
10. **Forms** — all input states, textarea, select, checkboxes, radios, toggles
11. **Token usage meter** — all 3 states (normal, warning, critical)
12. **Settings panel** — grouped settings rows with icons and toggles
13. **File attachment pills** — 3–4 pill examples
14. **Badges** — all 5 variants + badge-dot
15. **Motion section** — thinking indicator, typing cursor, spinner (3 sizes), skeleton loading, coral pulse button, message entrance
16. **Toast demos** — all 4 variants static
17. **Footer** — "Anthropic · Claude Design System · MIT License"

**Rules:**
- Zero JS required. CSS-only interactivity (toggles via `:checked`, focus states).
- Mobile-first. Responsive at 768px and 1024px.
- Dark mode works automatically via `@media (prefers-color-scheme: dark)`.
- Use only class names from the CSS files — no custom one-off styles except for page layout scaffolding.

---

## Component Pages

Each in `components/`. All link to `../tokens.css`, `../typography.css`, `../animations.css`, `../components.css`.

**Shared anatomy:**
- Sticky `.page-header` with "← Back" link to `../index.html` and page title
- Main content area, max-width ~860–960px, centered
- `.showcase-label` (11px caps) before each group
- `.showcase-desc` (14px secondary) describing each group
- Horizontal rules between sections

### `buttons.html`

All button variants × all sizes × all states (default, hover, disabled, loading) × icon buttons × send button (enabled + disabled) × button groups.

Include a spec table per variant showing class names and height values.

### `cards.html`

- Capability cards — 6 cards in grid-3 with emoji icons and Claude-themed copy
- Plan cards — Free / Pro (featured) / Team in grid-3
- Feature cards — 2 across in grid-2 (Projects, Artifacts)
- Standard cards — header/body/footer anatomy, wide card spanning 2 cols, profile card
- Card grid auto-fill example

### `forms.html`

- Text input: default, focus, required, success, error, disabled
- Input size variants (sm/md/lg shown side by side)
- Textarea: default + error state
- Select with custom chevron
- Checkboxes (checked, unchecked, disabled)
- Radio group (3 options)
- iOS toggles with labels and descriptions
- Full conversation input area (attachment pill + input box + toolbar + chips)
- Complete account settings form combining all elements

### `navigation.html`

- Full navbar rendered inside a demo frame
- Sidebar: 560px tall demo frame showing projects, conversation list, section labels, new conversation button
- Tabs: underline style + artifact panel tab style
- Breadcrumbs: 3 examples
- Model selector: triggers + open dropdown side by side

### `modals.html`

- Alert dialog (delete confirmation) — springIn in demo box
- Informational/upgrade modal — in demo box
- Sheet modal (bottom sheet with handle, share form)
- Action sheet (5 items, last is destructive)
- Toast notifications — all 4 variants (default, success, error, warning)
- Token usage meter — all 4 states (normal, warning, critical, full)
- File attachment pills — 4 variants (PDF, DOCX, CSV, PNG)
- Thinking animation — in full message--assistant context + standalone
- Typing cursor — in message context + standalone
- Skeleton loading — 3 message shapes

---

## Quality Checklist

Before finalizing, verify:

- [ ] All CSS custom properties used in HTML exist in `tokens.css`
- [ ] All class names used in HTML exist in `components.css` or `typography.css`
- [ ] No `<link>` to CDN or external URL anywhere
- [ ] No `<script>` tags (system is CSS-only)
- [ ] Every interactive element has `aria-label` where no visible text
- [ ] Dark mode renders correctly (spot check bg, text, borders, coral)
- [ ] Mobile layout works — no horizontal overflow at 375px
- [ ] Reduced motion: animations collapse to near-instant
- [ ] All component page "Back" links point to `../index.html`
- [ ] `index.html` links to all 5 component pages
- [ ] `prompt.md` is self-contained — someone can hand it to Claude Code and get the full system back

---

*Claude Design System v1.0.0 — Anthropic*
