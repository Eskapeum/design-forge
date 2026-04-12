# Component Patterns Reference

> Every component is a small product. Design it like someone will screenshot it.

## Table of Contents
1. Navigation
2. Hero Sections
3. Feature Sections
4. Cards
5. Call-to-Action
6. Forms
7. Testimonials & Social Proof
8. Pricing Tables
9. Footers

---

## 1. Navigation

### Design Principles
- Navigation should be INVISIBLE until needed. It supports the content, never competes.
- Maximum 6 items on the main bar. More than that = use dropdowns or mega menu.
- The CTA button in the nav should be the ONLY colored element. Everything else is neutral.
- On scroll: transition to a frosted/blurred compact version. Never just "stick" the same bar.

### The Premium Nav Pattern

```
┌─────────────────────────────────────────────────────────────┐
│  [Logo]    Products ▾    Solutions ▾    Pricing    Blog     │
│                                              [Sign In] [CTA]│
└─────────────────────────────────────────────────────────────┘

On scroll → glass effect, reduced padding, subtle shadow:

┌─────────────────────────────────────────────────────────────┐
│ [Logo]  Products ▾  Solutions ▾  Pricing  Blog  [Sign In][CTA]│
└─────────────────────────────────────────────────────────────┘
```

### Implementation Essentials
```css
.nav {
  position: fixed;
  top: 0;
  inset-inline: 0;
  z-index: var(--z-sticky);
  padding: 20px var(--grid-margin);
  transition:
    padding 0.4s var(--ease-out-expo),
    background 0.4s var(--ease-out-expo),
    backdrop-filter 0.4s var(--ease-out-expo);
}

.nav.scrolled {
  padding: 12px var(--grid-margin);
  background: rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
}
```

### Mobile Navigation
Full-screen overlay. Never a tiny dropdown. Stagger link animations with GSAP:

```tsx
// GSAP stagger for mobile nav links
import { useRef } from 'react';
import { useGSAP } from '@gsap/react';
import gsap from 'gsap';

const MobileNav = ({ isOpen }) => {
  const linksRef = useRef(null);

  useGSAP(() => {
    if (!isOpen) return;
    const mm = gsap.matchMedia();
    mm.add('(prefers-reduced-motion: no-preference)', () => {
      gsap.fromTo(
        linksRef.current.children,
        { opacity: 0, x: -24 },
        {
          opacity: 1,
          x: 0,
          duration: 0.5,
          ease: 'power4.out',
          stagger: 0.075,
        }
      );
    });
    return () => mm.revert();
  }, { scope: linksRef, dependencies: [isOpen] });

  return <nav ref={linksRef}>{/* nav links */}</nav>;
};
```

```
┌─────────────────────────────────┐
│  [Logo]                    [✕]  │
│                                 │
│                                 │
│         Products          →     │  (slides in at 0ms)
│         Solutions         →     │  (slides in at 75ms)
│         Pricing                 │  (slides in at 150ms)
│         Blog                    │  (slides in at 225ms)
│                                 │
│         ┌──────────────────┐    │
│         │    Get Started   │    │  (scales in at 400ms)
│         └──────────────────┘    │
│                                 │
│  ── ── ── ── ── ── ── ── ── ── │
│  Twitter · LinkedIn · GitHub    │  (fades in at 500ms)
└─────────────────────────────────┘
```

---

## 2. Hero Sections

### The Hierarchy of Hero Patterns (Ranked by Impact)

**Tier 1: Cinematic Hero (for brand/marketing sites)**
- Full viewport height
- Video or animated background
- One headline (max 8 words), one subline, one CTA
- Content absolutely centered or bottom-third positioned
- Scroll indicator at bottom

**Tier 2: Split Hero (for product/SaaS sites)**
- Text on left (55%), product screenshot/mockup on right (45%)
- Headline + paragraph + 2 CTAs (primary + ghost)
- Product image slightly overlaps the next section
- Social proof bar below (logos or metrics)

**Tier 3: Statement Hero (for editorial/portfolio)**
- Massive typography (80–150px display size)
- Minimal or no imagery
- Text might be animated (word-by-word reveal, gradient shift)
- Single scroll-down indicator

### Hero Content Formula
```
[Eyebrow]          →  "Introducing / New / Now Available"
[Headline]          →  What you do (benefit-first, max 8 words)
[Subheadline]       →  How you do it (1–2 sentences, max 25 words)
[Primary CTA]       →  Action-oriented verb ("Start Building", "Try Free")
[Secondary CTA]     →  Lower commitment ("See how it works", "View demo")
[Social Proof]      →  Logos, metrics, or testimonial snippet
```

### Hero Image Treatment
- Product screenshots should float with subtle shadow and 2–4° rotation
- Use `perspective` transforms for 3D depth on product images
- Background patterns: dot grids, subtle gradients, animated mesh
- Never use generic stock photography in a hero. Ever.

