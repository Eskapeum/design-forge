# Design Forge

The definitive Claude Code skill for building Awwwards-winning websites. A 7-stage, research-driven pipeline with human feedback gates, a living Design Contract, and Stitch MCP integration — so every pixel is grounded in discovery, aligned with research, and enforced through to ship.

## What It Does

Design Forge combines:

1. **A 7-stage pipeline** with human gates at every step (no auto-advance)
2. **Discovery → Design Contract** — a living document that binds every subsequent decision
3. **Stitch MCP** as the generation engine (presets, design systems, variants, polish)
4. **8 on-demand reference files** loaded per stage to keep context tight
5. **Contract enforcement** — every Stitch output is validated against the contract before it reaches you

### The Pipeline

| Stage | Name | Engine | Gate |
|-------|------|--------|------|
| 0   | Discovery            | Conversational questions            | Is the Design Contract correct? |
| 0.5 | Design System        | Stitch preset + token architecture  | Approve preset, fonts, palette? |
| 1   | Research             | WebSearch + WebFetch                | Are these references the right inspiration? |
| 2   | Explore              | Stitch `generate_screen_from_text`  | Is this heading the right way? |
| 3   | Iterate              | Stitch `generate_variants`          | Which variant wins? |
| 4   | Refine               | Stitch `edit_screens`               | Ready to ship this screen? |
| 5   | Integrate            | Manual + Stitch baton to next page  | Move to next screen? |

The **Design Contract** (created in Stage 0) flows forward into every Stitch call as non-negotiable directives, and every Stitch result is validated against it before presentation.

### Reference Files (loaded on-demand)

| File | Used In |
|------|---------|
| `references/discovery-framework.md`         | Stage 0 — discovery questions, preset mapping, contract template |
| `references/design-system-architecture.md`  | Stage 0.5 — three-layer tokens, DTCG spec, DESIGN.md template |
| `references/typography-system.md`           | Stage 2+ — font pairings, type scales, loading strategy |
| `references/color-and-light.md`             | Stage 2+ — palettes, gradients, shadows, dark mode |
| `references/layout-and-spatial.md`          | Stage 2+ — grids, spacing, composition, responsive architecture |
| `references/motion-and-interaction.md`      | Stage 2+ — GSAP patterns, scroll animations, micro-interactions |
| `references/component-patterns.md`          | Stage 2+ — nav, hero, cards, CTAs, forms, footers |
| `references/performance-and-craft.md`       | Stage 4+ — performance budgets, accessibility, pre-launch audit |

## Install

### Option 1: Clone into the Claude Code skills directory

```bash
git clone https://github.com/Eskapeum/design-forge.git ~/.claude/skills/design-forge
```

### Option 2: Manual copy

Copy `SKILL.md` and the `references/` directory into `~/.claude/skills/design-forge/`.

## Usage

Once installed, the skill triggers automatically when you:

- Say "design this", "create mockup", "visual design", "design the UI", "landing page", "hero section", "website design", "page design", "site build", or "design forge"
- Have a `SITE.md` with unchecked pages
- Invoke `/design-forge` directly

Design Forge will run Stage 0 (Discovery) first, build your Design Contract, then walk you through every stage with an explicit gate before advancing.

## Prerequisites

- **Stitch MCP server** configured in Claude Code (this is the generation engine)
- **WebSearch / WebFetch** tools available (for Stage 1 research)
- **`DESIGN.md`** — created/updated during Stage 0.5 (token architecture + design system)
- **`SITE.md`** — sitemap/roadmap of pages to design (optional but recommended)
- **`.design-forge/stitch.json`** — auto-created by the skill to persist Stitch project + design-system IDs

> **Note:** SuperDesign is no longer part of the pipeline. Stitch MCP replaced it in v2.

## What Changed in v2

- Removed SuperDesign dependency — Stitch MCP is now the sole generation engine
- Added **Stage 0 Discovery** and **Stage 0.5 Design System** (preset + token architecture)
- Introduced the **Design Contract** as the binding artifact injected into every Stitch call
- Added **contract validation** after every Stitch output
- Expanded motion reference to GSAP-first patterns
- On-demand reference loading to keep context tight

## License

MIT
