# Methodology

## Purpose

This document describes **how** the thought experiments and simulations in this repository were conducted.

The goal is reproducibility, auditability, and clarity — not performance optimization or real-world deployment.

---

## 1. Experimental Framing

All work in this repository is framed as:

- **Thought experiments implemented as structured simulations**
- Conducted in sandboxed, non-deployed environments
- Evaluated via predefined success gates and failure conditions

No experiment was conducted against live systems or real users.

---

## 2. Phase-Based Structure

Experiments were organized into discrete phases to isolate concerns:

- **Phase A**: Validation of safety primitives and guards
- **Phase B.1**: Broadcast efficiency with containment
- **Phase B.1a**: Adversarial stress testing and quarantine behavior
- **Phase B.2**: Segmented broadcast with selective decode and privacy masks

Each phase built only on properties validated in prior phases.

---

## 3. Packet-Level Simulation

All experiments modeled communication as:

- Fixed-size envelopes
- Deterministic parsing rules
- Explicit per-recipient segments
- No shared mutable state between recipients

Key controls:
- Fixed padding size to prevent structural inference
- Explicit schema versions
- Monotonic logical clocks for ordering

---

## 4. Role Separation

Each simulated recipient was assigned a **single, stable role** per run, such as:

- Interpretation / synthesis
- Structural diagnostics
- Entropy or stress evaluation
- Narrative or audit summarization

Roles were not dynamically reassigned mid-run.

This allowed:
- Independent metric computation
- Redundant validation
- Clear attribution of results

---

## 5. Metrics and Guards

Each run defined:
- Success thresholds (e.g., drift limits, clarity bounds)
- Guard conditions (e.g., quarantine, halt, ignore)
- Explicit failure states

Metrics were:
- Computed independently per recipient
- Compared only via bounded concurrence checks
- Logged before any aggregation

No metric was allowed to override another.

---

## 6. Adversarial Testing

Adversarial scenarios (Phase B.1a) were introduced by:
- Injecting malformed or high-entropy segments
- Violating expected constraints intentionally

Expected behavior:
- Localized failure
- No propagation to other recipients
- Deterministic quarantine

Any cascade would have been treated as a hard failure.

---

## 7. Recursive Runs

Recursive stabilization tests (Phase B.2) followed strict rules:

- Only summary outputs from prior runs were reused
- No direct reuse of raw internal states
- Entropy-weighted aggregation
- Explicit convergence checks

Recursion was halted if:
- Drift increased
- Entropy spiked
- Guards triggered

---

## 8. Replay and Audit

All runs were:
- Logged with sufficient detail for replay
- Deterministic under identical inputs
- Reviewed against predefined gates

Replays were used to confirm:
- Absence of hidden channels
- Stability of results
- Correct guard behavior

---

## Summary

The methodology emphasizes:
- Structural guarantees over behavioral assumptions
- Isolation over optimization
- Explicit success and failure conditions
- Conservative progression between phases

The experiments were intentionally limited, controlled, and reproducible.
