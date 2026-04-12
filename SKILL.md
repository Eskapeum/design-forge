---
name: design-forge
description: "Awwwards-level web design system with discovery, design system presets, contract enforcement, and a 7-stage pipeline with human feedback gates. Triggers on: design this, create mockup, visual design, design the UI, website design, landing page, hero section, page design, site build, design forge, or when SITE.md has unchecked pages."
---

# Design Forge — Awwwards-Level Design System

A **7-stage pipeline** with human feedback gates, design contract enforcement, and Stitch MCP integration. Every design decision is grounded in discovery, aligned with research, and enforced through a living contract.

## When to Use
- Designing any new screen, page, or major UI component
- Building an Awwwards-quality or portfolio-grade site
- `SITE.md` has unchecked pages in the roadmap

## When NOT to Use
- Quick component tweaks (use Stitch `edit_screens` directly)
- Bug fixes, backend work, text-only changes

## Reference Files

Loaded on-demand per stage. Do NOT load all at once.

| File | Load At | Purpose |
|------|---------|---------|
| `references/discovery-framework.md` | Stage 0 | Discovery questions, preset mapping, contract template |
| `references/design-system-architecture.md` | Stage 0.5 | Three-layer tokens, DTCG spec, DESIGN.md template |
| `references/typography-system.md` | Stage 2+ | Font selection, type scale, loading strategy |
| `references/color-and-light.md` | Stage 2+ | Palette construction, gradients, dark mode |
| `references/layout-and-spatial.md` | Stage 2+ | Grid, spacing, compositional techniques |
| `references/motion-and-interaction.md` | Stage 2+ | GSAP patterns, scroll animations, micro-interactions |
| `references/component-patterns.md` | Stage 2+ | Nav, heroes, cards, CTAs, forms, footers |
| `references/performance-and-craft.md` | Stage 4+ | Performance budgets, accessibility, pre-launch audit |

---

## The Pipeline

```
DISCOVER → GATE 0 → DESIGN SYSTEM → GATE 0.5 → RESEARCH → GATE 1 → EXPLORE → GATE 2 → ITERATE → GATE 3 → REFINE → GATE 4 → INTEGRATE → GATE 5 → DONE
    ↑                                                ↑              ↑                ↑                ↑                ↑
    └────────────────────────── feedback loops back to earlier stages as needed ──────┘────────────────┘────────────────┘

DESIGN CONTRACT flows forward through every stage. Every Stitch call includes the full contract.
```

**Every gate is a human decision point. The pipeline NEVER auto-advances past a gate.**

---

## The Design Contract

The Design Contract is the enforcement mechanism. It is a living document stored at `.design-forge/contract.md` that:

1. **Captures** every user decision (discovery answers, preset choice, gate approvals, feedback)
2. **Captures** every research finding (patterns to steal, layout approaches, techniques)
3. **Accumulates** — each gate adds to it, nothing gets dropped
4. **Gets injected** into every Stitch call as non-negotiable directives
5. **Gets validated** — after every Stitch output, the result is checked against the contract

### Contract Structure

```markdown
# Design Contract: {Project Name}
## Last Updated: {date}

## Identity
- **Brand Name:** {name}
- **Archetype:** {from discovery}
- **Emotional Target:** {2-3 feelings}
- **Visual Metaphor:** {what the site should feel like}
- **One Word:** {brand personality in one word}

## Audience
- **Primary User:** {who they are, what they need}
- **User Mindset:** {what they feel when they arrive}
- **Conversion Goal:** {what each page should accomplish}

## Design System
- **Stitch Preset:** {Bauhaus/Beam/Hand-draw/Kinetic/Luxury/Motion/Neumorphism/Newsprint/Playful/Uber/Win98}
- **Customizations:** {overrides applied on top of preset}
- **Primary Color:** {hex + emotional rationale}
- **Neutral Base:** {warm or cool + hex range}
- **Display Font:** {name + weights}
- **Body Font:** {name + weights}
- **Border Radius:** {system choice + rationale}
- **Spacing Base:** {8px default or custom}

## Research Directives (added at Gate 1)
- **From {Ref 1}:** {specific pattern to enforce}
- **From {Ref 2}:** {specific pattern to enforce}
- **From {Ref 3}:** {specific pattern to enforce}
- **From {Ref 4}:** {specific pattern to enforce}
- **Synthesis:** {combined approach}

## Accumulated Feedback (grows at every gate)
- **Gate 0:** {discovery refinements}
- **Gate 0.5:** {design system adjustments}
- **Gate 1:** {research direction notes}
- **Gate 2:** {first impression adjustments}
- **Gate 3:** {winner selection, hybrid instructions}
- **Gate 4:** {polish refinements}

## Hard Constraints (never violate)
- {List of explicit user deal-breakers}
- {List of explicit exclusions}

## Soft Preferences (follow unless user overrides)
- {List of user preferences detected from feedback patterns}
```

