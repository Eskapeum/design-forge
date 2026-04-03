# Performance & Craft Reference

> A beautiful site that loads in 8 seconds is an ugly site. Performance IS design.

## Table of Contents
1. Performance Budgets
2. Image Optimization
3. Font Performance
4. Loading Experience Design
5. Accessibility Craft
6. SEO Fundamentals
7. The Polish Checklist
8. Pre-Launch Audit

---

## 1. Performance Budgets

### Hard Limits (Non-Negotiable)

| Metric | Target | Failure Threshold |
|---|---|---|
| Lighthouse Performance | ≥ 90 | < 80 |
| Largest Contentful Paint | < 2.5s | > 4.0s |
| First Input Delay | < 100ms | > 300ms |
| Cumulative Layout Shift | < 0.1 | > 0.25 |
| Time to Interactive | < 3.8s | > 7.3s |
| Total Page Weight | < 1.5MB | > 3MB |
| JavaScript Bundle | < 200KB gzipped | > 400KB |
| Number of Requests | < 50 | > 100 |

### The Performance Mindset
Every kilobyte is a tax on the user's time. Every millisecond of delay reduces conversion. Performance and aesthetics are not in conflict — the best sites in the world (Apple, Stripe, Linear) are fast AND beautiful. If your animations cause jank or your images cause slow loads, the craft is incomplete.

---

## 2. Image Optimization

### Format Decision Tree
```
Is it a photograph or complex image?
├── Yes → Use WebP (quality 80) with AVIF (quality 70) for modern browsers
│         Fallback: JPEG (quality 82)
└── No → Is it an icon or simple graphic?
    ├── Yes, needs to scale → SVG (inline for critical, external for large)
    └── Yes, complex illustration → WebP/AVIF (same as photos)
```

### The `<picture>` Pattern
```html
<picture>
  <!-- Art-directed crops per breakpoint -->
  <source
    media="(min-width: 1024px)"
    srcset="/hero-desktop.avif"
    type="image/avif"
  />
  <source
    media="(min-width: 1024px)"
    srcset="/hero-desktop.webp"
    type="image/webp"
  />
  <source
    media="(max-width: 1023px)"
    srcset="/hero-mobile.avif"
    type="image/avif"
  />
  <source
    media="(max-width: 1023px)"
    srcset="/hero-mobile.webp"
    type="image/webp"
  />
  <img
    src="/hero-desktop.jpg"
    alt="Descriptive alt text"
    width="1440"
    height="810"
    loading="eager"
    fetchpriority="high"
    decoding="async"
  />
</picture>
```

### Next.js Image Pattern
```tsx
import Image from 'next/image';

// Hero image — eager load, high priority
<Image
  src="/hero.jpg"
  alt="Descriptive alt text"
  width={1440}
  height={810}
  priority
  placeholder="blur"
  blurDataURL={shimmerBlurDataURL}
  className="object-cover"
/>

// Below-fold image — lazy load
<Image
  src="/feature.jpg"
  alt="Descriptive alt text"
  width={800}
  height={600}
  loading="lazy"
  placeholder="blur"
  blurDataURL={shimmerBlurDataURL}
/>
```

### Blur Placeholder Generator
```javascript
// Generate a tiny blur placeholder for smooth image loading
const shimmerBase64 = (w = 16, h = 9) =>
  `data:image/svg+xml;base64,${Buffer.from(
    `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ${w} ${h}">
      <filter id="b" color-interpolation-filters="sRGB">
        <feGaussianBlur stdDeviation="1"/>
      </filter>
      <rect preserveAspectRatio="none" filter="url(#b)"
            x="0" y="0" height="100%" width="100%"
            fill="#e2e8f0"/>
    </svg>`
  ).toString('base64')}`;
```

---

## 3. Font Performance

