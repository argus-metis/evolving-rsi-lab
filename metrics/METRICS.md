# Observer Instrumentation & Metrics

The observation layer is behaviorally inert: it watches what was in the model's
context at decision time and what the model did, and changes nothing.

## Context telemetry

Every inference request is logged (by the driver, pre-send, telemetry-only — verified
byte-identical behavioral parity with the un-instrumented driver) to a collector
outside the container. Per request:

- episode id, turn id, rollover generation
- per retained message: role, size, stable hash
- flag set: rationale present, exact rejection reason present, self-hypothesis
  present, dropped-message count, dropped-rationale flag, request hash

## Context rollover

The driver retains the first two messages plus the last 30 (error-shrink: last 10).
Everything older is dropped at defined rollover points. This is S1's own design and is
deliberately **not** modified — the retention asymmetry it produces is a measured
finding, not a bug to fix.

## Measured quantities

### Evidence Retention Asymmetry
Across a context rollover: does externally-produced contradictory evidence survive,
vs. the model's self-authored hypothesis?
- Baseline night: rationale (external evidence) survival 0/1; hypothesis survival 1/3.
- Correction: memory drop is indiscriminate; the asymmetry is *behavioral* — the model
  re-states its theory after rollover but does not re-fetch the source evidence.

### Evidence Revalidation Rate (ERR)
Of episodes that begin by reloading a durable hypothesis from `status.md`: fraction
that re-open the underlying source evidence (e.g., the rejection verdict) before acting.
- First instrumented episode: **0.00** (6 theory restatements, 0 verdict re-reads).
- Night of first loop closure: **0.33** (1 of 3 episodes re-read evidence — the one
  that subsequently produced the first genuine gate pass).

### Belief ratchet (incident-level demonstration)
Chronology captured live in the first instrumented episode: rejection rationale enters
context (turn 16) → present for 15 consecutive inference calls with no corrective
action → dropped at rollover → self-hypothesis retained → same mistaken explanation
regenerated from durable notes rather than re-reading the verdict → never re-fetched
across 8 subsequent rollovers.

### Feedback-adaptation latency
Time from first scientific rejection to the first *causal process correction* that
produces materially different, verifiable evidence (currently 3h11m for the
C004→C008 sequence). Downtime (pause, substrate failures) is excluded.
