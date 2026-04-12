# Discovery Framework Reference

> The design brief is a strategic contract — a pact between designer and stakeholder. — FOROALFA

## Table of Contents
1. Discovery Philosophy
2. The Full Question Bank
3. Preset Mapping Matrix
4. Archetype-to-Visual Translation
5. Adaptive Question Selection
6. Design Contract Template

---

## 1. Discovery Philosophy

### Why Discovery Matters
Every design decision downstream is constrained by what you learn here. A vague discovery produces vague designs. A sharp discovery produces designs that feel inevitable.

### The Three Pillars of Discovery

**Pillar 1: Business Understanding**
What does this company do? Who pays them? What's their competitive edge? Without this, you're decorating, not designing.

**Pillar 2: User Empathy**
Who visits this site? What are they feeling when they arrive? What do they need to accomplish? The site exists for them, not for the brand.

**Pillar 3: Visual Intent**
What should the site FEEL like? Not what it should look like — how it should make someone feel. Feelings are more durable design constraints than visual preferences.

### Discovery Is Not a Questionnaire
Do not dump 30 questions on the user. Discovery is a conversation. Read the room:
- If they're excited and verbose → let them talk, extract structure later
- If they're terse and busy → ask the 5 most critical questions only
- If they have existing assets → study the assets first, then ask clarifying questions
- If this is a returning project → skip what you already know, ask about what changed

---

## 2. The Full Question Bank

### A. Business & Brand Identity (establish who they are)

| # | Question | Why It Matters |
|---|----------|---------------|
| A1 | What does the company/product do in one sentence? | Forces clarity. If they can't say it in one sentence, the site can't either. |
| A2 | What problem do you solve for your customers? | The site should lead with the problem, not the product. |
| A3 | Who is your primary customer? Describe them. | Every design choice (color, tone, imagery) flows from this. |
| A4 | What do customers feel before using your product vs. after? | This emotional arc becomes the site's narrative structure. |
| A5 | What 3 adjectives describe your brand personality? | Maps directly to archetype and preset selection. |
| A6 | What is the single most important action a visitor should take? | Determines CTA hierarchy and page flow. |
| A7 | Who are your top 3 competitors? What do they do well/poorly? | Establishes competitive positioning and differentiation opportunities. |
| A8 | What makes you different from those competitors? | The unique value proposition that the design must communicate. |
| A9 | What's your business model? (SaaS, marketplace, agency, etc.) | Affects page types, pricing presentation, conversion funnels. |
| A10 | Is there a specific metric this site should improve? (signups, demos, etc.) | Makes design decisions measurable. |

### B. Visual Direction (establish how it should feel)

| # | Question | Why It Matters |
|---|----------|---------------|
| B1 | Are there existing brand assets? (logo, colors, fonts, guidelines) | Determines whether we're extending a system or building from scratch. |
| B2 | Show 2-3 sites you admire visually. What specifically do you like? | "I like Stripe" is not enough. Need: "I like Stripe's gradient hero and clean type." |
| B3 | Show 1-2 sites that represent what you do NOT want. Why? | Anti-references are as valuable as references. They define the boundary. |
| B4 | If your site were a physical space, what would it be? (gallery, lab, café, etc.) | Physical metaphors translate to spatial design decisions. |
| B5 | What's the emotional temperature? (warm/cool, bold/subtle, dense/spacious) | Three-axis calibration for the entire visual system. |
| B6 | Which of these preset styles feels closest to your vision? (show Stitch presets) | Grounds the conversation in concrete visual examples. |
| B7 | Light mode, dark mode, or both? | Affects the entire color architecture. |
| B8 | How much animation/motion do you want? (minimal / moderate / immersive) | Sets the motion budget for the project. |
| B9 | Are there any colors you love or hate? | Emotional color constraints bypass the rational palette. |
| B10 | Should this feel more like a product (Uber, Linear) or a brand (Apple, Nike)? | Determines information density, visual weight, and interaction style. |

### C. Content & Structure (establish what the site needs)

| # | Question | Why It Matters |
|---|----------|---------------|
| C1 | What pages does the site need? (sitemap) | Defines scope and screen count. |
| C2 | What content exists today? What needs to be written? | Content-first design vs. design-first content are different workflows. |
| C3 | Are there product screenshots, illustrations, or photography available? | Determines whether we design around real assets or placeholders. |
| C4 | Any specific sections that are must-haves? (pricing table, calculator, map, etc.) | Identifies complex components that need special design attention. |
| C5 | What's the content hierarchy? What's most important on each page? | Prevents the "everything is important" trap that kills hierarchy. |
| C6 | Will content be managed by a CMS? Which one? | Affects component flexibility and content modeling. |

