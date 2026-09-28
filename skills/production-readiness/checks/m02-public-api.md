# M2 · Public API you expose

**Scope.** The API surface the product exposes to external developers or partner systems — its spec, auth, limits, and developer experience.

**Switched on when.** The product exposes a public API for external developers or partner systems to consume.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 2.1 | OpenAPI/spec published | T2 | Published OpenAPI/spec file or docs site URL | API exists only as ad hoc endpoints with no machine-readable spec |
| 2.2 | Versioning and deprecation policy | T2 | Written versioning scheme (e.g., URL/header version) and a stated deprecation timeline | Breaking changes ship on the same endpoint with no version bump or notice |
| 2.3 | API keys/OAuth with scopes, rotation, revocation | T1 | Auth config showing scoped keys/tokens with a rotation and revocation path | One all-access API key shared across every integration, never rotated |
| 2.4 | Per-key rate limits and quotas | T1 | Gateway/middleware config showing per-key limits enforced | No rate limiting, so one caller can degrade service for everyone |
| 2.5 | Pagination, idempotency keys on POST | T1 | API code/docs showing pagination on list endpoints and idempotency-key support on writes | A retried POST silently creates duplicate records |
| 2.6 | Consistent error format | T2 | API docs/tests showing one error schema used across all endpoints | Every endpoint returns errors in a different shape, breaking client error handling |
| 2.7 | Sandbox environment | T2 | Separate sandbox base URL/credentials documented and reachable | Developers must test against production, risking real data/side effects |
| 2.8 | Webhooks you send are signed, retried, and replayable | T1 | Webhook-sending code showing a signature, retry policy, and replay endpoint/log | Outbound webhooks fire once, unsigned, with no way to replay a missed event |
| 2.9 | Developer docs + changelog | T2 | Published docs site and a changelog with dated entries | Docs exist but haven't been updated since the API's first version |
| 2.10 | Usage metering if billed | T1 | Metering/billing dashboard showing usage tracked per key/customer | API is billed by usage but nothing actually meters calls |

**Right-sizing notes.**
- Items 2.3–2.5 and 2.8/2.10 are T1 because a leaked key, duplicate write, or unmetered billing directly costs users or money; spec, versioning, and docs polish (2.1, 2.2, 2.6, 2.7, 2.9) can mature at T2 once there's a real external developer base.
- A single-partner integration API can often skip the sandbox and public docs requirements — treat those as N/A rather than GAP when there's no external developer audience yet.
