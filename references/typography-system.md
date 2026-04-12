# Typography System Reference

> Typography is the voice of your design. Choose it like you'd choose the narrator for a film.

## Table of Contents
1. Font Selection Philosophy
2. Approved Font Pairings
3. Type Scale Systems
4. Advanced Typography Techniques
5. Font Loading Strategy
6. Common Mistakes

---

## 1. Font Selection Philosophy

### The Character Test
Every typeface has a personality. Before selecting, describe the personality of your project in three adjectives, then find a typeface that embodies them. Example:

- **Premium, precise, modern** → Neue Montreal, Satoshi, General Sans
- **Warm, editorial, trustworthy** → Playfair Display, Lora, Source Serif 4
- **Bold, rebellious, energetic** → Clash Display, Cabinet Grotesk, Space Grotesk
- **Elegant, luxurious, refined** → Cormorant Garamond, Tenor Sans, Didot
- **Technical, clean, systematic** → JetBrains Mono, IBM Plex, Söhne
- **Playful, friendly, approachable** → Quicksand, Nunito, Fredoka

### Display vs. Body: The Two-Voice Rule
Every site needs two voices:
- **Display voice** (headings, hero text, callouts): Distinctive, characterful, memorable. This is the voice people remember.
- **Body voice** (paragraphs, UI text, labels): Readable, neutral, invisible. This voice should never call attention to itself.

The tension between these two voices creates visual interest. A dramatic display font with a quiet body font creates hierarchy without effort.

### Font Sources — Ranked by Quality
1. **Self-hosted premium** (purchased licenses): Söhne, Circular, GT Walsheim, Untitled Sans — These are what Apple/Stripe-tier sites use.
2. **Google Fonts (curated picks)**: The best free options. See pairings below.
3. **Fontshare by Indian Type Foundry**: Excellent free alternatives — Satoshi, General Sans, Cabinet Grotesk, Clash Display.
4. **Adobe Fonts**: Good if the client has Creative Cloud.

Never use system font stacks for marketing sites. System fonts are for web apps where personality is secondary to performance.

---

## 2. Approved Font Pairings

### Tier 1 — Premium Feel (Free)

**Pairing A: "The Stripe"**
- Display: `Clash Display` (700, 600)
- Body: `General Sans` (400, 500, 600)
- Monospace: `JetBrains Mono` (for code/data)
- Feeling: Modern, confident, technical

**Pairing B: "The Editorial"**
- Display: `Playfair Display` (700, 800, 900)
- Body: `Source Sans 3` (400, 500, 600)
- Accent: `Source Serif 4` (italic, for pull quotes)
- Feeling: Refined, literary, trustworthy

**Pairing C: "The Startup"**
- Display: `Cabinet Grotesk` (800, 900)
- Body: `Satoshi` (400, 500, 700)
- Feeling: Fresh, energetic, tech-forward

**Pairing D: "The Luxury"**
- Display: `Cormorant Garamond` (600, 700)
- Body: `Tenor Sans` (400)
- Feeling: Elegant, high-fashion, gallery-like

**Pairing E: "The Builder"**
- Display: `Space Grotesk` (700) or `Syne` (700, 800)
- Body: `Inter` (400, 500, 600) — Inter is acceptable ONLY as body, never display
- Feeling: Technical, systematic, developer-friendly

**Pairing F: "The Storyteller"**
- Display: `Fraunces` (700, 900 Italic)
- Body: `Outfit` (300, 400, 500)
- Feeling: Warm, narrative, human

### Tier 2 — When Budget Allows Licensed Fonts

| Display | Body | Feeling |
|---|---|---|
| GT Super | Söhne | Premium minimalism |
| Neue Montreal | Neue Montreal Light | Geometric precision |
| Circular | Circular Book | Friendly authority |
| Canela | Graphik | Warm sophistication |
| Reckless Neue | Untitled Sans | Editorial boldness |

---

## 3. Type Scale Systems

