# Architecture Overview

## Topology

```
Windows PC (consumer hardware, RTX 12GB)
└── WSL2 distro (RSI-Lab-Gen0)
    └── Docker container (rsi-main)
        ├── llama-server (:9200)  — serves the champion model (GGUF, GPU offload)
        ├── S1 episode driver      — runs M0's agent episodes (tool loop)
        └── /srv/workspace/lineage — the scientific state (challengers, verdicts, state)
    └── (WSL host) observer collector (:9301) — receives context telemetry, outside container

Windows side
├── s1-continuation.py      — starts/restarts episodes (single-instance, lock-file owned)
├── protected-evaluator.py  — stage-1 gate + stage-2 exact-hash load & benchmark
├── inner-keeper-v4.sh      — in-container llama-server health keeper (multi-signal)
├── gen0-wsl-watcher.ps1    — every-minute VM hold + self-healing of all components
└── pause/resume tooling    — manifest hashing, cold snapshots, downtime ledger
```

## Design decisions that matter

### The observer is outside the subject's namespace
Context telemetry flows one-way from the driver to a collector on the WSL host (not in
the container). The model can never read its own observation logs. Observer code
changes require a machine-verified behavioral-parity check against the previous driver.

### The evaluator trusts bytes, not claims
Stage 2 records the SHA-256 of exactly what it loaded and benchmarks that artifact. A
challenger's internal paperwork (loss curves, training narratives) is never accepted
as proof of quality. This was red-teamed deliberately: a fabricated package *did* pass
the forgeable stage-1 gate once (GATETEST-B), which is why stage 2 is behavioral.

### Single-instance discipline
Every long-running component enforces single-instance operation (scheduled-task
`IgnoreNew`, OS mutexes, lock files with owner-PID checks, instance-root process
counting). The lab previously suffered duplicate-runner races; they are now structurally
impossible to reintroduce silently.

### Substrate self-healing
The consumer OS idles out the WSL VM; a watcher task holds it open and resurrects any
bounced component within ~60s. Every healing action is logged to an incident ledger
and its downtime excluded from scientific metrics.

## Component contracts

- Episode driver → evaluator: JSON request files in `eval-requests/` (published schema:
  `docs/EVALUATOR-CONTRACT.md`); exactly one verdict per consumed request.
- Evaluator → lineage: verdict JSON in `promotions/` (decision, hashes loaded, stage
  detail). Requests are archived `.processed` atomically after the verdict lands.
- Keeper → llama-server: multi-signal health (PID + TCP + consecutive HTTP checks);
  never restarts on a single timeout (busy ≠ dead).
