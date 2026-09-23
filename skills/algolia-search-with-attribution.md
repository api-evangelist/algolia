---
name: algolia-search-with-attribution
description: Run an Algolia search and correctly attribute the resulting clicks, conversions and purchases back to it, so Analytics, Recommend, Personalization and A/B Testing all receive usable signal. Use when wiring search telemetry or debugging why analytics or recommendations look empty.
api: Algolia Search API, Algolia Insights API
openapi:
  - openapi/algolia-search-api-openapi.yml
  - openapi/algolia-insights-api-openapi.yml
operations:
  - searchSingleIndex
  - search
  - searchForFacetValues
  - browse
  - pushEvents
generated: '2026-08-27'
method: generated
source: Grounded in operationIds read from openapi/algolia-search-api-openapi.yml and openapi/algolia-insights-api-openapi.yml
---

# Search with click and conversion attribution

Algolia's Analytics, Recommend, Personalization and A/B Testing products are all downstream of one thing:
Insights events that carry the right join keys. Get the keys wrong and every one of those products goes quiet
while the search itself keeps working — which is why this is worth doing once, correctly.

## 1. Search, asking for the join key

Call `searchSingleIndex` (single index) or `search` (multi-index) with:

- `clickAnalytics: true` — this is what makes Algolia return a `queryID` on the response.
- `userToken` — your own pseudonymous identifier for the end user. Stable per user, never a raw email or
  account ID; see the PII note below.
- `attributesToRetrieve` limited to what you will actually render. Response size is the main cost of an
  agent-driven search.

Pagination: `page` + `hitsPerPage`, capped at 20,000 reachable hits. To walk a whole index use `browse`
with `cursor`, which has no such ceiling.

## 2. Send the events

Call `pushEvents` on the Insights API (`https://insights.algolia.io`, or the regional
`https://insights.{region}.algolia.io`) with the `queryID` and the **same** `userToken` from step 1.

Event types that matter:

- `clickedObjectIDsAfterSearch` — requires `queryID` and `positions`. Without `queryID` the click is not
  attributed to the search and click-through rate stays at zero.
- `convertedObjectIDsAfterSearch` — requires `queryID`.
- `viewedObjectIDs` — no `queryID`, used for impression signal.
- `purchasedObjectIDs` — carries revenue; feeds revenue analytics and A/B test scoring.

## 3. Read it back

- `getTopSearches` and `getTopHits` accept `clickAnalytics: true` and `revenueAnalytics: true`, which add
  CTR, conversion rate, add-to-cart rate, purchase rate and revenue. **Only these two operations accept them.**
- Data has a 1–4 hour processing delay. Query ranges ending at least 4 hours ago or the tail looks like a
  collapse in traffic.
- Analytics is limited to 100 API calls per minute per application, and unlike the Search API it returns
  `x-ratelimit-limit` / `-remaining` / `-reset` headers. Read them.

## Common failures

| Symptom | Cause |
|---|---|
| Analytics shows searches but zero clicks | `clickAnalytics: true` was never set, so there is no `queryID` to attribute against |
| Recommend models never train | Insights events are being sent without a consistent `userToken` |
| Personalization has no affinity profiles | Same — `userToken` differs between search and event |
| Numbers look wrong for today | Reading inside the 1–4 hour processing window |

## PII

`userToken` is sent to Algolia and retained. Use a pseudonymous, rotating identifier. Do not put an email
address, a raw account ID, or anything re-identifying in it.

See `conventions/algolia-conventions.yml` and `data-model/algolia-data-model.yml` for the identifier graph.
