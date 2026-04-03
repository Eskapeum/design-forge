---
name: design-forge
description: "The definitive design skill for building Awwwards-winning websites. Combines a 5-stage research-driven forge workflow (Research → Explore → Iterate → Generate → Integrate) with comprehensive design standards, quality gates, and craft principles. Triggers on: design this, create mockup, visual design, design the UI, website design, landing page, hero section, page design, site build, design forge, or when a SITE.md roadmap exists with unchecked pages. This is the north star for every pixel that ships."
---

# Design Forge — Awwwards-Level Web Design System

> "Design is not just what it looks like and feels like. Design is how it works." — Steve Jobs

## How This Skill Works

This is a **unified design system** that combines:
1. A **5-stage pipeline** with human feedback gates at every stage
2. **Comprehensive design standards** that govern every visual decision
3. **6 deep-reference files** for specific design domains
4. **Quality enforcement** — nothing ships without meeting the bar

---

## When to Use

- Designing any new screen, page, or major UI component
- `SITE.md` has unchecked pages in the roadmap
- User asks for visual design before implementation
- Building an Awwwards-quality or portfolio-grade site
- User asks for "website design", "landing page", "hero section", "page design", or "site build"
- Any moment where the visual quality of a deliverable matters

## When NOT to Use

- Quick component tweaks (use SuperDesign directly)
- Text-only content changes (use CMS)
- Bug fixes to existing UI
- Backend or API work with no visual component

## Prerequisites

- SuperDesign CLI installed (`superdesign --version`)
- Stitch MCP server available
- `.superdesign/init/` context files populated
- `DESIGN.md` with:
  - Section 6: Design System Notes for Stitch Generation
  - Design personality brief (archetype, emotional target, visual metaphor)
  - Token foundation (spacing, radius, transitions, z-index CSS variables)
- `SITE.md` with sitemap roadmap

## Reference Files

These 6 deep-reference files live in `references/` alongside this skill. Consult them for domain-specific decisions:

| File | When to Use |
|------|-------------|
| `typography-system.md` | Choosing fonts, setting type scale, loading strategy |
| `color-and-light.md` | Palette construction, gradients, shadows, dark mode |
| `layout-and-spatial.md` | Grid architecture, spacing rhythm, compositional techniques |
| `motion-and-interaction.md` | Easing functions, scroll animations, micro-interactions |
| `component-patterns.md` | Navigation, heroes, cards, CTAs, forms, footers |
| `performance-and-craft.md` | Performance budgets, image optimization, pre-launch audit |

---

## Part 1: The Design Philosophy

> "Good design is as little design as possible." — Dieter Rams

### The Three Laws of Design

**Law 1: Intentional Restraint**
The best design decision is often what you remove, not what you add. Every element on the screen must earn its place. White space is not emptiness — it is architecture. It creates breathing room, directs focus, and communicates premium quality. Ask before adding anything: "Does this element serve the user, or does it serve my ego?"

Signs of restraint failure: cluttered heroes, too many CTAs, decorative elements that add noise, text that says what the visual already shows.

Signs of restraint mastery: Stripe's homepage — one gradient, one headline, one CTA. Linear's product page — maximum negative space, minimum words. Apple's product launches — one product, one light source, one sentence.

**Law 2: Obsessive Coherence**
Every design decision ripples through the entire site. If you choose a 4px border-radius for buttons, every card, input, and modal must use the same 4px system. If you choose a specific shade of indigo as your primary color, that shade must appear in every hover state, every active state, every gradient, every glow. Stripe's 4px radius is legendary because it appears on literally everything.

Coherence is what separates a designed site from a built site. Anyone can arrange elements. Only disciplined designers make every pixel feel like it belongs to the same system.

**Law 3: Sensory Reward**
Great websites feel physical. Hover states should feel like pressing a real button. Scroll reveals should feel like curtains parting. Page transitions should feel like turning a page. The goal is to make the user feel something — curiosity, delight, confidence, momentum.

Every interaction is an opportunity to reward the user for their attention. A site that offers no sensory feedback feels dead. A site that offers too much feels overwhelming. The craft is calibrating the right amount of reward for the right moments.

### The "Would Steve Ship It?" Test

Before finalizing any design, run it through these 5 questions. If any answer is no, keep refining.

1. **Can I remove one more thing?** If yes, remove it. If no, you might be done.
2. **Is every element aligned to the grid?** Random pixel placement is a sign of carelessness. Intentional grid breaks are signs of mastery.
3. **Is there a single, undeniable visual hierarchy?** The user's eye should land on exactly ONE thing first. If it could land on two, choose one and make the other smaller, lighter, or more distant.
4. **Does this feel like something?** Does it feel premium? Warm? Rebellious? Technical? It must feel like something specific — "fine" is not good enough.
5. **Would this win Site of the Day on Awwwards?** If you're not sure, it wouldn't. Keep going.

---

## Part 2: Design Token Foundation

Before any screen design begins, the design system must be defined. This is the foundation that makes coherence possible.

### Step 1: Design Personality Brief

Complete this brief for every project before touching any design tool:

```
ARCHETYPE: [Choose one: Bold Innovator / Warm Expert / Elegant Minimalist /
            Rebellious Creator / Trusted Authority / Playful Disruptor]

EMOTIONAL TARGET: When users land on this site, they should feel ___________
                  (choose 2-3: inspired / confident / curious / safe /
                  excited / impressed / understood / capable)

VISUAL METAPHOR: This site should feel like ___________
                 (e.g., "a gallery opening", "a precision instrument",
                 "a warm conversation", "a rocket launching")

REFERENCE SITES: [3 sites that nail the vibe you're going for]
ANTI-REFERENCES: [2 sites that represent what this site should NOT be]
ONE WORD: If this site were a person, they would be described as: ___________
```