> **Token Architecture Note**: Type scale values (`--text-xs` through `--text-7xl`) are primitive tokens. They feed into semantic tokens like `--font-size-body`, `--font-size-heading`, and `--font-size-display`. Component-level styles consume the semantic tokens, never the primitives directly. This keeps the scale decoupled from usage context.

### The Mathematical Scale
Never eyeball font sizes. Use a scale ratio and compute every size from it.

**Recommended Ratios:**
- `1.200` (Minor Third) — Subtle, dense UIs, dashboards
- `1.250` (Major Third) — Versatile, works for most marketing sites ★ DEFAULT
- `1.333` (Perfect Fourth) — Bold, editorial, headline-driven
- `1.500` (Perfect Fifth) — Dramatic, hero-heavy, minimal text
- `1.618` (Golden Ratio) — Maximum drama, use only for single-page sites

### Scale Table (1.250 ratio, 16px base)

```
--text-xs:    0.64rem   (10.24px)  — Captions, fine print
--text-sm:    0.80rem   (12.80px)  — Labels, metadata
--text-base:  1.00rem   (16.00px)  — Body text ★
--text-md:    1.25rem   (20.00px)  — Large body, intros
--text-lg:    1.563rem  (25.00px)  — H4, subheadings
--text-xl:    1.953rem  (31.25px)  — H3
--text-2xl:   2.441rem  (39.06px)  — H2
--text-3xl:   3.052rem  (48.83px)  — H1
--text-4xl:   3.815rem  (61.04px)  — Hero subheading
--text-5xl:   4.768rem  (76.29px)  — Hero heading
--text-6xl:   5.960rem  (95.37px)  — Display/statement
--text-7xl:   7.451rem  (119.2px)  — Maximum impact
```

### Responsive Type Scaling

Use `clamp()` for fluid typography that scales between breakpoints without media queries:

```css
/* Hero heading: 48px at 375px → 120px at 1440px */
.hero-heading {
  font-size: clamp(3rem, 2rem + 5.33vw, 7.5rem);
  line-height: 1.05;
  letter-spacing: -0.03em;
  font-weight: 700;
}

/* Body text: 16px at 375px → 18px at 1440px */
.body-text {
  font-size: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
  line-height: 1.6;
  letter-spacing: 0.01em;
}

/* Section heading: 32px at 375px → 64px at 1440px */
.section-heading {
  font-size: clamp(2rem, 1rem + 4vw, 4rem);
  line-height: 1.1;
  letter-spacing: -0.02em;
  font-weight: 700;
}
```

---

## 4. Advanced Typography Techniques

### Optical Sizing
Large text needs tighter letter-spacing. Small text needs looser. This is non-negotiable:

```css
/* Tighten tracking as size increases */
h1 { letter-spacing: -0.03em; }
h2 { letter-spacing: -0.025em; }
h3 { letter-spacing: -0.02em; }
h4 { letter-spacing: -0.01em; }
body { letter-spacing: 0.01em; }
.caption { letter-spacing: 0.02em; }
.overline { letter-spacing: 0.1em; text-transform: uppercase; }
```

### Text Balancing
Use `text-wrap: balance` for headings to prevent orphaned words:
```css
h1, h2, h3 {
  text-wrap: balance;
}
p {
  text-wrap: pretty; /* prevents orphans in paragraphs */
}
```

### Variable Fonts
When available, use variable fonts for precise weight control and animation:
```css
@font-face {
  font-family: 'Display';
  src: url('/fonts/display-variable.woff2') format('woff2-variations');
  font-weight: 100 900;
  font-display: swap;
}

/* Animate weight on hover */
.animated-text {
  font-weight: 400;
  transition: font-weight 0.3s var(--ease-out-expo);
}
.animated-text:hover {
  font-weight: 700;
}
```

### Typographic Color
"Color" in typography means the visual density of a text block. Achieve good typographic color by:
- Setting paragraph `max-width: 65ch` (the measure)
- Using `1.6` line-height for body
- Adding `margin-bottom` equal to the line-height value between paragraphs
- Never justifying text on the web (ragged right only)

---

