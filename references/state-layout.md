# State Layout — `.design-forge/` Directory Schema

Canonical directory + file contract for every project using Design Forge.

## Tree

```
.design-forge/
├── contract/
│   ├── v1.md                     # frozen at Gate 0
│   ├── v2.md                     # frozen at Gate 0.5
│   ├── v3.md                     # frozen at Gate 1
│   ├── v{N}.md                   # one per gate advancement
│   └── current.md                # symlink to latest v{N}.md
│
├── research/
│   └── {screen}.md               # one per screen, format from research-playbook.md
│
├── feedback/
│   └── {screen}.md               # final feedback log after Gate 5 SHIP IT
│
├── validator-log.md              # append-only, one entry per Stitch output
├── metrics.json                  # append-only JSONL, one row per gate decision
├── stitch.json                   # project + design-system IDs
├── blocked.md                    # only exists if pipeline is paused
│
└── init/
    ├── brand-assets/             # user-supplied logos, fonts, photography
    ├── competitors.md            # optional pre-populated competitor notes
    └── voice.md                  # optional brand voice / copy guidelines
```

## File schemas

### `contract/v{N}.md`
Full Markdown document per the template in `SKILL.md` + `## Changelog` section.

```markdown
---
version: {N}
frozen_at_gate: {gate_id}
frozen_on: {ISO-8601}
prev_version: v{N-1}
---

# Design Contract: {project}

{body per template}

## Changelog
- **Gate 0 (v1)**: initial capture from discovery
- **Gate 0.5 (v2)**: design system locked
- **Gate 1 (v3)**: research directives added
- **Gate N (vN+1)**: {summary of what changed}
```

Immutable once written. Edits create a new `v{N+1}.md` and repoint `current.md`.

### `stitch.json`
```json
{
  "projectId": "...",
  "designSystemId": "...",
  "preset": "LUXURY",
  "colorMode": "DARK",
  "customColor": "#C9A55A",
  "headlineFont": "PLAYFAIR_DISPLAY",
  "bodyFont": "INTER",
  "roundness": "ROUND_FOUR",
  "colorVariant": "TONAL_SPOT",
  "createdAt": "2026-04-15T12:00:00Z",
  "screens": {
    "home":      { "screenId": "...", "lastUpdated": "..." },
    "pricing":   { "screenId": "...", "lastUpdated": "..." }
  }
}
```

### `metrics.json`
JSONL, one row per gate decision:
```json
{"ts":"2026-04-15T12:00:00Z","screen":"home","stage":0,"gate":"GATE_0","verdict":"APPROVE","duration_sec":420,"stitch_calls":0,"regenerations":0}
{"ts":"2026-04-15T12:15:00Z","screen":"home","stage":2,"gate":"GATE_2","verdict":"GOOD_DIRECTION","duration_sec":180,"stitch_calls":1,"regenerations":0,"awwwards_score":6.8}
```

### `validator-log.md`
Append-only markdown, format per `contract-validator.md`.

### `blocked.md`
Only present when pipeline paused:
```markdown
# BLOCKED — {ISO-8601}
Screen: {screen}
Stage: {N}
Symptom: {...}
Attempted: {...}
Next human step: {...}
Last-good contract: contract/v{N}.md
```

### `feedback/{screen}.md`
```markdown
# Feedback Log — {screen}
Shipped: {ISO-8601}

## Gate 0  — {verdict}
- {bullets}

## Gate 0.5 — {verdict}
- {bullets}

## Gate 1–5 — {verdicts}

## Post-ship notes
- {what worked, what we'd change}
```

## Lifecycle

| Event | Files touched |
|---|---|
| Project init  | create `.design-forge/`, `init/` (optional), empty `stitch.json` |
| Gate 0 APPROVE | write `contract/v1.md`, repoint `current.md`, append metrics |
| Gate 0.5 APPROVE | update `stitch.json`, write `contract/v2.md`, repoint `current.md` |
| Stitch call (any) | append to `validator-log.md` |
| Gate N advance | write `contract/v{N+1}.md`, repoint `current.md`, append metrics |
| Gate 5 SHIP IT | write `feedback/{screen}.md`, mark `SITE.md` complete |
| Block | write `blocked.md`, pause all file writes until resolved |

## Init command

```bash
# bootstrap:
mkdir -p .design-forge/{contract,research,feedback,init/brand-assets}
: > .design-forge/stitch.json
: > .design-forge/metrics.json
: > .design-forge/validator-log.md
```

## `.gitignore` recommendation

Tracking everything in `.design-forge/` gives you full reproducibility, but secrets-free.
- **Track:** everything except `stitch.json` API IDs if you consider them sensitive
- **Ignore:** `init/brand-assets/*.psd`, large binaries, if they don't belong in git

Default `.gitignore` snippet:
```
# design-forge
.design-forge/init/brand-assets/*.psd
.design-forge/init/brand-assets/*.sketch
.design-forge/init/brand-assets/*.fig
```

## Safety rails

- Never overwrite a frozen `v{N}.md`. Always bump version.
- Never delete `validator-log.md` entries. Append-only.
- `current.md` is a symlink. If filesystem doesn't support symlinks, use a file with content `v{N}.md` as pointer; skill reads the pointer then the target.
