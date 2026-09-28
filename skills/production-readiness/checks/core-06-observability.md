# 06 · Observability

**Scope.** How errors, logs, metrics, and uptime are tracked so problems are caught before or when users hit them.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 6.1 | Error tracking with release tagging (e.g., Sentry) | T1 | Error-tracking dashboard/config showing errors tagged by release/version | No error tracker installed; errors only visible if a user reports them |
| 6.2 | Structured logs with request/trace IDs and PII redaction | T1 | Log config/sample output showing structured fields, a trace ID, and redaction of PII fields | Console.log-style output with raw user data (emails, names) printed straight into logs |
| 6.3 | Key metrics (rate, errors, duration) tracked per endpoint | T1 | Metrics dashboard or config showing RED metrics per endpoint | No per-endpoint metrics; only whatever the hosting platform shows by default |
| 6.4 | Uptime checks from outside the system | T1 | Uptime-monitor config/dashboard (e.g., a synthetic check hitting the public URL) | Nothing external polling the app, so an outage is discovered only when a user complains |
| 6.5 | Symptom-based alerts routed to a human who will actually see them | T1 | Alert-routing config showing the channel/person and the symptom-based trigger condition | Alerts configured to email an inbox nobody checks, or no alerts at all |
| 6.6 | Dashboards ready for launch day | T1 | Dashboard link showing the launch-day view (errors, traffic, latency) is built and accessible | Dashboards assembled ad hoc during the incident, not before it |

**Right-sizing notes.**
- All six observability items land at T1 — you cannot safely run even a small beta without knowing when it breaks, so this domain doesn't get lighter at lower tiers.
- What grows with tier is depth and process: T2 adds on-call rotation and runbooks (domain 10), and T3 adds audit-log retention and compliance-grade log handling (domain 11/M7).
- Avoid the anti-pattern of a beautiful dashboard nobody watches — the alert-routing check (6.5) matters more than the dashboard itself.
