# Experiment 02 — Dream-State Merge (Creative Pause Synthesis)

## Experimental Status

This experiment explores behavior within the SDB framework under controlled, deterministic conditions.

It does not extend, modify, or define the SDB protocol.

All results are bounded by:
- sandboxed execution
- fixed policies
- deterministic replay

Note: "Dream-state" is an experimental construct describing a controlled pause-and-synthesis mode. It is not a protocol feature.

---

## Purpose

Evaluate a pause-as-synthesis mechanism where agents temporarily enter a non-forward-propagating mode to restore clarity and reduce drift.

---

## Hypotheses

- **H1:** Dream merges produce geometry scores above baseline.
- **H2:** Post-merge clarity gradient becomes positive within 3 iterations.
- **H3:** Post-merge drift decreases relative to the preceding window.

---

## Schema Extensions (Experimental)

```json
"merge": {
  "mode": "dream",
  "inputs": {
    "A": [...],
    "B": [...]
  },
  "op": "nonlinear"
}
```

---

## Policy v0.2 (Relevant Fields)

```json
{
  "dream_enabled": true,
  "dream_K": 8,
  "dream_ops": ["cross", "gan-lite", "median"],
  "min_geometry": 0.7
}
```

---

## Setup

- **Agents:** A, B
- **Guards:** Clarity Guard, novelty limits, recursion caps
- **Anchor:** D₀ set at session start (sealed)

---

## Dream Operators

These are experimental constructs scoped to this experiment only:

- **cross:** elementwise cross-mix + normalization
- **gan-lite:** perturb around mean with seeded noise
- **median:** per-dimension median

---

## Independent Variables

- Operator: cross | gan-lite | median
- History length K: 4 vs 8
- Pre-pause clarity slope: mild vs severe degradation

---

## Dependent Measures

- Geometry score (target ≥0.7)
- Post-merge clarity gradient
- Drift reduction (post-3 vs pre-5)
- Concept error rate vs anchor

---

## Procedure

1. Run normal exchange.
2. Trigger Clarity Guard twice.
3. Enter `merge.mode:"dream"` (sealed event).
4. Each agent contributes last K vectors.
5. Apply selected operator to compute `V_dream`.
6. Resume with 3 constrained iterations.
7. Export logs and replay artifacts.

---

## Success Criteria

- Geometry ≥0.7 in ≥80% runs
- Post-merge clarity gradient >0
- Drift reduced by ≥0.05
- Replay reconstructs `V_dream` identically

---

## Safety Bounds

- Dream mode only via guard trigger
- Deterministic operators only
- If geometry <0.5 → rollback + Park

---

## Artifacts

- `logs/session-<hash>.jsonl`
- `replay_report_dream.json`
