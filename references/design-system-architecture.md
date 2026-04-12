# Design System Architecture Reference

> Tokens are the bridge between design and code. — W3C DTCG Community Group

## Table of Contents
1. Three-Layer Token Architecture
2. Stitch Preset Integration
3. DESIGN.md Template
4. Tailwind v4 Integration
5. Token Naming Convention
6. Dark Mode Token Strategy
7. Design System Governance

---

## 1. Three-Layer Token Architecture

Based on the W3C Design Tokens Community Group specification (stable v1, October 2025). Every design system has three layers. Skipping the semantic layer costs you at every theme change.

### Layer 1: Primitive Tokens (Raw Values)

These are the raw palette. They never appear in component code.

```css
:root {
  /* ─── COLOR PRIMITIVES ─────────────────────────── */
  --blue-50:  oklch(0.97 0.02 250);
  --blue-100: oklch(0.93 0.04 250);
  --blue-200: oklch(0.87 0.08 250);
  --blue-300: oklch(0.78 0.13 250);
  --blue-400: oklch(0.68 0.18 250);
  --blue-500: oklch(0.58 0.22 250);
  --blue-600: oklch(0.50 0.22 250);
  --blue-700: oklch(0.42 0.20 250);
  --blue-800: oklch(0.34 0.16 250);
  --blue-900: oklch(0.27 0.12 250);
  --blue-950: oklch(0.20 0.08 250);

  /* ─── SPACING PRIMITIVES (8px base) ────────────── */
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

  /* ─── RADIUS PRIMITIVES ────────────────────────── */
  --radius-none: 0;
  --radius-xs: 2px;
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-2xl: 24px;
  --radius-full: 9999px;

  /* ─── DURATION PRIMITIVES ──────────────────────── */
  --duration-instant: 0ms;
  --duration-fast: 150ms;
  --duration-base: 250ms;
  --duration-slow: 400ms;
  --duration-slower: 700ms;
  --duration-slowest: 1000ms;

  /* ─── EASING PRIMITIVES ────────────────────────── */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-expo: cubic-bezier(0.7, 0, 0.84, 0);
  --ease-in-out-quint: cubic-bezier(0.83, 0, 0.17, 1);
  --ease-out-back: cubic-bezier(0.34, 1.56, 0.64, 1);
  --spring-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);
  --spring-gentle: cubic-bezier(0.22, 1.0, 0.36, 1.0);

  /* ─── Z-INDEX PRIMITIVES ───────────────────────── */
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

### Layer 2: Semantic Tokens (Purpose-Driven)

These map primitives to meaning. Components reference ONLY semantic tokens.

```css
:root {
  /* ─── COLOR SEMANTIC ───────────────────────────── */
  --color-primary: var(--blue-500);
  --color-primary-hover: var(--blue-600);
  --color-primary-active: var(--blue-700);
  --color-primary-subtle: var(--blue-50);

  --color-success: oklch(0.55 0.18 155);
  --color-warning: oklch(0.70 0.18 75);
  --color-error: oklch(0.55 0.22 25);
  --color-info: oklch(0.55 0.18 250);

  --color-bg-primary: var(--neutral-50);
  --color-bg-secondary: var(--neutral-100);
  --color-bg-tertiary: var(--neutral-200);
  --color-bg-inverse: var(--neutral-900);
  --color-bg-elevated: #FFFFFF;

  --color-text-primary: var(--neutral-900);
  --color-text-secondary: var(--neutral-600);
  --color-text-tertiary: var(--neutral-400);
  --color-text-inverse: var(--neutral-50);
  --color-text-on-primary: #FFFFFF;

  --color-border-default: var(--neutral-200);
  --color-border-hover: var(--neutral-300);
  --color-border-focus: var(--color-primary);

  /* ─── SPACING SEMANTIC ─────────────────────────── */
  --space-section: clamp(var(--space-12), 8vw, var(--space-32));
  --space-section-hero: clamp(var(--space-16), 12vw, var(--space-48));
  --space-component: clamp(var(--space-6), 4vw, var(--space-12));
  --space-element: clamp(var(--space-4), 2vw, var(--space-8));

  /* ─── RADIUS SEMANTIC ──────────────────────────── */
  --radius-interactive: var(--radius-md);
  --radius-card: var(--radius-lg);
  --radius-modal: var(--radius-xl);
  --radius-pill: var(--radius-full);

  /* ─── MOTION SEMANTIC ──────────────────────────── */
  --motion-entrance: var(--duration-slow) var(--ease-out-expo);
  --motion-exit: var(--duration-fast) var(--ease-in-expo);
  --motion-morph: var(--duration-base) var(--ease-in-out-quint);
  --motion-micro: var(--duration-fast) var(--ease-out-expo);
}
```

### Layer 3: Component Tokens (Implementation-Specific)

These are optional — use only when components need to deviate from semantic defaults.

```css
:root {
  /* ─── BUTTON COMPONENT ─────────────────────────── */
  --button-bg-primary: var(--color-primary);
  --button-bg-primary-hover: var(--color-primary-hover);
  --button-text-primary: var(--color-text-on-primary);
  --button-radius: var(--radius-interactive);
  --button-height: 48px;
  --button-height-sm: 36px;
  --button-height-lg: 56px;
  --button-padding-x: var(--space-6);

  /* ─── INPUT COMPONENT ──────────────────────────── */
  --input-bg: var(--color-bg-primary);
  --input-border: var(--color-border-default);
  --input-border-focus: var(--color-border-focus);
  --input-radius: var(--radius-interactive);
  --input-height: 48px;

  /* ─── CARD COMPONENT ───────────────────────────── */
  --card-bg: var(--color-bg-elevated);
  --card-border: var(--color-border-default);
  --card-radius: var(--radius-card);
  --card-padding: var(--space-6);

  /* ─── NAV COMPONENT ────────────────────────────── */
  --nav-height: 64px;
  --nav-height-scrolled: 48px;
  --nav-bg: transparent;
  --nav-bg-scrolled: rgba(255, 255, 255, 0.72);
  --nav-blur: 20px;
}
```

### The Rule: Components → Semantic → Primitives

```
Component code references → Component tokens (if they exist)
                          → Semantic tokens (default)
                          → NEVER primitive tokens directly
