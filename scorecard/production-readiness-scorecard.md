# Production readiness scorecard — printable self-check

**Product:** ______________________  **Target tier:** T1 ☐ T2 ☐ T3 ☐  **Launch date:** __________
**Success metric (one number, target, by when):** ______________________________________________
**Pilot exit criteria (scale / kill):** ______________________________________________

Score every item **PASS · GAP · N/A · UNKNOWN**. A PASS needs evidence you can point at — a file, a config, a CI run, a dashboard, a dated doc. A README claim is not evidence. Only score items at or below your target tier; leave higher-tier items as N/A.

**Modules switched on:** M1 ☐ M2 ☐ M3 ☐ M4 ☐ M5 ☐ M6 ☐ M7 ☐ M8 ☐ M9 ☐ M10 ☐

---

## Core — every product

### 01 · Secrets & config

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 1.1 | No secrets in code or git history, checked with gitleaks/trufflehog over full history | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.2 | `.env` is git-ignored and a `.env.example` is present | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.3 | Production secrets live in the platform's secret store, not in code or CI YAML | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.4 | Separate keys for dev, staging, and prod | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.5 | Rotation plan exists and names who can rotate each secret | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.6 | Leaked-key response steps documented | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 02 · Identity & access

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 2.1 | Auth uses a proven provider or well-reviewed library, not hand-rolled crypto | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.2 | Server-side authorization on every data route (IDOR, missing tenant filters, permissive RLS) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.3 | Session/token lifetimes and revocation are defined | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.4 | Rate limits on login, signup, password reset, and OTP endpoints | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.5 | MFA available/required for admin accounts | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.6 | Service accounts and API keys follow least privilege | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.7 | Admin actions are logged | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 03 · Edge & app security

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 3.1 | HTTPS enforced with HSTS | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.2 | Security headers set (CSP, frame-ancestors, etc.) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.3 | CORS is tight, not wildcard | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.4 | Input validation at every boundary | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.5 | File upload limits and type checks | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.6 | SSRF guards on any URL-fetching feature | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.7 | WAF or bot protection in front of the app | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.8 | Dependency scanning and lockfiles in place | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.9 | SAST running in CI | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.10 | SBOM generated and license check run | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 04 · Data & backups

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 4.1 | Automated backups run on a schedule, and a restore has actually been tested | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.2 | Point-in-time recovery where the database supports it | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.3 | Migrations are backward-compatible (expand → migrate → contract) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.4 | Staging uses no raw production PII | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.5 | Retention and deletion path actually deletes across DB, storage, logs, and vendors | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.6 | Encryption at rest and in transit confirmed by default settings | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 05 · Reliability

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 5.1 | Timeouts set on every outbound call | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.2 | Retries use backoff + jitter, and only on idempotent operations | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.3 | Idempotency keys on payments, webhooks, and jobs | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.4 | Background work runs on a durable queue, not in-request or in-memory | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.5 | Graceful degradation when a dependency is down | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.6 | SLOs defined for availability and latency | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.7 | Load test at 3× expected peak | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.8 | Every external dependency listed with its failure impact, timeout and fallback | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.9 | Capacity headroom measured against known limits, and the scaling mechanism named | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.10 | Failure drill run at least once: primary database unavailable, cache down, disk or memory exhausted | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 06 · Observability

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 6.1 | Error tracking with release tagging (e.g., Sentry) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.2 | Structured logs with request/trace IDs and PII redaction | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.3 | Key metrics (rate, errors, duration) tracked per endpoint | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.4 | Uptime checks from outside the system | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.5 | Symptom-based alerts routed to a human who will actually see them | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.6 | Dashboards ready for launch day | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.7 | Alert thresholds written down with numbers, not adjectives | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.8 | Certificate and domain expiry monitored, with an alert at least 14 days ahead | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.9 | Traces follow a request across services, queues and third-party calls | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.10 | Logs shipped to a central store with a stated retention period | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 07 · CI/CD & release

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 7.1 | Required checks on main: lint, typecheck, tests, secret scan, dependency audit | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.2 | Preview or staging environment exists | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.3 | One-click rollback proven to work | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.4 | Feature flags for risky features | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.5 | Migrations run safely as part of deploy | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.6 | Release notes/changelog maintained | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.7 | Branch protection enabled on main | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 08 · Testing

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 8.1 | Tests on critical paths (auth, payments, data writes, permissions) over a coverage percentage | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.2 | Integration tests run against a real database | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.3 | E2E smoke tests on top user journeys, run post-deploy | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.4 | Contract tests or recorded fixtures for external APIs | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 09 · Performance & cost

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 9.1 | Core Web Vitals / app startup budgets defined and measured | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.2 | N+1 query and missing-index check run against real query patterns | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.3 | Caching / CDN in front of static and cacheable responses | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.4 | Per-vendor spend alerts and hard caps set (cloud, LLM, SMS, email) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.5 | Cost per active user estimated | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.6 | Abuse scenarios that can run up a bill are identified and mitigated | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 10 · Operations & support

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 10.1 | Owner/on-call named, even if it's one person | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.2 | Incident process defined: severity levels, communication path, postmortem | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.3 | Runbooks written for the top 5 failure modes | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.4 | Status page live | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.5 | Support channel and SLA defined | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.6 | Admin tooling exists for common support tasks | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.7 | Everyone on call has production access, the tooling and an escalation path that has been tested | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.8 | New responders shadow at least one incident or drill before going on call alone | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.9 | Architecture and data-flow diagram current and kept in the repo | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 11 · Legal & trust

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 11.1 | Terms of Service and Privacy Policy match actual data flows | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.2 | Cookie consent shown where required (EU/UK) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.3 | DPAs in place with vendors processing personal data | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.4 | Subprocessor list published and kept current | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.5 | Accessibility target set (WCAG 2.2 AA) and a basic audit done | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.6 | Open-source license compliance checked | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 11.7 | Trademark / name clearance done for the product name | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 12 · Product readiness

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 12.1 | Analytics on the activation funnel, with consent | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.2 | Onboarding and empty states designed | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.3 | Transactional emails actually deliver | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.4 | Help docs / FAQ published | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.5 | Pricing and billing live, if the product is paid | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.6 | Feedback loop in place | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 12.7 | Kill switch for problematic features | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### 13 · Adoption & operating model

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 13.1 | Success metric and pilot exit criteria written down before launch | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.2 | Documented release workflow with named approvers per risk tier and an agreed turnaround | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.3 | Launch communication drafted: what's changing, what isn't, known limits | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.4 | First-user/champion group identified with a way to hear from them | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.5 | In-product help, templates, or examples so users learn inside the tool | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.6 | Feedback loop (user feedback + usage metrics) with a review cadence | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 13.7 | Owner named for ongoing support as usage grows | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

