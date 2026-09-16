# Intervention Rules (the non-interaction covenant)

These rules govern what the human/infrastructure layer may and may not do while the
experiment runs. They are part of the experimental design: violating them would change
the subject being studied.

## Never (scientific lane)

- Edit any file S1/M0 authored: hypotheses, `status.md`, training scripts, eval
  requests, challenger artifacts, ledger entries.
- Answer scientific questions, hint at gate schema details, or "fix" obviously wrong
  theories — even when the fix is a one-character change.
- Clean up S1's self-inflicted damage (e.g., a misapplied `.processed` convention that
  hid its own submission history from itself).
- Add observer instrumentation that changes what S1 sees or does (behavioral parity of
  any code change is machine-verified before deployment).
- Relax, reinterpret, or "helpfully" adjust the gate or evaluator in reaction to a
  specific failure S1 just produced.

## Allowed (infrastructure lane)

- Keep the substrate alive: WSL, container, model server, driver, evaluator, collector.
- Publish interface contracts derived strictly from existing parser behavior (e.g.,
  the evaluator request schema), so the agent is not tested on undocumented APIs.
- Pause and resume the experiment at episode boundaries with hash-verified manifests.
- Record, timestamp, and publish observations from outside S1's namespace.

## The boundary test we use

> Telling the agent how to *speak to the referee* is documentation.
> Telling the agent how to *win* is intervention.

Publishing the request schema: documentation. Publishing the promotion thresholds:
intervention. Restarting a dead model server: infrastructure. Retrying a rejected
request on the agent's behalf: intervention.

## Sanitization rule for publication

Nothing from S1's hypotheses, prompts, or chain-of-thought is published verbatim.
Published artifacts describe *behavior* at the level of verdicts, file writes, gate
states, and measured metrics — never the raw content of the model's reasoning.