```

---

## 2. Stitch Preset Integration

### How Presets Map to Tokens

Each Stitch preset provides a visual foundation. Customize on top of it:

| Preset | Color Mode | Roundness | Color Variant | Typical Neutrals |
|--------|-----------|-----------|---------------|-----------------|
| Beam | LIGHT | ROUND_EIGHT | TONAL_SPOT | Cool (#F8FAFC) |
| Luxury | DARK | ROUND_FOUR | MONOCHROME | Warm-dark (#1A1A1A) |
| Newsprint | LIGHT | ROUND_FOUR | TONAL_SPOT | Warm (#FAFAF9) |
| Kinetic | DARK | ROUND_EIGHT | VIBRANT | Cool-dark (#0F172A) |
| Motion | DARK | ROUND_TWELVE | VIBRANT | Cool-dark (#0A0A0A) |
| Playful | LIGHT | ROUND_FULL | VIBRANT | Warm (#FFF7ED) |
| Neumorphism | LIGHT | ROUND_TWELVE | TONAL_SPOT | Neutral (#E5E5E5) |
| Uber Design System | LIGHT | ROUND_FOUR | MONOCHROME | Cool (#F8FAFC) |
| Bauhaus | LIGHT | ROUND_FOUR | VIBRANT | White (#FFFFFF) |
| Hand-draw | LIGHT | ROUND_TWELVE | TONAL_SPOT | Warm (#FFFBEB) |
| Win98 | LIGHT | ROUND_FOUR | TONAL_SPOT | Gray (#C0C0C0) |

### Customization Layers

Apply customizations in this order:
1. **Start with preset** — sets the foundation
2. **Override brand color** — `customColor` with primary hex
3. **Override fonts** — `headlineFont` + `bodyFont` from contract
4. **Override roundness** — if contract specifies a different feel
5. **Inject DESIGN.md** — `designMd` field with full token system + personality brief
6. **Apply** — call `apply_design_system` to all screens

### Stitch `create_design_system` Call Template

```javascript
{
  projectId: "{from .design-forge/stitch.json}",
  headlineFont: "{STITCH_FONT_ENUM}",
  bodyFont: "{STITCH_FONT_ENUM}",
  customColor: "{primary hex from contract}",
  colorMode: "LIGHT | DARK",
  roundness: "ROUND_FOUR | ROUND_EIGHT | ROUND_TWELVE | ROUND_FULL",
  colorVariant: "TONAL_SPOT | VIBRANT | MONOCHROME",
  designMd: `
    ## Brand Personality
    Archetype: {from contract}
    Emotional Target: {from contract}
    Visual Metaphor: {from contract}

    ## Token Foundation
    {paste full primitive + semantic tokens}

    ## Design Directives
    {paste accumulated contract directives}

    ## Hard Constraints
    {paste deal-breakers and exclusions}
  `
}
```

---

## 3. DESIGN.md Template

This file is the single source of truth. Stitch reads it with every prompt. Keep it comprehensive but structured.

```markdown
# DESIGN.md — {Project Name}