### Step 2: Design Token Foundation

These CSS custom properties form the design system. Define them in `globals.css` or `tokens.css` before writing any component styles:

```css
:root {
  /* ─── SPACING SCALE (8px base) ───────────────────────────── */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;
  --space-20: 80px;
  --space-24: 96px;
  --space-32: 128px;
  --space-48: 192px;

  /* ─── BORDER RADIUS ──────────────────────────────────────── */
  --radius-xs: 2px;
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-2xl: 24px;
  --radius-full: 9999px;

  /* ─── TRANSITIONS ────────────────────────────────────────── */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-expo: cubic-bezier(0.7, 0, 0.84, 0);
  --ease-in-out-quint: cubic-bezier(0.83, 0, 0.17, 1);
  --ease-out-back: cubic-bezier(0.34, 1.56, 0.64, 1);
  --spring-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
  --spring-gentle: cubic-bezier(0.22, 1.0, 0.36, 1.0);

  --duration-fast: 150ms;
  --duration-base: 250ms;
  --duration-slow: 400ms;
  --duration-slower: 700ms;
  --duration-slowest: 1000ms;

  /* ─── Z-INDEX SCALE ──────────────────────────────────────── */
  --z-below: -1;
  --z-base: 0;
  --z-raised: 10;
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-overlay: 300;
  --z-modal: 400;
  --z-toast: 500;
  --z-cursor: 9999;
}
```

### Step 3: Design in Layers

Every screen is composed of 5 layers. Design them in order:

1. **Background layer** — The ambient environment (gradient, texture, color). This sets the mood before any content appears.
2. **Content layer** — The actual information hierarchy (headlines, body, images). This is what the user came for.
3. **Interactive layer** — Buttons, links, inputs. These must be visually distinct from content but not distracting.
4. **Overlay layer** — Modals, drawers, tooltips. These sit above everything and demand focus.
5. **Feedback layer** — Loading states, success states, error states, toasts. These are temporary but must be cohesive.

---

## Part 3: Non-Negotiable Standards

These are not guidelines — they are requirements. Every design that ships must meet every standard below.

### Typography Standards

- **Minimum 2 typefaces**: One display (characterful, memorable) and one body (readable, invisible). Never use a single typeface for everything.
- **Mathematical type scale**: Use a ratio (1.250 is the default). Never set arbitrary font sizes. See `references/typography-system.md` for the full scale table.
- **Line height**: Body text 1.5–1.7. Headings 1.0–1.2. Never set the same line height for both.
- **Measure**: Body text `max-width: 65ch`. Never let body text run full-width across a 1440px container.
- **Optical sizing**: Letter-spacing must tighten as size increases. `h1: -0.03em`, `body: 0.01em`. See the reference file for the full table.
- **Font display**: Always `font-display: swap`. Never let layout shift caused by font loading.
- **Never**: Use Inter as a display font. Use more than 3 typefaces. Let text justify on the web.

### Color Standards

- **Maximum 5 colors**: One primary (brand champion), 2–3 neutrals, and functional colors (success, error, warning). Anything beyond 5 is noise.
- **60-30-10 rule**: 60% neutral backgrounds, 30% secondary color, 10% accent/brand.
- **WCAG AAA target**: 7:1 contrast ratio for body text. 4.5:1 minimum for all UI text. Use a contrast checker before shipping.
- **Dark mode is not optional**: Every site must support `[data-theme="dark"]` with a purposefully designed dark palette — not just inverted colors.
- **Never**: Use pure `#000000` or `#FFFFFF` as primary surface colors. Use stock color palettes without customization.

### Layout Standards

- **12-column grid on desktop**: Every element sits on the grid or deliberately breaks it. Accidental off-grid placement is always wrong.
- **4-column grid on mobile**: Gutter 16px, margin 16px.
- **Section padding**: `clamp(48px, 8vw, 128px)` vertical padding per section. Hero sections get more: `clamp(64px, 12vw, 192px)`.
- **Max-widths**: Marketing sites 1280px. Dashboards 1440px. Body text 65ch.
- **Negative space**: If a section feels "empty", resist filling it. The space is working.
- **Never**: Symmetric layouts on every section (monotonous). Horizontal scroll on mobile from content overflow. Elements touching the edge of the viewport.

### Motion Standards

- **Every interactive element has a hover and active state**: No bare, stateless elements.
- **No hard cuts**: Page transitions must exist. Even a simple fade is better than nothing.
- **IntersectionObserver for scroll reveals**: Content reveals as it enters the viewport. 70ms stagger between siblings.
- **Duration hierarchy**: Micro (100–200ms), Component (200–400ms), Section (400–700ms), Page (600–1000ms). Match duration to scope.
- **Never**: Use `linear` or `ease` easing. Animate layout properties (`width`, `height`, `margin`). Animate more than 3 properties simultaneously.

### Image Standards

- **WebP/AVIF formats**: Always. JPEG as fallback. Never PNG for photographs.
- **Lazy loading**: All below-fold images use `loading="lazy"`. Hero/LCP images use `loading="eager"` with `priority`.
- **Locked aspect ratios**: Images never reflow. Always set explicit `width` and `height`.
- **Art direction**: Use `<picture>` with `<source media>` for different crops on different breakpoints.
- **Video**: Autoplay only if `muted` and `prefers-reduced-motion: no-preference`.
- **Never**: Generic stock photography in heroes. Images without `alt` text. Images that resize without aspect ratio lock.

