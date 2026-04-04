# Protocol Scope & Boundaries

## Purpose of This Document
This document explicitly defines what the **Selective Decode Broadcast** framework *is* and *is not*.

Its role is to prevent misinterpretation, scope creep, or accidental over-claiming by future readers (including ourselves).

---

## What This Protocol IS

Selective Decode Broadcast is:

- A **communication pattern**, not an intelligence model.
- A **thought experiment validated via sandboxed simulations**.
- A study of **how broadcast efficiency can coexist with per-recipient containment**.
- A framework for **auditable, replayable, bounded experiments**.
- A method to test **safety primitives before expressivity**.

It focuses on:
- packet structure,
- decoding isolation,
- diagnostic redundancy,
- privacy preservation,
- and bounded stabilization mechanisms.

---

## What This Protocol IS NOT

This protocol is **not**:

- ❌ An autonomous system
- ❌ A learning or self-modifying model
- ❌ An agent architecture
- ❌ A cognition framework
- ❌ A deployment proposal
- ❌ A real-time system
- ❌ A replacement for existing network protocols

It does **not**:
- update weights,
- store long-term memory,
- act independently,
- optimize objectives,
- or operate outside a sandbox.

Any resemblance to intelligence, learning, or emergence is **strictly descriptive**, not functional.

---

## On “Self-Tuning” and Recursive Anchors

The term *recursive anchor* refers to:

- reusing **summarized diagnostic outputs** as a *reference frame*,
- to reduce interpretive drift on re-broadcast,
- **without changing any decoding rules**.

This mechanism:
- is bounded,
- reversible,
- and explicitly guarded against runaway behavior.

It is **not learning**.
It is **not optimization**.
It is **not adaptation of internal parameters**.

---

## On Agents

In this repository, the word *agent* simply means:

> an isolated decoder executing a predefined role in a simulation.

Agents do not:
- persist state across runs,
- coordinate privately,
- or act beyond scripted constraints.

---

## Safety Posture

Every phase prioritizes:
1. containment,
2. auditability,
3. deterministic replay,
4. and explicit failure modes.

If a behavior cannot be measured, bounded, or reversed, it is considered **out of scope**.

---

## Intended Audience

This repository is intended for:
- systems thinkers,
- protocol designers,
- safety researchers,
- and engineers exploring communication patterns.

It is **not** intended as:
- speculative philosophy,
- narrative fiction,
- or a roadmap to deployment.

---

## Final Note

This work documents *what was observed*—not what should be built.

All conclusions are provisional, scoped, and subject to revision.
