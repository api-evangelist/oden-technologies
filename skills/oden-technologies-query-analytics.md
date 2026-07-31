---
name: Query factory analytics with OQL and dashboards
description: Run Oden Query Language (OQL) queries and execute dashboards to analyze factory data.
api: openapi/oden-technologies-openapi-original.yml
operations: [run_oql_query, execute_dashboard, search_quality_tests, search_targets]
---

# Query factory analytics with OQL and dashboards

Analyze manufacturing performance with the Oden Query Language (a SQL-like language over factory data) and by executing dashboards.

## Auth & conventions
- Base URL `https://api.oden.app/v2`; header `Authorization: Token <api-key>`.
- Stay under ~1 request/second (rate limiting is planned). See lifecycle/oden-technologies-lifecycle.yml.

## Steps
1. `run_oql_query` — `POST /v2/oql/query` with an `OQLQuery` body to ask plain, SQL-like questions of factory data. See https://docs.oden.io/oql/ for syntax.
2. `execute_dashboard` — `POST /v2/dashboard/execute` with a range and filters to compute a saved dashboard's results.
3. `search_targets` — `POST /v2/target/search` to read metric targets/thresholds for products on lines.
4. `search_quality_tests` — `POST /v2/quality_test/search` to pull quality-assurance results attached to runs/batches.

## Errors
Errors return `{ error, retryable }`; retry only when `retryable` is true. See errors/oden-technologies-problem-types.yml.
