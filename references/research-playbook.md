# Research Playbook

Stage 1 rules, queries, sources, and reject-list.

## Search Query Templates

Compose queries from **archetype + density + primary asset**, not product category.

| Archetype        | Base Queries |
|---|---|
| Luxury           | `"editorial" dark site:awwwards.com`, `fintech serif landing`, `private banking homepage 2025` |
| Kinetic / Motion | `scroll-driven hero awwwards`, `gsap ScrollTrigger case study 2024..2026`, `cinematic landing site:godly.website` |
| Bauhaus          | `grid poster web`, `swiss typography landing site:siteInspire.com`, `geometric primary colors homepage` |
| Luxury + Product | `premium product hero dark site:awwwards.com`, `boutique hardware landing` |
| Hand-draw        | `illustrated portfolio site:awwwards.com`, `hand drawn landing page` |
| Playful          | `colorful SaaS landing 2025`, `friendly onboarding illustration landing` |
| Uber / System    | `design system marketing site`, `documentation homepage` |
| Newsprint        | `editorial magazine web 2025`, `long-form longread homepage` |
| Neumorphism      | `soft UI landing 2025` (use sparingly, often dated) |
| Win98 / Retro    | `y2k brutalist landing 2024..2026`, `pixel ui revival` |

Always pin the year range (`2024..2026`) to avoid aged references.

## Curated Source List (GREEN by default)

- **Awwwards** — `awwwards.com/sites/` (filter SOTD or Developer Awards)
- **SiteInspire** — `siteinspire.com`
- **Godly** — `godly.website`
- **One Page Love** — `onepagelove.com`
- **Muzli** — `muz.li` (design dashboard)
- **Httpster** — `httpster.net`
- **Typewolf** — `typewolf.com/site-of-the-day`
- **Land-book** — `land-book.com`
- **SaaSLandingPage** — `saaslandingpage.com`
- **Refero** — `refero.design`

## Reject-List (never pull from these for production reference)

- Dribbble hero-only shots (no system, no context)
- Pinterest boards (collage, no source)
- Template marketplaces (ThemeForest, TemplateMonster, Elementor)
- Generic portfolio grids (Behance unless the project is live & verified)
- Rendered-in-Figma mockups shown as live sites
- Anything older than 3 years without "classic" rationale

## Traffic-Light Scoring

For each of the 4 references, score 5 dimensions:

| Dimension | GREEN | YELLOW | RED |
|---|---|---|---|
| Layout      | Unique + works | Solid but common | Generic or broken |
| Color       | Intentional palette with rationale | Fine, forgettable | Harmful or off-brand |
| Typography  | Award-grade pairing & scale | Competent | System / default |
| Motion      | Meaningful, performant | Present, unremarkable | Broken or gratuitous |
| Performance | LCP<2.5s, CLS<0.1 | 2.5–4s | > 4s or layout shift |

Only extract patterns from GREEN rows. YELLOW rows may provide context but no directives.

## Reference Mix Rule

| Slot | Type | Why |
|---|---|---|
| 1 | Direct competitor     | Industry visual conventions |
| 2 | Direct competitor     | Triangulate conventions |
| 3 | Indirect competitor   | Same UX pattern, different industry — breaks monotony |
| 4 | Aspirational benchmark | Award-winning, ceiling-setter |

Never 4 competitors. Never 4 aspirational. The mix forces grounded creativity.

## Output Format — `.design-forge/research/{screen}.md`

```markdown
# Research: {screen}
Date: {YYYY-MM-DD}
Preset target: {preset}

## Reference 1 — {title} ({url})
Type: direct-competitor | indirect-competitor | aspirational
| Dim | Score | Note |
|---|---|---|
| Layout | GREEN | {what to steal} |
| Color | YELLOW | {why not useful} |
| Typography | GREEN | {what to steal} |
| Motion | GREEN | {what to steal} |
| Performance | YELLOW | — |

Pattern to steal: {one sentence}

## Reference 2 — ...
## Reference 3 — ...
## Reference 4 — ...

## Synthesis
Combined approach for this screen:
- From {Ref 1}: ...
- From {Ref 2}: ...
- From {Ref 3}: ...
- From {Ref 4}: ...

Contract alignment check:
- Identity: {pass/fail}
- Hard constraints: {list of any conflicts}
- Preset fit: {pass/fail}
```

## Tripwires

Stop the research stage if:
- 3 search rounds and no GREEN layouts found → the archetype may be wrong
- Every reference scores YELLOW on Typography → search query missing a type-specific term
- Aspirational reference is actually a direct competitor → rotate slots

## Cross-project Learning

After shipping, successful reference URLs get written to `~/.design-forge/reference-library.md` keyed by `archetype × preset`. Stage 1 consults this library *first* before web search on future projects.
