# Open Questions & Known Limits

This document records unresolved questions and observed boundaries.
Its purpose is to preserve intellectual honesty and guide future exploration.

---

## 1. Scaling Limits

**Question:**  
At what scale does entropy-weighted consensus lose useful curvature?

**Observation:**  
- Simulations suggest meaningful stabilization up to ~100–300 recipients.
- Beyond that, low-entropy dominance may flatten consensus vectors.
- This triggers safe halts, not failures—but limits expressivity.

**Open:**  
Would hierarchical grouping preserve signal without reintroducing coupling?

---

## 2. Adversarial Diversity

**Question:**  
How does the system behave under *heterogeneous adversarial conditions*?

**Observed (B.1a):**
- Single adversarial segment was quarantined locally.
- No cascade or cross-segment contamination occurred.

**Unexplored:**
- Multiple adversarial segments simultaneously
- Adversaries mimicking low-entropy behavior
- Masked adversaries across privacy tiers

---

## 3. Metric Sensitivity

**Question:**  
How sensitive are outcomes to metric thresholds?

**Observation:**
- Tight drift bounds improve safety but reduce interpretive flexibility.
- Looser bounds increase expressivity but stress diagnostics.

**Open:**
- Optimal threshold tuning remains context-dependent.
- No universal parameterization identified.

---

## 4. Diagnostic Redundancy Depth

**Question:**  
Is dual validation (geometry + entropy) sufficient at larger scales?

**Observation:**
- Two independent metrics caught all injected anomalies so far.
- Diagnostic Guild prevented silent failures.

**Open:**
- Would a third orthogonal metric add value?
- Or would it introduce unnecessary overhead?

---

## 5. Replay vs. Real-Time Dynamics

**Question:**  
How do these patterns translate to non-deterministic environments?

**Limitation:**
- All experiments were replayable and deterministic.
- No real-time clock drift, network jitter, or asynchronous failure was modeled.

**Open:**
- Real-world noise may require additional guard layers.

---

## 6. Interpretive Bias

**Question:**  
Do role assignments bias outcomes?

**Observation:**
- Different roles produced consistent but distinct metric profiles.
- Narrative-focused roles scored lower on geometry but improved clarity.

**Open:**
- How neutral can role definitions truly be?
- Does role ecology shape consensus outcomes?

---

## 7. Formal Verification

**Question:**  
Can these properties be formally proven?

**Status:**
- Properties are empirically validated via simulation.
- No formal proofs included.

**Open:**
- Mapping these patterns to existing verification frameworks remains future work.

---

## Closing Note

These questions are not failures.
They define the *edge of understanding* reached so far.

Future work should aim to:
- stress these boundaries deliberately,
- refine metrics cautiously,
- and preserve containment above all else.
