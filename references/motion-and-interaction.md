# Motion & Interaction Reference

> Motion is the difference between a website and an experience.

## Table of Contents
1. Motion Philosophy
2. Easing Functions Bible
3. Scroll Animation System
4. Micro-Interactions Library
5. Page Transition Patterns
6. Advanced Effects
7. Performance & Accessibility

---

## 1. Motion Philosophy

### The Four Purposes of Motion
Every animation must serve one of these purposes. If it doesn't, remove it.

1. **Orientation**: Help the user understand where they are (page transitions, scroll progress)
2. **Focus**: Direct attention to what matters (entrance animations, pulsing CTAs)
3. **Feedback**: Confirm that an action was registered (button press, form submit)
4. **Delight**: Create an emotional response (Easter eggs, playful hovers, loading art)

### The Duration Hierarchy
Motion duration must match the scope of the change:

| Scope | Duration | Easing | Example |
|---|---|---|---|
| Micro | 100–200ms | ease-out | Button color change, icon swap |
| Component | 200–400ms | ease-out-expo | Card expansion, dropdown open |
| Section | 400–700ms | ease-out-quart | Section reveal, image transition |
| Page | 600–1000ms | ease-in-out-quint | Route change, hero entrance |
| Cinematic | 1000–2000ms | custom | Full-page intro, brand moment |

### The Stagger Principle
When multiple elements enter, stagger them. Never bring everything in simultaneously. The delay between siblings should be 50–100ms. This creates a "cascade" effect that feels organic.

```css
.stagger-enter > * {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.6s var(--ease-out-expo) forwards;
}

.stagger-enter > *:nth-child(1) { animation-delay: 0ms; }
.stagger-enter > *:nth-child(2) { animation-delay: 75ms; }
.stagger-enter > *:nth-child(3) { animation-delay: 150ms; }
.stagger-enter > *:nth-child(4) { animation-delay: 225ms; }
.stagger-enter > *:nth-child(5) { animation-delay: 300ms; }

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

---

## 2. Easing Functions Bible

### Named Curves

```css
/* Entrances — elements arriving on screen */
--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);       /* ★ Primary entrance */
--ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);      /* Gentler entrance */
--ease-out-back: cubic-bezier(0.34, 1.56, 0.64, 1);   /* Bouncy entrance */

/* Exits — elements leaving the screen */
--ease-in-expo: cubic-bezier(0.7, 0, 0.84, 0);        /* Quick exit */
--ease-in-quart: cubic-bezier(0.5, 0, 0.75, 0);       /* Gentle exit */

/* Morphs — elements changing in place */
--ease-in-out-quint: cubic-bezier(0.83, 0, 0.17, 1);  /* ★ Primary morph */
--ease-in-out-expo: cubic-bezier(0.87, 0, 0.13, 1);   /* Dramatic morph */

/* Physics-based */
--spring-bounce: cubic-bezier(0.34, 1.56, 0.64, 1);   /* Playful spring */
--spring-gentle: cubic-bezier(0.22, 1.0, 0.36, 1.0);  /* Subtle spring */
```

### When to Use What
- **ease-out-expo**: Default for EVERYTHING entering the viewport
- **ease-in-out-quint**: Anything that changes size, color, or position in-place
- **ease-out-back**: Popups, modals, toast notifications (adds playful overshoot)
- **spring curves**: Buttons, toggles, anything that should feel "springy"
- **NEVER use `linear`** for UI. Linear motion looks robotic.
- **NEVER use `ease`** (the CSS default). It's too generic and lacks character.

---

## 3. Scroll Animation System

### IntersectionObserver Pattern (CSS-only first)

```css
/* Base state — element starts invisible and shifted */
[data-animate] {
  opacity: 0;
  transform: translateY(32px);
  transition:
    opacity 0.7s var(--ease-out-expo),
    transform 0.7s var(--ease-out-expo);
}

/* Revealed state */
[data-animate].is-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Variant: slide from left */
[data-animate="slide-left"] {
  transform: translateX(-48px);
}
[data-animate="slide-left"].is-visible {
  transform: translateX(0);
}

/* Variant: scale up */
[data-animate="scale"] {
  transform: scale(0.9);
}
[data-animate="scale"].is-visible {
  transform: scale(1);
}

/* Variant: blur in */
[data-animate="blur"] {
  filter: blur(10px);
  transform: translateY(16px);
}
[data-animate="blur"].is-visible {
  filter: blur(0);
  transform: translateY(0);
}
```

### JavaScript Observer

```javascript
// Minimal, performant scroll reveal
const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        observer.unobserve(entry.target); // Animate once only
      }
    });
  },
  {
    threshold: 0.15,    // Trigger when 15% visible
    rootMargin: '0px 0px -50px 0px'  // Slightly before fully in view
  }
);

document.querySelectorAll('[data-animate]').forEach((el) => {
  observer.observe(el);
});
```

### Framer Motion (React/Next.js)

```tsx
import { motion } from 'framer-motion';

// Reusable fade-up component
const FadeUp = ({ children, delay = 0 }) => (
  <motion.div
    initial={{ opacity: 0, y: 32 }}
    whileInView={{ opacity: 1, y: 0 }}
    viewport={{ once: true, margin: '-50px' }}
    transition={{
      duration: 0.7,
      delay,
      ease: [0.16, 1, 0.3, 1], // ease-out-expo
    }}
  >
    {children}
  </motion.div>
);

// Staggered container
const StaggerContainer = ({ children }) => (
  <motion.div
    initial="hidden"
    whileInView="visible"
    viewport={{ once: true }}
    variants={{
      hidden: {},
      visible: {
        transition: { staggerChildren: 0.08 },
      },
    }}
  >
    {children}
  </motion.div>
);

