---
name: "production-readiness"
description: "Assess and harden an MVP or vibe-coded product for production launch — security, reliability, ops, integrations, APIs, app stores, AI, payments, compliance, dev-tool/OSS distribution, and adoption — with an evidence-based go/no-go and gap backlog."
license: MIT
---

# Production Readiness (MVP → Production)

Goal: tell the owner, with evidence, whether a product is ready for real users, what blocks launch, and the smallest set of work to close the gaps. Right-sized to the product — never a generic 200-item wishlist.

## Hard rules
1. **Evidence or it's Unknown.** Every item is PASS / GAP / N/A / UNKNOWN, and PASS needs proof (file path, config, CI run, dashboard, doc link). Never mark PASS from a README claim.
2. **Right-size by tier.** Don't demand multi-region DR for a 50-user beta. Tag each gap with the tier it's required at.
3. **Verify platform rules live.** App store, OAuth, payment, and email-sender rules change yearly. Before citing a store/vendor requirement, check the vendor's official docs (web search) and cite the link + date checked.
4. **Reuse, don't duplicate.** If `pm-ai-shipping:ship-check`, `security-audit-static`, `performance-audit-static`, or `derive-tests` are available, run them for code-level evidence and fold results in. This skill owns everything around the code.
5. **Plain output.** Owner reads a one-page scorecard; details go in the appendix and the backlog.
6. **Governance inside the workflow, not at the end.** Prefer checks that run where work happens (CI, PR templates, pre-commit, in-product guardrails) over review meetings bolted on before launch. A gate that only runs at the end becomes the bottleneck.
7. **Shipped ≠ adopted.** Most products stall after launch because people and process didn't change, not because the code failed. Readiness includes the adoption plan (domain 13), not just the system.

## Readiness tiers
| Tier | Meaning | Typical bar |
|---|---|---|
| T1 Public beta | Real users, low scale, can tolerate some downtime | No secret leaks, auth solid, backups restore, errors tracked, legal pages, rollback works |
| T2 GA | Paying users, SLA expectations | + SLOs/alerts/on-call, load tested, runbooks, support path, integration fallbacks |
| T3 Enterprise / regulated | B2B contracts, PHI/PCI/children, audits | + SSO/SCIM, audit logs, DPAs/BAAs, pen test, SOC 2 / HIPAA controls, DR drills |

## Workflow

