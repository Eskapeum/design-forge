# Batch Mode — Parallel Multi-Screen Pipelines

For sites with 5+ pages, serial execution wastes hours. Batch mode parallelizes where safe and serializes where necessary.

## What can parallelize

| Stage | Parallelizable? | Why |
|---|---|---|
| 0 Discovery         | No  | Single contract for the whole project |
| 0.5 Design System   | No  | Single design system |
| 1 Research          | **Yes** | Each screen's references are independent |
| 2 Explore           | **Yes (with care)** | Generation is independent; contract shared |
| 3 Iterate           | No  | User must pick winners one at a time |
| 4 Refine            | No  | Depends on winner selection |
| 5 Integrate         | **Yes** | Independent file writes |

## The rule

```
[serial]  Stage 0 → Stage 0.5
[parallel] Stage 1 for all P0 screens  → batch gate
[parallel] Stage 2 for all P0 screens  → batch gate
[serial]  Stage 3 → Stage 4 per screen
[parallel] Stage 5 across approved screens
```

## Batch Gate format

Shown after a parallel stage completes for N screens:

```
BATCH GATE — Stage {N} — {M} screens

home:      {summary} — validator PASS
pricing:   {summary} — validator FLAG (accent color drift)
about:     {summary} — validator PASS

Per-screen options:
- APPROVE all
- APPROVE {screen}, revise {other}
- HOLD all, revise together
```

## Dispatching parallel research

Spawn one subagent per screen with scoped prompts. Use this structure:

```
Subagent: research-screen
Inputs:
  - contract: .design-forge/contract/current.md
  - screen: {name}
  - type: {from SITE.md}
  - goal: {from SITE.md}
Outputs:
  - .design-forge/research/{screen}.md
Rules:
  - Stop after 4 references
  - Use research-playbook.md query templates
  - No web search beyond 8 total queries per screen
```

Dispatch N of these concurrently. Use the `superpowers:dispatching-parallel-agents` skill as the mechanism.

## Dispatching parallel Stage 2

Higher risk — each Stitch call must include the full contract and must not modify shared state except the validator log.

Rules:
- One subagent per screen
- Each receives: full contract, screen research, Contract Injection Template
- Each returns: Stitch screen ID + validator report
- No cross-screen writes to contract (main agent aggregates)
- If any BLOCK in a subagent: that screen goes into its own serial remediation; others continue

## Ordering constraint: shared component pages

If two screens share a navigation/footer, those components must be designed **once** and propagated. Path:

1. Identify shared sections (read `sections` field in SITE.md)
2. Run a "shared chrome" mini-pipeline first (Stages 1–4 for nav + footer)
3. Pin those artefacts in the contract as `## Shared Chrome`
4. All per-screen batch work must incorporate the pinned chrome

## Token budget awareness

Each subagent reads the full contract once. Size the contract to fit 5 parallel workers × (contract + research + Stitch response) within model context. If contract > 20KB, create `contract/current-brief.md` (identity + constraints only) and use that for parallel work; full contract stays for serial stages.

## When NOT to batch

- Fewer than 3 screens (overhead dominates)
- First screen of a new preset (you want serial learnings)
- Contract is still evolving (wait until Gate 1 approvals stabilize)
- User is present and wants full control (serial keeps them in the loop)

## Failure isolation

If one parallel subagent fails:
- Other subagents continue
- Failed screen gets its own `blocked.md` row
- Main agent reports: "{N-1} of {N} screens completed; {screen} blocked"

## Exit criteria for batch gate

Advance only when:
- Every parallel artifact exists
- Every validator report is attached
- No BLOCK-level violations in the batch
- User has approved the batch summary

Otherwise: isolate the failures, re-run just those subagents.
