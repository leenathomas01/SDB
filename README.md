# Selective Decode Broadcast (SDB)

**Concept Note — March 2026**

---

***Note:** This document records a stabilized communication pattern derived through phased validation and tested in sandboxed simulations. It is not a production protocol, deployment specification, or cryptographic standard. Only the abstraction boundary and validated properties are described here.*

---

## 1. The Structural Problem

Multi-recipient communication systems face a fundamental trade-off:

* **Unicast:** Safe containment, poor efficiency (O(n) transmissions)
* **Broadcast:** Efficient transmission, zero containment (all recipients see all content)

Existing systems resolve this by choosing one property—they do not attempt both.

This is not an implementation constraint. It is an architectural fact about how information spreads.

---

## 2. The Pattern: Selective Decode

SDB introduces a hybrid model where:

* A **single broadcast packet** contains multiple recipient-specific segments
* Each recipient is **structurally constrained** to decode only its assigned segment
* Decoding is enforced by **protocol structure, not trust**
* All other content remains opaque and non-interpretable

The key insight: isolation and efficiency are not mutually exclusive if decoding sovereignty is enforced *before* interpretation occurs.

> SDB does not add trust. It removes the need for it.

---

## 3. How It Works

### Packet Structure

A broadcast envelope contains:
* Shared metadata (versioning, timing, signatures)
* Recipient-specific segments (role-scoped, key-isolated)
* Fixed-size padding (prevents structural inference)
* Deterministic failure modes (abort, quarantine, null)

### Decode Mechanism

Recipients receive:
* Complete packet (like traditional broadcast)
* Segment-specific keys and grammar rules (their portion only)
* No access to other segments or their context

Non-target segments:
* Cannot be decoded (key not available)
* Cannot be inferred (padding obscures structure)
* Cannot be partially interpreted (grammar constraints are role-scoped)

Attempts to violate these constraints produce safe failures, not partial information leakage.

### Containment Principle

Failure is localized:
* If one recipient's segment has an issue, only that recipient is affected
* No cascade to other recipients
* No shared mutable state to corrupt
* No global halt required

This is achieved through **structural isolation**, not behavioral compliance or post-hoc filtering.

---

## 4. What It Achieves

### Efficiency

Single transmission replaces multiple unicasts:
* Measured reduction in Transmission Efficiency Coefficient (TEC): ~50% vs sequential unicast
* Scales with recipient count
* No degradation in interpretation quality or safety

### Containment

Per-recipient isolation is preserved:
* Cross-segment leakage: 0 (structurally impossible)
* Adversarial segment detection: Immediate and local
* Cascade failures: None observed under tested conditions
* Audit trail: Deterministic and replayable

### Auditability

All behavior is observable:
* Deterministic packet structure (no randomness in decode)
* Sealed logs with cryptographic signatures
* Bit-exact replay for third-party verification
* Explicit failure modes (abort, quarantine, null)

---

## 5. Validation Approach

SDB was validated through **phased structural testing** in sandboxed simulations:

### Phase A: Safety Primitives

Established that core constraints can be enforced:
* Isolation by default (no unintended information flow)
* Explicit decode constraints (malformed input fails safely)
* Drift detection (divergence stays bounded and observable)
* Deterministic replay (all behavior is auditable)

**Exit criteria:** All safety primitives validated before proceeding.

### Phase B.1: Broadcast Containment

Demonstrated that efficiency and isolation coexist:
* Per-recipient decode isolation held
* No cross-segment inference observed
* Efficiency gains measured without safety regression
* Independent diagnostics produced consistent results

### Phase B.1a: Adversarial Isolation

Tested behavior under deliberate malice:
* Injected high-entropy, structurally invalid segments
* System detected and quarantined locally
* No cascade effects
* Other recipients unaffected

### Phase B.2: Segmented Decode (Advanced)

Validated complex multi-segment scenarios:
* Four concurrent recipient roles
* Zero-knowledge privacy masks
* Recursive consensus anchoring for stability
* All diagnostic metrics converged within tolerance

**Key result:** TEC reduction ~52% with advanced features; drift improved through consensus-driven stabilization.

---

## 6. What It Does NOT Do

SDB is defined as much by exclusion as inclusion.

It does **not**:

* Guarantee semantic equivalence across recipients
* Provide learning or adaptation (no weight updates, no persistent state modification)
* Define shared vocabularies or ontologies
* Perform reasoning, inference, or moderation
* Support chaining or accumulation of packets over time
* Operate in real-time with true adversaries (all testing is deterministic, sandboxed)
* Prevent misuse by administrators or protocol designers

SDB is a **communication pattern for multi-recipient isolation**, not a complete system.

---

## 7. Boundary of Validity

SDB operates under explicit assumptions:

* Recipients respect structural constraints (decode isolation is enforced by parsing, not goodwill)
* Packet structure is not adversarially probed for side-channel inference
* Administrators do not intentionally weaken isolation (e.g., by sharing keys)
* Segments are not used to encode reconstructable information outside protocol scope
* Systems maintain deterministic replay capability (no asynchronous jitter, no real-time clocks)

Within these conditions, the validated properties hold.

Outside them, they may degrade or fail. SDB does not prevent protocol-level misuse; it bounds what the pattern itself retains and transmits.

---

## 8. Validated Properties

The following properties held consistently under defined conditions across all test phases:

| Property | Evidence | Scope |
|----------|----------|-------|
| Per-recipient decode isolation | Phase B.2 | No cross-segment leakage observed |
| Broadcast efficiency with containment | Phase B.1, B.2 | TEC reduction ~50–52% vs unicast |
| Localized failure and quarantine | Phase B.1a | Adversarial segments isolated; no cascade |
| Diagnostic redundancy | All phases | Independent metrics converged within ±0.05 |
| Bounded recursive stabilization | Phase B.2 | Consensus anchors improved drift; no runaway |
| Deterministic auditability | All phases | All runs replayed bit-exact |

These are not theoretical guarantees. They are properties that held under explicit test conditions with predefined guards and success criteria.

---

## 9. What Was Rejected

Several designs were considered and deliberately excluded because they failed to maintain both efficiency and safety:

* **Trust-based containment:** Relies on behavioral compliance; not auditable under adversarial conditions
* **Post-hoc filtering:** Allows partial interpretation before filtering; breaks isolation guarantees
* **Global halt on anomaly:** Over-fragile; allows one faulty segment to disrupt all recipients
* **Unbounded recursion:** Risk of oscillation; difficult to reason about stability
* **Heuristic-only safety:** Non-deterministic; fails to support replay
* **Shared mutable state:** Enables indirect coupling; violates containment

These rejections are intentional design decisions, not limitations to be worked around.

---

## 10. Open Questions

SDB identifies several boundaries where understanding remains incomplete:

* **Scaling limits:** At what recipient count does consensus entropy-weighting flatten, reducing signal curvature?
* **Heterogeneous adversaries:** How does the system behave under simultaneous, masked adversarial conditions?
* **Metric sensitivity:** Is dual validation (geometry + entropy) sufficient at larger scales, or does a third metric add value?
* **Replay vs. real-time:** How do these patterns translate to non-deterministic environments with network jitter and asynchronous failures?
* **Role bias:** Do role assignments systematically bias outcome metrics? Is role ecology neutral?
* **Formal verification:** Can these properties be formally proven, or are they bounded empirical observations?

These are not failures. They define the edge of what has been explored.

---

## 11. Why It Matters

SDB reframes broadcast communication:

> from (efficiency XOR containment) → (efficiency AND containment)

This removes a lower-level constraint on system design:

* Multi-recipient scenarios no longer force choice between scalability and safety
* Audit trails can be deterministic and replayable
* Failure remains local and observable
* Efficiency gains do not require trust assumptions

It does not solve higher-level problems (semantics, reasoning, coordination). It changes what is possible at the communication layer.

---

## 12. Limitations

This work is bounded by explicit constraints:

* **Not a production specification:** Cryptographic details are illustrative, not hardened
* **Not a learning system:** Recursive anchoring is bounded stabilization, not adaptation
* **Not a real-time protocol:** All testing assumed deterministic, replayable execution
* **Not a human-interpretable system:** Narratives are observational, not evaluative
* **Not optimal:** Passing validation gates means "correct under tested conditions," not "best possible"
* **Not general-purpose:** These properties hold for the specific pattern tested; extensions require new validation

---

## 13. Methodology

All results in this repository come from:

* **Thought experiments implemented as structured simulations**
* **Sandboxed environments with no external connectivity**
* **Explicit success gates and failure conditions per phase**
* **Role-separated agents with fixed, non-adaptive rules**
* **Deterministic packet structure and sealed, cryptographically signed logs**
* **Replayable, bit-exact execution for auditability**

This methodology prioritizes reproducibility and auditability over performance optimization or real-world scalability claims.

---

## 14. Intended Audience

SDB is relevant to:

* Systems thinkers exploring communication patterns
* Protocol designers considering multi-recipient architectures
* Safety researchers examining containment under adversarial conditions
* Engineers building auditable, replayable systems

It is **not** intended as:

* Speculative philosophy or narrative fiction
* A roadmap to deployment
* A complete communication system
* A claim about emergence or autonomy

---

## Note

This document captures a communication pattern that has been derived, phased-validated, and explicitly bounded.

Its utility depends on how it interacts with specific system requirements, not on the abstraction alone.

All claims are provisional, scoped to simulation conditions, and subject to revision when tested in different contexts.

---

*Concept note created March 2026. Parked as a stabilized primitive within the research index.*