**GSAP ScrollTrigger Parallax for Hero Images:**
```tsx
import { useRef } from 'react';
import { useGSAP } from '@gsap/react';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

const HeroImage = ({ src, alt }) => {
  const ref = useRef(null);

  useGSAP(() => {
    const mm = gsap.matchMedia();
    mm.add('(prefers-reduced-motion: no-preference)', () => {
      gsap.fromTo(
        ref.current,
        { y: 0 },
        {
          y: -80,
          ease: 'none',
          scrollTrigger: {
            trigger: ref.current,
            start: 'top bottom',
            end: 'bottom top',
            scrub: true,
          },
        }
      );
    });
    return () => mm.revert();
  }, { scope: ref });

  return <img ref={ref} src={src} alt={alt} />;
};
```

---

## 3. Feature Sections

### The Feature Grid (Apple-style Bento)
Best for 4–6 features with visual hierarchy:
```
┌───────────────────┬──────────┐
│                   │          │
│   Feature 1       │ Feature 2│
│   (large card)    │ (small)  │
│                   │          │
├──────────┬────────┴──────────┤
│          │                   │
│ Feature 3│   Feature 4       │
│ (small)  │   (large card)    │
│          │                   │
└──────────┴───────────────────┘
```

### The Sticky Scroll Feature (Linear/Vercel-style)
For 3–5 features that need detailed explanation:
- Left column: Feature titles stacked vertically, each becomes "active" as you scroll
- Right column: Visual/screenshot for the active feature, sticky-positioned
- The active feature highlights while others dim

### The Icon Feature Row
For 3–4 simple features:
```
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│     [icon]   │  │     [icon]   │  │     [icon]   │
│              │  │              │  │              │
│  Feature 1   │  │  Feature 2   │  │  Feature 3   │
│  Description │  │  Description │  │  Description │
│  text here   │  │  text here   │  │  text here   │
└──────────────┘  └──────────────┘  └──────────────┘
```

Rules: Icons must be custom-styled (not generic icon library defaults). Descriptions max 2 lines. Equal height cards.

---

## 4. Cards

### The Card Elevation System
```
Level 0: Flat — border only, no shadow (used in grids)
Level 1: Resting — subtle shadow (default state)
Level 2: Hover — medium shadow + slight Y lift
Level 3: Active — deep shadow + slight Y press
Level 4: Floating — dramatic shadow (modals, popovers)
```

### Card Anatomy
Every card needs:
1. **Visual** — Image, icon, or color block at top
2. **Content** — Title (bold, 1 line) + description (regular, max 3 lines)
3. **Action** — Link, button, or the entire card is clickable
4. **Metadata** — Date, category tag, or author (optional, small text)

### The Click-Target Rule
If a card is clickable, the ENTIRE card surface must be the click target. Don't make only the title or a "Read more" link clickable. Use an `<a>` that wraps everything, or use `::after` pseudo-element stretching technique.

```css
.card {
  position: relative;
}
.card__link::after {
  content: '';
  position: absolute;
  inset: 0;
  z-index: 1;
}
```

---

## 5. Call-to-Action

### Button Hierarchy (Per Page)
- **ONE primary CTA** per viewport. Maximum. No exceptions.
- **Secondary CTAs**: Ghost style (outline) or text-link style.
- **Tertiary CTAs**: Plain text with arrow icon.

### CTA Copywriting Rules
- Start with a verb: "Start", "Try", "Get", "Build", "Create"
- Add specificity: "Start free trial" > "Get started"
- Reduce friction: "No credit card required" under the button
- Create urgency without sleaze: "Join 10,000+ teams" > "LIMITED TIME"

### The CTA Section (Before Footer)
Every marketing page should have a full-width CTA section before the footer:

```
┌─────────────────────────────────────────────┐
│                                             │
│     Ready to build something amazing?       │
│     Start your free trial today.            │
│                                             │
│          ┌──────────────────────┐           │
│          │    Get Started Free  │           │
│          └──────────────────────┘           │
│                                             │
│     No credit card · 14-day free trial      │
│                                             │
└─────────────────────────────────────────────┘
```

This section should have a distinct background (gradient, dark theme, or brand color) to create visual separation from the content above.

---

## 6. Forms

### Input Design Rules
- Label above input (never placeholder-only, never floating label for complex forms)
- 48px minimum input height on desktop, 56px on mobile (touch target)
- Focus state: brand color ring (2px) with subtle glow
- Error state: red border + error message below (not just color — use icon + text)
- Success state: green checkmark icon inside the input

### Form Layout
- Single column for forms with < 6 fields
- Two-column only for closely related fields (first name / last name, city / state)
- Submit button should be full-width on mobile, auto-width on desktop
- Progress indicator for multi-step forms

