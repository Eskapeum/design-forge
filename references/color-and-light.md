# Color & Light System Reference

> Color is emotion. Light is dimension. Together they create atmosphere.

## Table of Contents
1. Color Philosophy
2. Palette Construction Method
3. Gradient Mastery
4. Shadow & Depth System
5. Glassmorphism & Frosted Effects
6. Dark Mode Architecture
7. CSS Implementation

---

## 1. Color Philosophy

### The Emotion Map
Every color evokes something. Choose deliberately:

| Color Family | Evokes | Best For |
|---|---|---|
| Deep Navy (#0A1628) | Trust, depth, authority | Finance, legal, enterprise |
| Warm Black (#1A1A1A) | Sophistication, editorial | Luxury, portfolio, fashion |
| Soft White (#FAFAF9) | Warmth, paper, craftsmanship | Editorial, artisan, organic |
| Cool White (#F8FAFC) | Clean, technical, precise | SaaS, developer tools, medical |
| Indigo (#4F46E5) | Innovation, intelligence | AI, tech, startup |
| Emerald (#059669) | Growth, health, wealth | Finance, wellness, sustainability |
| Amber (#D97706) | Energy, warmth, urgency | Food, construction, alerts |
| Rose (#E11D48) | Passion, boldness, creativity | Fashion, entertainment, art |
| Violet (#7C3AED) | Creativity, premium, magic | Creative tools, gaming, music |

### The "One Color Does The Work" Rule
The best palettes have ONE color that carries all the emotional weight. Everything else is neutral support. Look at Stripe — they have dozens of colors, but the hero gradient IS the brand. Look at Linear — one shade of indigo does all the heavy lifting.

Pick your champion color. Give it the spotlight. Make neutrals serve it.

---

## 2. Palette Construction Method

> **Three-Layer Token Architecture**: Color tokens are organized in three layers — primitives (raw values like `--brand-500`), semantic tokens (meaning-based like `--color-primary`), and component tokens (context-specific like `--btn-bg`). This maps 1:1 to CSS custom properties at each layer. See `design-system-architecture.md` for the full token hierarchy and implementation.

### Step 1: Choose Your Neutral Base
This is 60–70% of what users see. Get it right.

**Warm Neutral Scale (for friendly, editorial, organic brands):**
```css
--neutral-50:  #FAFAF9;
--neutral-100: #F5F5F4;
--neutral-200: #E7E5E4;
--neutral-300: #D6D3D1;
--neutral-400: #A8A29E;
--neutral-500: #78716C;
--neutral-600: #57534E;
--neutral-700: #44403C;
--neutral-800: #292524;
--neutral-900: #1C1917;
--neutral-950: #0C0A09;
```

**Cool Neutral Scale (for technical, precise, modern brands):**
```css
--neutral-50:  #F8FAFC;
--neutral-100: #F1F5F9;
--neutral-200: #E2E8F0;
--neutral-300: #CBD5E1;
--neutral-400: #94A3B8;
--neutral-500: #64748B;
--neutral-600: #475569;
--neutral-700: #334155;
--neutral-800: #1E293B;
--neutral-900: #0F172A;
--neutral-950: #020617;
```

### Step 2: Generate Your Brand Color Scale
From your champion color, generate a 10-step scale. Use OKLCH for perceptual uniformity:

```css
/* Example: Indigo brand scale in OKLCH */
--brand-50:  oklch(0.97 0.02 275);
--brand-100: oklch(0.93 0.04 275);
--brand-200: oklch(0.87 0.08 275);
--brand-300: oklch(0.78 0.13 275);
--brand-400: oklch(0.68 0.18 275);
--brand-500: oklch(0.58 0.22 275);  /* ← Primary */
--brand-600: oklch(0.50 0.22 275);
--brand-700: oklch(0.42 0.20 275);
--brand-800: oklch(0.34 0.16 275);
--brand-900: oklch(0.27 0.12 275);
--brand-950: oklch(0.20 0.08 275);
```

### Step 3: Define Semantic Colors
Map brand colors to semantic meaning:

```css
/* Semantic tokens */
--color-primary: var(--brand-500);
--color-primary-hover: var(--brand-600);
--color-primary-active: var(--brand-700);
--color-primary-subtle: var(--brand-50);

--color-success: #059669;
--color-warning: #D97706;
--color-error: #DC2626;
--color-info: #2563EB;

--color-text-primary: var(--neutral-900);
--color-text-secondary: var(--neutral-600);
--color-text-tertiary: var(--neutral-400);
--color-text-inverse: var(--neutral-50);

--color-bg-primary: var(--neutral-50);
--color-bg-secondary: var(--neutral-100);
--color-bg-tertiary: var(--neutral-200);
--color-bg-inverse: var(--neutral-900);

--color-border-default: var(--neutral-200);
--color-border-hover: var(--neutral-300);
--color-border-focus: var(--brand-500);
```

---

## 3. Gradient Mastery

### The "Stripe Gradient" Technique
Stripe's gradients work because they use multiple color stops with careful hue rotation:

```css
/* Stripe-style hero gradient */
.hero-gradient {
  background: linear-gradient(
    135deg,
    #0A2FFF 0%,
    #6B3FA0 25%,
    #E040FB 50%,
    #FF6F00 75%,
    #FFC107 100%
  );
}

/* Animated version using @property */
@property --gradient-angle {
  syntax: '<angle>';
  initial-value: 135deg;
  inherits: false;
}

.animated-gradient {
  --gradient-angle: 135deg;
  background: linear-gradient(
    var(--gradient-angle),
    #667eea,
    #764ba2,
    #f093fb
  );
  animation: gradient-rotate 8s ease-in-out infinite;
}

@keyframes gradient-rotate {
  0%, 100% { --gradient-angle: 135deg; }
  50% { --gradient-angle: 315deg; }
}
```

### Mesh Gradients
For organic, Apple-like backgrounds:

```css
.mesh-gradient {
  background-color: #0A0A0A;
  background-image:
    radial-gradient(at 20% 80%, hsla(220, 95%, 50%, 0.3) 0px, transparent 50%),
    radial-gradient(at 80% 20%, hsla(280, 95%, 50%, 0.25) 0px, transparent 50%),
    radial-gradient(at 50% 50%, hsla(340, 95%, 50%, 0.15) 0px, transparent 50%),
    radial-gradient(at 80% 80%, hsla(180, 95%, 50%, 0.2) 0px, transparent 50%);
}
```

### Text Gradients
For hero headlines:
```css
.gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #f093fb 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## 4. Shadow & Depth System

### Layered Shadow Scale
Never use a single `box-shadow`. Realistic shadows require multiple layers:

```css
/* Elevation system — each level adds perceived height */
--shadow-xs: 0 1px 2px rgba(0,0,0,0.05);

--shadow-sm:
  0 1px 2px rgba(0,0,0,0.06),
  0 1px 3px rgba(0,0,0,0.10);

--shadow-md:
  0 2px 4px rgba(0,0,0,0.04),
  0 4px 6px rgba(0,0,0,0.06),
  0 12px 16px rgba(0,0,0,0.08);

--shadow-lg:
  0 2px 4px rgba(0,0,0,0.02),
  0 4px 8px rgba(0,0,0,0.04),
  0 8px 16px rgba(0,0,0,0.06),
  0 16px 32px rgba(0,0,0,0.08);

--shadow-xl:
  0 4px 8px rgba(0,0,0,0.02),
  0 8px 16px rgba(0,0,0,0.04),
  0 16px 32px rgba(0,0,0,0.06),
  0 32px 64px rgba(0,0,0,0.08),
  0 64px 128px rgba(0,0,0,0.10);

/* Colored shadows for brand elements */
--shadow-brand:
  0 4px 14px rgba(79, 70, 229, 0.25),
  0 8px 32px rgba(79, 70, 229, 0.15);
```

### The "Lift on Hover" Pattern
Cards and interactive elements should visually lift:
```css
.card {
  box-shadow: var(--shadow-sm);
  transform: translateY(0);
  transition:
    box-shadow 0.3s var(--ease-out-expo),
    transform 0.3s var(--ease-out-expo);
}
.card:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-4px);
}
```

---

## 5. Glassmorphism & Frosted Effects

### The Right Way to Do Glass
```css
.glass-surface {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: var(--radius-lg);
}

/* For navigation bars */
.glass-nav {
  background: rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}

/* Apple-style frosted header */
.apple-header {
  background: rgba(251, 251, 253, 0.8);
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
}
```

---

## 6. Dark Mode Architecture

### Principles
- Dark mode is NOT just inverting colors. It requires a separate, intentional palette.
- Dark backgrounds should use warm-tinted near-blacks, not pure #000000.
- Elevation in dark mode is shown with LIGHTER surfaces (not shadows).
- Reduce image brightness and saturation slightly in dark mode.
- Borders become MORE visible in dark mode (use subtle light borders).

### Implementation Pattern

```css
:root {
  /* Light mode tokens */
  --bg-primary: #FFFFFF;
  --bg-secondary: #F8FAFC;
  --bg-tertiary: #F1F5F9;
  --bg-elevated: #FFFFFF;
  --text-primary: #0F172A;
  --text-secondary: #475569;
  --text-tertiary: #94A3B8;
  --border-default: #E2E8F0;
  --border-subtle: #F1F5F9;
}

[data-theme="dark"] {
  /* Dark mode — note: NOT just inverted values */
  --bg-primary: #09090B;
  --bg-secondary: #111113;
  --bg-tertiary: #19191D;
  --bg-elevated: #1C1C21;     /* Lighter = higher elevation */
  --text-primary: #FAFAFA;
  --text-secondary: #A1A1AA;
  --text-tertiary: #52525B;
  --border-default: #27272A;
  --border-subtle: #1C1C21;
}

/* Reduce image intensity in dark mode */
[data-theme="dark"] img:not([data-no-dim]) {
  filter: brightness(0.9) saturate(0.95);
}

/* Note: [data-theme="dark"] overrides should target semantic tokens only.
   Never re-define primitive tokens (--brand-500, --neutral-900) inside
   [data-theme="dark"]. Only semantic tokens (--color-primary, --bg-primary,
   --text-primary, etc.) should change. Primitives stay constant across themes. */
```

---

## 7. CSS Implementation

---

## 8. Tailwind v4 Integration

### Registering Color Tokens via `@theme`

In Tailwind v4 the `@theme` directive replaces the `theme.extend` config object. Register your color primitives and semantic tokens directly in CSS so Tailwind generates utility classes automatically:

```css
/* globals.css (or a dedicated tokens.css imported into globals) */
@import "tailwindcss";

@theme {
  /* Brand primitives — maps to bg-brand-500, text-brand-500, etc. */
  --color-brand-50:  oklch(0.97 0.02 275);
  --color-brand-100: oklch(0.93 0.04 275);
  --color-brand-200: oklch(0.87 0.08 275);
  --color-brand-300: oklch(0.78 0.13 275);
  --color-brand-400: oklch(0.68 0.18 275);
  --color-brand-500: oklch(0.58 0.22 275);
  --color-brand-600: oklch(0.50 0.22 275);
  --color-brand-700: oklch(0.42 0.20 275);
  --color-brand-800: oklch(0.34 0.16 275);
  --color-brand-900: oklch(0.27 0.12 275);

  /* Semantic aliases — maps to bg-primary, text-secondary, etc. */
  --color-primary:        var(--color-brand-500);
  --color-primary-hover:  var(--color-brand-600);
  --color-bg-primary:     #FFFFFF;
  --color-bg-secondary:   #F8FAFC;
  --color-text-primary:   #0F172A;
  --color-text-secondary: #475569;
  --color-border-default: #E2E8F0;
}
```

> Tailwind v4 generates utilities for every `--color-*` variable defined in `@theme`. You can then use `bg-primary`, `text-brand-500`, `border-border-default`, etc. directly in JSX without any additional config.

---

## 7. CSS Implementation

### The Grain Overlay (For Photographic Warmth)
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

### Ambient Glow Effect
```css
.ambient-glow {
  position: relative;
}
.ambient-glow::before {
  content: '';
  position: absolute;
  inset: -50%;
  background: radial-gradient(
    circle at 50% 50%,
    rgba(99, 102, 241, 0.15) 0%,
    transparent 70%
  );
  filter: blur(80px);
  pointer-events: none;
  z-index: -1;
}
```