### Contract Rules

1. **Create** the contract at the end of Stage 0 (Discovery)
2. **Enrich** the contract at Gate 0.5 (Design System) and Gate 1 (Research)
3. **Inject** the full contract into every Stitch prompt from Stage 2 onward
4. **Update** the contract after every gate with new feedback
5. **Validate** every Stitch output against the contract before presenting to user
6. **Never remove** a directive unless the user explicitly says to

---

## Stage 0: DISCOVERY

**Goal:** Understand the project deeply before any visual work. Build Design Contract v1.

**Load:** `references/discovery-framework.md`

**Process:**

1. Read any existing project context (DESIGN.md, SITE.md, brand assets, `.design-forge/init/`)
2. Assess what's already known vs. what's missing
3. Ask discovery questions organized by category (see reference file for full framework):

### Discovery Categories

**A. Business & Brand Identity**
- What does the company/product do in one sentence?
- Who is the primary audience? What do they care about?
- What 3 adjectives describe the brand personality?
- What's the single most important action a visitor should take?
- Who are the top 3 competitors? What do they do well/poorly?

**B. Visual Direction**
- Are there existing brand assets (logo, colors, fonts, guidelines)?
- Show 2-3 sites whose visual style you admire. What specifically do you like about each?
- Show 1-2 sites that represent what you do NOT want. Why?
- Which Stitch preset feels closest to your vision?
  - **Bauhaus** — geometric, grid-heavy, primary colors
  - **Beam** — clean, modern, light
  - **Hand-draw** — sketchy, organic, informal
  - **Kinetic** — motion-forward, dynamic
  - **Luxury** — dark, serif, high-contrast, premium
  - **Motion** — animation-centric, fluid
  - **Neumorphism** — soft shadows, extruded UI
  - **Newsprint** — editorial, column-based, typographic
  - **Playful** — rounded, colorful, friendly
  - **Uber Design System** — systematic, neutral, functional
  - **Win98** — retro, pixel borders, nostalgic
- What's the emotional temperature? (warm/cool, bold/subtle, dense/spacious)

**C. Content & Structure**
- What pages does the site need? (sitemap)
- What content exists today? What needs to be written?
- Are there product screenshots, illustrations, or photography available?
- Any specific sections or features that are must-haves?

**D. Technical Constraints**
- Existing codebase or framework? (Next.js, Astro, etc.)
- CMS requirements?
- Performance constraints? (audience internet speed, device types)
- Accessibility requirements beyond WCAG AA?

**E. Deal-Breakers & Non-Negotiables**
- What must absolutely NOT appear? (specific elements, styles, patterns)
- Any brand guidelines that cannot be bent?
- Budget or timeline constraints affecting scope?

### Adaptive Questioning

Do NOT ask all questions. Assess what's already known and only ask what's missing:
- If DESIGN.md exists -> skip visual direction basics, ask refinement questions
- If SITE.md exists -> skip content/structure, ask about specific pages
- If brand assets exist -> skip brand identity, ask about extending the system
- First project -> ask more (10-15 questions across categories)
- Returning screen -> ask less (2-3 questions about this specific screen)

### GATE 0: Discovery Review

Present a summary of what you learned and the draft Design Contract. Use **AskUserQuestion**.