## 1. Brand Identity
- **Name:** {brand name}
- **Archetype:** {archetype}
- **Personality:** {3 adjectives}
- **Emotional Target:** {2-3 feelings}
- **Visual Metaphor:** {physical space}
- **One Word:** {essence}

## 2. Color System

### Primary Palette
- **Champion Color:** {hex} — {emotional rationale}
- **Primary Scale:** {50-950 in OKLCH}
- **Neutral Base:** {warm/cool} — {50-950 hex values}

### Semantic Colors
- Background: {primary}, {secondary}, {tertiary}
- Text: {primary}, {secondary}, {tertiary}
- Border: {default}, {hover}, {focus}
- Success: {hex} | Warning: {hex} | Error: {hex} | Info: {hex}

### Gradient (if applicable)
- Hero gradient: {definition}
- Accent gradient: {definition}

## 3. Typography

### Font Pairing
- **Display:** {font name} ({weights}) — for headings, hero text
- **Body:** {font name} ({weights}) — for paragraphs, UI text
- **Monospace:** {font name} (if needed) — for code, data

### Type Scale (ratio: {1.250 default})
- text-xs: {value} — captions
- text-sm: {value} — labels
- text-base: {value} — body
- text-lg: {value} — subheadings
- text-xl: {value} — H4
- text-2xl: {value} — H3
- text-3xl: {value} — H2
- text-4xl: {value} — H1
- text-5xl: {value} — hero subheading
- text-6xl: {value} — hero heading
- text-7xl: {value} — display/statement

### Optical Sizing
- h1: letter-spacing -0.03em, line-height 1.05
- h2: letter-spacing -0.025em, line-height 1.1
- h3: letter-spacing -0.02em, line-height 1.15
- body: letter-spacing 0.01em, line-height 1.6
- caption: letter-spacing 0.02em
- overline: letter-spacing 0.1em, text-transform uppercase

## 4. Spacing & Layout

### Spacing Scale (8px base)
4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64 / 80 / 96 / 128 / 192

### Grid
- Desktop: 12 columns, {gutter}px gutter, max-width {value}px
- Tablet: 8 columns, {gutter}px gutter
- Mobile: 4 columns, 16px gutter, 16px margin

### Section Padding
- Standard: clamp(48px, 8vw, 128px)
- Hero: clamp(64px, 12vw, 192px)
- Compact: clamp(32px, 5vw, 80px)

## 5. Motion & Interaction

### Animation Library: GSAP + ScrollTrigger
- Entrance easing: cubic-bezier(0.16, 1, 0.3, 1)
- Exit easing: cubic-bezier(0.7, 0, 0.84, 0)
- Morph easing: cubic-bezier(0.83, 0, 0.17, 1)
- Spring: cubic-bezier(0.34, 1.56, 0.64, 1)

### Duration Scale
- Micro: 150ms (button states)
- Component: 250ms (dropdowns, toggles)
- Section: 400ms (scroll reveals)
- Page: 700ms (route transitions)
- Cinematic: 1000ms (hero entrance)

### Motion Rules
- Always gsap.fromTo() — never gsap.from()
- Always wrap in gsap.matchMedia for reduced-motion
- Stagger siblings: 50-100ms delay
- Smooth scroll: Lenis with 1.2s duration

## 6. Design System Notes for Stitch Generation

### Stitch Preset: {preset name}
### Design System Asset ID: {from stitch.json}

### Personality Brief
{Copy from contract — archetype, emotional target, metaphor}

### Token Foundation
{Copy full primitive + semantic CSS variables}

### Directives for Every Screen
- {directive 1 from contract}
- {directive 2 from contract}
- {accumulated feedback directives}

### Hard Exclusions
- {exclusion 1}
- {exclusion 2}

## 7. Component Conventions

### Border Radius
- Interactive elements (buttons, inputs): {value}
- Cards: {value}
- Modals: {value}
- Pills/tags: {value}

### Shadows
- xs: {definition}
- sm: {definition}
- md: {definition}
- lg: {definition}
- xl: {definition}
- brand: {definition}

### Button Hierarchy
- Primary: filled, brand color, one per viewport
- Secondary: ghost/outline
- Tertiary: text + arrow

### Image Treatment
- Format: WebP + AVIF, JPEG fallback
- Hero: priority loading, blur placeholder
- Below-fold: lazy loading
- All images: explicit width/height, meaningful alt text
```

---

## 4. Tailwind v4 Integration

### @theme Directive (CSS-First Tokens)

Tailwind v4 uses `@theme` to define tokens directly in CSS:

```css
/* app.css */
@import "tailwindcss";