### Step 0 — Profile the product (ask once, batch the questions)
Capture: target tier and launch date; **the one success metric and its target** (what makes this launch a win, measured how, by when); named owner and sign-off stakeholders (product, engineering, security, legal/privacy, support, marketing — flag legal/privacy on day one if personal data, AI output, or regulated users are involved); surfaces (web, iOS, Android, desktop, public API, CLI, browser extension, developer tool/plugin/library distributed to other devs); hosting/stack; data types (PII, PHI, payment, minors' data); users (B2C/B2B), regions (US/EU/other); AI/LLM features; payments; **every external integration** (APIs consumed, webhooks received, marketplaces/app stores published to, SSO/IdPs). Scan the repo first (package manifests, env templates, SDK imports) to pre-fill the integration list, then ask the owner only to confirm/fill gaps.

The profile selects which modules apply. Record it at the top of the report.

### Step 1 — Gather evidence
Repo (code, CI config, IaC, env templates, migrations), hosting dashboards/connectors if available (Vercel, Railway, Supabase, Render, etc.), issue tracker, existing docs. Run available audit skills. Note what could not be inspected → UNKNOWN.

### Step 2 — Assess core domains (always) + applicable modules
Score each item. Severity: **BLOCKER** (can't launch at target tier) / **HIGH** (fix within first 2 weeks) / **LATER**.

### Step 3 — Deliver
1. **Scorecard (1 page):** Go / Go-with-conditions / No-go; count of blockers; per-domain RAG table; top 5 risks in plain English.
2. **Gap backlog:** one ticket per gap — title, why it matters, acceptance criterion, evidence needed to close, tier, severity, rough size (S/M/L). If Linear/Jira/GitHub Issues is connected, offer to create them as a project/milestone; else a table.
3. **Hardening kit (on request):** generate repo-specific CI quality gate, agent rules file (CLAUDE.md/.cursorrules), `.env.example`, runbook stubs — built from what the repo actually uses, not a template dump.
4. **Re-run mode:** on later runs, diff against the last report and show only what moved.

## Core domains (always assessed)

**1. Secrets & config** — no secrets in code or git history (gitleaks/trufflehog over full history); `.env` ignored, `.env.example` present; prod secrets in platform secret store; separate dev/staging/prod keys; rotation plan and who can rotate; leaked-key response steps.

**2. Identity & access** — proven auth provider or well-reviewed library (no hand-rolled crypto); server-side authorization on every data route (check for IDOR / missing tenant filters / permissive RLS); session/token lifetimes and revocation; rate limits on login, signup, reset, OTP; MFA for admins; least-privilege service accounts; admin actions logged.

**3. Edge & app security** — HTTPS + HSTS; security headers (CSP, frame-ancestors, etc.); tight CORS; input validation at boundaries; file upload limits/type checks; SSRF guards on URL fetchers; WAF/bot protection at T2+; dependency scanning + lockfiles; SAST in CI; SBOM and license check at T3.

**4. Data** — automated backups **and a tested restore** (record the actual restore time); point-in-time recovery where the DB supports it; backward-compatible migrations (expand → migrate → contract); staging uses no raw prod PII; retention + deletion path (user account deletion actually deletes across DB, storage, logs, vendors); encryption at rest/in transit defaults confirmed.

**5. Reliability** — timeouts on every outbound call; retries with backoff + jitter only on idempotent ops; idempotency keys for payments/webhooks/jobs; background work on a durable queue; graceful degradation when a dependency is down; SLOs defined (availability, latency) at T2+; capacity/load test at expected peak ×3 at T2+.

**6. Observability** — error tracking with release tagging (e.g., Sentry); structured logs with request/trace IDs and **PII redaction**; key metrics (rate, errors, duration) per endpoint; uptime checks from outside; symptom-based alerts routed to a human who will actually see them; dashboards for launch day.

**7. CI/CD & release** — required checks on main (lint, typecheck, tests, secret scan, dependency audit); preview/staging env; one-click rollback proven once; feature flags for risky features; migrations run safely in deploy; release notes/changelog; branch protection.

**8. Testing** — tests on critical paths (auth, payments, data writes, permissions) over a coverage %; integration tests against real DB; E2E smoke on top user journeys run post-deploy; contract tests or recorded fixtures for external APIs.

**9. Performance & cost** — Core Web Vitals / app startup budgets; N+1 and missing-index check; caching/CDN; per-vendor spend alerts and hard caps (cloud, LLM, SMS, email); cost per active user estimate; abuse scenarios that can run up a bill (signup spam, LLM prompt loops, SMS pumping).

**10. Operations & support** — owner/on-call named even if one person; incident process (severity, comms, postmortem); runbooks for top 5 failure modes; status page at T2+; support channel and SLA; admin tooling for common support tasks (so fixes don't need raw SQL).

**11. Legal & trust** — Terms, Privacy Policy matching actual data flows; cookie consent where required (EU/UK); DPAs with vendors processing personal data; subprocessor list at T3; accessibility target (WCAG 2.2 AA) and a basic audit; open-source license compliance; trademark/name clearance for the product name.

**12. Product readiness** — analytics on activation funnel (with consent); onboarding and empty states; transactional emails deliver (see Web module); help docs/FAQ; pricing/billing live if paid; feedback loop; kill switch for problematic features.

**13. Adoption & operating model** — success metric and pilot exit criteria written down before launch (what moves it from pilot to "scale" or "kill"); documented release workflow with named approvers per risk tier (low-risk changes = one reviewer, high-risk = more) and an agreed turnaround so sign-off doesn't stall; launch communication (what's changing, what isn't, known limits); first-user/champion group and a way to hear from them; in-product help, templates, or examples so users learn inside the tool; feedback loop (user feedback + usage metrics) with a review cadence (e.g., 30/60/90 days, then quarterly); owner for ongoing support as usage grows.

## Conditional modules

**M1. Integrations you consume (one sheet per vendor)** — production account/keys (not sandbox) and who owns the account; rate limits & quotas vs expected peak; pricing ceiling & alerts; auth type and token refresh; webhook signature verification, replay protection, idempotent handlers, retry/backoff and dead-letter; API version pinned + deprecation watch (subscribe to changelog); timeout + circuit breaker + user-visible fallback; vendor status page subscribed; ToS allows your use (resale, AI training, scraping); exit plan — you own your data/prompts/config and can export them, contract has no multi-year lock without break clauses; data residency/DPA; OAuth app verification/review requirements (e.g., Google sensitive/restricted scopes, Microsoft publisher verification, Slack/Zoom app review) — verify current rules live.

**M2. Public API you expose** — OpenAPI/spec published; versioning and deprecation policy; API keys/OAuth with scopes, rotation, revocation; per-key rate limits and quotas; pagination, idempotency keys on POST; consistent error format; sandbox environment; webhooks you send are signed, retried, and replayable; developer docs + changelog; usage metering if billed.

**M3. Mobile & app stores** — Verify each against current official docs before citing:
- *Apple:* App Review Guidelines; privacy nutrition labels match real collection; privacy manifest incl. third-party SDKs; in-app account deletion if accounts can be created; Sign in with Apple rule when offering third-party login; IAP rules for digital goods; TestFlight external testing; export compliance.
- *Google Play:* current target API level deadline; Data safety form; closed-testing requirement for new personal developer accounts; Play App Signing and upload-key custody; account deletion web link.
- *Both:* crash reporting; forced/soft update mechanism for breaking API changes; deep/universal links; push credentials owned by the company account; store listing assets, age rating, support URL, privacy URL; review-rejection buffer in the launch plan (plan days, not hours).

**M4. Web & email** — custom domain, DNS owned by company account, registrar lock + auto-renew; SEO basics (titles, sitemap, robots, OG tags) if discoverability matters; 404/500 pages; email sender auth SPF, DKIM, DMARC and one-click unsubscribe for bulk mail (check current Gmail/Yahoo sender rules); bounce/complaint handling; separate transactional vs marketing streams.

**M5. AI / LLM features** — provider abstraction or gateway with fallback model; timeouts and retry on 429/5xx; structured output validated by schema (Zod/Pydantic); eval set of real cases run in CI before prompt/model changes; prompt-injection defenses where the model reads untrusted content or can call tools (least-privilege tools, human confirm for destructive actions); per-user and global cost caps; PII handling and provider data-retention settings; model deprecation dates tracked; AI disclosure to users where required; brand/quality guardrails on generated output (banned terms, tone checks, human review tiered by risk); UI tells users the limits ("verify facts", sources shown for claims); prompt/model changes tested first in a sandbox on historical or sample data, then rolled out to a small share of traffic before everyone; scheduled (e.g., semiannual) model/vendor review.

**M6. Payments** — hosted checkout to minimize PCI scope; webhook-driven state (never trust client redirect); idempotent fulfillment; refunds, disputes, dunning; tax collection per region; test clock/sandbox covered; revenue reconciliation.

**M7. Regulated data** — PHI → HIPAA: BAA with every vendor touching PHI, access logging, minimum necessary. PCI beyond hosted checkout → SAQ scope. Children → COPPA/age gating. EU/UK users → GDPR lawful basis, DSAR process, transfers. California → CCPA/CPRA. Flag for legal review; do not give legal conclusions.

**M8. B2B / enterprise** — tenant isolation tested (cross-tenant access test); SSO (SAML/OIDC) and SCIM at T3; audit log export; roles/permissions model; data export; security questionnaire pack (architecture, subprocessors, pen test, policies); uptime SLA and credits.

**M9. Marketplaces you publish into** — Chrome Web Store, Slack/Teams/Zoom app directories, Shopify, MCP/plugin registries, etc.: listing requirements, review timelines, permission justification, privacy disclosures — verify live.

**M10. Developer tools, libraries, plugins & open source** — license chosen deliberately (copyleft like AGPL can block company adoption; permissive like MIT/Apache spreads faster) and NOTICE/third-party licenses correct; `SECURITY.md` with a private disclosure channel; semantic versioning, CHANGELOG, and a tested upgrade/migration path for any stored data or config format; supported-platform matrix actually tested in CI (OS × runtime versions × each client/IDE it claims to support); install verified from a clean machine for every documented path; package names reserved on each registry (PyPI, npm, plugin marketplaces); signed releases / build provenance; telemetry off or opt-in and documented; CONTRIBUTING, code of conduct, issue/PR templates; a "what this is not" section so users don't misuse it.

## Scorecard template
```
PRODUCT: <name>   TARGET: T1/T2/T3   LAUNCH: <date>   VERDICT: GO | GO-WITH-CONDITIONS | NO-GO
Blockers: N   High: N   Unknown: N
Success metric: <metric + target + date>   Pilot exit criteria: <scale / kill conditions>

| Domain | Status | Blockers | Note |
|---|---|---|---|
| Secrets & config | 🟢/🟡/🔴/⚪ | 0 | ... |
...
Top risks (plain English):
1. ...
Next action: <single most valuable step>
```

## Gap ticket template
```
Title: [Domain] <imperative fix>
Why: <user/business impact in one line>
Done when: <testable acceptance criterion>
Evidence to close: <link/screenshot/CI run expected>
Tier: T1|T2|T3   Severity: BLOCKER|HIGH|LATER   Size: S|M|L
```

## Anti-patterns to flag
- Coverage % as the quality gate while auth/payment paths are untested.
- Custom webhook bridges for things a native integration already does (e.g., issue-tracker ↔ Git status sync).
- Copy-pasted CI templates referencing actions that don't exist — verify every third-party action/repo resolves.
- Enterprise controls on a beta (over-engineering) or beta controls on a paid GA (under-engineering).
- Single personal account owning domain, app store, cloud, or payment accounts — bus-factor risk.
- A pilot with no success metric or exit criteria — it never graduates and never dies ("pilot purgatory").
- Launching the tool without changing the workflow around it — users drift back to the old way.
## Kit layout (Production Readiness Kit by Viaknox)
- `checks/` — one file per domain and module: each row gives the check, the tier it is required at, the evidence that satisfies it and the common gap in AI-built products. Use these as the item list in Step 2.
- `templates/profile.md`, `templates/scorecard.md`, `templates/gap-ticket.md` — the outputs for Step 0 and Step 3. Write results to `readiness/` in the target repo.
- Source: https://github.com/viaknox/production-readiness · Article: https://viaknox.com/blog/fast-to-build-slow-to-ship