### Accessibility Standards

- **Semantic HTML**: `<header>`, `<main>`, `<nav>`, `<section>`, `<article>`, `<footer>`. Never use `<div>` when a semantic element exists.
- **Focus visible**: `:focus-visible` with a 2px brand-colored outline. Mouse users should not see focus rings; keyboard users must always see them.
- **Keyboard navigation**: Every interactive element reachable and operable by keyboard alone.
- **ARIA**: Only when semantic HTML cannot convey the meaning. Never ARIA for decoration.
- **Reduced motion**: `@media (prefers-reduced-motion: reduce)` on all animations. Users who need it get instant transitions.
- **Screen reader tested**: VoiceOver (Mac) and NVDA (Windows) before shipping.

---

## Part 4: The Pipeline — 5 Stages with Human Feedback Gates

```
RESEARCH → GATE 1 → EXPLORE → GATE 2 → ITERATE → GATE 3 → GENERATE → GATE 4 → INTEGRATE → GATE 5 → DONE
    ↑____________↑_______↑___________________↑___________________↑___________________↑
                       (feedback loops at each gate back to earlier stages as needed)
```

**Every gate is a human decision point. The pipeline NEVER auto-advances past a gate.**

### Human Feedback Format

At every gate, present the work and ask for structured feedback using this format:

```
GATE {N}: {Gate Name}

Here's what I produced: {show screenshot / describe output}

Please review on these dimensions:
1. LAYOUT    — Is the structure right? (spacing, hierarchy, flow)
2. COLOUR    — Do the colours feel right? (contrast, mood, brand)
3. TYPOGRAPHY — Are the fonts/sizes working? (readability, impact)
4. VIBE      — Does it feel world-class? (energy, polish, "wow" factor)
5. CONTENT   — Is the right content shown? (what's missing, what's extra)

Your options:
- APPROVE  → Move to next stage
- REVISE   → I'll adjust based on your notes (stays in current stage)
- PIVOT    → Go back to a previous stage (specify which)
- ADD      → Keep this but add/change something specific
```

**Always use AskUserQuestion** to present the gate. Include the 5 dimensions as context so the user gives structured feedback, not just "looks good."

### Feedback Log

All feedback is logged to `.superdesign/feedback/{screen-name}.md` for continuity across sessions and as a reference for future screens.

**Log format:**

```markdown
# Feedback Log: {Screen Name}

## Gate 1: Research Review
- **Decision:** {Approved / Swapped Ref 2 for X}
- **Notes:** "{User's exact feedback}"
- **Action taken:** {What was changed}

## Gate 2: First Impression
- **Decision:** {Good direction / Wrong direction}
- **Liked:** "{What the user liked}"
- **Disliked:** "{What the user didn't like}"
- **Action taken:** {Prompt adjustment or re-research}

## Gate 3: Winner Selection
- **Decision:** {Picked Variant B / Hybrid A+B}
- **From A:** "{Elements to keep from A}"
- **From B:** "{Elements to keep from B}"
- **Original:** "{Elements to keep from original}"
- **Action taken:** {Final iteration instructions}

## Gate 4: Fidelity Check
- **Decision:** {Matches / Regenerate}
- **Gaps:** "{What doesn't match the winning design}"
- **Action taken:** {Stitch prompt adjustments}

## Gate 5: Final Sign-Off
- **Decision:** {Ship / Minor fixes / Major revision}
- **Notes:** "{Final feedback}"
- **Action taken:** {Integration completed / revisions made}
```

---

### Stage 1: RESEARCH — 4 Inspiration References

**Goal:** Ground the design in real-world excellence. Never design from memory alone.

**Process:**

1. Identify the screen type (e.g., "cinematic opener", "data dashboard", "calculator form")
2. Web search for 4 reference sites that excel at this specific screen type
3. For each reference, extract:
   - **Layout pattern** — how content is structured
   - **Colour usage** — light/dark, accent placement
   - **Typography** — heading/body hierarchy, size scale
   - **Interaction** — hover states, scroll behaviour, animations
   - **What makes it award-winning** — the specific "wow" element
4. Save research to `.superdesign/research/{screen-name}.md`

**Research file format:**

```markdown
# Research: {Screen Name}

## Reference 1: {Site Name} ({URL})
- **Type:** {What kind of site/page}
- **Layout:** {Description of structure}
- **Steal this:** {Specific pattern to incorporate}
- **Screenshot/description:** {Visual description}

## Reference 2: ...
## Reference 3: ...
## Reference 4: ...

## Synthesis
Patterns to combine for our design:
1. {Pattern from Ref 1} + {Pattern from Ref 3}
2. {Specific layout approach}
3. {Typography/colour decision}
4. {Interaction/animation approach}
```

**Search strategies by screen type:**

| Screen Type | Search Terms |
|-------------|-------------|
| Hero/opener | "awwwards site of the year hero", "cinematic web intro 2025" |
| Data dashboard | "best data visualization websites", "stripe dashboard design" |
| Form/calculator | "best web form UX design", "interactive calculator website" |
| Map/interactive | "interactive map website awwwards", "3D web experience" |
| Chat/AI interface | "best AI chatbot UI 2025", "conversational interface design" |
| Card grid | "apple product page scroll", "metric card design system" |
| Mobile responsive | "best mobile web experience awwwards", "mobile-first design" |

### GATE 1: Research Review

