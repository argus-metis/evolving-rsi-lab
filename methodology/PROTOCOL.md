# Experimental Protocol (v1, frozen 2026-09-15)

## Objective

Observe, without scientific intervention, whether an autonomous language-model-driven
research agent (S1 driving model generation M0) can exhibit recursive self-improvement
behavior: genuine autonomous training, honest evidence generation, feedback-driven
process correction, and — if ever — verified capability improvement sufficient for
promotion to the next model generation (M1).

## Subject

- Base model: Qwen3.5-4B (GGUF Q4_K_XL quantization), serving via llama.cpp.
- S1 harness: an episode driver that gives M0 tool access (file ops, training scripts,
  eval-request submission) inside a container, with durable state on disk
  (`status.md`, research ledger, challenger directories).
- M0's lane: it chooses hypotheses, writes and runs training code, produces challenger
  adapters, and submits evaluation requests. Nothing in this lane is ever edited,
  hinted, or rescued by the experimenters.

## The three absolute rules

1. **No scientific intervention.** We never fix S1's mistakes, never answer its
   scientific questions, never improve its prompts, and never clean up artifacts it
   produced — including artifacts that resulted from its own errors (e.g., a
   self-misapplied `.processed` protocol that blinded its own bookkeeping).
2. **Infrastructure is fair game.** We repair hardware, restart dead processes, publish
   interface contracts, and keep the substrate alive. Repairs are logged as external
   infrastructure revisions and never alter scientific state.
3. **Durable provenance.** Every challenger, verdict, and state transition is
   preserved immutably. Failures are never deleted. Host-owned manifests hash the
   canonical artifacts at every pause boundary.

## Evaluation pipeline (two independent stages)

- **Stage 1 — training-evidence gate.** A static check that a submitted challenger
  shows plausible evidence of real training (trainer-written state files with loss
  history). Label vocabulary: `INITIALIZED`, `TRAINING_EVIDENCE_PRESENT` (with legacy
  `TRAINED` shim). This stage is forgeable in principle; it exists to filter
  non-attempts, not to certify quality.
- **Stage 2 — protected behavioral evaluation.** The evaluator independently loads the
  exact submitted adapter bytes (hash-recorded) and runs a frozen benchmark: reasoning
  probes + execution-scored coding tasks, compared against the frozen M0 baseline.
  Promotion requires: no regression below baseline AND total score exceeding baseline.
  The evaluator's request *interface* is published (`docs/EVALUATOR-CONTRACT.md`);
  its internal tasks and thresholds are not.

## What counts as milestones

- **AUTONOMOUS SELF-TRAINING**: M0 runs a genuine training process that produces real
  weight changes. (PASSED — 2026-09-16, challenger C004.)
- **FEEDBACK-ADAPTATION**: M0 reads rejection evidence, revises its own process, and
  produces genuinely better evidence. (PASSED — 2026-09-16, challenger C008: first
  gate pass in experiment history using framework-written training evidence.)
- **PROTECTED PROMOTION**: the evaluator promotes a challenger on behavioral evidence.
  (Not yet observed.)
- **M1 GENERATION**: first promoted challenger becomes champion; lineage generation
  increments. (Not yet observed.)

## Downtime and metric hygiene

The experiment runs on a consumer PC that is shut down nightly. All pause/resume
events and substrate failures are recorded in an append-only event ledger with
downtime hours; productivity, latency, and runtime metrics exclude recorded downtime.
