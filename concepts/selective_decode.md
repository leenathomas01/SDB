# Selective Decode

## Definition

Selective decode is a communication model where:

- a single transmission contains multiple recipient-specific payloads  
- each recipient is structurally constrained to decode only its assigned segment  
- all other content remains non-interpretable  

Enforcement is structural, not behavioral.

---

## Core Properties

### Decode Sovereignty

Each recipient:
- has access only to its assigned decode context  
- cannot access keys, grammar, or structure of other segments  

Out-of-scope decoding fails deterministically.

---

### Structural Enforcement

Isolation is enforced through:
- segment-specific keys  
- role-scoped grammar  
- fixed-size padding  

No reliance on:
- trust  
- post-hoc filtering  

---

### Non-Observability

Recipients cannot infer:
- number of segments  
- roles of others  
- structure beyond their scope  

---

## Failure Behavior

Invalid decode attempts result in:
- abort  
- quarantine  
- null output  

No partial interpretation is permitted.

---

## Role in SDB

Selective decode is the **core mechanism** enabling:

- broadcast containment (Phase B.1)  
- adversarial isolation (Phase B.1a)  
- segmented transmission (Phase B.2)