Present the 4 references with descriptions of what to steal from each, plus the synthesis. Ask:

```
GATE 1: Research Review

I found 4 inspiration references for {screen name}:
1. {Ref 1} — stealing: {pattern}
2. {Ref 2} — stealing: {pattern}
3. {Ref 3} — stealing: {pattern}
4. {Ref 4} — stealing: {pattern}

Synthesis: {combined approach}

Your options:
- APPROVE  → These references are solid, let's design
- SWAP     → Replace reference {N} with something else (tell me what)
- ADD      → Keep all 4 but also look at {specific site/style}
- REDIRECT → Wrong direction entirely, search for {new terms}
```

**Do NOT proceed to Stage 2 until user approves the references.**

---

### Stage 2: EXPLORE — SuperDesign Draft

**Goal:** Create the first design incorporating all 4 approved research references.

**Design Standards Check:** Before writing the SuperDesign prompt, verify the design brief aligns with:
- **The Three Laws**: Does the prompt enforce restraint, coherence, and sensory reward?
- **The token foundation**: Is the prompt using the correct spacing, radius, transitions, and z-index values from DESIGN.md?
- **The non-negotiable standards**: Does the prompt specify the correct type scale, max-widths, motion easing, and accessibility requirements?

**Process:**

1. Read ALL `.superdesign/init/` context files
2. Read `.superdesign/research/{screen-name}.md`
3. Read `DESIGN.md` (especially Section 6)
4. Build the SuperDesign prompt combining:
   - Design system constraints from DESIGN.md
   - Specific patterns from the 4 references
   - Screen requirements from SITE.md
   - Component patterns from init/components.md
   - Any specific feedback from Gate 1
   - The Three Laws of Design as explicit directives
5. Run `superdesign create-design-draft` with:
   - `-p` flag: the combined prompt
   - `--context-file`: design-system.md, globals.css, relevant init files
6. Save the draft screenshot and ID

**Prompt template:**

```
Design a {screen type} for {project name}.

DESIGN SYSTEM: {Copy Section 6 from DESIGN.md}

DESIGN LAWS TO ENFORCE:
- Law 1 (Restraint): Remove anything that doesn't serve a purpose. White space is intentional architecture.
- Law 2 (Coherence): Every radius, spacing, and color decision must follow the token system exactly.
- Law 3 (Sensory Reward): Every interactive element must have a hover/active state. Scroll reveals must feel physical.

SCREEN REQUIREMENTS: {From SITE.md}

INSPIRATION REFERENCES (incorporate these patterns):
1. From {Ref 1}: {specific pattern to steal}
2. From {Ref 2}: {specific pattern to steal}
3. From {Ref 3}: {specific pattern to steal}
4. From {Ref 4}: {specific pattern to steal}

SYNTHESIS: {Combined approach from research}

HUMAN DIRECTION: {Any specific notes from Gate 1}
```

### GATE 2: First Impression

Present the first draft and ask for a quick direction check. This is NOT about perfection — it's about whether the overall direction is right.

```
GATE 2: First Impression

Here's the first design draft for {screen name}: {show screenshot}

Quick direction check on these dimensions:
1. LAYOUT    — Is the structure heading the right way?
2. COLOUR    — Do the colours feel right for this screen?
3. TYPOGRAPHY — Are the font choices landing?
4. VIBE      — Does it feel like it could be world-class with refinement?
5. CONTENT   — Is the right content represented?

Your options:
- GOOD DIRECTION → Move to variations (I'll create 2 alternatives)
- ADJUST         → Tweak the prompt and regenerate (tell me what to change)
- WRONG DIRECTION → Go back to research (the references aren't translating)
```

**Do NOT move to variations if the direction is wrong. Fix the foundation first.**

---

### Stage 3: ITERATE — Design Variations

**Goal:** Explore 2 variations that push different influences, then pick the winner with user input.

**Process:**

1. Run `superdesign iterate-design-draft` with 2 variation prompts:
   - **Variant A:** Push influence of Reference 1 + 2 (e.g., "more cinematic, darker, bolder")
   - **Variant B:** Push influence of Reference 3 + 4 (e.g., "cleaner, more minimal, lighter")
   - Incorporate any feedback from Gate 2
2. Present all 3 designs side by side (original + 2 variants)

**Craft Audit:** When evaluating variations, check for these award-winning details. The winning variation should score highest on this checklist:

- [ ] **Custom Cursor Interaction**: Does the cursor transform near CTAs or interactive zones?
- [ ] **Magnetic Buttons**: Do primary CTAs have a 4–8px magnetic pull effect with elastic easing?
- [ ] **Text Reveal Animations**: Do headings reveal character-by-character or word-by-word with mask/overflow-hidden?
- [ ] **Parallax Depth**: Are there 3 parallax layers (background 0.3x, midground 0.6x, foreground 1x) for depth?
- [ ] **Grain and Texture**: Is there a subtle SVG noise overlay (3–5% opacity) adding photographic warmth?
- [ ] **Smooth Scroll with Momentum**: Is Lenis (or equivalent) providing physics-based scroll momentum?
- [ ] **Color-Shifting Gradients**: Are background gradients animated via CSS `@property` for a living quality?
- [ ] **Loading Choreography**: Is there an orchestrated entrance sequence (0–1000ms) instead of a page pop?
- [ ] **Footer as a Destination**: Does the footer have large typography, a CTA, and a visual moment?
- [ ] **Easter Egg**: Is there a hidden delight element (console art, secret key combo, hover surprise)?

Not every design needs all 10 — but the best designs incorporate at least 3–5 of these craft details.

