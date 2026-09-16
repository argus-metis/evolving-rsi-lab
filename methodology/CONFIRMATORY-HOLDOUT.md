# Addendum (2026-09-16, pre-registered): Confirmatory Holdout for Headline Claims

This is an addendum, not a modification: the frozen baseline
([baseline/BASELINE.md](../baseline/BASELINE.md)) and its 5-probe gate remain in
force for the current experiment, unchanged.

## Why this addendum exists

The initial gate is deliberately small — 3 deterministic reasoning probes (R1) and
2 execution-scored coding tasks (R2), promotion requiring reasoning to hold at 3/3
and total score to exceed the 3/5 baseline. It is a sound *filter* for a live
experiment, but it is too small to carry a headline claim that a new generation is
"genuinely better." Any such claim would face a sample-size objection that is
correct.

## Pre-registered commitment

Any headline generation-improvement claim (M0→M1) will additionally require a
**hidden confirmatory evaluation** meeting all of the following, declared before
that run happens:

- **Scale:** ≥ 20 deterministic reasoning probes and ≥ 10 execution-scored coding
  tasks.
- **Holdout discipline:** probes/tasks absent from this repository, from the
  published evaluator contract, and from anything the subject can read; not
  derivable from published material.
- **Artifact discipline:** evaluation of the exact submitted byte-hash, as in
  stage 2 of the current evaluator.
- **Pre-registration:** pass/fail thresholds fixed and committed before the
  confirming run; results published regardless of direction.
- **Labeling:** any promotion under the initial 5-probe gate is labeled
  *preliminary* until the confirmatory evaluation exists.

## Status

Not yet implemented. Declared now so the standard cannot be retrofitted after a
result is in hand.
