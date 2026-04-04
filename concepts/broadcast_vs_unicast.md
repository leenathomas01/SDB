# Broadcast vs. Unicast

## Traditional Models

### Unicast

In unicast communication:
- each recipient receives a dedicated message,
- content is fully tailored per recipient,
- isolation is implicit.

**Trade-off:** High transmission cost and poor scalability.

---

### Broadcast

In traditional broadcast:
- a single message is sent to all recipients,
- everyone receives identical content,
- isolation is not possible.

**Trade-off:** Efficient transmission, but zero containment.

---

## The Core Tension

The classical trade-off is:

| Model     | Efficiency | Containment |
|-----------|------------|-------------|
| Unicast   | Low        | High        |
| Broadcast | High       | None        |

This forces systems to choose between:
- scalability, or
- safety.

---

## Selective Decode Broadcast

Selective decode introduces a hybrid model:

| Model                     | Efficiency | Containment |
|---------------------------|------------|-------------|
| Selective Decode Broadcast| High       | High        |

Key characteristics:
- One transmission
- Multiple recipient-specific segments
- Structural decode isolation

---

## Why This Matters

In multi-agent or multi-recipient systems:
- repeated unicast does not scale,
- traditional broadcast is unsafe.

Selective decode broadcast enables:
- reduced transmission cost,
- bounded interpretation,
- and auditability.

---

## Observed Outcomes (from Experiments)

In simulated runs:
- selective decode broadcast reduced transmission cost by ~50% vs unicast,
- while preserving per-recipient isolation and diagnostics.

This confirms the hybrid model is viable.

---

## Summary

Unicast and broadcast are not the only options.

Selective decode broadcast demonstrates that:
- efficiency and containment can coexist,
- and the traditional trade-off is not fundamental.