```css
.input {
  width: 100%;
  padding: 12px 16px;
  border: 1.5px solid var(--color-border-default);
  border-radius: var(--radius-md);
  font-size: 1rem;
  background: var(--bg-primary);
  color: var(--color-text-primary);
  transition:
    border-color 0.2s ease,
    box-shadow 0.2s ease;
}

.input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.15);
}

.input:invalid:not(:placeholder-shown) {
  border-color: var(--color-error);
  box-shadow: 0 0 0 3px rgba(220, 38, 38, 0.1);
}
```

---

## 7. Testimonials & Social Proof

### The Three Formats

**Quote Card** (most common):
```
┌──────────────────────────────────┐
│  ★★★★★                          │
│                                  │
│  "This tool changed how our      │
│   team builds products."         │
│                                  │
│  ┌───┐                          │
│  │ 📷│  Jane Doe                │
│  └───┘  VP Engineering, Acme    │
└──────────────────────────────────┘
```

**Logo Bar** (for B2B trust):
```
Trusted by
[Logo] [Logo] [Logo] [Logo] [Logo] [Logo]
```
- Logos should be grayscale, ~40% opacity, with hover to full color
- Minimum 5 logos, maximum 8 per row
- Auto-scrolling marquee for many logos

**Metrics Bar** (for traction):
```
 10,000+        99.9%         4.8/5
 Active Users   Uptime        Rating
```
- Use tabular/monospace numbers for alignment
- Animate numbers counting up on scroll-in
- Maximum 3–4 metrics

---

## 8. Pricing Tables

### The Three-Tier Rule
- **Starter / Free**: Establish baseline, attract leads
- **Pro / Growth**: The one you WANT them to pick (visually emphasized)
- **Enterprise**: Custom pricing, "Contact us"

### Visual Hierarchy of the Preferred Plan
```
       ┌──────────┐
       │ POPULAR  │ ← badge
 ┌─────┴──────────┴─────┐
 │                       │
 │    Pro Plan           │ ← larger card
 │    $49/mo             │ ← prominent price
 │                       │ ← brand-colored border
 │    [Get Started]      │ ← primary button (filled)
 │                       │
 └───────────────────────┘
```

While the other cards use ghost buttons and no border emphasis.

**Pricing Card Entrance Animation:**
```javascript
// GSAP entrance for pricing cards using IntersectionObserver
import gsap from 'gsap';

const pricingCards = document.querySelectorAll('.pricing-card');

const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (!entry.isIntersecting) return;
      const mm = gsap.matchMedia();
      mm.add('(prefers-reduced-motion: no-preference)', () => {
        gsap.fromTo(
          entry.target,
          { opacity: 0, y: 40, scale: 0.97 },
          {
            opacity: 1,
            y: 0,
            scale: 1,
            duration: 0.6,
            ease: 'power4.out',
          }
        );
      });
      mm.add('(prefers-reduced-motion: reduce)', () => {
        gsap.set(entry.target, { opacity: 1, y: 0, scale: 1 });
      });
      observer.unobserve(entry.target);
    });
  },
  { threshold: 0.15, rootMargin: '0px 0px -40px 0px' }
);

pricingCards.forEach((card, i) => {
  // Stagger start state so cards arrive in sequence
  gsap.set(card, { opacity: 0, y: 40, scale: 0.97 });
  // Offset observer by card index for natural cascade
  setTimeout(() => observer.observe(card), i * 80);
});
```

---

## 9. Footers

### Footer Philosophy
The footer is the LAST impression. Make it count. Types:

**The Mega Footer** (for marketing sites with many pages):
- 4–5 columns of organized links
- Newsletter signup
- Social links
- Legal links in a sub-footer bar

**The Statement Footer** (for brand sites):
- One large CTA headline
- Minimal links
- Brand moment (large logo, animation, or visual)

**The Minimal Footer** (for apps/dashboards):
- Single row: logo, key links, legal
- Unobtrusive

### Footer Must-Haves
1. Logo (always)
2. Copyright with auto-updated year
3. Privacy Policy + Terms links
4. Social media icons (custom-styled, not default)
5. Contact method (email, phone, or form link)

### The Sub-Footer Pattern
```
┌──────────────────────────────────────────────────────┐
│   [Logo]                                             │
│                                                      │
│   Product       Resources      Company     Legal     │
│   Features      Docs           About       Privacy   │
│   Pricing       Blog           Careers     Terms     │
│   Changelog     Templates      Contact     Cookies   │
│   Integrations  Community      Press                 │
│                                                      │
│   ┌──────────────────────────────────────────────┐   │
│   │  Stay updated: [email          ] [Subscribe] │   │
│   └──────────────────────────────────────────────┘   │
│                                                      │
├──────────────────────────────────────────────────────┤
│   © 2026 Company. All rights reserved.    𝕏 in gh   │
└──────────────────────────────────────────────────────┘
```
