---
name: algolia-agent-safe-key
description: Mint the narrowest possible Algolia API key for an agent or an untrusted client, and restore one that was deleted by mistake. Use before giving any agent access to an Algolia application, or when a key has been leaked, over-scoped, or accidentally removed.
api: Algolia Search API
openapi: openapi/algolia-search-api-openapi.yml
operations:
  - addApiKey
  - getApiKey
  - listApiKeys
  - updateApiKey
  - deleteApiKey
  - restoreApiKey
  - waitForApiKey
  - generateSecuredApiKey
generated: '2026-08-27'
method: generated
source: Grounded in operationIds read from openapi/algolia-search-api-openapi.yml and the ACL model documented at https://www.algolia.com/doc/guides/security/api-keys/in-depth/api-key-restrictions
---

# Mint an agent-safe Algolia API key

Algolia has no OAuth on its REST surface and no scope strings. Authorization lives entirely in the **ACL and
restrictions attached to an API key**. That makes key minting the whole of access control — and it means the
Admin key must never reach an agent.

## Never hand out

- The **Admin API key**. It can delete every index in the application.
- The raw **Search-only key** to a browser, if the index holds anything you would not publish. It can be
  scraped in full.

## Mint a narrow key

`addApiKey` with only what the task needs:

- `acl` — the smallest set. `["search"]` for a read-only agent. Add `browse` only if it must walk a whole index.
  Write ACLs (`addObject`, `deleteObject`, `deleteIndex`, `editSettings`) belong to a deploy pipeline, not an agent.
- `indexes` — restrict to the exact index names. Wildcards suffix-match; prefer explicit names.
- `validity` — seconds until expiry. Set it. An agent key should be short-lived.
- `maxQueriesPerIPPerHour` — caps scraping and runaway loops.
- `maxHitsPerQuery` — caps exfiltration per call.
- `referers` / `sources` — pin to your origins or CIDRs where the caller is fixed.
- `description` — say which agent holds it. You will need this when auditing 5,000 keys.

Key creation is asynchronous like every other write: poll `waitForApiKey` before using the new key, or the
first request with it will 403.

## Per-end-user keys

For multi-tenant data, do not mint a key per user. Use `generateSecuredApiKey` to sign a search-only key with
embedded filters (for example `filters: 'tenant:acme'`). It is generated locally, needs no API call, and the
filter cannot be stripped by the client.

## Restore a deleted key

This is the one genuinely reversible destructive operation on the Algolia surface, and it has a real window:

- `restoreApiKey` brings back a deleted **or expired** key.
- **Algolia retains only the last 1,000 deleted keys per application.** Beyond that it is gone.
- A restored key comes back with its **validity reset to 0 (unlimited)** — the original expiry does *not*
  return. Immediately `updateApiKey` to reapply the intended `validity`, or you have just created a permanent key.

Deleting a user deletes their associated API keys, which is the most common way keys disappear unintentionally.

## Audit

`listApiKeys` then `getApiKey` per key. Look for keys with no `validity`, no `indexes` restriction, or write
ACLs held by anything that is not a deploy pipeline.

Limit: 5,000 API keys per application.

See `scopes/algolia-scopes.yml` for the full ACL and restriction vocabulary.
