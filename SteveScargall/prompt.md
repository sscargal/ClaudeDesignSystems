# Steve Scargall Design System — Generation Prompt

## Site Research Status

WebFetch was unavailable during generation. The design system was constructed using a
well-reasoned brand model for Steve Scargall based on publicly known information about him:

- Senior Technology Executive
- Author of *Programming Persistent Memory* (Apress, 2020, co-author)
- NVIDIA Fellow
- Persistent Memory Development Kit (PMDK) ecosystem contributor
- CXL Consortium engagement
- Topics: AI, Memory Computing, CXL Architecture, PMDK, NVIDIA, Open Source, Performance Engineering
- Personal site: stevescargall.com

## Brand Personality

**Developer-forward. Technically rigorous. Authoritative but approachable.**

The aesthetic is that of a respected technical author who writes for senior engineers.
It avoids marketing fluff — every element earns its place through clarity.
Dark mode is the preferred aesthetic (technical audiences default to dark terminals and editors).
Light mode is clean and professional, appropriate for conference slides and formal contexts.

## Color System

### Primary Palette (Light Mode)

| Token                    | Value     | Usage                              |
|--------------------------|-----------|-------------------------------------|
| `--color-accent`         | `#0070F3` | Primary interactive elements, links |
| `--color-accent-hover`   | `#005CC5` | Hover state for accent elements     |
| `--color-teal`           | `#06B6D4` | Secondary accent, code elements     |
| `--color-deep-blue`      | `#1E3A8A` | Gradient anchor, hero backgrounds   |
| `--color-indigo`         | `#6366F1` | Code highlights, technical accents  |
| `--color-bg-primary`     | `#FAFBFC` | Main background (warm off-white)    |
| `--color-bg-secondary`   | `#FFFFFF` | Card and surface backgrounds        |
| `--color-bg-code`        | `#0D1117` | Code block backgrounds (GitHub dark)|
| `--color-bg-terminal`    | `#1A1A2E` | Terminal block backgrounds          |
| `--color-label-primary`  | `#0F172A` | Primary text (Slate 900)            |
| `--color-label-secondary`| `#475569` | Secondary text (Slate 600)          |
| `--color-label-tertiary` | `#94A3B8` | Muted text, timestamps, captions    |

### Primary Palette (Dark Mode)

| Token                    | Value     | Usage                                        |
|--------------------------|-----------|----------------------------------------------|
| `--color-bg-primary`     | `#0A0F1E` | Deep space navy main background              |
| `--color-bg-secondary`   | `#0F172A` | Slate 900 secondary background               |
| `--color-bg-tertiary`    | `#1E293B` | Card backgrounds                             |
| `--color-accent`         | `#3B9EFF` | Brightened blue for dark background contrast |
| `--color-teal`           | `#22D3EE` | Brightened teal                              |
| `--color-label-primary`  | `#F1F5F9` | Near-white text                              |
| `--color-label-secondary`| `#94A3B8` | Muted slate text                             |

### Topic Tag Colors

| Topic         | Color     | Background Token             |
|---------------|-----------|------------------------------|
| AI / ML       | `#7C3AED` | `--color-tag-ai-bg`          |
| Memory        | `#0891B2` | `--color-tag-memory-bg`      |
| CXL           | `#0070F3` | `--color-tag-cxl-bg`         |
| Open Source   | `#10B981` | `--color-tag-opensource-bg`  |
| Performance   | `#F59E0B` | `--color-tag-performance-bg` |
| NVIDIA        | `#76B900` | `--color-tag-nvidia-bg`      |

## Typography

### Font Stack

- **Display / UI**: Inter → SF Pro Display → system-ui → -apple-system → Helvetica → Arial
- **Body / Prose**: Inter → SF Pro Text → system-ui → -apple-system → Helvetica → Arial
- **Code / Mono**: JetBrains Mono → Fira Code → Cascadia Code → ui-monospace → SF Mono → Menlo → Consolas

**No external CDN imports.** System fallbacks ensure the design system works with zero network dependency.
If Inter or JetBrains Mono are installed on the local machine, they will be used automatically.

### Type Scale

| Token          | Size  | Usage                                           |
|----------------|-------|-------------------------------------------------|
| `--text-7xl`   | 72px  | Display hero — design system showcase only      |
| `--text-6xl`   | 60px  | Hero headline                                   |
| `--text-5xl`   | 48px  | H1, page title, post title featured             |
| `--text-4xl`   | 40px  | H2, section headings, post title                |
| `--text-3xl`   | 32px  | H3, featured card titles                        |
| `--text-2xl`   | 26px  | H4, pullquote text                              |
| `--text-xl`    | 22px  | H5, lead text, author name                      |
| `--text-lg`    | 19px  | H6, body emphasis                               |
| `--text-md`    | 17px  | Body copy (blog article reading size)           |
| `--text-base`  | 16px  | Standard UI text                                |
| `--text-sm`    | 13px  | Captions, metadata, navigation links            |
| `--text-xs`    | 11px  | Labels, tags, timestamps, uppercase caps        |

### Reading Metrics

- **Article body size**: 17px
- **Article line-height**: 1.75 (`--leading-article`)
- **Article max-width**: 720px (`--max-width-content`)
- **Body line-height**: 1.50 (`--leading-normal`)

## Spacing

4px base grid. Key spacings:
- `--space-6` (24px) — standard padding for cards and sections
- `--space-8` (32px) — section internal gaps
- `--space-12` (48px) — vertical section padding
- `--space-16` (64px) — major section separation
- `--space-20` (80px) — hero padding

## Border Radius

Developer/tech aesthetic — moderate, not overly rounded:

