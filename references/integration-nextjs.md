# Integration Guide — Next.js (Stage 5)

Turning an approved Stitch mockup into production Next.js App Router code.

## Pre-flight (before writing any code)

1. Contract is frozen at `v{N}.md` for this screen
2. Stitch design system tokens are exportable (colors, fonts, radius, spacing)
3. `.design-forge/stitch.json` has the current `designSystemId` and `screenId`
4. shadcn/ui is installed OR you have a component lib decision in contract

## Step 1 — Token export

Pull tokens from contract + Stitch design system. Write to `app/globals.css`:

```css
:root {
  /* Primitives (from contract) */
  --color-primary-raw: #C9A55A;
  --color-neutral-50: #0A0A0A;
  --color-neutral-900: #F5F5F0;

  /* Semantic (design-system mappings) */
  --color-bg: var(--color-neutral-50);
  --color-fg: var(--color-neutral-900);
  --color-accent: var(--color-primary-raw);

  /* Typography */
  --font-display: 'Playfair Display', serif;
  --font-body: 'Inter', sans-serif;

  /* Radius / Spacing */
  --radius: 4px;
  --space-section: clamp(4rem, 8vw, 8rem);
}
```

Tailwind v4 (`@theme` block) is preferred if in use:
```css
@theme {
  --color-accent: #C9A55A;
  --font-display: 'Playfair Display', serif;
  --radius: 4px;
}
```

## Step 2 — Font loading (`app/layout.tsx`)

Prefer `next/font` local files over Google CDN:
```tsx
import { Playfair_Display, Inter } from "next/font/google";

const display = Playfair_Display({
  subsets: ["latin"], variable: "--font-display", display: "swap",
});
const body = Inter({
  subsets: ["latin"], variable: "--font-body", display: "swap",
});

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={`${display.variable} ${body.variable}`}>
      <body className="bg-[--color-bg] text-[--color-fg] font-[family-name:var(--font-body)]">
        {children}
      </body>
    </html>
  );
}
```

## Step 3 — Component extraction from Stitch output

For each section in the Stitch mockup:
1. Identify the semantic role (Hero, FeatureGrid, PricingTable, Footer, etc.)
2. Check shadcn for a primitive (`button`, `card`, `input`, `dialog`)
3. Map Stitch tokens to your CSS vars; never hardcode hex from the mockup
4. Preserve the hierarchy from Stitch exactly — same widths, spacings, orders

Folder layout:
```
app/
├── (marketing)/
│   ├── page.tsx               # home
│   ├── pricing/page.tsx
│   └── layout.tsx             # marketing chrome
├── globals.css
└── layout.tsx
components/
├── ui/                        # shadcn primitives
├── marketing/
│   ├── hero.tsx
│   ├── feature-grid.tsx
│   ├── cta-banner.tsx
│   └── footer.tsx
└── shared/
```

## Step 4 — Animation wiring (GSAP)

- Use `useGSAP` from `@gsap/react` — never raw `useEffect` for GSAP
- Use `gsap.fromTo()` — never `gsap.from()` (Lenis conflict)
- Wrap in `gsap.matchMedia` with `(prefers-reduced-motion: no-preference)` branch
- ScrollTrigger lives in `gsap-scrolltrigger` skill — load it when scroll animations are needed

Baton-pass rule: when writing GSAP, invoke `gsap-react` / `gsap-scrolltrigger` skills for exact current API.

## Step 5 — Images

- `next/image` only; no raw `<img>` in marketing
- Explicit `width` + `height` to prevent CLS
- `priority` on hero image; `loading="lazy"` everywhere else
- AVIF + WebP sources via `next/image` defaults
- Source images: ≤ 200KB each at 1x; use Squoosh/imagemin before commit

## Step 6 — Accessibility pass

Run before Gate 5 sign-off:
- [ ] All interactive elements reachable by keyboard
- [ ] Focus states visible and within brand palette
- [ ] `aria-label` on icon-only buttons
- [ ] Heading order not skipped (h1 → h2 → h3)
- [ ] Color contrast AA for body, AAA for critical actions
- [ ] `prefers-reduced-motion` branch exists for every animation
- [ ] Form fields: labels, error states, live region for validation
- [ ] Page has a unique `<title>` and `<meta name="description">`

## Step 7 — Performance pass

Pre-ship budget:
| Metric | Target |
|---|---|
| LCP   | ≤ 2.0s |
| CLS   | ≤ 0.05 |
| INP   | ≤ 200ms |
| TTFB  | ≤ 800ms |
| JS transferred (marketing) | ≤ 100KB gz |

Quick wins:
- `export const dynamic = 'force-static'` on marketing routes
- Prefer Server Components; only `"use client"` where GSAP / Lenis / state is needed
- Lazy-load heavy sections with `next/dynamic` + `ssr: false` for animation-only pieces

## Step 8 — Token-to-Tailwind mapping

| Stitch token | Tailwind class |
|---|---|
| `color-accent`       | `text-accent` / `bg-accent` (arbitrary: `bg-[--color-accent]`) |
| `font-display`       | `font-display` (configured in `@theme`) |
| `radius`             | `rounded-[--radius]` or `rounded-md` mapped in theme |
| `space-section`      | `py-[--space-section]` |

If using Tailwind v4, all CSS vars become Tailwind classes via `@theme`. If v3, set `theme.extend` in `tailwind.config.ts`.

## Handoff to sibling skills

- **`shadcn`** — for component installation and primitive styling
- **`gsap-react`** / **`gsap-scrolltrigger`** — for animation syntax
- **`react-components`** — for converting Stitch mockups into modular components
- **`design-review`** — for visual QA pass between code-complete and Gate 5
- **`performance-and-craft.md`** (this repo) — pre-launch audit checklist

## Common pitfalls

| Pitfall | Fix |
|---|---|
| Hardcoded hex in component | Always reference CSS var from `globals.css` |
| `gsap.from()` with Lenis | Switch to `gsap.fromTo()` with explicit start + end |
| `<img>` instead of `next/image` | Always `next/image`; sizing props required |
| Font flash | `display: 'swap'`, preload critical glyphs |
| Client bundle bloat | Move static content to RSC; client boundary only where needed |
| shadcn styled inline | Style via `globals.css` variables, not `className` overrides |
