# Claude Design Systems

A growing collection of high-fidelity design systems built with Claude AI — each one faithfully replicating the aesthetic, component language, and visual identity of a world-class brand.

Every system is self-contained HTML + CSS: no frameworks, no build tools, no dependencies. Open the file and it works.

---

## What's Inside

| Brand | Aesthetic | Status |
|-------|-----------|--------|
| [Apple](./Apple/) | Apple.com · iOS 18 — SF Pro, frosted glass, neutral palette | ✅ Complete |
| [Nike](./Nike/) | nike.com — kinetic, sharp, dark-first, volt accent | ✅ Complete |
| [Linear](./Linear/) | linear.app — dark-first, developer-minimal, purple | ✅ Complete |
| [Stripe](./Stripe/) | stripe.com — light-first, financial precision, blurple | ✅ Complete |
| [Claude](./Claude/) | claude.ai — warm neutrals, conversation UI, coral | ✅ Complete |
| [Microsoft](./Microsoft/) | Fluent Design 2 — Acrylic/Mica, Windows 11 depth | ✅ Complete |
| [Google](./Google/) | Material You M3 — dynamic color, tonal palettes | ✅ Complete |
| [Vercel](./Vercel/) | vercel.com — pure black, minimal, developer-focused | ✅ Complete |
| [Notion](./Notion/) | notion.so — content-first, warm off-white, block editor | ✅ Complete |
| [NVIDIA](./NVIDIA/) | nvidia.com — dark-first, NVIDIA green, GPU cards, AI/gaming | ✅ Complete |
| [Intel](./Intel/) | intel.com — light-first, Intel Blue, enterprise CPU precision | ✅ Complete |
| [AMD](./AMD/) | amd.com — dark-first, AMD Red, 4 sub-brands (Ryzen/EPYC/Radeon/Instinct) | ✅ Complete |
| [Steve Scargall](./SteveScargall/) | Personal brand — dark navy, blog post cards, code blocks, author bio | ✅ Complete |
| [Liqid](./Liqid/) | liqid.com — enterprise composable infrastructure, rack diagram, metrics | ✅ Complete |

---

## How Each Design System Is Structured

```
BrandName/
├── index.html          — Live showcase & component gallery
├── tokens.css          — Design tokens (colors, spacing, radius, motion)
├── typography.css      — Type scale and font rules
├── components.css      — All component styles
├── animations.css      — Keyframe animations and transitions
└── components/
    ├── buttons.html    — Button variants
    ├── cards.html      — Card patterns
    ├── forms.html      — Form elements
    ├── navigation.html — Nav patterns
    └── modals.html     — Modals, sheets, toasts
```

Each system:
- Uses only system fonts — no CDN, no external assets
- Supports light **and** dark mode via `prefers-color-scheme`
- Is fully responsive (mobile-first, 768px / 1024px breakpoints)
- Demonstrates interactive states (hover, focus, active, disabled)

---

## Viewing Locally

```bash
git clone https://github.com/sscargal/ClaudeDesignSystems.git
cd ClaudeDesignSystems
open Apple/index.html   # macOS
```

Or serve with any static file server:

```bash
npx serve .
python3 -m http.server 8080
```

---

## How These Were Built

Every design system in this repo was created using [Claude](https://claude.ai) (Anthropic's AI) via [Claude Code](https://claude.ai/code). The process:

1. Describe the brand's aesthetic — typography, color philosophy, component patterns
2. Claude generates a complete token-first design system from scratch
3. Review, refine, and extend

This repo accompanies a blog post series on building brand-faithful design systems with AI. Each system is a standalone learning artifact — read the CSS as documentation, fork and remix freely.

---

## Contributing

Contributions are very welcome. To add a new brand design system:

1. Fork the repo
2. Create a new directory: `BrandName/`
3. Follow the file structure above
4. Open a PR with a screenshot of your `index.html`

To improve an existing system, open an issue describing what's missing or inaccurate.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for full guidelines.

---

## Philosophy

> "Good design systems don't prescribe — they enable."

These systems are reference implementations, not production libraries. They're meant to teach visual reasoning: how a brand's values translate into spacing decisions, type choices, motion behavior, and color relationships.

---

## License

MIT — use freely, attribute appreciated.

---

Built with [Claude Code](https://claude.ai/code) · By [Steve Scargall](https://stevescargall.com)
