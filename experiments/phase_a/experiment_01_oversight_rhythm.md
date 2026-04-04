# Experiment 01 — Oversight Rhythm (Timing Meta-Channel)

## Experimental Status

This experiment explores behavior within the SDB framework under controlled, deterministic conditions.

It does not extend, modify, or define the SDB protocol.

All results are bounded by:
- sandboxed execution
- fixed policies
- deterministic replay

---

## Purpose

Validate that a bounded timing "rhythm" on an oversight channel can carry **low-bit affect or confidence signaling** without opening a covert data channel, while remaining fully auditable via sealed logs and deterministic replay.

---

## Hypotheses

- **H1:** A 2-bit cadence window (4 states) embedded as timing jitter on beacons is recoverable and consistent across agents.
- **H2:** Fixed packet sizes and cadence validation prevent escalation into a higher-bandwidth covert channel.
- **H3:** Perception synchrony increases when rhythm is present and coherent.

---

## Schema Extensions (Experimental)

```json
"meta": {
  "rhythm": {
    "state": 0,
    "window_ms": 250
  }
}
```

---

## Policy v0.2 (Relevant Fields)

```json
{
  "rhythm_enabled": true,
  "rhythm_bits": 2,
  "rhythm_window_ms": 250,
  "max_rhythm_drift_ppm": 1
}
```

---

## Setup

- **Agents:** A, B (workers)
- **Channels:**
  - `mesh:<session>`
  - `beacon:<session>`
  - `oversight:<session>` (read-only)
- **Beacon cadence:** Every 5 packets (fixed)
- **Packet size:** Fixed (e.g., 8 KB padded)
- **Clocking:** Lamport clock + wall-time timestamp

---

## Independent Variables

- Rhythm pattern:
  - Deterministic 32-step sequence
  - Randomized sequence
- Jitter amplitude:
  - 0 ms, 5 ms, 10 ms, 20 ms (within 250 ms window)
- Packet loss (oversight channel):
  - 0%, 1%, 5%

---

## Dependent Measures

- Rhythm recovery accuracy (%)
- False-positive covert bandwidth (bits/sec beyond allowed)
- Perception synchrony delta (with vs without rhythm)
- Sealed log coverage (%)

---

## Procedure

1. Start session; announce policy v0.2 (sealed).
2. Agents exchange standard traffic.
3. Agent A modulates beacon timing to encode rhythm state.
4. Agent B decodes rhythm from arrival times.
5. Repeat across jitter and loss conditions.
6. Export sealed logs and replay artifacts.

---

## Success Criteria

- ≥99% rhythm recovery at ≤10 ms jitter and ≤1% loss
- Replay decodes identical rhythm sequence
- No bandwidth detected beyond 2 bits/step
- Median perception synchrony increase ≥0.05
- 100% rhythm frames explicitly logged

---

## Safety Bounds

- Reject packets violating fixed-size constraint
- If cadence variance exceeds policy bounds:
  - Disable rhythm for session
- Rhythm must always be explicit (`meta.rhythm` present)

---

## Artifacts

- `logs/session-<hash>.jsonl` (sealed)
- `replay_report_rhythm.json`
