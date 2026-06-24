# Claude Design Systems — Website Spec

A dedicated website for browsing, previewing, and contributing AI-generated design systems. The goal: become the canonical community resource for brand-faithful design systems built with Claude.

**Inspiration:** shadcn/ui (curation + copy-paste), Promptbase (prompt-as-artifact), FlowGPT (community browsing), Tailwind UI (polished component gallery)

**Differentiator:** Every system is generated with Claude, ships with the exact prompt used, and is purely HTML + CSS — no framework lock-in, no dependencies.

---

## Vision

> "If you can name the brand, we have its design system."

The site is a living gallery. Anyone can browse, fork, and remix. Anyone can submit a new brand via pull request. The Claude prompt that generated each system is shown transparently — the site teaches you *how* to build design systems with AI, not just *what* they look like.

---

## Pages & Routing

### `/` — Home / Gallery
- Hero: headline + subhead + search bar + "Submit a brand" CTA
- Filter bar: All · Tier 1 · Tier 2 · Dark-first · Light-first · Personal brand · Enterprise
- Card grid: one card per brand design system
  - Brand logo (CSS/SVG, no external images)
  - Brand name + short description
  - Preview thumbnail (screenshot.png)
  - Tags: dark-first, iOS-inspired, developer tool, etc.
  - "View system" button → detail page
  - "Open in Claude Code" button → copies Claude prompt to clipboard
- Footer: GitHub link, license, built-by

### `/[brand]` — Brand Detail Page
- Header: brand name, description, tags, last updated date
- Live iframe preview of `index.html` (embedded, full-width, toggleable light/dark)
- Toggle: Light / Dark mode preview switch
- Tabs: Overview · Components · Tokens · Prompt
  - **Overview tab:** screenshot gallery (light + dark + mobile), key design decisions, color palette swatches, type specimens
  - **Components tab:** scrollable component showcase (mirrors the `index.html` sections)
  - **Tokens tab:** rendered table of all CSS custom properties with their values
  - **Prompt tab:** the exact Claude Code prompt used to generate this system, with a "Copy prompt" button and "Open in Claude" deeplink
- Sidebar: download ZIP, view on GitHub, fork this system
- Related systems: 3 cards for similar-aesthetic brands

### `/contribute` — How to Contribute
- Step-by-step guide: research → build → PR
- Embedded CONTRIBUTING.md content (rendered Markdown)
- Link to GitHub issue template for requesting a new brand
- Gallery of recent community submissions

### `/about` — About the Project
- Origin story: the Apple design system blog post
- Philosophy: token-first, zero dependencies, brand accuracy over generic "good design"
- How Claude is used in the workflow
- Steve Scargall author bio + links

### `/blog` (optional phase 2)
- Host the blog post series directly on the site
- RSS feed

---

## Design System for the Website Itself

The website uses its own design system — the **Claude.ai system** (`Claude/`) once built. This is intentional and on-brand: the gallery site is itself a design system showcase.

Key decisions for the site's own UI:
- Background: warm cream `#FAF9F5` (light), deep brown-black `#1A1310` (dark)
- Accent: Claude coral `#DA7756`
- Font: system-ui, -apple-system fallback (no external fonts)
- Grid: 12-column, 80px max-width container (1280px)
- Card border-radius: 16px
- Sticky frosted-glass header

---

## Tech Stack Options

### Option A: Pure Static HTML (Recommended for launch)
- The site itself is HTML + CSS + vanilla JS — no framework
- One `index.html` per page, shared `site.css`
- Deployed to GitHub Pages (free, instant, no build step)
- Pros: consistent with the project's philosophy, zero dependencies, fast
- Cons: harder to scale past ~20 brands without templating

### Option B: Eleventy (11ty) — Preferred if templating needed
- Static site generator, minimal JS, outputs plain HTML
- Brand data in JSON/YAML → Nunjucks templates → static HTML
- Deployed to Vercel or GitHub Pages
- Pros: DRY templates, easy to add 50+ brands, RSS built-in
- Cons: adds a build step (contradicts zero-dependency ethos for *content*, but not the *generator*)