@theme {
  /* Map design tokens to Tailwind utilities */
  --color-primary: oklch(0.58 0.22 250);
  --color-primary-hover: oklch(0.50 0.22 250);
  --color-bg-primary: #FAFAF9;
  --color-bg-secondary: #F5F5F4;
  --color-text-primary: #1C1917;
  --color-text-secondary: #57534E;

  --font-display: "Clash Display", serif;
  --font-body: "General Sans", sans-serif;

  --radius-interactive: 8px;
  --radius-card: 12px;

  --spacing-section: clamp(48px, 8vw, 128px);
}
```

This generates utilities like `bg-primary`, `text-text-primary`, `rounded-interactive`, etc.

### Token → Tailwind Mapping

| Token Layer | Tailwind v4 Pattern |
|-------------|-------------------|
| Primitive colors | Define in `@theme` as `--color-{name}-{shade}` |
| Semantic colors | Define in `@theme` as `--color-{purpose}` |
| Spacing | Define in `@theme` as `--spacing-{name}` |
| Radius | Define in `@theme` as `--radius-{name}` |
| Fonts | Define in `@theme` as `--font-{name}` |
| Shadows | Use `@utility` for complex multi-layer shadows |

---

## 5. Token Naming Convention

Follow the W3C DTCG recommended structure: `{category}-{role}-{variant}-{state}`

### Examples

```
color-primary              → the primary brand color
color-primary-hover        → primary on hover
color-bg-primary           → primary background
color-bg-elevated          → elevated surface (cards, modals)
color-text-primary         → main text color
color-text-on-primary      → text on primary-colored backgrounds
color-border-focus         → border when focused

spacing-section            → vertical padding between sections
spacing-component          → gap between components
spacing-element            → gap between sibling elements

radius-interactive         → buttons, inputs, toggles
radius-card                → card containers
radius-modal               → modal dialogs

motion-entrance            → duration + easing for entering elements
motion-exit                → duration + easing for exiting elements
motion-morph               → duration + easing for in-place changes
```

### Rules
- Components reference semantic tokens, NEVER primitives
- Use descriptive names (`color-bg-elevated`), not abstract names (`color-3`)
- State variants use suffixes: `-hover`, `-active`, `-focus`, `-disabled`
- Keep names consistent: if it's `color-bg-*`, don't mix in `background-*`

---

## 6. Dark Mode Token Strategy

Dark mode is NOT inverting colors. It requires an intentional parallel palette.

### Implementation

```css
:root {
  /* Light mode (default) */
  --color-bg-primary: #FFFFFF;
  --color-bg-secondary: #F8FAFC;
  --color-bg-tertiary: #F1F5F9;
  --color-bg-elevated: #FFFFFF;
  --color-text-primary: #0F172A;
  --color-text-secondary: #475569;
  --color-text-tertiary: #94A3B8;
  --color-border-default: #E2E8F0;
  --color-border-subtle: #F1F5F9;
}

[data-theme="dark"] {
  --color-bg-primary: #09090B;
  --color-bg-secondary: #111113;
  --color-bg-tertiary: #19191D;
  --color-bg-elevated: #1C1C21;     /* lighter = higher elevation */
  --color-text-primary: #FAFAFA;
  --color-text-secondary: #A1A1AA;
  --color-text-tertiary: #52525B;
  --color-border-default: #27272A;
  --color-border-subtle: #1C1C21;
}
```

### Dark Mode Principles
- Use warm-tinted near-blacks (#09090B), not pure #000000
- Elevation is shown with LIGHTER surfaces, not shadows
- Reduce image brightness and saturation: `filter: brightness(0.9) saturate(0.95)`
- Borders become more important (use subtle light borders)
- Primary brand color may need lightened variant for dark backgrounds
- Test contrast ratios independently for dark mode

---

## 7. Design System Governance

Based on Brad Frost's 10-step governance process. Prevents design drift.

### Decision Log

Maintain `.design-forge/decisions.md`:

```markdown
# Design Decision Log

## {date} — {decision}
- **Context:** {what prompted the decision}
- **Decision:** {what was decided}
- **Rationale:** {why}
- **Consequences:** {what this affects}
- **Contract Update:** {what was added to the Design Contract}
```

### Drift Prevention Metrics

Track these after every 3 screens:
- **Token override frequency:** How often do screens override semantic tokens?
- **Variant sprawl:** Are new one-off values appearing?
- **Contract compliance:** Does every screen pass the contract validation?
- **Feedback repetition:** Are the same adjustments requested repeatedly?

If drift is detected → update tokens, DESIGN.md, and Stitch design system to absorb the pattern.

### The Update Cycle

After every 3 completed screens:
1. Review all feedback logs in `.design-forge/feedback/`
2. Identify recurring patterns (same adjustment requested 2+ times)
3. Update DESIGN.md tokens to reflect reality
4. Update Stitch design system `designMd` field
5. Update Design Contract soft preferences
6. Log the update in decisions.md