const StaggerItem = ({ children }) => (
  <motion.div
    variants={{
      hidden: { opacity: 0, y: 24 },
      visible: {
        opacity: 1, y: 0,
        transition: { duration: 0.6, ease: [0.16, 1, 0.3, 1] }
      },
    }}
  >
    {children}
  </motion.div>
);
```

---

## 4. Micro-Interactions Library

### Button Hover (Premium Feel)

```css
.btn-primary {
  position: relative;
  padding: 14px 28px;
  background: var(--color-primary);
  color: white;
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  overflow: hidden;
  transition:
    transform 0.3s var(--ease-out-expo),
    box-shadow 0.3s var(--ease-out-expo);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-brand);
}

.btn-primary:active {
  transform: translateY(0);
  box-shadow: var(--shadow-sm);
}

/* Shine sweep on hover */
.btn-primary::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    105deg,
    transparent 40%,
    rgba(255,255,255,0.2) 45%,
    rgba(255,255,255,0.2) 50%,
    transparent 54%
  );
  transform: translateX(-100%);
  transition: transform 0.6s var(--ease-out-expo);
}

.btn-primary:hover::after {
  transform: translateX(100%);
}
```

### Magnetic Button (Awwwards Signature)

```javascript
// Magnetic button — follows cursor within proximity
const magneticButtons = document.querySelectorAll('[data-magnetic]');

magneticButtons.forEach((btn) => {
  btn.addEventListener('mousemove', (e) => {
    const rect = btn.getBoundingClientRect();
    const x = e.clientX - rect.left - rect.width / 2;
    const y = e.clientY - rect.top - rect.height / 2;

    btn.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px)`;
  });

  btn.addEventListener('mouseleave', () => {
    btn.style.transform = 'translate(0, 0)';
    btn.style.transition = 'transform 0.5s cubic-bezier(0.16, 1, 0.3, 1)';
  });

  btn.addEventListener('mouseenter', () => {
    btn.style.transition = 'none';
  });
});
```

### Link Underline Animation

```css
.link-animated {
  position: relative;
  text-decoration: none;
  color: var(--color-text-primary);
}

.link-animated::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 100%;
  height: 1.5px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.4s var(--ease-out-expo);
}

.link-animated:hover::after {
  transform: scaleX(1);
  transform-origin: left;
}
```

### Text Reveal (Character by Character)

```tsx
// React component for character-split text reveal
const TextReveal = ({ text, delay = 0 }) => {
  return (
    <span style={{ display: 'inline-flex', overflow: 'hidden' }}>
      {text.split('').map((char, i) => (
        <motion.span
          key={i}
          initial={{ y: '100%' }}
          whileInView={{ y: 0 }}
          viewport={{ once: true }}
          transition={{
            duration: 0.5,
            delay: delay + i * 0.03,
            ease: [0.16, 1, 0.3, 1],
          }}
          style={{ display: 'inline-block' }}
        >
          {char === ' ' ? '\u00A0' : char}
        </motion.span>
      ))}
    </span>
  );
};
```

---

## 5. Page Transition Patterns

### Crossfade (Universal Default)

```tsx
// app/template.tsx (Next.js App Router)
'use client';
import { motion, AnimatePresence } from 'framer-motion';

export default function Template({ children }) {
  return (
    <motion.div
      initial={{ opacity: 0, y: 12 }}
      animate={{ opacity: 1, y: 0 }}
      exit={{ opacity: 0, y: -12 }}
      transition={{ duration: 0.4, ease: [0.16, 1, 0.3, 1] }}
    >
      {children}
    </motion.div>
  );
}
```

---

## 6. Advanced Effects

### Parallax Scroll (CSS Only)

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

.parallax-content {
  transform: translateZ(0);
  position: relative;
}
```

### Cursor Trail Effect

```javascript
const trail = [];
const trailLength = 12;

for (let i = 0; i < trailLength; i++) {
  const dot = document.createElement('div');
  dot.className = 'cursor-trail-dot';
  dot.style.cssText = `
    position: fixed;
    width: ${8 - i * 0.5}px;
    height: ${8 - i * 0.5}px;
    background: var(--color-primary);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    opacity: ${1 - i / trailLength};
    transition: transform ${0.1 + i * 0.02}s ease-out;
  `;
  document.body.appendChild(dot);
  trail.push(dot);
}

document.addEventListener('mousemove', (e) => {
  trail.forEach((dot) => {
    dot.style.transform = `translate(${e.clientX - 4}px, ${e.clientY - 4}px)`;
  });
});
```

### Smooth Scroll (Lenis Setup)

```javascript
import Lenis from '@studio-freight/lenis';

const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  smoothWheel: true,
  touchMultiplier: 2,
});

function raf(time) {
  lenis.raf(time);
  requestAnimationFrame(raf);
}

requestAnimationFrame(raf);
```

---

## 7. Performance & Accessibility

### Respect Reduced Motion — Always

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### GPU-Accelerated Properties Only
Only animate these properties for smooth 60fps:
- `transform` (translate, scale, rotate)
- `opacity`
- `filter` (blur, brightness)
- `clip-path`

NEVER animate: `width`, `height`, `top`, `left`, `margin`, `padding`, `border`, `font-size`. These trigger layout recalculations and cause jank.

### Will-Change (Use Sparingly)
```css
/* Only add to elements that WILL animate soon */
.about-to-animate {
  will-change: transform, opacity;
}

/* Remove after animation completes */
.done-animating {
  will-change: auto;
}
```
