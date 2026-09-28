# 10 · Operations & support

**Scope.** Who is on the hook when something breaks or a user needs help, and whether that person has the process and tools to respond.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 10.1 | Owner/on-call named, even if it's one person | T1 | Named individual in the doc/roster, with a paging or notification path (phone, PagerDuty, Slack alert) that reaches them | No one is named; alerts (if any) go to a channel nobody watches after hours |
| 10.2 | Incident process defined: severity levels, communication path, postmortem | T2 | Incident-response doc naming severity tiers, who gets notified, and a postmortem template with at least one filled example | Team improvises during the first real incident with no shared definition of "how bad is this" |
| 10.3 | Runbooks written for the top 5 failure modes | T2 | Runbook docs for the 5 most likely failures (e.g., DB down, queue backed up, third-party outage, deploy failure, data-corruption), each with concrete steps | Tribal knowledge in one engineer's head; nothing written down for anyone else to follow |
| 10.4 | Status page live | T2 | Public or customer-facing status page URL, connected to real health checks | No status page; users find out about an outage from a support ticket instead of a page |
| 10.5 | Support channel and SLA defined | T2 | Support channel (email, chat, ticket system) documented with a stated response-time SLA | "Just message me on Slack" is the entire support plan, with no committed response time |
| 10.6 | Admin tooling exists for common support tasks | T2 | Admin UI or internal tool covering the top support actions (reset a user, reissue an invite, replay a failed job) without raw SQL | Every support request requires an engineer to run a manual database query in production |

**Right-sizing notes.**
- T1 only requires a named owner (10.1) — a solo founder writing their own name down is enough evidence at this tier.
- The rest of this domain (10.2–10.6) is what separates a beta from a GA product with paying users and an SLA to honor; don't demand a status page or formal incident process before there's traffic worth watching.
- Admin tooling (10.6) is the item most often skipped by AI-built products because it's not user-facing — but it's what keeps support from turning into ad hoc production database surgery.