```
GATE 0: Discovery Review

Based on our conversation, here's what I understand:

BRAND: {summary}
AUDIENCE: {who + mindset}
VISUAL DIRECTION: {archetype + emotional target + references}
PRESET RECOMMENDATION: {preset} because {rationale}
CONTENT SCOPE: {pages/sections}
DEAL-BREAKERS: {constraints}

Does this capture your vision? Your options:
- APPROVE  -> Lock this in, move to design system setup
- CORRECT  -> Fix specific items (tell me what's wrong)
- EXPAND   -> Add context I missed
```

**After APPROVE:** Write Design Contract v1 to `.design-forge/contract.md`

---

## Stage 0.5: DESIGN SYSTEM

**Goal:** Select and customize a Stitch preset, define the three-layer token architecture, create DESIGN.md.

**Load:** `references/design-system-architecture.md`

**Process:**

1. Read the Design Contract from Stage 0
2. Map discovery answers to Stitch preset selection (see mapping table in reference file)
3. Set up Stitch project and design system:

### Stitch Setup

1. **Check for existing project:** Call `list_projects`
2. **Create project if needed:** Call `create_project` with site name
3. **Create design system from preset + customizations:**
   Call `create_design_system` with:
   - Base preset from discovery (e.g., Luxury, Beam, Kinetic)
   - `headlineFont` / `bodyFont`: Map from contract's font choices to Stitch enums
   - `customColor`: Primary brand color (hex) from contract
   - `colorMode`: LIGHT or DARK from contract
   - `roundness`: Map contract radius to ROUND_FOUR / ROUND_EIGHT / ROUND_TWELVE / ROUND_FULL
   - `designMd`: Full design personality brief + token foundation + contract directives
   - `colorVariant`: Choose based on brand personality (TONAL_SPOT default, VIBRANT for bold, MONOCHROME for minimal)
4. **Store IDs:** Save to `.design-forge/stitch.json`

### Three-Layer Token Architecture

Define tokens at three levels (see reference file for full architecture):

```
PRIMITIVE -> Raw values (colors, sizes, durations)
SEMANTIC  -> Purpose-driven mappings (color-background-primary -> brand-500)
COMPONENT -> Implementation-specific (button-bg-primary -> color-primary)
```

### GATE 0.5: Design System Review

```
GATE 0.5: Design System Review

Here's the design system I've configured:

PRESET: {name} -- {why this matches the brand}
CUSTOMIZATIONS:
- Primary: {color} ({emotional rationale})
- Fonts: {display} + {body} ({pairing name from reference})
- Radius: {value} ({feel it creates})
- Mode: {light/dark} ({rationale})

TOKEN EXAMPLES:
- color-background-primary: {value}
- color-text-primary: {value}
- spacing-section: {value}

Does this feel right? Your options:
- APPROVE     -> Design system locked, move to research
- SWAP PRESET -> Try a different preset base
- ADJUST      -> Change specific tokens (tell me which)
- COMPARE     -> Show me 2 presets side by side
```

**After APPROVE:** Update Design Contract with design system details. Write DESIGN.md.

---

## Stage 1: RESEARCH

**Goal:** Ground the design in real-world excellence. Never design from memory.

**Process:**

1. Identify the screen type (e.g., "cinematic hero", "pricing page", "calculator form")
2. Web search for 4 reference sites using the competitive analysis framework:
   - 2 direct competitors (same industry/product type)
   - 1 indirect competitor (different industry, similar UX pattern)
   - 1 aspirational benchmark (Awwwards SOTD or equivalent)
3. For each reference, extract with traffic-light scoring:

| Dimension | Score | Notes |
|-----------|-------|-------|
| Layout | GREEN/YELLOW/RED | {specific pattern} |
| Color | GREEN/YELLOW/RED | {palette approach} |
| Typography | GREEN/YELLOW/RED | {type treatment} |
| Motion | GREEN/YELLOW/RED | {interaction quality} |
| Performance | GREEN/YELLOW/RED | {load speed, CWV} |

4. Synthesize: which GREEN patterns to combine, aligned with Design Contract
5. Save to `.design-forge/research/{screen-name}.md`

### GATE 1: Research Review