## 5. Font Loading Strategy

### The FOUT Prevention Pattern (Next.js)

```tsx
// app/layout.tsx
import { Clash_Display, General_Sans } from 'next/font/google';
// OR for Fontshare/self-hosted:
import localFont from 'next/font/local';

const displayFont = localFont({
  src: [
    { path: '../fonts/ClashDisplay-Bold.woff2', weight: '700' },
    { path: '../fonts/ClashDisplay-Semibold.woff2', weight: '600' },
  ],
  variable: '--font-display',
  display: 'swap',
});

const bodyFont = localFont({
  src: [
    { path: '../fonts/GeneralSans-Regular.woff2', weight: '400' },
    { path: '../fonts/GeneralSans-Medium.woff2', weight: '500' },
    { path: '../fonts/GeneralSans-Semibold.woff2', weight: '600' },
  ],
  variable: '--font-body',
  display: 'swap',
});

export default function RootLayout({ children }) {
  return (
    <html className={`${displayFont.variable} ${bodyFont.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

```css
/* globals.css */
h1, h2, h3, h4 {
  font-family: var(--font-display), serif;
}
body, p, li, a, button, input {
  font-family: var(--font-body), sans-serif;
}
```

---

## 7. Tailwind v4 Font Integration

### Registering Fonts via `@theme`

In Tailwind v4, register font families inside `@theme` so they become utility classes (`font-display`, `font-body`, etc.):

```css
/* globals.css */
@import "tailwindcss";

@theme {
  /* Font family tokens — maps to font-display, font-body, font-mono */
  --font-display: 'Clash Display', serif;
  --font-body:    'General Sans', sans-serif;
  --font-mono:    'JetBrains Mono', monospace;
}
```

### Bridge Pattern: `next/font/local` → CSS Variable → `@theme`

`next/font` injects a CSS variable on `<html>`. Alias that variable into your `@theme` so Tailwind utilities pick it up:

```tsx
// app/layout.tsx
import localFont from 'next/font/local';

const displayFont = localFont({
  src: [
    { path: '../fonts/ClashDisplay-Bold.woff2', weight: '700' },
    { path: '../fonts/ClashDisplay-Semibold.woff2', weight: '600' },
  ],
  variable: '--font-display-loaded', // Next.js injects this on <html>
  display: 'swap',
});

const bodyFont = localFont({
  src: [
    { path: '../fonts/GeneralSans-Regular.woff2', weight: '400' },
    { path: '../fonts/GeneralSans-Medium.woff2', weight: '500' },
    { path: '../fonts/GeneralSans-Semibold.woff2', weight: '600' },
  ],
  variable: '--font-body-loaded',
  display: 'swap',
});

export default function RootLayout({ children }) {
  return (
    <html className={`${displayFont.variable} ${bodyFont.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

```css
/* globals.css — bridge next/font variables into @theme */
@import "tailwindcss";

@theme {
  --font-display: var(--font-display-loaded), serif;
  --font-body:    var(--font-body-loaded), sans-serif;
}
```

Now `font-display` and `font-body` are available as Tailwind utilities throughout the project.

---

## 6. Common Mistakes

| Mistake | Why It's Bad | Fix |
|---|---|---|
| Using Inter for everything | Invisible, generic, says "I didn't try" | Pick a display font with character |
| Same weight everywhere | Destroys hierarchy, creates visual monotone | Use min 3 weights: regular, medium, bold |
| No letter-spacing adjustment | Large text looks too loose, small text too tight | Apply optical sizing rules above |
| Arbitrary font sizes | Creates visual noise, no rhythm | Use mathematical type scale |
| Line-height too tight on body | Unreadable, cramped, hostile | Minimum 1.5 for body text |
| Measure too wide | Lines too long, eyes get lost | Cap at `max-width: 65ch` |
| All caps without tracking | Looks crude and amateurish | Always add `letter-spacing: 0.05em+` to uppercase |
| Mixing more than 3 fonts | Visual cacophony | Two fonts. Three absolute maximum. |
