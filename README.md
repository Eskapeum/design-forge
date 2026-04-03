# Design Forge

The definitive Claude Code skill for building Awwwards-winning websites. Combines a 5-stage research-driven workflow with comprehensive design standards, quality gates, and craft principles.

## What It Does

Design Forge is a complete design system that merges:

1. **A 5-stage pipeline** with human feedback gates at every stage
2. **Comprehensive design standards** governing every visual decision
3. **6 deep-reference files** for specific design domains
4. **Quality enforcement** — nothing ships without meeting the bar

### The Forge Pipeline

| Stage | Tool | Gate |
|-------|------|------|
| 1. Research | WebSearch + WebFetch | Are these 4 references the right inspiration? |
| 2. Explore | SuperDesign `create-design-draft` | Is this heading the right way? |
| 3. Iterate | SuperDesign `iterate-design-draft` | Which design wins? |
| 4. Generate | Stitch `generate_screen_from_text` | Does the HTML match the design? |
| 5. Integrate | Manual + Stitch baton | Ready to move to next screen? |

### Reference Files

| File | Domain |
|------|--------|
| `references/typography-system.md` | Font pairings, type scales, loading strategy |
| `references/color-and-light.md` | Palettes, gradients, shadows, glassmorphism, dark mode |
| `references/layout-and-spatial.md` | Grids, spacing, composition, responsive architecture |
| `references/motion-and-interaction.md` | Easing, scroll animations, micro-interactions |
| `references/component-patterns.md` | Nav, hero, cards, CTAs, forms, footers |
| `references/performance-and-craft.md` | Performance budgets, image optimization, polish checklist |

## Install

### Option 1: Clone into Claude Code skills directory

```bash
git clone https://github.com/Eskapeum/design-forge.git ~/.claude/skills/design-forge
```

### Option 2: Manual copy

Copy the `SKILL.md` and `references/` directory into `~/.claude/skills/design-forge/`.

## Usage

Once installed, the skill triggers automatically when you:

- Ask to "design this", "create mockup", "visual design", or "design the UI"
- Have a `SITE.md` with unchecked pages
- Run `/design-forge` directly

## Prerequisites

- SuperDesign CLI installed
- Stitch MCP server available
- `.superdesign/init/` context files populated
- `DESIGN.md` with design system notes
- `SITE.md` with sitemap roadmap

## License

MIT
