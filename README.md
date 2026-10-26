# Algolia (algolia)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Algolia is a hosted search and discovery platform that delivers fast, typo-tolerant search, browse, recommendations, and personalization through a suite of REST APIs and edge-distributed infrastructure. It powers search experiences for ecommerce, media, SaaS, and content sites, pairing a synchronous indexing and query control plane with event-driven Insights, Recommend, A/B Testing, and Personalization products.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/algolia/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/algolia/refs/heads/main/apis.yml)

## Tags

- Search
- Discovery
- Recommendations
- Personalization
- Analytics
- Ecommerce

## Timestamps

- **Created:** 2026-05-04
- **Modified:** 2026-06-16

## APIs

### Algolia Search API

Core indexing and search API for adding, updating, and deleting records and querying them with typo-tolerant, faceted, geo-aware, and rule-driven search served from globally distributed search nodes (DSN).

- **Human URL:** [https://www.algolia.com/doc/rest-api/search/](https://www.algolia.com/doc/rest-api/search/)
- **Base URL:** `https://{appid}-dsn.algolia.net`

#### Tags

- Search
- Indexing
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/search/)
- [API Reference](https://www.algolia.com/doc/api-reference/)

### Algolia Insights API

Inbound event-ingestion API for click, conversion, view, and purchase signals that feed Personalization, Recommend, A/B Testing, and Analytics. Accepts events; does not emit them.

- **Human URL:** [https://www.algolia.com/doc/rest-api/insights/](https://www.algolia.com/doc/rest-api/insights/)
- **Base URL:** `https://insights.algolia.io`

#### Tags

- Analytics
- Events
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/insights/)

### Algolia Recommend API

Returns related-products, frequently-bought-together, trending, and look-alike recommendations trained from Insights events and catalog data.

- **Human URL:** [https://www.algolia.com/doc/rest-api/recommend/](https://www.algolia.com/doc/rest-api/recommend/)
- **Base URL:** `https://{appid}-dsn.algolia.net`

#### Tags

- Recommendations
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/recommend/)

### Algolia Analytics API

Reports top searches, no-result searches, click/conversion rates, and other search analytics aggregated from query and Insights data.

- **Human URL:** [https://www.algolia.com/doc/rest-api/analytics/](https://www.algolia.com/doc/rest-api/analytics/)
- **Base URL:** `https://analytics.algolia.com`

#### Tags

- Analytics
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/analytics/)

### Algolia A/B Testing API

Creates and manages A/B tests across index configurations and relevance settings, scoring variants on click-through and conversion.

- **Human URL:** [https://www.algolia.com/doc/rest-api/abtesting/](https://www.algolia.com/doc/rest-api/abtesting/)
- **Base URL:** `https://analytics.algolia.com`

#### Tags

- Experimentation
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/abtesting/)

### Algolia Personalization API

Configures and applies user-affinity profiles built from Insights events to re-rank search and browse results per user.

- **Human URL:** [https://www.algolia.com/doc/rest-api/personalization/](https://www.algolia.com/doc/rest-api/personalization/)
- **Base URL:** `https://{region}.algolia.com`

#### Tags

- Personalization
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/personalization/)

### Algolia Crawler API

Manages Algolia's hosted web crawler that extracts content from websites and pushes it into indices on a schedule.

- **Human URL:** [https://www.algolia.com/doc/tools/crawler/getting-started/overview/](https://www.algolia.com/doc/tools/crawler/getting-started/overview/)
- **Base URL:** `https://crawler.algolia.com`

#### Tags

- Crawler
- Ingestion
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/tools/crawler/getting-started/overview/)

### Algolia Ingestion API

Connector-based data ingestion that pulls records from sources (databases, storage, ecommerce platforms) into Algolia indices via managed tasks.

- **Human URL:** [https://www.algolia.com/doc/rest-api/ingestion/](https://www.algolia.com/doc/rest-api/ingestion/)
- **Base URL:** `https://data.{region}.algolia.com`

#### Tags

- Ingestion
- Connectors
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/ingestion/)

### Algolia Query Suggestions API

Generates and maintains query-suggestion indices from popular searches to power as-you-type autocomplete.

- **Human URL:** [https://www.algolia.com/doc/rest-api/query-suggestions/](https://www.algolia.com/doc/rest-api/query-suggestions/)
- **Base URL:** `https://query-suggestions.{region}.algolia.com`

#### Tags

- Search
- Autocomplete
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/query-suggestions/)

### Algolia Monitoring API

Exposes server status, latency, indexing, and reachability metrics for an application's Algolia infrastructure.

- **Human URL:** [https://www.algolia.com/doc/rest-api/monitoring/](https://www.algolia.com/doc/rest-api/monitoring/)
- **Base URL:** `https://status.algolia.com`

#### Tags

- Monitoring
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/monitoring/)

### Algolia Usage API

Returns per-application usage metrics (operations, records, search volume) for cost and quota tracking.

- **Human URL:** [https://www.algolia.com/doc/rest-api/usage/](https://www.algolia.com/doc/rest-api/usage/)
- **Base URL:** `https://usage.algolia.com`

#### Tags

- Usage
- FinOps
- REST

#### Properties

- [Documentation](https://www.algolia.com/doc/rest-api/usage/)

## Common Properties

- [Website](https://www.algolia.com)
- [Documentation](https://www.algolia.com/doc/)
- [API Reference](https://www.algolia.com/doc/api-reference/)
- [Sign Up](https://dashboard.algolia.com/users/sign_up)
- [Pricing](https://www.algolia.com/pricing/)
- [GitHub Organization](https://github.com/algolia)
- [Status](https://status.algolia.com)
- [Plans](plans/algolia-plans-pricing.yml)
- [Rate Limits](rate-limits/algolia-rate-limits.yml)
- [Fin Ops](finops/algolia-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