---

## Modules — only the ones switched on

### M1 · Integrations you consume

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 1.1 | Production account/keys (not sandbox) and who owns the account | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.2 | Rate limits & quotas vs expected peak | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.3 | Pricing ceiling & alerts | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.4 | Auth type and token refresh | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.5 | Webhook signature verification, replay protection, idempotent handlers, retry/backoff and dead-letter | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.6 | API version pinned + deprecation watch (subscribed to changelog) | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.7 | Timeout + circuit breaker + user-visible fallback | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.8 | Vendor status page subscribed | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.9 | ToS allows your use (resale, AI training, scraping) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.10 | Exit plan — you own your data/prompts/config and can export them, contract has no multi-year lock without break clauses | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.11 | Data residency/DPA | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 1.12 | OAuth app verification/review requirements (e.g., Google sensitive/restricted scopes, Microsoft publisher verification, Slack/Zoom app review) — verify current rules live | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M2 · Public API you expose

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 2.1 | OpenAPI/spec published | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.2 | Versioning and deprecation policy | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.3 | API keys/OAuth with scopes, rotation, revocation | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.4 | Per-key rate limits and quotas | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.5 | Pagination, idempotency keys on POST | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.6 | Consistent error format | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.7 | Sandbox environment | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.8 | Webhooks you send are signed, retried, and replayable | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.9 | Developer docs + changelog | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 2.10 | Usage metering if billed | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M3 · Mobile & app stores

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 3.1 | (Apple) App Review Guidelines followed | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.2 | (Apple) Privacy nutrition labels match real data collection | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.3 | (Apple) Privacy manifest incl. third-party SDKs | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.4 | (Apple) In-app account deletion if accounts can be created | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.5 | (Apple) Sign in with Apple rule when offering third-party login | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.6 | (Apple) IAP rules for digital goods | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.7 | (Apple) TestFlight external testing | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.8 | (Apple) Export compliance | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.9 | (Google Play) Current target API level deadline met | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.10 | (Google Play) Data safety form accurate | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.11 | (Google Play) Closed-testing requirement for new personal developer accounts | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.12 | (Google Play) Play App Signing and upload-key custody | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.13 | (Google Play) Account deletion web link | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.14 | (Both) Crash reporting wired up | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.15 | (Both) Forced/soft update mechanism for breaking API changes | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.16 | (Both) Deep/universal links | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.17 | (Both) Push credentials owned by the company account | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.18 | (Both) Store listing assets, age rating, support URL, privacy URL | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 3.19 | (Both) Review-rejection buffer in the launch plan | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M4 · Web & email

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 4.1 | Custom domain, DNS owned by company account, registrar lock + auto-renew | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.2 | SEO basics (titles, sitemap, robots, OG tags) if discoverability matters | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.3 | 404/500 pages | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.4 | Email sender auth SPF, DKIM, DMARC and one-click unsubscribe for bulk mail (current Gmail/Yahoo sender rules checked) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.5 | Bounce/complaint handling | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 4.6 | Separate transactional vs marketing streams | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M5 · AI & LLM features

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 5.1 | Provider abstraction or gateway with fallback model | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.2 | Timeouts and retry on 429/5xx | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.3 | Structured output validated by schema (Zod/Pydantic) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.4 | Eval set of real cases run in CI before prompt/model changes | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.5 | Prompt-injection defenses where the model reads untrusted content or can call tools (least-privilege tools, human confirm for destructive actions) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.6 | Per-user and global cost caps | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.7 | PII handling and provider data-retention settings | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.8 | Model deprecation dates tracked | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.9 | AI disclosure to users where required | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.10 | Brand/quality guardrails on generated output (banned terms, tone checks, human review tiered by risk) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.11 | UI tells users the limits ("verify facts", sources shown for claims) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.12 | Prompt/model changes tested first in a sandbox on historical/sample data, then rolled out to a small share of traffic before everyone | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 5.13 | Scheduled (e.g., semiannual) model/vendor review | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M6 · Payments

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 6.1 | Hosted checkout to minimize PCI scope | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.2 | Webhook-driven state (never trust client redirect) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.3 | Idempotent fulfillment | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.4 | Refunds, disputes, dunning | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.5 | Tax collection per region | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.6 | Test clock/sandbox covered | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 6.7 | Revenue reconciliation | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M7 · Regulated data

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 7.1 | PHI → HIPAA: BAA with every vendor touching PHI, access logging, minimum necessary | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.2 | PCI beyond hosted checkout → SAQ scope | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.3 | Children → COPPA/age gating | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.4 | EU/UK users → GDPR lawful basis, DSAR process, transfers | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 7.5 | California → CCPA/CPRA | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M8 · B2B & enterprise

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 8.1 | Tenant isolation tested (cross-tenant access test) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.2 | SSO (SAML/OIDC) and SCIM at T3 | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.3 | Audit log export | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.4 | Roles/permissions model | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.5 | Data export | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.6 | Security questionnaire pack (architecture, subprocessors, pen test, policies) | T3 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 8.7 | Uptime SLA and credits | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M9 · Marketplaces you publish into

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 9.1 | Listing requirements met | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.2 | Review timelines planned for | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.3 | Permission justification documented | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 9.4 | Privacy disclosures accurate | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

