# Quickstart — Your First Screen in 5 Minutes

A worked example: **luxury-fintech dashboard hero** for an imaginary product "Ledger".

## 0. State bootstrap

```
mkdir -p .design-forge/{research,feedback,contract}
touch SITE.md DESIGN.md
```

`SITE.md` (minimal):
```yaml
---
project: ledger
version: 0.1
---

# Pages
- [ ] home :: landing :: convert-trial :: P0
- [ ] pricing :: marketing :: convert-paid :: P1
- [ ] dashboard :: product :: retain :: P2
```

## 1. Stage 0 — Discovery (3 questions, not 15)

DESIGN.md is empty → ask the minimum to produce a contract:

- Brand: *"Ledger is a private-banking-grade P&L tool for indie fund managers."*
- Three adjectives: *"sovereign, precise, quiet."*
- Anti-preferences: *"No neon. No '3D glass'. No stock photography."*

Map to preset: **Luxury** (dark + serif + high contrast + editorial whitespace).

Write `.design-forge/contract/v1.md` using the template in `SKILL.md`.

## 2. Stage 0.5 — Design System (one Stitch call)

```
create_design_system({
  preset: "LUXURY",
  colorMode: "DARK",
  customColor: "#C9A55A",      // aged-gold primary
  headlineFont: "PLAYFAIR_DISPLAY",
  bodyFont: "INTER",
  roundness: "ROUND_FOUR",
  colorVariant: "TONAL_SPOT",
  designMd: "<paste contract identity + hard constraints>"
})
```

Save the returned IDs to `.design-forge/stitch.json`.

## 3. Stage 1 — Research (4 refs, 1 paragraph each)

Save to `.design-forge/research/home.md`:
```markdown
# Research: home
1. linear.app — green: restrained gradient stage, editorial spacing
2. mercury.com — green: serif display + mono numerical data pairing
3. arc.net — green: cinematic scroll reveal, yellow: too playful for us
4. studio.design (aspirational) — green: micro-type pairings, density

Synthesis: editorial dark stage, aged-gold accent only on numbers,
serif display + mono numerals, one cinematic hero scroll reveal.
```

## 4. Stage 2 — Explore (one Stitch call with full contract)

Use the **Contract Injection Template** in `SKILL.md`. Output must match:
- primary `#C9A55A` (exact)
- fonts: Playfair Display + Inter
- zero neon, zero 3D glass, zero stock photos

Run the validator (see `contract-validator.md`). If any BLOCK-level mismatch → regenerate.

## 5. Stage 3 → 5 — Iterate / Refine / Integrate

Each gate produces an append to `.design-forge/contract/current.md` changelog.

When the user says `SHIP IT` at Gate 5:
1. Mark `home` complete in `SITE.md`
2. Append metrics row to `.design-forge/metrics.json`
3. Announce next screen (`pricing`)

---

## Copy-paste skeleton

```
.design-forge/
├── contract/
│   ├── v1.md
│   ├── v2.md
│   └── current.md            -> v2.md  (symlink)
├── research/
│   └── home.md
├── feedback/
│   └── home.md
├── stitch.json
├── metrics.json
└── init/
    └── brand-assets/         (optional user-supplied)
```
