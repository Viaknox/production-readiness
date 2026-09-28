# 05 · Reliability

**Scope.** How the system handles slow or failing dependencies, retries, background work, and expected load.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 5.1 | Timeouts set on every outbound call | T1 | Client/HTTP config showing an explicit timeout per external call | Generated code uses default client timeouts (or none), so one slow vendor call hangs a whole request |
| 5.2 | Retries use backoff + jitter, and only on idempotent operations | T1 | Retry wrapper/config showing backoff+jitter and the idempotency check before retrying | A non-idempotent write (e.g., "create order") retried blindly on timeout, creating duplicates |
| 5.3 | Idempotency keys on payments, webhooks, and jobs | T1 | Code/schema showing an idempotency key column or header checked before processing | Webhook handler re-processes the same event on every retry from the vendor, double-charging or double-sending |
| 5.4 | Background work runs on a durable queue, not in-request or in-memory | T1 | Queue/worker config (e.g., a managed queue or job table) showing background work is durable across restarts | Long-running work kicked off with `setTimeout`/fire-and-forget in the request handler, lost on redeploy |
| 5.5 | Graceful degradation when a dependency is down | T1 | Code path showing a fallback/cached response or clear user-facing error when a dependency fails | One vendor outage takes down the whole app because no fallback path exists |
| 5.6 | SLOs defined for availability and latency | T2 | Doc or dashboard defining the SLO targets and how they're measured | No stated target, so "is it reliable enough" has no answer until users complain |
| 5.7 | Capacity/load test at expected peak times three | T2 | Load-test report (tool, date, peak RPS tested, results) at 3x expected peak | Never load tested; first real traffic spike is the first time capacity is checked |

**Right-sizing notes.**
- T1 covers the request-path fundamentals (timeouts, safe retries, idempotency, durable background work, graceful degradation) — these prevent cascading failures even at low scale.
- SLOs and load testing (5.6, 5.7) are T2 concerns tied to SLA expectations; don't require a formal load-test report for a 50-user beta.
- Multi-region failover and active-active reliability aren't in this checklist at all — that's beyond T3 scope for most products and should be called out separately if a specific SLA demands it.