### M10 · Dev tools & open source

| # | Check | Tier | Score | Evidence |
|---|---|---|---|---|
| 10.1 | License chosen deliberately (copyleft like AGPL can block company adoption; permissive like MIT/Apache spreads faster) and NOTICE/third-party licenses correct | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.2 | `SECURITY.md` with a private disclosure channel | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.3 | Semantic versioning, CHANGELOG, and a tested upgrade/migration path for any stored data or config format | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.4 | Supported-platform matrix actually tested in CI (OS × runtime versions × each client/IDE it claims to support) | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.5 | Install verified from a clean machine for every documented path | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.6 | Package names reserved on each registry (PyPI, npm, plugin marketplaces) | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.7 | Signed releases / build provenance | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.8 | Telemetry off or opt-in and documented | T1 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.9 | CONTRIBUTING, code of conduct, issue/PR templates | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |
| 10.10 | A "what this is not" section so users don't misuse it | T2 | ☐ PASS ☐ GAP ☐ N/A ☐ UNK | |

---

## Roll-up

| Domain | Items scored | PASS | GAP | UNKNOWN | % PASS | Blocker? |
|---|---|---|---|---|---|---|
| 01 Secrets & config | | | | | | ☐ |
| 02 Identity & access | | | | | | ☐ |
| 03 Edge & app security | | | | | | ☐ |
| 04 Data & backups | | | | | | ☐ |
| 05 Reliability | | | | | | ☐ |
| 06 Observability | | | | | | ☐ |
| 07 CI/CD & release | | | | | | ☐ |
| 08 Testing | | | | | | ☐ |
| 09 Performance & cost | | | | | | ☐ |
| 10 Operations & support | | | | | | ☐ |
| 11 Legal & trust | | | | | | ☐ |
| 12 Product readiness | | | | | | ☐ |
| 13 Adoption & operating model | | | | | | ☐ |
| Modules on | | | | | | ☐ |

% PASS is a progress number, not the verdict. One blocker at your target tier is a NO-GO however high the percentage.

## Verdict

**GO ☐  GO-WITH-CONDITIONS ☐  NO-GO ☐**   Blockers: ____  High: ____  Unknown: ____

**Top five risks in plain English**
1. 
2. 
3. 
4. 
5. 

**Next action (one):** ______________________________________________

## Sign-off

| Role | Name | Date | Signature |
|---|---|---|---|
| Engineering owner | | | |
| Operations / on-call owner | | | |
| Product or business owner | | | |

Sign-off means: the evidence above was inspected, every blocker at the target tier is closed or has a dated exception, and the named owner (13.7) accepts the product after launch.

*Production Readiness Kit by Viaknox · viaknox.com · CC BY 4.0. Full item guidance in `skills/production-readiness/checks/`.*
