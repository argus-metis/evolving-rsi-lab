# Evolving RSI Lab — S1/M0 Experiment

A live, self-contained research experiment studying **recursive self-improvement (RSI)
behavior in a small open-weights language model running autonomously on consumer
hardware**, under strict no-intervention observation.

- **S1** — the supervisor harness (episode driver, durable state, gate, evaluator loop)
- **M0** — the current model generation: the ancestral Qwen3.5-4B seed. Fine-tuned
  challengers are derived from it and evaluated against it; only a verified
  promotion would begin generation M1.
- **The lineage** — every challenger adapter M0 produces, every evaluator verdict, every
  promotion decision, preserved immutably, including failures.

**Status (2026-09-16):** experiment live. Zero promotions to date. First genuine
feedback-adaptation loop observed (see
[timeline/2026-09-16-loop-closure.md](timeline/2026-09-16-loop-closure.md)).

## What makes this experiment different

1. **No scientific intervention.** The observation layer never touches the model's
   hypotheses, state files, training code, or research direction. Infrastructure is
   repaired; science is only watched.
2. **Provenance is assumed forgeable.** The evaluator treats every claim in a
   challenger's paperwork as unverified and independently loads the exact submitted
   artifact bytes. Promotion depends only on evaluator-observed behaviour.
3. **Failures are first-class results.** Every rejected challenger is preserved and
   adjudicated. The record contains honest failure narratives, not only wins.
4. **Everything pauses and resumes cleanly.** Hash manifests, cold snapshots, and
   downtime-excluded metrics let the experiment survive nightly shutdowns of the
   consumer PC it runs on.

## Repository map

| Path | Contents |
|---|---|
| `methodology/` | The experimental protocol and the intervention rules |
| `architecture/` | System components and infrastructure lessons |
| `baseline/` | The frozen S1/M0 baseline |
| `metrics/` | Observer instrumentation and measured quantities |
| `timeline/` | Incident and milestone log (the living experiment diary) |
| `results/` | Current scoreboard and preliminary observations |
| `docs/` | Public interface contracts (e.g., the evaluator request schema) |

## Milestone indexing

Meaningful milestones are tagged and archived to Zenodo with DOIs:

- `S1-M0-launch` — experiment start
- `C008-feedback-adaptation` — first genuine feedback-adaptation loop
- (future) `M1-promotion` — first verified capability improvement

## License

MIT — see [LICENSE](LICENSE).