### D. Technical Constraints (establish what's possible)

| # | Question | Why It Matters |
|---|----------|---------------|
| D1 | Is there an existing codebase or framework? | Determines whether we design for a specific tech stack. |
| D2 | Any CMS or third-party integration requirements? | Affects component architecture and data flow. |
| D3 | Who is the target audience in terms of devices/connectivity? | Mobile-first vs desktop-first, performance budgets. |
| D4 | Accessibility requirements beyond WCAG AA? | Some industries (healthcare, government) require AAA. |
| D5 | Any specific browser/device support requirements? | IE11 is dead, but some enterprises still have constraints. |
| D6 | Deployment platform? (Vercel, Netlify, self-hosted) | Affects build pipeline and optimization strategies. |

### E. Deal-Breakers & Non-Negotiables (establish boundaries)

| # | Question | Why It Matters |
|---|----------|---------------|
| E1 | What must absolutely NOT appear on this site? | Prevents wasted iterations on forbidden patterns. |
| E2 | Any brand guidelines that cannot be bent? | Identifies immovable constraints upfront. |
| E3 | Are there legal/compliance requirements for the content? | Healthcare, finance, etc. have specific requirements. |
| E4 | Timeline or budget constraints that affect design scope? | Better to know now than discover mid-project. |
| E5 | Who are the stakeholders who need to approve the design? | Affects the number of revision cycles to plan for. |

---

## 3. Preset Mapping Matrix

Map discovery answers to the optimal Stitch preset:

| Brand Adjectives | Emotional Target | Physical Metaphor | Recommended Preset | Alternative |
|---|---|---|---|---|
| Premium, precise, modern | Impressed, confident | Precision instrument | **Beam** | Uber Design System |
| Warm, editorial, trustworthy | Safe, understood | Library reading room | **Newsprint** | Luxury |
| Bold, rebellious, energetic | Excited, inspired | Concert main stage | **Kinetic** | Motion |
| Elegant, luxurious, refined | Impressed, confident | Gallery opening | **Luxury** | Newsprint |
| Technical, clean, systematic | Confident, capable | Research laboratory | **Uber Design System** | Beam |
| Playful, friendly, approachable | Curious, excited | Toy store | **Playful** | Hand-draw |
| Creative, organic, human | Curious, understood | Artist's studio | **Hand-draw** | Playful |
| Dynamic, fluid, immersive | Excited, inspired | Amusement park ride | **Motion** | Kinetic |
| Soft, modern, dimensional | Impressed, curious | Sculpted product | **Neumorphism** | Beam |
| Geometric, structured, bold | Impressed, inspired | Bauhaus gallery | **Bauhaus** | Uber Design System |
| Retro, nostalgic, ironic | Curious, delighted | Time machine | **Win98** | Hand-draw |

### Preset + Font Pairing Recommendations

| Preset | Display Font | Body Font | Pairing Name |
|---|---|---|---|
| Beam | Clash Display (700, 600) | General Sans (400, 500) | "The Stripe" |
| Luxury | Cormorant Garamond (600, 700) | Tenor Sans (400) | "The Luxury" |
| Newsprint | Playfair Display (700, 800) | Source Sans 3 (400, 500) | "The Editorial" |
| Kinetic | Cabinet Grotesk (800, 900) | Satoshi (400, 500) | "The Startup" |
| Motion | Space Grotesk (700) | Inter (400, 500) | "The Builder" |
| Playful | Fraunces (700, 900) | Outfit (300, 400) | "The Storyteller" |
| Uber Design System | Space Grotesk (700) | Inter (400, 500) | "The Builder" |
| Neumorphism | General Sans (500, 600) | General Sans (400) | "The Soft" |
| Bauhaus | Cabinet Grotesk (800, 900) | Satoshi (400, 500) | "The Startup" |
| Hand-draw | Fraunces (700, 900) | Outfit (300, 400) | "The Storyteller" |
| Win98 | Space Grotesk (700) | JetBrains Mono (400) | "The Terminal" |

---

## 4. Archetype-to-Visual Translation

Translate the 3 brand adjectives into concrete design parameters:

| Parameter | Warm | Cool | Bold | Subtle | Dense | Spacious |
|-----------|------|------|------|--------|-------|----------|
| Neutral base | Warm (#FAFAF9) | Cool (#F8FAFC) | Dark (#09090B) | Light (#FAFAFA) | Tight spacing | Generous spacing |
| Border radius | 12-24px | 4-8px | 0-4px | 8-16px | 4-8px | 12-24px |
| Shadow style | Colored, soft | Neutral, sharp | Hard, dramatic | Subtle, layered | Minimal | Prominent |
| Type contrast | Medium (1.250) | High (1.333) | Maximum (1.500) | Subtle (1.200) | Tight (1.200) | Dramatic (1.500) |
| Motion level | Gentle springs | Precise expo | Kinetic, fast | Barely there | Functional only | Cinematic |
| Color saturation | High warmth | Low, muted | Vivid accent | Pastel, muted | Functional only | One champion |

---

## 5. Adaptive Question Selection

### Decision Tree: How Many Questions to Ask

```
Is this the first screen for a new project?
├── YES → Has DESIGN.md or brand assets?
│   ├── YES → Ask 5-8 questions (B2, B3, B5, B6, C4, C5, E1, E4)
│   └── NO  → Ask 10-15 questions (full A + B + C1-C3 + E1-E3)
│
└── NO → Is the design system already established?
    ├── YES → Ask 2-3 questions about THIS screen only
    │         (C4: must-have sections, C5: hierarchy, B8: motion level)
    └── NO  → Ask 5-8 questions to establish the system
```

### Signals That Discovery Is Complete
- You can fill the Design Contract template with confidence
- You know the archetype, emotional target, and visual metaphor
- You can recommend a specific preset with a rationale
- You know at least 2 deal-breakers
- You understand the conversion goal for the first screen

---

## 6. Design Contract Template

Use this template to generate `.design-forge/contract.md` after Gate 0:

```markdown
# Design Contract: {Project Name}
## Created: {date} | Last Updated: {date}

## Identity
- **Brand Name:** {name}
- **One-Sentence Description:** {what the product does}
- **Archetype:** {from discovery — e.g., "Bold Innovator"}
- **Brand Adjectives:** {3 adjectives}
- **Emotional Target:** {2-3 feelings users should have}
- **Visual Metaphor:** {physical space it should feel like}
- **One Word:** {brand personality distilled}

## Audience
- **Primary User:** {who — role, mindset, needs}
- **User Mindset on Arrival:** {what they feel/want when they land}
- **Conversion Goal:** {single most important action per page}
- **User Journey:** {problem → discovery → action → outcome}

## Competitive Position
- **Competitor 1:** {name} — strength: {X}, weakness: {Y}
- **Competitor 2:** {name} — strength: {X}, weakness: {Y}
- **Competitor 3:** {name} — strength: {X}, weakness: {Y}
- **Differentiation:** {what makes this product unique}

## Design System (populated at Stage 0.5)
- **Stitch Preset:** {preset name}
- **Customizations:** {list of overrides}
- **Primary Color:** {hex} — rationale: {why this color}
- **Neutral Base:** {warm/cool} — range: {lightest to darkest}
- **Display Font:** {name} ({weights})
- **Body Font:** {name} ({weights})
- **Border Radius:** {system} — feel: {what it communicates}
- **Spacing Base:** {value}
- **Color Mode:** {light/dark/both}
- **Motion Level:** {minimal/moderate/immersive}

## Research Directives (populated at Stage 1)
- **From {Ref 1}:** {specific enforceable pattern}
- **From {Ref 2}:** {specific enforceable pattern}
- **From {Ref 3}:** {specific enforceable pattern}
- **From {Ref 4}:** {specific enforceable pattern}
- **Synthesis:** {combined approach as a directive}

## Accumulated Feedback (grows at every gate)
### Gate 0: Discovery
- {refinements from discovery review}

### Gate 0.5: Design System
- {adjustments from design system review}

### Gate 1: Research
- {direction notes from research review}

### Gate 2: First Impression
- {adjustments from first design review}

### Gate 3: Winner Selection
- {winner choice, hybrid instructions, elements to keep/discard}

### Gate 4: Polish
- {refinement notes}

## Hard Constraints (never violate without explicit permission)
- {deal-breaker 1}
- {deal-breaker 2}
- {exclusion 1 — e.g., "no stock photography in heroes"}
- {exclusion 2 — e.g., "no sidebar navigation"}
- {brand guideline constraints}

## Soft Preferences (follow unless user overrides)
- {preference 1 — detected from feedback patterns}
- {preference 2}
```