```
GATE 1: Research Review

4 references for {screen name}:

1. {Ref 1 -- direct competitor} -- steal: {pattern}
2. {Ref 2 -- direct competitor} -- steal: {pattern}
3. {Ref 3 -- indirect competitor} -- steal: {pattern}
4. {Ref 4 -- aspirational benchmark} -- steal: {pattern}

Synthesis: {combined approach aligned with Design Contract}

Contract alignment:
- Preset {X} supports these patterns: YES/NO
- Brand personality match: {how it aligns}
- Deal-breaker check: {no violations}

Your options:
- APPROVE    -> References locked, move to design
- SWAP {N}   -> Replace reference N (tell me what to look for)
- ADD        -> Keep all 4 but also investigate {specific site/style}
- REDIRECT   -> Wrong direction, search for {new terms}
```

**After APPROVE:** Update Design Contract with Research Directives.

---

## Stage 2: EXPLORE -- Stitch First Draft

**Goal:** Create the first design via Stitch incorporating the full Design Contract.

**Load:** Relevant reference files for the screen type (typography, color, layout, motion, component patterns)

**Process:**

1. Read the full Design Contract (`.design-forge/contract.md`)
2. Read research (`.design-forge/research/{screen-name}.md`)
3. Read DESIGN.md
4. Verify Stitch design system is applied
5. Build the Stitch prompt using the Contract Injection Template (below)
6. Call `generate_screen_from_text` with `modelId: GEMINI_3_1_PRO`
7. **Validate output against contract** before presenting to user

### Contract Injection Template (CRITICAL -- used for ALL Stitch calls)

Every Stitch prompt MUST follow this structure:

```
You are a world-class UI/UX design expert with 30 years of experience. You have won multiple Awwwards Site of the Day, FWA awards, and Webby Awards. Your design philosophy combines Swiss precision with emotional storytelling. Every pixel is intentional. Every whitespace is architectural.

Your principles:
- LESS IS MORE: Remove everything that doesn't serve the user
- EVERY DETAIL MATTERS: Spacing, typography, color -- all mathematically precise
- EMOTION THROUGH RESTRAINT: Premium quality from what you leave out
- AWARD-WINNING STANDARD: Every screen must be worthy of Awwwards SOTD

CRITICAL: Generate EXACTLY what is described. NO sidebars, NO navigation panels, NO dashboard layout, NO extra UI chrome unless explicitly requested.

=== DESIGN CONTRACT (NON-NEGOTIABLE) ===

{Paste full Design Contract here -- identity, design system, research directives, accumulated feedback, hard constraints}

=== SCREEN REQUIREMENTS ===

{From SITE.md -- what this specific screen needs}

=== RESEARCH PATTERNS TO INCORPORATE ===

1. From {Ref 1}: {specific pattern}
2. From {Ref 2}: {specific pattern}
3. From {Ref 3}: {specific pattern}
4. From {Ref 4}: {specific pattern}

Synthesis: {combined approach}

=== EXPLICIT EXCLUSIONS ===

{From contract hard constraints + deal-breakers}
DO NOT include: {list everything that should NOT appear}

=== ACCUMULATED HUMAN DIRECTION ===

{All feedback from previous gates, formatted as bullet directives}
```

### Post-Generation Validation

Before presenting to user, check the Stitch output against the contract:

| Contract Directive | Output Match? | Issue |
|---|---|---|
| Preset: {X} | YES/NO | {mismatch} |
| Primary color: {hex} | YES/NO | {mismatch} |
| Font: {display} | YES/NO | {mismatch} |
| No {exclusion} | YES/NO | {violation} |
| Research pattern: {X} | YES/NO | {miss} |

If any NO: regenerate or edit before presenting. Do NOT show contract-violating output to the user.

### GATE 2: First Impression

```
GATE 2: First Impression -- {screen name}

Here's the first Stitch design: {show/describe output}

Contract validation: All {N} directives met.

Quick direction check (Awwwards-weighted):
1. DESIGN (40%)     -- Does the visual system feel right?
2. USABILITY (30%)  -- Is the hierarchy clear? Navigation intuitive?
3. CREATIVITY (20%) -- Does it feel original, not template-like?
4. CONTENT (10%)    -- Is the right content represented?

Your options:
- GOOD DIRECTION -> Move to variations
- ADJUST         -> Tweak and regenerate (tell me what)
- WRONG DIRECTION -> Go back to research
```

**After feedback:** Update Design Contract Accumulated Feedback section.

