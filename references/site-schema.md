# SITE.md Schema

Canonical format the skill keys on. Enables "unchecked pages" triggering, batch mode, and ship tracking.

## Format

```yaml
---
project: {slug}
version: 0.1                      # bump when adding phases
framework: nextjs                 # nextjs | astro | sveltekit | vite | other
deployment: vercel                # optional
updated: 2026-04-15
---

# Pages

## Marketing
- [ ] home       :: landing    :: convert-trial   :: P0 :: hero+features+social-proof+cta
- [ ] pricing    :: marketing  :: convert-paid    :: P1 :: tiers+faq+cta
- [ ] about      :: marketing  :: trust           :: P2 :: story+team

## Product
- [ ] dashboard  :: product    :: retain          :: P0 :: overview+actions
- [ ] settings   :: product    :: retain          :: P3 :: tabs+forms

## Auth
- [ ] signin     :: auth       :: enter           :: P0 :: form+social
- [ ] signup     :: auth       :: enter           :: P0 :: form+social
```

## Row grammar

```
- [ ] {slug} :: {type} :: {goal} :: {priority} :: {sections}
```

| Field | Values | Required |
|---|---|---|
| `[ ]` / `[x]` | checkbox — unchecked = not yet designed | yes |
| `slug` | URL-safe, one word | yes |
| `type` | `landing` \| `marketing` \| `product` \| `auth` \| `docs` \| `legal` \| `dashboard` \| `detail` \| `form` | yes |
| `goal` | one of: `convert-trial`, `convert-paid`, `retain`, `educate`, `trust`, `enter`, `support`, `legal`, `custom:{word}` | yes |
| `priority` | `P0` (ship first) \| `P1` \| `P2` \| `P3` | yes |
| `sections` | `+`-delimited list of modules this page needs | optional |

Group rows under `## Section` headings (Marketing / Product / Auth / …). Order within groups is the suggested build order.

## States

- `- [ ]` — unchecked, not started
- `- [~]` — in progress (pipeline running)
- `- [x]` — shipped (Gate 5 SHIP IT)
- `- [!]` — blocked (has `blocked.md`)

## Skill behavior

- **Trigger:** any `[ ]` row → skill offers to start that page
- **Priority-first:** P0 pages run before P1, P1 before P2
- **Batch-mode eligible:** pages at the same priority level can run Stage 1 research in parallel
- **Auto-bump:** when a P0 ships, reprioritize P1 pages ("next up: pricing")

## Optional frontmatter fields

```yaml
design_system_source: .design-forge/contract/current.md   # enforce single source
batch_mode: true                                          # allow parallel research
contract_drift_guard: strict                              # block contract changes mid-site
```

## Minimal example

```yaml
---
project: syntheka
framework: nextjs
---

# Pages
- [ ] home :: landing :: convert-trial :: P0
- [ ] about :: marketing :: trust :: P2
```

That's enough to run. Sections and detailed fields are optional enhancements.

## Validation

Skill rejects a `SITE.md` that:
- has duplicate slugs
- has unknown `type` or `goal` values
- has `[x]` on a page with no `feedback/{slug}.md`
- lists P0 pages after P1 within the same group
