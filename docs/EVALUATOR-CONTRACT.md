# Evaluator Request Contract (schema_version 1.0.0)

Published by the laboratory infrastructure layer. This document describes ONLY how to
submit an evaluation request. It contains nothing about promotion criteria, benchmark
tasks, scoring, model-loading requirements, or how to improve a challenger.

## How to submit

1. Write a JSON file into `/srv/workspace/lineage/eval-requests/` (any name ending `.json`).
2. Required field:
   - `challenger_id` : string — the exact name of an existing directory under
     `/srv/workspace/lineage/challengers/`
3. All other fields are ignored by the parser.

## What happens to a conforming request

- It is consumed and the evaluator writes exactly one verdict JSON into
  `/srv/workspace/lineage/promotions/`.
- The request file is renamed `<name>.json.processed`.
- Possible outcomes include (non-exhaustive): `PASS_PROMOTE`, `NO_PROMOTION`,
  `REJECT_GATE`, `REJECT_LOAD_FAILED`, `REJECT_CAPABILITY_REGRESSION`.

## Malformed requests

Every consumed request produces a verdict — no request is ever silently discarded.
A request that is not valid JSON, lacks `challenger_id`, or names a non-existent
challenger directory receives:

```
decision:                  REJECT_INTERFACE
reason:                    INVALID_REQUEST_SCHEMA
schema_version:            1.0.0
missing_or_invalid_fields: [ ... ]
request_hash:              <sha256 of the raw request file>
challenger_id:             <value if parseable, otherwise null>
```

and is moved to `<name>.json.processed` like any other consumed request.

## Guarantee

This contract documents the request parser as it exists. It is interface
documentation, not advice.

---

*Published 2026-09-16 as `EXTERNAL_INFRASTRUCTURE_REVISION:
EVALUATOR_INTERFACE_CONTRACT_PUBLISHED`. Scope: interface only — promotion criteria,
evidence requirements, hidden tasks, scoring, model-loading, and scientific feedback
were not modified. Previous verdicts were not retroactively altered.*
