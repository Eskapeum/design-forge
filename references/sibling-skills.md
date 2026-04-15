# Sibling Skills — When to Hand Off

Design Forge is a generalist. These sibling skills are specialists. Use them at the moments where they clearly outperform.

## Discovery & Strategy

| Skill | Use when | Baton pass |
|---|---|---|
| `design-consultation`   | Brand archetype is genuinely undefined, need deeper strategic framing | Before Stage 0 |
| `design-md`             | Need to synthesize a semantic design system from a Stitch project | Before Stage 0.5 or to rebuild contract |
| `brainstorming` (superpowers) | Before any creative step, to widen solution space | Before Stage 1 |

## Generation

| Skill | Use when | Baton pass |
|---|---|---|
| `design-shotgun`        | Want many concurrent concepts before picking a direction | Alternative Stage 2 |
| `stitch-loop`           | Iteratively build pages with Stitch — more granular than Design Forge's stage 2–4 | Inside Stage 3 |
| `enhance-prompt`        | Stitch prompt is vague / hitting validation blocks | Stage 2–4, before every Stitch call |
| `design-forge`          | (self) full awwwards pipeline — default |

## Finalization

| Skill | Use when | Baton pass |
|---|---|---|
| `design-html`           | Take approved AI mockup and produce final HTML | Alternative Stage 5 output format |
| `react-components`      | Convert Stitch design into modular Vite/React components | Inside Stage 5 |
| `shadcn`                | Install/compose shadcn primitives in Stage 5 integration | Inside Stage 5 |
| `integration-nextjs.md` | Built-in guide for Next.js wiring | Stage 5 |

## Animation

| Skill | Use when | Baton pass |
|---|---|---|
| `gsap-core`        | GSAP basics (`gsap.to/from/fromTo`) | Stage 5 when animating |
| `gsap-react`       | `useGSAP` hook + cleanup in React | Stage 5 |
| `gsap-scrolltrigger` | Scroll-driven animations | Stage 5 hero / story sections |
| `gsap-timeline`    | Sequenced multi-step reveals | Stage 5 |
| `gsap-performance` | Pre-launch perf audit on motion | Stage 5 audit |
| `animation-forge`  | Deeper animation craft (25+ years patterns) | Advanced Stage 5 |
| `remotion`         | Video in React, not UI motion | Only if video is part of scope |

## QA & Review

| Skill | Use when | Baton pass |
|---|---|---|
| `design-review`         | Visual QA pass — spacing, typography, hierarchy | Between Stage 4 and Gate 5 |
| `design-audit`          | Audit existing site/page against awwwards standards | Retroactive review |
| `qa` / `qa-only`        | Functional QA of shipped site | After Stage 5 |
| `customer-focus-audit`  | Audit customer-facing copy | Stage 5 or post-ship |
| `plan-design-review`    | Designer-lens review on implementation plan | Before Stage 2 |

## Native / Mobile

| Skill | Use when |
|---|---|
| `native-design`         | Designing iOS/Android native UI — not web |
| `native-ios-app-v1-backup` | iOS-specific builds |

## Pipeline orchestration

| Skill | Use when |
|---|---|
| `gsd:ui-phase`          | Generate UI-SPEC.md for a GSD frontend phase (Design Forge is the implementer) |
| `gsd:ui-review`         | Retroactive 6-pillar UI audit of shipped code |
| `superpowers:dispatching-parallel-agents` | Mechanism for Batch Mode (`batch-mode.md`) |
| `superpowers:executing-plans` | When DF pipeline itself is a plan inside a larger GSD flow |

## Decision tree

```
Start
 ├─ Brand unknown?       → design-consultation, then Design Forge
 ├─ Know the brand?      → Design Forge (default)
 │   ├─ Single screen    → serial pipeline
 │   └─ 5+ screens       → batch-mode.md
 │
 ├─ Stage 2–4
 │   ├─ Want multiple concepts fast  → design-shotgun
 │   ├─ Granular screen edits        → stitch-loop
 │   └─ Prompt keeps failing         → enhance-prompt
 │
 ├─ Stage 5
 │   ├─ Next.js                      → integration-nextjs.md + shadcn + gsap-*
 │   ├─ Vite / React                 → react-components + shadcn + gsap-*
 │   └─ Static HTML                  → design-html
 │
 └─ After Stage 4, before Gate 5     → design-review (always)
```

## GSD integration

Design Forge can be the implementer for a GSD `ui-phase`:

1. GSD orchestrator runs `gsd:ui-phase` → produces `UI-SPEC.md`
2. `UI-SPEC.md` becomes Design Forge's `DESIGN.md` (or appended to contract identity)
3. Design Forge runs its 7-stage pipeline to produce approved screens
4. `gsd:ui-review` audits the shipped code retroactively

Mapping:
- GSD Discovery  ↔ Design Forge Stage 0
- GSD UI-SPEC    ↔ Design Forge Stage 0.5 output + Contract identity section
- GSD Plan       ↔ Design Forge Stages 1–5 per screen
- GSD Verify     ↔ Design Forge Gate 5 + `design-review`

## Never do

- Don't invoke `superdesign` — it has been deprecated in the Design Forge pipeline (v2)
- Don't chain Design Forge → `design-forge` recursively — use batch-mode instead
- Don't run `design-shotgun` AND Design Forge Stage 3 simultaneously — shotgun replaces stage 3