---

## Stage 3: ITERATE -- Stitch Variants

**Goal:** Explore variations, then pick the winner.

**Process:**

1. Call `generate_variants` with full contract injection:
   - `modelId`: GEMINI_3_1_PRO
   - `prompt`: Contract Injection Template + variation direction + Gate 2 feedback
   - `variantOptions`:
     - `variantCount`: 2 (or 3 for complex screens)
     - `creativeRange`: EXPLORE (default) or REFINE (if Gate 2 said "good direction")
     - `aspects`: Choose which to vary (LAYOUT, COLOR_SCHEME, IMAGES, TEXT_FONT, TEXT_CONTENT)
2. Validate ALL variants against the contract
3. Present all designs (original + variants) for comparison

### GATE 3: Pick Winner

```
GATE 3: Pick Winner -- {screen name}

Three directions (all contract-validated):

ORIGINAL: {description}
VARIANT A: {description -- what it pushes differently}
VARIANT B: {description -- what it pushes differently}

Compare on Awwwards criteria:
1. DESIGN (40%)     -- Which visual system is strongest?
2. USABILITY (30%)  -- Which hierarchy and flow works best?
3. CREATIVITY (20%) -- Which feels most original?
4. CONTENT (10%)    -- Which presents content best?

Your options:
- PICK ONE  -> "Go with {X}" (move to polish)
- HYBRID    -> "Take {element} from A and {element} from B"
- NONE      -> "None work" -- new variants with your direction
- RESTART   -> Back to explore with new prompt
```

**Hybrid rule:** ONE merge iteration, then mini-gate. Max 3 total rounds at this stage.

**After feedback:** Update Design Contract.

---

## Stage 4: REFINE -- Stitch Polish

**Goal:** Polish the winner into production-ready quality.

**Load:** `references/performance-and-craft.md`

**Process:**

1. Call `edit_screens` with full contract + all accumulated feedback
2. Apply specific refinements from Gate 3
3. Optionally call `apply_design_system` to ensure token consistency
4. Run Craft Checklist and Squint Test
5. Validate against contract + performance standards

### GATE 4: Polish Check

```
GATE 4: Polish Check -- {screen name}

Refined design: {show/describe output}

Contract validation: All directives met.
Craft score: {N}/10 craft details incorporated
Squint test: PASS/FAIL

Review (Awwwards-weighted):
1. DESIGN (40%)     -- Pixel-perfect? Coherent with system?
2. USABILITY (30%)  -- Production-ready? All states covered?
3. CREATIVITY (20%) -- Still original after polish?
4. CONTENT (10%)    -- All content present, correct, formatted?

Your options:
- SHIP READY    -> Move to integration
- TWEAK         -> One more edit pass (tell me what)
- MORE VARIANTS -> Back to Stage 3
- DESIGN ISSUE  -> Fundamental problem -- back to Stage {N}
```

**Refinement limit:** Max 3 edit passes.

---

## Stage 5: INTEGRATE -- Site Assembly

**Goal:** Wire the approved screen into the site.

**Process:**

1. Export screen from Stitch
2. Convert to project framework (Next.js/Astro/etc. per contract)
3. Wire navigation links
4. Ensure header/footer consistency
5. Update SITE.md (mark page complete)
6. Save all feedback to `.design-forge/feedback/{screen-name}.md`

### GATE 5: Final Sign-Off

```
GATE 5: Final Sign-Off -- {screen name}

Screen integrated into site:
- Page: {path}
- Navigation: {links wired}
- Consistency: {design system coherence with other pages}

Final review:
1. DESIGN      -- Works in full site context?
2. USABILITY   -- Consistent navigation and flow?
3. CREATIVITY  -- Quality maintained in context?
4. CONTENT     -- Anything missing?

Your options:
- SHIP IT       -> Done. Next screen.
- MINOR FIXES   -> Small tweaks (list them)
- MAJOR REVISION -> Back to Stage {N}
```

**After SHIP IT:**
1. Update Design Contract with final feedback
2. Log to `.design-forge/feedback/{screen-name}.md`
3. Announce next screen from SITE.md

---

## Craft Checklist

Before presenting at Gate 4+, score against these. Aim for 3-5 per project:

- [ ] Custom cursor interaction (expands on interactive elements)
- [ ] Magnetic buttons (4-8px pull with elastic easing)
- [ ] Text reveal animations (GSAP SplitText, overflow-hidden mask)
- [ ] Parallax depth (3 layers: 0.3x, 0.6x, 1x)
- [ ] Grain/texture overlay (3-5% opacity SVG noise)
- [ ] Smooth scroll with Lenis momentum
- [ ] Color-shifting gradients (CSS @property animation)
- [ ] Loading choreography (orchestrated entrance 0-1000ms)
- [ ] Footer as destination (visual moment + final CTA)
- [ ] Easter egg (console art, hidden interaction)

---

## Animation Standards (GSAP)

All animation uses GSAP + ScrollTrigger:

- **Always `gsap.fromTo()`** -- never `gsap.from()` (prevents stuck-at-initial-state bugs with Lenis)
- **Always `useGSAP` hook** from `@gsap/react` for cleanup
- **Always `gsap.matchMedia`** with `(prefers-reduced-motion: no-preference)` and reduce fallback
- **Custom cursor:** plain `requestAnimationFrame` + `lerp`, NOT `gsap.quickTo`
- **Lenis package:** `lenis` (not deprecated `@studio-freight/lenis`)
- **Easing:** Named curves from design tokens, never `linear` or default `ease`

---

## Tech Stack

Read from project config. Defaults if not specified:

| Layer | Default | Alternatives |
|-------|---------|-------------|
| Framework | Next.js App Router | Astro, SvelteKit, Vite |
| Styling | Tailwind CSS v4 + CSS custom properties | CSS Modules |
| Components | shadcn/ui | Radix primitives |
| Animation | GSAP + ScrollTrigger | CSS keyframes for simple motion |
| Scroll | Lenis (`lenis`) | Native smooth scroll |
| Fonts | `next/font` (local preferred) | Google Fonts |
| Images | `next/image` | `<picture>` with AVIF/WebP |
| Deployment | Vercel | Netlify, Cloudflare |

---

## Quality Enforcement

### The Squint Test
Squint until blurry. Must still identify:
1. Where the hero is (most dominant zone)
2. Where the primary CTA is (bright spot)
3. Visual hierarchy (3+ levels of weight)
4. Rhythm (alternating section density)
5. Color story (one dominant palette)

If any fails -> fix macro-composition before details.

### Awwwards Scoring (Gate 4+)

| Criterion | Weight | Score 1-10 | Notes |
|-----------|--------|------------|-------|
| Design | 40% | | Visual hierarchy, typography, color, micro-details |
| Usability | 30% | | Navigation, performance, responsive, accessibility |
| Creativity | 20% | | Original solutions, custom interactions |
| Content | 10% | | Real copy, content-design integration |
| **Weighted Total** | | **/10** | 8.0+ for SOTD consideration |

### Feedback Pattern Detection

After every 3 screens, review feedback logs and update:
- DESIGN.md if user consistently adjusts the same values
- Stitch design system `designMd` if Stitch consistently misses patterns
- Contract Hard Constraints if new deal-breakers emerge
- Contract Soft Preferences if patterns in user choices appear

### Common Mistakes

| Mistake | Fix |
|---------|-----|
| Auto-advancing past a gate | NEVER skip. Every gate is a human decision. |
| Not injecting full contract | Every Stitch prompt gets the full contract. |
| Showing contract-violating output | Validate before presenting. Regenerate if needed. |
| Forgetting previous feedback | Read contract before every prompt. It accumulates. |
| Stitch invents layouts | Start every prompt with explicit exclusions. |
| Vague Stitch prompts | Exact hex, font names + sizes in px, positions, dimensions. |
| Using `gsap.from()` | Always `gsap.fromTo()` with explicit start AND end states. |
| Framer Motion for scroll animations | GSAP + ScrollTrigger. FM only for layout animations if needed. |
| `@studio-freight/lenis` | Package is now `lenis`. |
| Skipping design system preset | Always start from a Stitch preset, then customize. |
| Generic discovery | Adapt questions to what's already known. |
| Not logging feedback | Every gate -> `.design-forge/feedback/` and contract update. |
