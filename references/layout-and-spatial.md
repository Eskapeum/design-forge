# Layout & Spatial Design Reference

> The grid is the skeleton. Spacing is the breath. Composition is the soul.

## Table of Contents
1. Grid Architecture
2. The Spacing Philosophy
3. Compositional Techniques
4. Responsive Architecture
5. Breakpoint Strategy
6. Advanced Layout Patterns

---

## 1. Grid Architecture

### The 12-Column System
Every Awwwards-level site is built on a grid. The grid provides structure. Breaking the grid provides drama. You need both.

```css
.grid-container {
  --grid-columns: 12;
  --grid-gutter: 32px;
  --grid-margin: clamp(16px, 4vw, 80px);
  --grid-max-width: 1280px;

  display: grid;
  grid-template-columns: repeat(var(--grid-columns), 1fr);
  gap: var(--grid-gutter);
  max-width: var(--grid-max-width);
  margin-inline: auto;
  padding-inline: var(--grid-margin);
}

/* Responsive grid */
@media (max-width: 768px) {
  .grid-container {
    --grid-columns: 4;
    --grid-gutter: 16px;
  }
}

@media (min-width: 769px) and (max-width: 1024px) {
  .grid-container {
    --grid-columns: 8;
    --grid-gutter: 24px;
  }
}
```

### Column Spanning Patterns

```css
/* Full bleed — breaks out of the grid */
.full-bleed {
  grid-column: 1 / -1;
  margin-inline: calc(-1 * var(--grid-margin));
  padding-inline: var(--grid-margin);
}

/* Content widths */
.narrow { grid-column: 4 / 10; }     /* 6 cols — ideal for body text */
.medium { grid-column: 3 / 11; }     /* 8 cols — content with some imagery */
.wide { grid-column: 2 / 12; }       /* 10 cols — content-heavy sections */
.full { grid-column: 1 / -1; }       /* 12 cols — hero, image grids */

/* Asymmetric splits — THE Awwwards move */
.split-40-60 {
  display: grid;
  grid-template-columns: 5fr 7fr;
  gap: var(--grid-gutter);
}

.split-golden {
  display: grid;
  grid-template-columns: 1fr 1.618fr;
  gap: var(--grid-gutter);
}
```

---

## 2. The Spacing Philosophy

### Vertical Rhythm
All vertical spacing should be multiples of your base unit (8px). This creates rhythm:

```
8px   — micro (icon-to-label, inline gaps)
16px  — tight (related elements within a group)
24px  — default (between form fields, list items)
32px  — comfortable (between content blocks)
48px  — section inner padding
64px  — between distinct groups
96px  — section separation (desktop)
128px — major landmark separation
192px — cinematic breath (hero padding)
```

### The "Relationship Proximity" Rule
Spacing communicates relationships:
- **4–8px**: These elements are a single unit (icon + label)
- **16–24px**: These elements are siblings (items in a list)
- **32–48px**: These elements are cousins (groups within a section)
- **64–128px**: These elements are strangers (separate sections)

If two things look related but shouldn't be, increase spacing. If two things look disconnected but belong together, decrease spacing. Spacing is information architecture.

### Section Padding Formula

```css
/* Responsive section padding */
.section {
  padding-block: clamp(48px, 8vw, 128px);
}

/* Hero sections get more breath */
.hero-section {
  padding-block: clamp(64px, 12vw, 192px);
}

/* Compact sections (features grid, logos bar) */
.compact-section {
  padding-block: clamp(32px, 5vw, 80px);
}
```

---

## 3. Compositional Techniques

### The Z-Pattern (for marketing pages)
The eye naturally scans in a Z shape on content-light pages:
1. Top-left (logo) → Top-right (CTA)
2. Diagonal sweep to bottom-left (content start)
3. Bottom-left → Bottom-right (next action)

Place your most important elements along this Z-path.

### The F-Pattern (for content-heavy pages)
For pages with lots of text, the eye scans in an F:
1. Horizontal sweep across the top
2. Second horizontal sweep slightly lower
3. Vertical scan down the left side

Front-load important information at the beginning of each section.

### Asymmetry Is Sophistication
Symmetric layouts feel safe and corporate. Asymmetric layouts feel designed and intentional. Ways to introduce asymmetry:
- **Offset grids**: Content sits on 7 columns, not centered
- **Staggered cards**: Cards at different vertical positions
- **Oversized numbers/letters**: A huge "01" that bleeds off the edge
- **Mixed alignment**: Left-aligned heading, centered subtext
- **Broken grid moments**: An image that extends past its column

