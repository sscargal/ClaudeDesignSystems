# Claude Design Systems — CLAUDE.md

This file tells Claude Code how to work effectively in this repository.

---

## Project Overview

This repo is a collection of brand-faithful design systems — each one replicating the aesthetic and component language of a world-class brand, built entirely with HTML and CSS (no frameworks, no build step).

**Owner:** Steve Scargall (steve.scargall@gmail.com)  
**Blog post in progress:** Documenting the process of building each system with Claude Code.

---

## Repository Structure

```
ClaudeDesignSystems/
├── BrandName/              — One directory per brand
│   ├── index.html          — Main showcase (self-contained)
│   ├── tokens.css          — CSS custom properties only
│   ├── typography.css      — Type scale
│   ├── components.css      — All components
│   ├── animations.css      — Keyframes + transitions
│   └── components/         — Individual component showcases
│       ├── buttons.html
│       ├── cards.html
│       ├── forms.html
│       ├── navigation.html
│       └── modals.html
├── README.md
├── CLAUDE.md               — This file
└── CONTRIBUTING.md
```

---

## Standards for Every Design System

### Non-Negotiable Rules
- **Zero external dependencies.** No CDN links, no npm packages, no Google Fonts. System fonts only.
- **Self-contained HTML.** Each `index.html` works by opening the file directly in a browser.
- **Token-first.** All values (color, spacing, radius, shadow, duration) must be defined as CSS custom properties in `tokens.css` and referenced everywhere else.
- **Dark mode required.** Use `@media (prefers-color-scheme: dark)` on the `:root` block in `tokens.css`.
- **Responsive.** Mobile-first. Breakpoints at 768px and 1024px minimum.
- **Accessible.** Semantic HTML5, meaningful focus states, sufficient color contrast.
- **`prefers-reduced-motion`.** All animations must be suppressed or reduced when this media query fires.

### CSS Architecture
1. `tokens.css` — Custom properties ONLY. No selectors other than `:root` and `[data-theme]`.
2. `typography.css` — Type classes only. Imports nothing.
3. `animations.css` — `@keyframes` and animation utility classes only.
4. `components.css` — All component classes. References tokens via `var(--token-name)`.
5. `index.html` links all four in that order.

### Naming Conventions
- Tokens: `--color-blue-primary`, `--space-4`, `--radius-pill`, `--shadow-medium`, `--duration-300`
- Component classes: BEM-ish — `.btn`, `.btn--primary`, `.btn--lg`, `.card`, `.card--glass`
- Animation classes: `.animate-fade-in`, `.animate-slide-up`, `.delay-200`

---

## Adding a New Brand

When adding a new brand design system:

1. Research the brand's current website and any public design documentation
2. Identify: primary typeface, color palette (hex values), spacing philosophy, signature components
3. Create `BrandName/` directory following the structure above
4. Start with `tokens.css` — get all values defined before writing any components
5. Update `README.md` table to mark the new brand as ✅ Complete
6. Add a screenshot to `BrandName/screenshot.png` (1400×900px, light mode)

### Brands Planned
- [ ] Nike — bold, high-contrast, kinetic typography
- [ ] Microsoft — Fluent Design, Acrylic material, depth layers
- [ ] Claude.ai — Anthropic brand language, warm neutrals, AI-first
- [ ] Steve Scargall personal brand — stevescargall.com
- [ ] Liqid — enterprise storage tech, precision engineering aesthetic
- [ ] Google Material You — dynamic color, adaptive surfaces
- [ ] Stripe — financial precision, clean data tables
- [ ] Linear — developer tool aesthetic, dark-first, keyboard-centric
- [ ] Vercel — minimal, dark, developer-focused

---

## Claude-Specific Guidance

### When building a new design system
- Always read the brand's live website before starting (use WebFetch or WebSearch)
- Extract exact hex colors from the site if possible — don't guess
- Match the brand's actual typeface fallback stack
- Prioritize brand accuracy over generic "good design"

### When updating an existing system
- Never change token values without checking all component references
- Test dark mode after every token change
- Keep `components.css` file size reasonable — split into multiple files if over ~2000 lines

### File writing
- Always write complete files — no truncation, no placeholders, no TODO comments
- Write the showcase HTML last, after all CSS is finalized
- Every component in `components.css` must appear in the matching `index.html` showcase section

### What NOT to do
- Don't add JavaScript frameworks (vanilla JS only, and sparingly)
- Don't reference external fonts, icons, or images
- Don't use CSS preprocessors or variables that require compilation
- Don't create build scripts — this repo has no build step by design

---

## Blog Post Context

Steve is writing a blog post series documenting how to build brand-faithful design systems using Claude Code. The repo is the companion artifact. Each design system should be self-explanatory from reading the code — the CSS itself is the documentation.

Key themes for the blog:
- Token-first design workflow
- How to read a brand from its website
- The role of AI in design systems work
- Community contribution model

---

## Git Workflow

- Branch naming: `add/brand-name` for new systems, `fix/brand-name-issue` for fixes
- Commit messages: imperative, lowercase, no period — e.g. `add Nike design system`
- PRs require a screenshot in the description
- `main` branch is always deployable