| Token          | Value  | Usage                    |
|----------------|--------|--------------------------|
| `--radius-sm`  | 4px    | Tags, inline code        |
| `--radius-md`  | 6px    | Code blocks, small UI    |
| `--radius-lg`  | 8px    | Buttons, inputs          |
| `--radius-xl`  | 12px   | Cards, form wrappers     |
| `--radius-2xl` | 16px   | Featured cards, modals   |
| `--radius-pill`| 9999px | Badges, avatar circles   |

## Shadow System

Subtle, professional — shadows communicate depth, not decoration:

```
--shadow-sm:   0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04)
--shadow-md:   0 4px 12px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.04)
--shadow-lg:   0 8px 24px rgba(0,0,0,0.09), 0 4px 8px rgba(0,0,0,0.05)
--shadow-accent: 0 8px 32px rgba(0,112,243,0.22)
--shadow-focus:  0 0 0 3px rgba(0,112,243,0.25)
```

Dark mode shadows are significantly stronger to maintain visual separation against dark surfaces.

## Motion

Professional, purposeful — never decorative:

| Token               | Value  | Usage                                      |
|---------------------|--------|--------------------------------------------|
| `--duration-fast`   | 150ms  | Hover states, button presses               |
| `--duration-normal` | 200ms  | Transitions, dropdown opens                |
| `--duration-moderate`| 300ms | Cards, panels, reveals                     |
| `--duration-slow`   | 400ms  | Image zooms, page transitions              |

All animations include `prefers-reduced-motion: reduce` overrides that eliminate movement.

## Layout

| Token                 | Value  | Usage                                   |
|-----------------------|--------|-----------------------------------------|
| `--max-width-content` | 720px  | Article reading column                  |
| `--max-width-site`    | 960px  | Standard page width                     |
| `--max-width-wide`    | 1200px | Wide layout (site nav, grids)           |
| `--nav-height`        | 64px   | Sticky nav height                       |

Breakpoints: 480px (mobile-sm), 640px (mobile), 768px (tablet), 1024px (desktop).
Grid collapses: 3-col → 2-col at 1024px → 1-col at 768px.

## Components

### Blog Post Card (.post-card)
The primary content unit. Three variants:
- `.post-card` — standard 3-column grid card with 16:9 image, tags, title, excerpt, byline, read more
- `.post-card--featured` — full-width 2-column layout, image left / content right, larger title
- `.post-card--compact` — horizontal list layout, small thumbnail, 2-line excerpt

Card image uses CSS gradient placeholders themed per topic category (AI: purple, CXL: blue, memory: navy-to-cyan, open source: green, performance: amber, NVIDIA: green).

### Author Bio Block (.author-bio)
Three variants: standard (row), inline (compact for post footer), hero (about page, centered).
All use a CSS gradient circle as avatar placeholder with "SS" initials.

### Tags (.tag)
Six topic-specific color variants: `--ai`, `--memory`, `--cxl`, `--opensource`, `--performance`, `--nvidia`.
Plus `--active` (filled accent) and `--link` (interactive pointer).

### Code Block (.code-block)
GitHub-dark themed (`#0D1117`). macOS traffic light dots, language label, copy button.
Syntax token classes: `.kw`, `.str`, `.num`, `.cmt`, `.fn`, `.cls`, `.op`, `.pun`, `.var`, `.type`, `.macro`.
Supports `.code-block--lined` for line numbers via CSS table layout.
Companion `.terminal-block` uses deep navy (`#1A1A2E`) with prompt, cmd, output, success, error classes.

### Newsletter Card (.newsletter-card)
Full-width gradient card (deep blue → accent blue → teal) with decorative circle overlays.
Inline form with transparent input on gradient background, white submit button.

### Site Navigation (.site-nav)
Sticky, glassmorphism backdrop (blur + saturate). Height 64px. Dark/light mode toggle.
Mobile: hamburger menu, nav links slide down with animation.

## File Structure

```
SteveScargall/
├── index.html          — Full showcase of all components
├── tokens.css          — CSS custom properties (light + dark mode)
├── typography.css      — Type scale, prose, links, blockquotes, inline code
├── components.css      — All component styles
├── animations.css      — Keyframes, scroll reveal, skeleton shimmer
├── prompt.md           — This file
└── components/
    ├── buttons.html    — Button variants showcase
    ├── cards.html      — Post card variants showcase
    ├── forms.html      — Form component showcase
    ├── navigation.html — Nav, breadcrumb, TOC, social links showcase
    └── modals.html     — Modal and toast showcase (with live JS demos)
```

## Brand Logo

SVG wordmark using "SS" initials in a rounded rectangle with the brand gradient
(deep blue `#1E3A8A` → accent blue `#0070F3` → teal `#06B6D4`).
Implemented as inline SVG in `.brand-logo-mark` with accompanying `.brand-logo-wordmark`
containing `.brand-logo-name` ("Steve Scargall") and `.brand-logo-tagline` ("Memory · AI · Open Source").

## JavaScript (index.html)

Minimal vanilla JS — no frameworks or libraries:
1. **Theme toggle** — reads/writes `data-theme` on `<html>`, persists to `localStorage`
2. **Nav scroll shadow** — adds `.scrolled` class when `window.scrollY > 20`
3. **Scroll progress bar** — updates `width` of `.scroll-progress-bar` based on page scroll
4. **Mobile hamburger** — toggles `.open` class on `.site-nav-links`, manages `aria-expanded`
5. **Scroll reveal** — `IntersectionObserver` adds `.is-visible` to `.reveal` elements at 12% threshold

## Generation Date

2026-06-24

## Generated By

Claude Sonnet 4.6 — Steve Scargall Design System v1.0.0