```css
/* Staggered card layout */
.staggered-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}
.staggered-grid > :nth-child(2) {
  margin-top: 64px; /* Second card drops down */
}
.staggered-grid > :nth-child(3) {
  margin-top: 128px; /* Third card drops further */
}
```

### The "Hero + Scroll Reveal" Pattern
The most common Awwwards pattern:
1. Full-viewport hero with minimal content
2. Scroll down → first content section fades/slides in
3. Each subsequent section reveals with slight stagger
4. The page feels like a presentation being unveiled

### Negative Space as Content
Awwwards winners use negative space aggressively. The white space IS the design. Rules:
- Never fill a section just because it looks "empty"
- A section with ONE centered sentence and 200px padding is more powerful than a dense info block
- Let images breathe — add 32–64px padding inside image containers
- Between hero and first section: minimum 128px gap

---

## 4. Responsive Architecture

### The Fluid Design Approach
Instead of designing for fixed breakpoints, design a fluid system:

```css
/* Fluid spacing using clamp */
:root {
  --space-section: clamp(48px, 8vw, 128px);
  --space-component: clamp(24px, 4vw, 48px);
  --space-element: clamp(16px, 2vw, 32px);

  /* Fluid max-width for text content */
  --max-text-width: min(65ch, 90vw);
  --max-content-width: min(1280px, 100vw - 32px);
}
```

### Container Queries (The Modern Way)
For component-level responsiveness:

```css
.card-container {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 24px;
  }
}

@container card (max-width: 399px) {
  .card {
    display: flex;
    flex-direction: column;
  }
}
```

---

## 5. Breakpoint Strategy

### The Recommended Breakpoints

```css
/* Mobile first */
--bp-sm: 640px;    /* Large phones, landscape */
--bp-md: 768px;    /* Tablets */
--bp-lg: 1024px;   /* Small laptops */
--bp-xl: 1280px;   /* Standard desktop */
--bp-2xl: 1536px;  /* Large desktop */
--bp-3xl: 1920px;  /* Ultra-wide */
```

### Layout Shifts Per Breakpoint

| Breakpoint | Columns | Gutter | Margin | Nav Style |
|---|---|---|---|---|
| < 640px | 4 | 16px | 16px | Hamburger overlay |
| 640–767px | 4 | 20px | 24px | Hamburger overlay |
| 768–1023px | 8 | 24px | 32px | Condensed horizontal |
| 1024–1279px | 12 | 28px | 48px | Full horizontal |
| 1280–1535px | 12 | 32px | 64px | Full horizontal |
| ≥ 1536px | 12 | 32px | 80px | Full horizontal |

---

## 6. Advanced Layout Patterns

### The "Bento Grid" (Apple-style)
```css
.bento-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(200px, auto);
  gap: 16px;
}

/* Feature card spans */
.bento-large { grid-column: span 2; grid-row: span 2; }
.bento-wide { grid-column: span 2; grid-row: span 1; }
.bento-tall { grid-column: span 1; grid-row: span 2; }
.bento-small { grid-column: span 1; grid-row: span 1; }

@media (max-width: 768px) {
  .bento-grid { grid-template-columns: repeat(2, 1fr); }
  .bento-large { grid-column: span 2; }
}
```

### The "Sticky Side-by-Side" (Linear/Vercel-style)
Content scrolls on the left. Visual stays pinned on the right.

```css
.sticky-split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
}

.sticky-split__content {
  /* Scrolling content */
}

.sticky-split__visual {
  position: sticky;
  top: 100px;
  height: fit-content;
}
```

### The "Full-Bleed Alternating" Pattern
Sections alternate between constrained content and full-width visuals:

```css
.alternating-section:nth-child(odd) {
  max-width: var(--max-content-width);
  margin-inline: auto;
  padding-inline: var(--grid-margin);
}

.alternating-section:nth-child(even) {
  width: 100%;
  padding: 0; /* Full bleed image/video */
}
```

### The "Horizontal Scroll" Showpiece
For portfolio or feature showcases:

```css
.horizontal-scroll {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  gap: 24px;
  padding-inline: var(--grid-margin);
  scrollbar-width: none;
}

.horizontal-scroll::-webkit-scrollbar { display: none; }

.horizontal-scroll > * {
  flex: 0 0 min(400px, 85vw);
  scroll-snap-align: start;
}
```
