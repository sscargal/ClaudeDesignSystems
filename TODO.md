# TODO — Claude Design Systems

Tracking all planned design systems and the companion website. Check off items as they ship.

---

## Design Systems

### Tier 1 — High Impact (Build These First)

- [x] **Nike** `Nike/`
  - Aesthetic: kinetic, aggressive, full-bleed — maximum contrast to Apple
  - Typography: Futura Bold / Trade Gothic condensed, extreme weight contrast
  - Colors: Pure black `#111111`, white `#FFFFFF`, Nike volt `#CFFC03`, sport red
  - Signature components: full-bleed hero with overlay text, product card with hover zoom, scrolling marquee ticker, split-screen layouts, large CTA with underline animation
  - Dark-first: yes — black canvas is the default
  - Reference: nike.com

- [x] **Linear** `Linear/`
  - Aesthetic: developer cult favorite, dark-first, keyboard-centric, ultra-minimal
  - Typography: Inter, tight tracking, monospace accents for metadata
  - Colors: Deep black `#0F0F11`, Linear purple `#5E6AD2`, muted surface grays, subtle borders
  - Signature components: issue row list (priority icon + title + meta), command palette (⌘K style), cycle/sprint sidebar, breadcrumb trail, keyboard shortcut badges, progress rings, inline status chips
  - Dark-first: yes — light mode is secondary
  - Reference: linear.app

- [x] **Stripe** `Stripe/`
  - Aesthetic: B2B gold standard — precision prose, pastel gradient heroes, polished data
  - Typography: Sohne (system fallback: Inter), careful line-length control, well-spaced body
  - Colors: Blurple `#635BFF`, soft indigo gradients, white canvas, precise gray scale
  - Signature components: gradient mesh hero, API code block (multi-language tab switcher), pricing table, transaction data table with status pills, dashboard sidebar, terminal-style log viewer
  - Dark-first: no — light canvas with optional dark code blocks
  - Reference: stripe.com, stripe.com/docs

- [x] **Claude.ai** `Claude/`
  - Aesthetic: Anthropic brand — warm neutrals, conversation-first UI, calm and intelligent
  - Typography: Styrene (fallback: system-ui), generous line-height, high legibility
  - Colors: Claude orange-coral `#DA7756`, warm cream `#FAF9F5`, deep brown-black `#1A1310`, muted sand tones
  - Signature components: conversation thread (human + assistant bubbles), model selector dropdown, artifact panel (side-by-side code/preview), prompt suggestion chips, thinking animation (animated dots), file attachment pill, token usage meter
  - Dark-first: both — Claude has excellent light/dark parity
  - Reference: claude.ai

### Tier 2 — Broader Audience

- [x] **Microsoft Fluent** `Microsoft/`
  - Aesthetic: Fluent Design 2 — Acrylic/Mica materials, depth layers, Windows 11 language
  - Typography: Segoe UI Variable, clear hierarchy, dense information
  - Colors: Microsoft blue `#0078D4`, Fluent neutrals, semantic color system (success/warning/error/info)
  - Signature components: Acrylic sidebar (blur + tint), Reveal highlight (mouse-tracking border glow), Pivot/tab control, Fluent dialog, command bar, breadcrumb + back button, adaptive cards, data grid
  - Dark-first: both — Windows respects system preference
  - Reference: fluent2.microsoft.design, microsoft.com

- [x] **Google Material You** `Google/`
  - Aesthetic: Material Design 3 — dynamic color, adaptive surfaces, expressive motion
  - Typography: Google Sans / Roboto, Material type scale (Display → Label)
  - Colors: Dynamic tonal palette (primary, secondary, tertiary, surface, error tones) — simulate with a fixed seed color
  - Signature components: FAB (Floating Action Button), Navigation bar, Navigation rail, Bottom sheet, Chips (assist/filter/input/suggestion), Snackbar, Card (elevated/filled/outlined), M3 TextField, Segmented button
  - Dark-first: both — M3 has robust dark semantics
  - Reference: m3.material.io