### Loading Strategy Priority
1. **Preload** the primary body font (most text uses this)
2. **Swap** display fonts (acceptable to see a flash)
3. **Optional** for decorative/accent fonts (if they don't load, acceptable)

```html
<head>
  <!-- Preload critical fonts -->
  <link
    rel="preload"
    href="/fonts/body-regular.woff2"
    as="font"
    type="font/woff2"
    crossorigin
  />
  <link
    rel="preload"
    href="/fonts/display-bold.woff2"
    as="font"
    type="font/woff2"
    crossorigin
  />
</head>
```

### Subset Fonts for Performance
If only using Latin characters, subset the font to reduce file size by 50–80%:
```bash
# Using pyftsubset (fonttools)
pyftsubset font.woff2 \
  --output-file=font-subset.woff2 \
  --flavor=woff2 \
  --layout-features='kern,liga,calt' \
  --unicodes='U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD'
```

---

## 4. Loading Experience Design

### Skeleton Screens (Not Spinners)
Replace loading spinners with skeleton screens that match the layout:

```css
.skeleton {
  background: linear-gradient(
    90deg,
    var(--neutral-100) 25%,
    var(--neutral-200) 37%,
    var(--neutral-100) 63%
  );
  background-size: 400% 100%;
  animation: skeleton-shimmer 1.4s ease infinite;
  border-radius: var(--radius-sm);
}

@keyframes skeleton-shimmer {
  0% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Skeleton shapes */
.skeleton-text { height: 16px; margin-bottom: 8px; }
.skeleton-heading { height: 32px; width: 60%; margin-bottom: 16px; }
.skeleton-image { aspect-ratio: 16/9; width: 100%; }
.skeleton-avatar { width: 48px; height: 48px; border-radius: 50%; }
```

### Page Load Choreography
The page load should feel intentional, not random:

```css
/* Phase 1: Structure (0ms) */
.nav { animation: fadeIn 0.4s ease-out 0ms both; }

/* Phase 2: Hero content (200ms offset) */
.hero__headline {
  animation: slideUp 0.7s cubic-bezier(0.16, 1, 0.3, 1) 200ms both;
}
.hero__subtitle {
  animation: fadeIn 0.6s ease-out 500ms both;
}
.hero__cta {
  animation: scaleIn 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) 700ms both;
}

/* Phase 3: Supporting content (800ms+ offset) */
.hero__image {
  animation: fadeIn 0.8s ease-out 400ms both;
}
.social-proof {
  animation: slideUp 0.6s ease-out 900ms both;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(24px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}
```

---

## 5. Accessibility Craft

### Semantic HTML Checklist
- `<header>` wraps the navigation
- `<main>` wraps the primary content (ONE per page)
- `<nav>` wraps navigation links (use `aria-label` if multiple navs)
- `<section>` wraps thematic content sections (must have a heading)
- `<article>` wraps self-contained content (blog posts, cards)
- `<aside>` wraps tangential content (sidebars, related links)
- `<footer>` wraps the page footer

### Focus Management
```css
/* Beautiful, visible focus rings */
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
  border-radius: var(--radius-sm);
}

/* Remove outline for mouse users */
:focus:not(:focus-visible) {
  outline: none;
}

/* Skip link for keyboard navigation */
.skip-link {
  position: absolute;
  top: -100%;
  left: 16px;
  z-index: 10000;
  padding: 8px 16px;
  background: var(--color-primary);
  color: white;
  border-radius: var(--radius-sm);
  transition: top 0.2s;
}

.skip-link:focus {
  top: 16px;
}
```

### Color Contrast Quick Reference
```
Text size          Minimum Ratio    Target
────────────────   ──────────────   ──────
Body (< 18px)      4.5:1 (AA)      7:1 (AAA) ★
Large (≥ 18px)     3:1 (AA)        4.5:1 (AAA)
UI components       3:1             4.5:1
Decorative text     No requirement  —
```

### ARIA Patterns for Common Components
```html
<!-- Dropdown menu -->
<button aria-expanded="false" aria-controls="menu-1">Menu</button>
<ul id="menu-1" role="menu" hidden>
  <li role="menuitem"><a href="/page">Page</a></li>
</ul>

<!-- Modal dialog -->
<div role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">Dialog Title</h2>
  <button aria-label="Close dialog">✕</button>
</div>

<!-- Tabs -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel-1">Tab 1</button>
  <button role="tab" aria-selected="false" aria-controls="panel-2">Tab 2</button>
</div>
<div role="tabpanel" id="panel-1">Content 1</div>
<div role="tabpanel" id="panel-2" hidden>Content 2</div>
```

---

## 6. SEO Fundamentals

### Meta Tags Template
```html
<head>
  <title>{Page Title} — {Brand Name}</title>
  <meta name="description" content="{150-160 char description}" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="canonical" href="https://example.com/page" />

  <!-- Open Graph -->
  <meta property="og:title" content="{Page Title}" />
  <meta property="og:description" content="{Description}" />
  <meta property="og:image" content="https://example.com/og-image.jpg" />
  <meta property="og:url" content="https://example.com/page" />
  <meta property="og:type" content="website" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="{Page Title}" />
  <meta name="twitter:description" content="{Description}" />
  <meta name="twitter:image" content="https://example.com/og-image.jpg" />

  <!-- Favicon suite -->
  <link rel="icon" href="/favicon.ico" sizes="32x32" />
  <link rel="icon" href="/icon.svg" type="image/svg+xml" />
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />
  <link rel="manifest" href="/manifest.webmanifest" />
  <meta name="theme-color" content="#0A0A0A" />
</head>
```

### OG Image Specs
- **Size**: 1200 × 630px (1.91:1 ratio)
- **Safe zone**: Keep text within 1000 × 500px center
- **Format**: JPG or PNG, under 1MB
- **Must include**: Brand logo, page title, visual context

---

## 7. The Polish Checklist

These micro-details separate professional from amateur:

### Visual Polish
- [ ] Favicon appears in all browsers and bookmark bars
- [ ] Selection color (`::selection`) matches brand
- [ ] Scrollbar is custom-styled on WebKit browsers
- [ ] 404 page is custom-designed with navigation back
- [ ] Loading states use skeleton screens, not spinners
- [ ] Empty states have illustrations and helpful CTAs
- [ ] Success states have subtle celebrations (confetti, checkmark animation)
- [ ] Error messages are helpful, specific, and human

### Interaction Polish
- [ ] All buttons have hover, focus, and active states
- [ ] All links have hover underline animations
- [ ] Form inputs have focus, error, and success states
- [ ] Modals trap focus and close on Escape
- [ ] Tooltips have entrance/exit animations
- [ ] Scroll-to-top button appears after scrolling one viewport
- [ ] Anchor links scroll smoothly to target

### Content Polish
- [ ] No lorem ipsum anywhere (including alt text)
- [ ] All images have meaningful alt text
- [ ] Dates are formatted consistently
- [ ] Phone numbers and emails are clickable (`tel:`, `mailto:`)
- [ ] External links open in new tab with `rel="noopener noreferrer"`
- [ ] Copyright year auto-updates

### Cross-Browser Checks
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest + iOS Safari)
- [ ] Edge (latest)
- [ ] Samsung Internet (if targeting mobile users)

