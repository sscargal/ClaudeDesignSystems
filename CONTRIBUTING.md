# Contributing to Claude Design Systems

Thank you for your interest in contributing! This project is a community collection of brand-faithful design systems built with Claude AI. Every contribution helps make it a richer learning resource.

---

## Ways to Contribute

- **Add a new brand design system** — the most impactful contribution
- **Improve an existing system** — fix inaccuracies, add missing components, improve dark mode
- **Report issues** — broken layouts, wrong colors, inaccessible components
- **Improve documentation** — clearer explanations, better code comments

---

## Adding a New Brand Design System

### 1. Check for duplicates
Look at the [README](./README.md) table and open issues to make sure no one is already working on the same brand.

### 2. Open an issue first
Before building, open an issue titled `[Brand] Add XYZ design system`. This lets maintainers confirm the brand is appropriate and avoids duplicated effort.

### 3. Research the brand
- Study the brand's current live website thoroughly
- Look for any public design documentation or style guides
- Extract exact hex values from computed styles in DevTools
- Note the typeface, spacing rhythm, signature components

### 4. Create the directory structure

```
BrandName/
├── index.html
├── tokens.css
├── typography.css
├── components.css
├── animations.css
└── components/
    ├── buttons.html
    ├── cards.html
    ├── forms.html
    ├── navigation.html
    └── modals.html
```

### 5. Follow the standards

**Required:**
- Zero external dependencies (no CDN, no npm, no Google Fonts)
- Full dark mode support via `prefers-color-scheme`
- Mobile responsive (768px, 1024px breakpoints)
- Token-first: all values in `tokens.css` as CSS custom properties
- `prefers-reduced-motion` respected in all animations
- Semantic HTML5 throughout

**File order in `index.html`:**
```html
<link rel="stylesheet" href="tokens.css">
<link rel="stylesheet" href="typography.css">
<link rel="stylesheet" href="animations.css">
<link rel="stylesheet" href="components.css">
```

### 6. Open a Pull Request

PR title: `Add [Brand] design system`

PR description must include:
- A screenshot of `index.html` in light mode (1400×900px ideal)
- A screenshot in dark mode
- Brief note on any brand-specific decisions or tradeoffs

---

## Improving an Existing System

1. Open an issue describing what's inaccurate or missing
2. Reference the specific component or token
3. If you have a fix, link to a screenshot comparison (brand website vs. current system)
4. Submit a PR with targeted changes — avoid rewriting unrelated parts

---

## Code Style

- CSS: 2-space indent, one property per line
- HTML: 2-space indent, semantic elements preferred
- Token names: `--category-variant-modifier` (e.g., `--color-blue-primary`, `--space-16`, `--shadow-large`)
- Component classes: `.component`, `.component--modifier`, `.component--size` (BEM-ish)
- No minification — readability is the goal

---

## What We Don't Accept

- Systems that use external dependencies (fonts, icons, frameworks)
- Purely hypothetical brands with no real reference website
- Copyrighted brand assets (logos as image files, etc.) — use CSS/SVG recreations only
- AI-slop: placeholder text, TODO comments, incomplete implementations

---

## License

By submitting a PR, you agree that your contribution is licensed under the project's [MIT License](./LICENSE).

---

Questions? Open an issue or reach out to [Steve Scargall](https://stevescargall.com).
