---
name: algolia-atomic-reindex
description: Replace the entire contents of an Algolia index with no downtime and a working rollback, using replaceAllObjects or an explicit temporary-index move. Use when reloading a full catalog, migrating a data source, or recovering from a bad bulk write.
api: Algolia Search API
openapi: openapi/algolia-search-api-openapi.yml
operations:
  - replaceAllObjects
  - saveObjects
  - operationIndex
  - getSettings
  - setSettings
  - getTask
  - waitForTask
  - indexExists
generated: '2026-08-27'
method: generated
source: Grounded in operationIds read from openapi/algolia-search-api-openapi.yml and the semantics documented at https://www.algolia.com/doc/guides/sending-and-managing-data/send-and-update-your-data/in-depth/index-operations-are-asynchronous
---

# Atomic reindex of an Algolia index

Replacing every record in an index is the highest-risk routine write on the Algolia surface, because
**`deleteIndex` and `deleteObjects` are not reversible through the API**. This flow never deletes first.

## Before you start

- Confirm the index exists: `indexExists`.
- Capture the current settings: `getSettings`. This is your rollback plan — Algolia does not store the
  previous settings for you, and `setSettings` fully overwrites.

## The managed path

Call `replaceAllObjects` with the full record set. Algolia populates a temporary index, then moves it over the
destination in one operation, so readers never see a partial index.

- Default `maxRetries` was raised from 100 to 800 in client 5.55.1 — long reindexes now survive by default.
- Empty objects emit a warning as of 5.57.0. Treat that warning as an error; an empty object is almost always
  a serialization bug upstream.

## The explicit path (when you want a rollback artifact)

1. `saveObjects` into `<indexName>_tmp`. Every record must carry an explicit `objectID` — see *Retry safety* below.
2. `getSettings` on the live index, `setSettings` onto `<indexName>_tmp` so relevance is identical.
3. `operationIndex` with `move` to promote `<indexName>_tmp` over `<indexName>`.
4. **Keep the displaced index.** It is the only thing that makes this reversible. Algolia does not retain it.

To roll back, `operationIndex` the retained index back over the destination.

## Wait for the task

Every one of these operations is asynchronous and returns a `taskID`. The 200 means *queued*, not *committed*.

- Poll `getTask`, or use `waitForTask`.
- Do not read back before the task completes. A search immediately after a write returns the old data and
  looks like a failed write.

## Retry safety

`batch` and `multipleBatch` carry an `addObject` action that mints a **new** `objectID` on every call. A retried
batch containing `addObject` duplicates records. Use `saveObjects` / `addOrUpdateObject` with explicit
`objectID`s so the write is idempotent under retry — Algolia publishes no `Idempotency-Key` header.

## Errors and limits

- Retry `5xx` against the fallback hosts `-1`, `-2`, `-3.algolianet.com`, randomized. This is required, not optional.
- `429` at 100 pending requests per application. Batch rather than firing per-record.
- Batch body cap 1 GB; record cap 10 KB (Free) to 100 KB by plan; `objectID` max 200 characters.
- Errors are flat `{"message": "...", "status": n}` — not RFC 9457. The `message` string is the only discriminator.

See `conventions/algolia-conventions.yml`, `errors/algolia-problem-types.yml`, `rate-limits/algolia-rate-limits.yml`.