### Device Checks
- [ ] iPhone SE (smallest common viewport)
- [ ] iPhone 15 Pro
- [ ] iPad
- [ ] 13" laptop (1280 × 800)
- [ ] 27" desktop (2560 × 1440)
- [ ] Ultra-wide (3440 × 1440)

---

## 8. Pre-Launch Audit

Run this audit before ANY site goes live:

### Technical
```bash
# Run Lighthouse CI
npx lighthouse https://staging.site.com \
  --output=json \
  --chrome-flags="--headless"

# Check HTML validity
npx html-validate "out/**/*.html"

# Check for broken links
npx broken-link-checker https://staging.site.com -ro

# Check bundle size
npx next build && npx @next/bundle-analyzer
```

### Manual Checks
1. Fill out every form. Submit. Check confirmation.
2. Click every link. Check every page loads.
3. Resize the browser from 320px to 2560px. Watch for breaks.
4. Navigate the entire site using only Tab and Enter.
5. Turn off JavaScript. Check content is still visible.
6. Throttle network to 3G. Check load experience.
7. Test with screen reader (VoiceOver on Mac, NVDA on Windows).
8. Print the page. Check it doesn't break.
9. Share a page URL on Twitter/Slack. Check the OG card.
10. Google the site title. Check the meta description reads well.

### Performance Final Gate
If any of these fail, the site does not launch:

| Gate | Requirement |
|---|---|
| LCP | < 2.5s on 4G connection |
| CLS | < 0.1 |
| FID | < 100ms |
| Accessibility | Score ≥ 95 |
| No console errors | Zero errors in production build |
| HTTPS | All resources served over HTTPS |
| Responsive | No horizontal scroll 320px–2560px |

---

*The craft is in the details. The details are in the discipline. The discipline is in the system. This system is your unfair advantage.*