- [x] **Vercel** `Vercel/`
  - Aesthetic: minimal, dark-first, developer-focused, precision whitespace
  - Typography: Geist (custom, fallback: Inter), monospace for paths/code, clean hierarchy
  - Colors: Pure black `#000000`, white `#FFFFFF`, Vercel teal `#50E3C2`, muted gray `#888888`
  - Signature components: deployment status row (git branch + status chip + domain), project card with live preview thumbnail, CLI output terminal, framework icon grid, edge network globe, speed insight meter
  - Dark-first: yes
  - Reference: vercel.com

- [x] **Notion** `Notion/`
  - Aesthetic: content-first, block editor, soft neutrals, almost invisible chrome
  - Typography: ui-sans-serif fallback, medium weight, generous line-height, emoji-friendly
  - Colors: Soft white `#FFFFFF`, light gray surfaces, Notion black `#191919`, 8 block colors (gray/brown/orange/yellow/green/blue/purple/pink)
  - Signature components: block editor row (drag handle + type switcher + content), page header with cover + icon, inline database (table/board/gallery views), callout block (emoji + colored background), toggle block, comment thread, sidebar page tree
  - Dark-first: both
  - Reference: notion.so

### Tier 3 — Personal & Niche

- [ ] **Steve Scargall Personal Brand** `SteveScargall/`
  - Source: stevescargall.com
  - Extract: actual colors, fonts, and component patterns from the live site
  - Components: blog post card, author bio block, tech tag pills, code snippet block, newsletter signup
  - Note: scrape site before building to ensure accuracy

- [ ] **Liqid** `Liqid/`
  - Source: liqid.com
  - Aesthetic: enterprise storage/compute — precision engineering, data-dense, technical credibility
  - Extract: actual brand colors, typography from live site
  - Components: product spec table, rack unit diagram (CSS-drawn), performance metrics dashboard, enterprise nav with mega-menu, data sheet download card

### Stretch Goals

- [ ] **GitHub** `GitHub/` — Primer design system, developer-native, Markdown-heavy
- [ ] **Tailwind UI** `Tailwind/` — utility-class aesthetic translated to vanilla CSS tokens
- [ ] **Figma** `Figma/` — multiplayer-product design, bold color, clean tool chrome
- [ ] **Arc Browser** `Arc/` — gradient identity, sidebar-first, personal computing revival
- [ ] **Resend** `Resend/` — email API, minimal dark, developer micro-brand done right
- [ ] **Raycast** `Raycast/` — launcher aesthetic, dark + blur, command palette culture

---

## Companion Website

A dedicated site for browsing, previewing, and contributing design systems — think shadcn/ui meets Promptbase, purpose-built for Claude-generated design systems.

See [WEBSITE.md](./WEBSITE.md) for the full spec.

**Status:** Planning

- [ ] Define tech stack (see WEBSITE.md)
- [ ] Design the site's own design system (self-referential — use the Claude.ai system)
- [ ] Build gallery index page
- [ ] Build individual system detail/preview page
- [ ] Build contribute / submission flow
- [ ] Set up GitHub Pages or Vercel deployment
- [ ] Write launch blog post
- [ ] Submit to Hacker News, Product Hunt, Designer News

---

## Blog Post Series

- [ ] **Post 1:** "I built Apple's design system with one Claude prompt" — Apple system, process walkthrough, before/after
- [ ] **Post 2:** "Nike vs Apple: How brands translate into CSS" — contrast two opposing aesthetics
- [ ] **Post 3:** "Building a design system for your personal brand with AI" — Steve Scargall system, personal brand process
- [ ] **Post 4:** "The meta post: a Claude design system built in Claude" — Claude.ai system
- [ ] **Post 5:** "Open-sourcing a gallery of AI-generated design systems" — website launch post

---

## Repo Hygiene

- [ ] Add `screenshot.png` (1400×900, light mode) to each completed design system directory
- [ ] Add `screenshot-dark.png` (1400×900, dark mode) to each completed design system directory
- [ ] Update README.md table as each system completes
- [ ] Set up GitHub Actions to validate HTML on PR (htmlhint or similar)
- [ ] Add issue templates: `new-brand.md`, `bug-report.md`, `improvement.md`
- [ ] Add PR template with screenshot checklist
- [ ] Tag first release `v1.0.0` once 4 systems are complete
- [ ] Set up GitHub Discussions for community brand requests
