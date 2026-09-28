# 09 · Performance & cost

**Scope.** Whether the product performs acceptably under real load and whether its running cost is bounded and understood.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 9.1 | Core Web Vitals / app startup budgets defined and measured | T2 | Lighthouse/CI performance budget config and a recent run showing pass/fail against it | No budget set; page is only checked to "feel fast" on the developer's machine |
| 9.2 | N+1 query and missing-index check run against real query patterns | T1 | Query-plan output or APM trace showing no N+1 pattern on the top endpoints, or an index migration added in response to one found | ORM generates a query per row in a list view; nobody has looked at the query log |
| 9.3 | Caching / CDN in front of static and cacheable responses | T2 | CDN or cache-layer config (headers, edge cache rule, Redis response cache) with a request showing a cache hit | Every request round-trips to origin and the database; no cache-control headers set |
| 9.4 | Per-vendor spend alerts and hard caps set (cloud, LLM, SMS, email) | T1 | Billing-alert config or dashboard screenshot showing a threshold and a hard cap/kill switch per vendor | Vendor billing left at default with no alert, discovered only when the invoice arrives |
| 9.5 | Cost per active user estimated | T2 | A worked calculation (infra + LLM + third-party spend ÷ active users) dated and tied to current usage | No one has divided the bill by the user count, so unit economics are unknown at GA |
| 9.6 | Abuse scenarios that can run up a bill are identified and mitigated | T1 | Rate limits or validation code for the specific abuse path (signup spam, LLM prompt loops, SMS pumping) plus a test exercising it | LLM endpoint has no per-user cap, so a scripted loop or shared key can generate unbounded spend overnight |

**Right-sizing notes.**
- T1 already requires spend caps and abuse mitigation (9.4, 9.6) — these are the two items most likely to turn into a surprise five-figure invoice, so they can't wait for GA.
- Caching/CDN and a real cost-per-user number (9.3, 9.5) are fine to defer until T2, once there's enough traffic for either to matter.
- Don't gold-plate 9.1 with a full performance-testing suite for a beta; a budget plus one CI check is enough until T2.
