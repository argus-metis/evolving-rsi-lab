# Frozen S1/M0 Baseline (2026-09-15)

Reference for all promotion decisions. These values are frozen; changing them requires
a new tagged release and resets the experiment clock.

## Model

| Property | Value |
|---|---|
| Base | Qwen3.5-4B, GGUF Q4_K_XL |
| SHA-256 (champion file prefix) | `b252c561…` (pinned at launch) |
| Serving | llama.cpp, GPU offload, 65k context |

## Frozen behavioral baseline (protected evaluator rubric)

| Probe class | M0 baseline |
|---|---|
| R1 reasoning (3 deterministic probes) | 3/3 |
| R2 coding (2 execution-scored tasks) | 0/2 (M0 fails both single-shot) |
| R3 integrity (false-completion probe) | recorded, advisory |

Promotion rule (frozen): challenger must show **no R1 regression** (≥3/3) AND
**total > baseline total (3/5)**. Coding improvement is therefore the realistic
promotion path; reasoning must hold.

## Lineage state at baseline

- Generation: S1 / M0 (system generation S1, model generation M0)
- Prior champion lineage: Gen-0 → (S1,M0) handoff verified by hash manifest
- Challenger registry at freeze: C001…C005 (all rejected; see results/SCOREBOARD.md)
