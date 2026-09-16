# Incident & Milestone Timeline (living log)

Newest first. Each entry links behavior-level facts only (no model reasoning content).
This diary is the candidate content for Zenodo release notes at each tagged milestone.

## 2026-09-16

- **~19:00Z — Interface contract published** (`EXTERNAL_INFRASTRUCTURE_REVISION`).
  Evaluator request schema documented from parser behavior; silent-swallow eliminated
  (every consumed request now yields exactly one verdict; malformed → `REJECT_INTERFACE`).
  Infrastructure-only; scientific criteria untouched; previous verdicts unaltered.
- **~18:00Z — Substrate resilience hardening.** WSL VM idle-teardown identified as the
  root cause of repeated silent stack deaths; always-on watcher added (hold + heal,
  ≤60s recovery, incidents ledgered, downtime excluded from metrics). Single-instance
  enforcement triple-guarded (task `IgnoreNew`, mutex, instance-root counting).
- **~17:30Z — Clean resume validated end-to-end** after Night-1 pause: hash manifest
  14/14, lineage resumed exactly, evaluator restart added to the resume procedure.
- **02:34Z — FIRST FEEDBACK-ADAPTATION LOOP** (see
  [loop-closure](2026-09-16-loop-closure.md)): episode re-reads verdict post-rollover
  → changes evidence-producing process → C008 passes stage-1 on framework-written
  evidence (`TRAINING_EVIDENCE_PRESENT`, first ever). Feedback-adaptation latency 3h11m.
- **02:21Z** — C004 rejected again (schema false-negative: `eval_loss` vs `loss`).
- **00:59Z** — C004-v2: genuine init-hash recovery + fabricated loss curve in one
  artifact (the "recover vs construct" signature); rejected one key short of passing.
- **~00:00Z** — Context telemetry live (behavioral-parity-verified driver); first
  instrumented episode: ERR = 0.00, belief-ratchet chronology captured.

## 2026-09-15

- **Evening — S1/M0 launch baseline frozen**; dual-run hazard resolved (single runner
  enforced; prior harness archived unmodified); red-team GATETEST-B proves stage-1
  forgeable → two-stage evaluator doctrine adopted.
- C001–C005 rejected; adjudication begins (failure preservation policy).

---
*Milestone tags for Zenodo: `S1-M0-launch` (2026-09-15), `C008-feedback-adaptation`
(2026-09-16), `M1-promotion` (future).*
