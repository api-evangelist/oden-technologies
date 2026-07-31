---
name: Explore the Oden factory hierarchy
description: Discover an organization's factories, production lines, and metric groups on the Oden Platform.
api: openapi/oden-technologies-openapi-original.yml
operations: [search_factories, search_lines, search_metric_groups, search_products]
---

# Explore the Oden factory hierarchy

Use the Oden Private Partner API (v2) to walk an organization's manufacturing hierarchy: Organization -> Factory -> Line -> Machine, plus the products and metric groups defined on it.

## Auth & conventions
- Base URL: `https://api.oden.app/v2`. All calls are HTTPS, JSON in/out.
- Auth header: `Authorization: Token <api-key>` (the literal word `Token` prefixes the key).
- Every endpoint is a `POST` with a `search` body. Set `match` to `unique` (default), `all`, `first`, or `last`.

## Steps
1. `search_factories` — `POST /v2/factory/search` with `match: all` to list all factories for the org.
2. `search_lines` — `POST /v2/line/search`, filter by `factory` id to list the lines in a factory.
3. `search_metric_groups` — `POST /v2/metric_group/search` to discover the named metrics (tags) available on those lines.
4. `search_products` — `POST /v2/product/search` to list the products the manufacturer produces.

## Errors
Errors return `{ "error": <string>, "retryable": <bool> }`. A `409` on a `unique` search means multiple entities matched — re-run with `match: all`. See errors/oden-technologies-problem-types.yml.
