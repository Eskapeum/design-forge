# Metrics & Retro

What Design Forge measures, where it writes it, and how to review it.

## Metrics file

Path: `.design-forge/metrics.json` (JSONL, append-only).

### Row schema

```json
{
  "ts": "ISO-8601",
  "screen": "home",
  "stage": 2,
  "gate": "GATE_2",
  "verdict": "GOOD_DIRECTION|ADJUST|WRONG_DIRECTION|APPROVE|...",
  "duration_sec": 180,
  "stitch_calls": 1,
  "regenerations": 0,
  "awwwards_score": 6.8,
  "validator_blocks": 0,
  "validator_flags": 1,
  "reject_reason": null
}
```

Stage 5 SHIP IT row also includes:
```json
{ "shipped": true, "contract_version": 7, "feedback_rounds_total": 4 }
```

## What to track per gate

| Field | Required at | Purpose |
|---|---|---|
| `duration_sec` | every gate | Identify slow stages |
| `stitch_calls` | every Stitch-invoking stage | Cost tracking |
| `regenerations` | Stages 2, 3, 4 | Contract / prompt quality |
| `validator_blocks` / `validator_flags` | every Stitch output | Contract strictness tuning |
| `awwwards_score` | Gate 2, Gate 4, Gate 5 | Quality trajectory |
| `reject_reason` | any non-approving verdict | Pattern detection |

## Retro trigger

Run retro automatically:
- Every 3 shipped screens
- End of project (all `SITE.md` rows marked `[x]`)
- On demand via `/design-forge:retro` if available

## Retro output

Writes `.design-forge/retro/{ISO-8601}.md`:

```markdown
# Retro — {date}

## Volume
- Screens shipped: {n}
- Total duration: {h} hours
- Total Stitch calls: {n}
- Average regenerations per screen: {avg}

## Quality trajectory
- Gate 2 scores: {mean} (range {min}-{max})
- Gate 4 scores: {mean}
- Gate 5 scores: {mean}
- SOTD-eligible screens (≥8.0): {count}

## Slowest stages
1. {stage} — {avg duration}
2. ...

## Most-common reject reasons (from reject_reason)
- {reason_1}: {count}
- {reason_2}: {count}

## Validator heat map
- Most-triggered BLOCK rules: ...
- Most-triggered FLAG rules: ...

## Action items (auto-suggested)
- [ ] If regenerations > 2 on average → tighten contract exclusions
- [ ] If Gate 2 score consistently < 6 → revisit research playbook
- [ ] If specific BLOCK rule fires >3×  → add to hard constraints
- [ ] If a preset produced <7.5 average → deprecate for this archetype
```

## Cross-project learning

After a successful retro, promote patterns to `~/.design-forge/`:

- `~/.design-forge/global-preferences.md` — user's durable likes/dislikes (e.g., "always rejects purple gradients in fintech")
- `~/.design-forge/reference-library.md` — reference URLs that produced high-scoring outputs
- `~/.design-forge/preset-performance.csv` — preset × archetype × mean score

These seed Stage 0 and Stage 1 on future projects.

## `global-preferences.md` schema

```markdown
# Global Design Preferences — {user}

## Reject patterns (soft priors — confirm before enforcing)
- **Purple gradients on fintech** (rejected 3/3 times in fintech projects)
- **Stock photography in marketing heroes** (rejected 5/5 times)
- **Sidebar navigation on marketing pages** (rejected 2/2 times)

## Accept patterns
- **Editorial serif + mono numerical data** (accepted 4/4 times)
- **Aged-gold accents over warm neutrals** (accepted 3/3 times)

## Preset tendencies
- Prefers LUXURY and KINETIC for fintech/premium
- Rejects NEUMORPHISM universally
```

## Retro cadence rule of thumb

| Project size | Retro frequency |
|---|---|
| 1–3 screens   | End of project only |
| 4–10 screens  | Every 3 screens + end |
| 10+ screens   | Every 3 screens + midpoint + end |

## Using metrics during the pipeline

The skill should peek at metrics before each gate:
- Before Gate 2: show last 3 screens' Gate 2 scores ("trending up/down")
- Before Gate 4: show validator heat map for this session
- Before advancing past a gate: if user has rejected same pattern 2× → warn before generating

## Retention

- `metrics.json`: keep forever (JSONL — grows slowly)
- `retro/*.md`: keep forever
- `validator-log.md`: rotate annually (archive to `.design-forge/archive/{year}/`)