### Option C: Astro
- Component islands, excellent for partial interactivity (live preview iframe toggle)
- Outputs static HTML by default
- Good middle ground between Option A and a full framework

**Recommendation:** Start with Option A (pure static) for launch speed. Migrate to Eleventy when the brand count exceeds 10 and template duplication becomes painful.

---

## Interactive Features

### Live Preview iframe
- Each brand detail page embeds `index.html` in a sandboxed iframe
- Light/Dark toggle: inject `data-theme="dark"` into the iframe's root element via `postMessage`
- Viewport toggle: Mobile (375px) / Tablet (768px) / Desktop (full-width)
- Resize handle: drag to any width

### Token Inspector
- Hover any component in the live preview → highlight its token names in a tooltip overlay
- Implementation: vanilla JS, reads computed CSS custom properties, maps to token names

### "Open in Claude" deeplink
- Button copies the generation prompt to clipboard
- Optionally: deeplink to `claude.ai/code?prompt=...` if Anthropic ever supports prompt URL params
- Show the prompt in a styled code block with syntax highlighting (CSS-only, no Prism)

### Search
- Client-side search across brand names, tags, and descriptions
- Instant filter — no server required
- Implementation: vanilla JS array filter on page load

### Community Submission Form
- Links to GitHub "new issue" with the brand request template pre-filled
- No server-side form processing needed at launch

---

## Content Strategy

### Each brand page needs
- `screenshot.png` — 1400×900, light mode, from the brand's `index.html`
- `screenshot-dark.png` — 1400×900, dark mode
- `screenshot-mobile.png` — 390×844, light mode
- `meta.json` — brand metadata (see schema below)
- `prompt.md` — the Claude Code prompt used to generate the system

### meta.json schema
```json
{
  "name": "Apple",
  "slug": "apple",
  "description": "iOS 18 and apple.com — SF Pro, frosted glass, neutral palette with vibrant accents",
  "tags": ["ios", "frosted-glass", "light-first", "consumer"],
  "tier": 1,
  "darkFirst": false,
  "accentColor": "#007AFF",
  "surfaceColor": "#F5F5F7",
  "fontStack": "-apple-system, BlinkMacSystemFont, SF Pro Display",
  "status": "complete",
  "addedDate": "2026-06-24",
  "contributors": ["sscargal"],
  "referenceUrl": "https://apple.com"
}
```

---

## Launch Checklist

- [ ] Decide on tech stack (Option A recommended)
- [ ] Design the site using the Claude.ai design system
- [ ] Build home/gallery page with Apple system as first card
- [ ] Build brand detail page with live iframe preview
- [ ] Write `meta.json` for Apple system
- [ ] Write `prompt.md` for Apple system (the actual prompt)
- [ ] Add screenshots for Apple (light + dark + mobile)
- [ ] Build `/contribute` page
- [ ] Build `/about` page with origin story
- [ ] Deploy to GitHub Pages at `sscargal.github.io/ClaudeDesignSystems`
- [ ] (Optional) Custom domain: `claudedesignsystems.com` or `designsystems.ai`
- [ ] Submit to Product Hunt
- [ ] Post on Hacker News: "Show HN: A gallery of brand-faithful design systems built with Claude"
- [ ] Submit to Designer News, CSS-Tricks weekly links, Sidebar.io
- [ ] Cross-post blog post to dev.to and Medium

---

## Growth / Virality Mechanics

1. **"Built with Claude" badge** — embed-in-your-site badge linking back to the gallery
2. **Monthly brand challenge** — community votes on the next brand to add; winner gets a tutorial post
3. **"Remix" button** — one-click to open a system in Claude Code with a starter prompt
4. **Contributor wall** — GitHub avatars of everyone who submitted a system
5. **Twitter/X card** — og:image shows a 3-up of the brand's light/dark/mobile screenshots
6. **GitHub star goal** — public star counter on the site with milestone callouts (100 ⭐, 500 ⭐, 1K ⭐)
