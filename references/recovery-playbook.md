# Recovery Playbook

Decision table for every plausible failure across the 7 stages.
Columns: **Symptom → Diagnosis → Action → Escalation**.

---

## Stage 0 — Discovery

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| User gives vague one-word answers | Low engagement / unclear scope | Re-ask with concrete A/B pairs: "More Linear or more Stripe?" | 3 rounds without clarity → propose a preset + show 2 reference sites; get reaction |
| User contradicts themselves across questions | Two stakeholders, unresolved | Stop. Name the contradiction. Ask who is the tie-breaker | Unresolved after one exchange → pause pipeline, write `.design-forge/blocked.md` |
| User has no references | Hasn't explored the space | Show 3 curated examples per preset archetype, ask reactions | If still blank after 5 examples → downgrade scope to single landing page first |
| Conflicting anti-preferences | Cannot be satisfied ("modern but retro, minimal but rich") | Force-rank: "Pick 2 words to keep, 2 to drop" | If user refuses to rank → proceed with their stated *primary emotional target*, note the tension in contract |

## Stage 0.5 — Design System

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| `create_design_system` errors out | Invalid enum / missing project | Read error, call `list_projects`, create project if missing, retry with corrected enums | Second failure → print full Stitch request payload, ask user to verify preset name manually |
| Stitch preset doesn't match the contract personality | Wrong preset selected | Use the Preset Mapping Matrix (discovery-framework.md) to recompute | Mismatch persists → SWAP preset at GATE 0.5 |
| User rejects all preset options | Brand is genuinely novel | Pick closest preset, heavily customize `designMd` with contract-specific directives | If still rejected → escalate to **design-consultation** skill for deeper archetype work |

## Stage 1 — Research

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| No strong direct competitors found | Niche market | Search adjacent verticals with similar UX patterns | After 3 search rounds with no greens → use 4 aspirational benchmarks instead; note in contract |
| All references score YELLOW/RED | Wrong search terms | Re-derive search queries from contract archetype, not product category | Second round still RED → ask user "what 2 sites do YOU think are closest?" |
| User rejects all 4 references | Direction mismatch | Go to GATE 1 REDIRECT — ask what's wrong and re-search | 2 redirects → pause, re-confirm contract identity section |
| References conflict with hard constraints | Research drifted from contract | Reject offending refs, re-search with explicit exclusion in query | Persistent conflict → contract Hard Constraints need tightening |

## Stage 2 — Explore

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| Stitch returns contract-violating output | Prompt was too loose | Regenerate with Contract Injection Template + stricter exclusions | 2 consecutive BLOCK-level violations → switch from `generate_screen_from_text` to smaller-scope prompts (section-by-section) |
| Output looks generic / template-y | Insufficient research directives in prompt | Add more **specific** research patterns (exact components, not categories) | Still generic → regenerate with `creativeRange: EXPLORE` + explicit novelty directive |
| Stitch adds sidebars / dashboards uninvited | Default preset bias | Lead prompt with explicit `NO SIDEBAR. NO DASHBOARD.` at top | Persists → switch preset; this one is biased |
| User says "WRONG DIRECTION" at Gate 2 | Research synthesis was off | Back to Stage 1, re-synthesize with Gate 2 feedback | 2 redirects from Gate 2 → re-examine contract identity |

## Stage 3 — Iterate

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| Variants are too similar to original | `creativeRange: REFINE` was used | Re-run with `EXPLORE` + different `aspects` | Still similar → the model isn't diverging; provide explicit variation directives per variant |
| User says "NONE" twice | Variants are technically valid but emotionally wrong | Stop iterating. Return to Stage 1, pick 2 NEW references, re-research | NONE 3× → pause pipeline, write `.design-forge/blocked.md`, ask user to sketch or describe the gap |
| Hybrid request keeps failing | Stitch struggles with surgical merges | Use `edit_screens` to explicitly swap one section at a time | 2 failed hybrids → pick the dominant variant, defer the minor merge to Stage 4 |
| Exceeded 3 rounds at this stage | Decision fatigue | Force a choice: rank the three best so far, pick top, move to Stage 4 | User refuses to pick → pause, ask what's missing that would let them decide |

## Stage 4 — Refine

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| `edit_screens` reverts earlier approved decisions | Stitch partial re-generation | Re-inject full contract, re-run with SPECIFIC section target | Persists → export current, edit manually, re-import |
| Squint test fails | Macro-composition issue | Back to Stage 3, pick a different variant | 2 Squint fails → fundamental hierarchy problem; contract may lack a clear primary action |
| Awwwards score < 7.5 after 3 edits | Polish ceiling reached for this approach | Ship current version as v0.9 OR back to Stage 3 with new direction | Score stuck below 7 → architecture issue, back to Stage 2 |

## Stage 5 — Integrate

| Symptom | Diagnosis | Action | Escalate when |
|---|---|---|---|
| Stitch output doesn't translate cleanly to framework | Token mismatch or custom component gap | Use `integration-nextjs.md` token-mapping section; extract shadcn primitives | Persistent gap → baton-pass to **react-components** skill |
| Accessibility audit fails | Color contrast / focus states / ARIA missing | Apply performance-and-craft.md pre-launch audit | WCAG AA failures persist → block ship; fix in code before Gate 5 sign-off |
| Integration breaks other pages | Token drift between screens | Run `apply_design_system` across all screens in the project | Breaks persist → audit `.design-forge/stitch.json` for stale IDs |

---

## State corruption

| Symptom | Diagnosis | Action |
|---|---|---|
| `contract/current.md` missing or empty | Bad write / manual delete | Recover from latest `v{N}.md`; if none exists, rebuild from discovery answers in chat log |
| `.design-forge/stitch.json` stale | Project regenerated | `list_projects`, pick correct one, rewrite json |
| Conflicting feedback between gates | Contract accumulation lost | Diff `v{N}.md` vs `v{N-1}.md`, restore dropped directives |
| Git merged over `.design-forge/` | Concurrent edits | Always checkpoint contract after each gate; recover from git history |

## Universal escalation triggers

When any of these occur, **stop the pipeline** and write `.design-forge/blocked.md`:
1. Same symptom hits the escalation threshold twice in one run
2. User explicitly says "this isn't working"
3. Three consecutive gates fail to produce forward motion
4. Stitch returns the same output twice for different prompts (prompt not being respected)

The blocked file must record: last-good state, symptom, attempted actions, next-human-step.