### GATE 3: Pick Winner

```
GATE 3: Pick Winner

Three design directions for {screen name}:

ORIGINAL: {description of original approach}
VARIANT A: {description — pushes Ref 1+2 influence}
VARIANT B: {description — pushes Ref 3+4 influence}

Review each on:
1. LAYOUT    — Which structure works best?
2. COLOUR    — Which colour approach wins?
3. TYPOGRAPHY — Which type treatment is strongest?
4. VIBE      — Which feels most world-class?
5. CONTENT   — Which presents the content best?

Your options:
- PICK ONE     → "Go with {Original/A/B}" (move to production)
- HYBRID       → "Take {element} from A and {element} from B" (one more iteration)
- NONE         → "None are right" — I'll create 2 new variants with your direction
- START OVER   → Go back to explore with a new prompt
```

**Hybrid rule:** If user requests a hybrid, run ONE more iteration with specific merge instructions. Then present the hybrid at a mini-gate:

```
HYBRID CHECK: Does this capture what you wanted?
- YES → Move to production
- CLOSE → One more small tweak: {tell me}
- NO → Let's try a different combination
```

**Max iterations:** 3 rounds at this stage. If not converging after 3, STOP and ask: "We've done 3 rounds — should we step back and re-research, or pick the closest and refine in production?"

---

### Stage 4: GENERATE — Stitch Production HTML (2 Variations)

**Goal:** Convert the winning design direction into production-quality HTML via Stitch. ALWAYS generate 2 variations.

### Stitch Prompt Rules (CRITICAL — follow exactly)

Stitch tends to invent layouts, add sidebars, navigation panels, dashboards, and UI chrome that was never in the approved design. You MUST prevent this:

1. **Start every prompt with explicit exclusions:** "CRITICAL: Reproduce the approved design EXACTLY. NO sidebars, NO navigation panels, NO dashboard layout, NO menus, NO tabs, NO extra UI chrome."
2. **Describe every element with exact specs:** hex colours, font names, font sizes in px, exact positions (top-left, center, bottom-right), exact dimensions (%, px, vw).
3. **List what should NOT appear:** If the design is a full-screen cinematic, say "The ENTIRE viewport is the experience. No standard web layout components."
4. **Include all accumulated human feedback** from Gates 1-3 as explicit directives.
5. **The more specific the prompt, the closer Stitch gets.** Vague prompts produce wrong layouts. Pixel-level descriptions produce matches.

### Process

1. Write TWO hyper-specific Stitch prompts:
   - **Variation A:** Faithful reproduction of the approved SuperDesign
   - **Variation B:** Same content and layout, but push one design element further (e.g., bolder typography, more atmospheric effects, different emphasis)
   - Both prompts include: Design System block, exact layout, hex colours, font specs, component patterns, reference patterns, explicit exclusions
2. Get or create Stitch project (check `stitch.json`)
3. Call `generate_screen_from_text` TWICE — once per variation:
   - `projectId`: from stitch.json
   - `prompt`: the variation-specific prompt
   - `deviceType`: DESKTOP (generate mobile separately later)
4. Download BOTH outputs:
   - HTML to `queue/{screen-name}-a.html` and `queue/{screen-name}-b.html`
   - Screenshots to `queue/{screen-name}-a.png` and `queue/{screen-name}-b.png`
5. Present both side-by-side for Gate 4

### GATE 4: Fidelity Check (2 Variations)

Compare BOTH Stitch outputs against the winning SuperDesign direction.

```
GATE 4: Fidelity Check

Winning design (from SuperDesign): {show/describe}
Stitch Variation A: {show screenshot — faithful reproduction}
Stitch Variation B: {show screenshot — pushed variation}

Which matches the approved design best?

1. LAYOUT    — Does the structure match?
2. COLOUR    — Are colours accurate?
3. TYPOGRAPHY — Are fonts/sizes right?
4. VIBE      — Does the production version capture the energy?
5. CONTENT   — Is all content present and correct?

Your options:
- PICK A        → Variation A matches, use it
- PICK B        → Variation B is better, use it
- HYBRID        → Combine elements from A and B
- CLOSE ENOUGH  → Minor differences I can live with, proceed with {A/B}
- REGENERATE    → Neither matches, try again with tighter prompts
- DESIGN ISSUE  → The design itself needs more work (back to Stage 3)
```

**Regeneration limit:** Max 2 rounds (4 total variations). If Stitch can't match after 2 rounds, note the gaps and proceed — they'll be fixed in code implementation.

---

### Stage 5: INTEGRATE — Site Assembly + Baton

**Goal:** Add the generated page to the site and prepare the next screen.

**Process:**

1. Move `queue/{screen-name}.html` to `site/public/{screen-name}.html`
2. Fix asset paths (make relative to public/)
3. Wire navigation links (replace any `href="#"` with real paths)
4. Ensure header/footer consistency with existing pages
5. Update `SITE.md`:
   - Mark page as `[x]` in Section 4 (Sitemap)
   - Remove consumed ideas from Section 6
6. Save all feedback to `.superdesign/feedback/{screen-name}.md`

### GATE 5: Final Sign-Off

```
GATE 5: Final Sign-Off for {screen name}

The screen is integrated into the site. Here's the final state:
- Page: site/public/{screen-name}.html
- Screenshot: {show final screenshot}
- Navigation: {links wired to/from this page}

Final review:
1. LAYOUT    — Does it work in the context of the full site?
2. COLOUR    — Consistent with other pages?
3. TYPOGRAPHY — Consistent with design system?
4. VIBE      — Still world-class in context?
5. CONTENT   — Anything missing before we move on?

Your options:
- SHIP IT        → This screen is done. Move to next screen.
- MINOR FIXES    → Small tweaks needed (list them) — fix and re-check
- MAJOR REVISION → Significant issues — go back to {Stage N}
```

