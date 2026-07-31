---
name: Record production intervals and scrap/yield
description: Create runs, batches, and states on an Oden line and log scrap/yield output.
api: openapi/oden-technologies-openapi-original.yml
operations: [set_interval, bulk_set_intervals, search_intervals, set_scrap_yield, search_scrap_yield]
---

# Record production intervals and scrap/yield

Log what happens on a production line: production intervals (runs, batches, states) and the scrap/yield output produced during them.

## Auth & conventions
- Base URL `https://api.oden.app/v2`; header `Authorization: Token <api-key>`.
- `set` operations are create-or-update (upsert) keyed on the entity's natural identifiers. There is no formal Idempotency-Key. See conventions/oden-technologies-conventions.yml.
- Timestamps are ISO 8601 UTC (`YYYY-MM-DDTHH:MM:SSZ`).

## Steps
1. `set_interval` — `POST /v2/interval/set` to create or update a single interval (run/batch/state) on a `line`.
2. `bulk_set_intervals` — `POST /v2/intervals/set` to create many intervals at once.
3. `search_intervals` — `POST /v2/interval/search` to read back intervals on a line over a time range.
4. `set_scrap_yield` — `POST /v2/scrap_yield/set` to record good/bad output for a run or batch, per the factory's Scrap/Yield schema.
5. `search_scrap_yield` — `POST /v2/scrap_yield/search` to verify recorded output.

## Errors
`400` for malformed bodies, `404` if the referenced line/interval does not exist, `409` on conflicting writes. Envelope: `{ error, retryable }`.