**After SHIP IT:**
1. Write `next-prompt.md` baton for the next screen
2. Log final feedback to `.superdesign/feedback/{screen-name}.md`
3. Announce: "Screen {N} complete. Next up: {next screen name}. Ready to start research?"

---

## Part 5: The Craft Details That Win Awards

These 10 details are the difference between a good site and a Site of the Day. They are not decorations — they are signals of craft mastery. Implement at least 3–5 on every project.

### 1. Custom Cursor Interactions

The cursor is the user's primary point of contact with your interface. A custom cursor signals immediately that this is not a template site.

```css
/* Hide default cursor on interactive elements */
[data-cursor] { cursor: none; }

/* Custom cursor element */
.cursor {
  position: fixed;
  width: 12px;
  height: 12px;
  background: var(--color-primary);
  border-radius: 50%;
  pointer-events: none;
  z-index: var(--z-cursor);
  transform: translate(-50%, -50%);
  transition:
    width 0.3s var(--ease-out-expo),
    height 0.3s var(--ease-out-expo),
    background 0.3s var(--ease-out-expo);
  mix-blend-mode: difference;
}

/* Expand on hover over links/buttons */
.cursor.is-hovering {
  width: 48px;
  height: 48px;
}
```

The cursor should respond to context: small dot on empty space, expanding circle on clickable elements, text cursor on text, custom icon for special interactions.

### 2. Magnetic Buttons

Primary CTAs should feel physically attracted to the cursor when it's nearby. This creates a satisfying, almost physical interaction.

The button pulls toward the cursor by 4–8px. The pull uses elastic easing. On mouseleave, it springs back.

```javascript
const magneticButtons = document.querySelectorAll('[data-magnetic]');

magneticButtons.forEach((btn) => {
  btn.addEventListener('mousemove', (e) => {
    const rect = btn.getBoundingClientRect();
    const x = e.clientX - rect.left - rect.width / 2;
    const y = e.clientY - rect.top - rect.height / 2;
    // Pull factor: 0.3 for subtle, 0.5 for strong
    btn.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px)`;
  });

  btn.addEventListener('mouseleave', () => {
    btn.style.transform = 'translate(0, 0)';
    btn.style.transition = 'transform 0.5s cubic-bezier(0.16, 1, 0.3, 1)';
  });

  btn.addEventListener('mouseenter', () => {
    btn.style.transition = 'none'; // Immediate tracking while inside
  });
});
```

### 3. Text Reveal Animations

Headings that reveal themselves create anticipation and feel cinematic. Two approaches:

**Character split (for short hero headlines):**
Each character slides up from behind a mask. The word "DESIGN" arrives one letter at a time.

**Word split (for longer phrases):**
Each word arrives separately with a 75ms stagger. Feels like a typewriter but smoother.

Both require `overflow: hidden` on the parent element to create the mask effect. Never reveal letters by fading — they must slide from behind a hidden edge.

```tsx
const TextReveal = ({ text, delay = 0 }) => (
  <span style={{ display: 'inline-flex', overflow: 'hidden' }}>
    {text.split('').map((char, i) => (
      <motion.span
        key={i}
        initial={{ y: '100%' }}
        whileInView={{ y: 0 }}
        viewport={{ once: true }}
        transition={{ duration: 0.5, delay: delay + i * 0.03, ease: [0.16, 1, 0.3, 1] }}
        style={{ display: 'inline-block' }}
      >
        {char === ' ' ? '\u00A0' : char}
      </motion.span>
    ))}
  </span>
);
```

### 4. Parallax Depth

Three layers, three speeds. This creates a sense that the screen has physical depth.

- **Background layer**: `0.3x` scroll speed. Barely moves. Creates the sensation of a distant horizon.
- **Midground layer**: `0.6x` scroll speed. Content images, subtle elements.
- **Foreground layer**: `1x` scroll speed (normal). The primary content.

Implement with CSS `perspective` for zero JavaScript:
```css
.parallax-container {
  height: 100svh;
  overflow-y: auto;
  perspective: 1px;
  perspective-origin: center;
}
.parallax-bg {
  transform: translateZ(-2px) scale(3);
  position: absolute;
  inset: 0;
  z-index: -1;
}
```

Or use JavaScript-driven scroll listeners for more control. Never use `background-attachment: fixed` — it's a jank machine.

### 5. Grain and Texture Overlays

Pure flat color feels digital and cold. A subtle grain overlay (3–5% opacity) adds photographic warmth and makes the design feel physical, like a printed piece.

```css
.grain-overlay::after {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  opacity: 0.03;
  pointer-events: none;
  z-index: 9999;
  mix-blend-mode: overlay;
}
```

This overlay sits on top of everything using `mix-blend-mode: overlay`. At 3% opacity, it's invisible to most users consciously — but subconsciously, the design feels more premium.

### 6. Smooth Scroll with Momentum

Native browser scroll is abrupt. Lenis provides momentum-based smooth scrolling that makes the page feel like a physical object you're sliding.

```javascript
import Lenis from '@studio-freight/lenis';

const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)), // exponential ease-out
  smoothWheel: true,
  touchMultiplier: 2,
});

function raf(time) {
  lenis.raf(time);
  requestAnimationFrame(raf);
}

requestAnimationFrame(raf);
```

Always integrate Lenis with Framer Motion's `useScroll` and `GSAP ScrollTrigger` when applicable. Without this integration, scroll-based animations will be choppy.

### 7. Color-Shifting Gradients

Static gradients feel designed but fixed. Animated gradients feel alive. CSS `@property` enables smooth interpolation between gradient states — something that was impossible before.

```css
@property --gradient-angle {
  syntax: '<angle>';
  initial-value: 135deg;
  inherits: false;
}

.living-gradient {
  --gradient-angle: 135deg;
  background: linear-gradient(
    var(--gradient-angle),
    #667eea 0%,
    #764ba2 50%,
    #f093fb 100%
  );
  animation: gradient-shift 8s ease-in-out infinite;
}

@keyframes gradient-shift {
  0%, 100% { --gradient-angle: 135deg; }
  50% { --gradient-angle: 315deg; }
}
```

Use this for hero backgrounds, section dividers, and button backgrounds. Never animate more than one gradient simultaneously — it becomes visually overwhelming.

### 8. Loading Choreography

The page load should feel like a performance, not a wall of content suddenly appearing. Orchestrate the entrance:

```
0ms:    Nav fades in
200ms:  Hero headline slides up
500ms:  Subtitle fades in
700ms:  CTA scales in with spring bounce
400ms:  Hero image fades in (parallel with subtitle)
900ms:  Social proof slides up
```

This sequence takes less than 1 second but makes the page feel considered and cinematic. Every element knows when it's supposed to arrive.

```css
.hero__headline { animation: slideUp 0.7s cubic-bezier(0.16, 1, 0.3, 1) 200ms both; }
.hero__subtitle { animation: fadeIn 0.6s ease-out 500ms both; }
.hero__cta { animation: scaleIn 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) 700ms both; }
```

### 9. Footer as a Destination

Most footers are afterthoughts — a list of links dumped below the real content. An Awwwards footer is a destination: it has a visual moment, a CTA, and a final brand impression that sends the user away with a memory.

Three approaches:
- **Large statement typography**: The brand name or a final headline at 100–200px, almost filling the footer
- **Dark inversion**: If the site is light, the footer goes deep dark — a dramatic tonal shift
- **Animated visual**: A looping animation, a parallax image, or a gradient that only appears in the footer

The footer must also answer: "What should the user do next?" If the answer is nothing, they leave without converting. Always include a final CTA.

### 10. Easter Eggs

Easter eggs are small hidden interactions that reward curious users. They turn visitors into fans.

Examples:
- **Console art**: ASCII art of the logo/mascot when DevTools opens
- **Konami code**: Arrow up, up, down, down, left, right, left, right, B, A — triggers a brand moment
- **Cursor hold**: Hold click for 3 seconds — something unexpected happens
- **Shake to shuffle**: Tilt on mobile triggers a random color palette switch
- **Secret link**: An invisible click target in the footer that leads to a "you found it!" page

Easter eggs are not required, but they generate enormous word-of-mouth. When a developer discovers the console art, they tweet about it. That tweet is worth a thousand impressions.

---

## Part 6: Tech Stack Mandate

Every project built with this design system uses this tech stack. No exceptions without explicit client constraint.

### The Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| Framework | Next.js App Router + RSC | Best-in-class performance, SEO, and DX |
| Styling | Tailwind CSS + CSS custom properties | Design tokens in CSS, utility classes for speed |
| Components | shadcn/ui | Unstyled, accessible base components |
| Animation | Framer Motion | Best React animation library, integrates with Lenis |
| Scroll | Lenis (`@studio-freight/lenis`) | Physics-based smooth scroll |
| Fonts | `next/font` (Google or local) | Zero layout shift, automatic optimization |
| Images | `next/image` | WebP conversion, lazy loading, blur placeholders |
| CMS | Sanity (if content-managed) | Best developer experience, real-time preview |
| Deployment | Vercel | Native Next.js hosting, edge network, analytics |

### Code Quality Checkpoints

Before any screen is marked complete, verify:

- [ ] **Lighthouse Performance**: ≥ 90 (run in incognito, desktop)
- [ ] **Largest Contentful Paint**: < 2.5s on simulated 4G
- [ ] **Cumulative Layout Shift**: < 0.1 (no layout shifts after fonts load)
- [ ] **First Input Delay**: < 100ms
- [ ] **Accessibility score**: ≥ 95
- [ ] **No console errors** in production build
- [ ] **No `any` TypeScript types** in component files
- [ ] **All images have `alt` text** (meaningful, not empty)
- [ ] **All interactive elements keyboard-navigable**
- [ ] **`prefers-reduced-motion`** handled on all animations

---

## Part 7: Quick Decision Matrix

When in doubt, use this table to make fast design decisions consistently:

| Decision | Default Choice | Alternative (and when) |
|---------|----------------|------------------------|
| Heading font | Clash Display or Cabinet Grotesk | Playfair Display (editorial/luxury) |
| Body font | General Sans or Satoshi | Inter (only for dashboards/apps) |
| Section padding | `clamp(48px, 8vw, 128px)` | `clamp(32px, 5vw, 80px)` (compact sections) |
| Button hover | `translateY(-2px)` + shadow lift | Scale 1.02 (for icon buttons) |
| Hero height | 100svh (full viewport) | 80vh (when content below needs peeking) |
| Background | Off-white (#FAFAF9 warm, #F8FAFC cool) | Dark (#09090B) for premium/night mode |
| Mobile nav | Full-screen overlay with staggered links | Bottom sheet (for app-like interfaces) |
| Image format | WebP with AVIF fallback | SVG for icons, JPEG for photos over 2MB |
| Page transitions | Crossfade (opacity + y: 12px) | Slide (for clearly sequential flows) |
| Loading states | Skeleton screens | Spinner only for individual async actions |
| Error states | Inline validation with icon + text | Toast for system-level errors |
| Easing (entrance) | `cubic-bezier(0.16, 1, 0.3, 1)` | `cubic-bezier(0.34, 1.56, 0.64, 1)` (bouncy) |
| Easing (morph) | `cubic-bezier(0.83, 0, 0.17, 1)` | `cubic-bezier(0.87, 0, 0.13, 1)` (dramatic) |
| Card radius | `--radius-lg` (12px) | `--radius-2xl` (24px) for softer feel |
| Grid max-width | 1280px marketing | 1440px dashboards |

---

## Part 8: Quality Enforcement

### The Squint Test

Squint at the design until it's blurry. You should still be able to identify:
1. **Where the hero is** — the most visually dominant zone
2. **Where the primary CTA is** — a bright spot that stands out
3. **The visual hierarchy** — at least 3 levels of visual weight
4. **The overall rhythm** — sections should have alternating density
5. **The color story** — one dominant palette reading

If you can't identify all 5 while squinting, the design lacks sufficient contrast and hierarchy. Stop designing details until the macro-composition is correct.

### Quick Reference

| Stage | Tool | Gate | Key Question |
|-------|------|------|-------------|
| 1. Research | WebSearch + WebFetch | References right? | "Are these 4 references the right inspiration?" |
| 2. Explore | SuperDesign `create-design-draft` | Direction right? | "Is this heading the right way?" |
| 3. Iterate | SuperDesign `iterate-design-draft` | Winner chosen? | "Which design wins?" |
| 4. Generate | Stitch `generate_screen_from_text` | Fidelity OK? | "Does the HTML match the design?" |
| 5. Integrate | Manual + Stitch baton | Ship it? | "Ready to move to next screen?" |

### Feedback Patterns to Watch For

Over multiple screens, patterns will emerge in the feedback log. Use these to improve:

| Pattern | Action |
|---------|--------|
| User always swaps a reference type | Pre-filter that reference category |
| User always picks Variant A style | Bias the original draft toward that direction |
| User consistently adjusts colours | Update DESIGN.md colour tokens |
| User requests same typography change | Update init/theme.md font specs |
| Stitch consistently misses a pattern | Add that pattern to the permanent Stitch prompt block |

**After every 3 screens:** Review the feedback log across all screens and update DESIGN.md, init files, and prompt templates to incorporate recurring preferences.

### Common Mistakes

| Mistake | Source | Fix |
|---------|--------|-----|
| Auto-advancing past a gate without asking | Pipeline discipline | NEVER skip a gate. Every diamond is a human decision. |
| Presenting feedback without the 5 dimensions | Pipeline discipline | Always include LAYOUT, COLOUR, TYPOGRAPHY, VIBE, CONTENT |
| Not logging feedback | Pipeline discipline | Every gate decision goes to `.superdesign/feedback/` |
| Iterating forever at Stage 3 | Pipeline discipline | Max 3 rounds. Then ask if we should re-research or proceed. |
| Forgetting previous gate feedback in later stages | Pipeline discipline | Read the feedback log before writing each new prompt. |
| Not updating DESIGN.md after pattern detection | Pipeline discipline | Review log every 3 screens and propagate learnings. |
| Stitch invents new layouts (sidebars, dashboards) | Stage 4 | Start EVERY Stitch prompt with explicit exclusions: "NO sidebars, NO navigation, NO dashboard." List what should NOT appear. Be pixel-specific. |
| Generating only 1 Stitch variation | Stage 4 | ALWAYS generate 2 Stitch variations. Variation A = faithful reproduction, Variation B = pushed emphasis. |
| Vague Stitch prompts | Stage 4 | Stitch needs hyper-specific prompts: exact hex colours, font names + sizes in px, positions, dimensions. |
| Using Inter as a display font | Typography | Inter is for body text only. Pick a display typeface with character. |
| Same weight everywhere | Typography | Use minimum 3 weights: regular, medium, bold. |
| Symmetric layouts on every section | Layout | Introduce asymmetry: offset grids, staggered cards, broken grid moments. |
| No motion on interactive elements | Motion | Every button, link, and card needs hover + active states. |
| Pure #000000 or #FFFFFF as surfaces | Color | Use warm-tinted near-blacks and warm-tinted near-whites. |
| Forgetting dark mode | Color | Dark mode is not optional. Design it intentionally, not by inverting. |
| Generic stock photography in heroes | Image | Never. Use product screenshots, custom illustration, or abstract visuals. |
| Missing `prefers-reduced-motion` | Accessibility | Add the override media query to ALL animated elements. |
| Designing only for desktop | Responsive | Mobile design is not a resize. Redesign the layout for 4-column grid. |
| Skipping the Squint Test | Quality | Run the Squint Test before every gate presentation. |

### Batch Execution

Run the pipeline screen-by-screen in `SITE.md` Section 5 order. Each screen's Gate 5 sets up the next screen's baton.

For parallel execution: Stages 1–3 can run in parallel for independent screens. Stages 4–5 must be sequential for site consistency.

**Cross-screen coherence:** After completing a design phase (e.g., all 3 Phase A screens), do a **cohesion review** — view all screens together and check for visual consistency before moving to the next phase. Run the Squint Test on all screens side by side.
