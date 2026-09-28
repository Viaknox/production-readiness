# 12 · Product readiness

**Scope.** Whether the product itself is ready for a real user to arrive, understand it, use it, pay for it if applicable, and be told when something goes wrong.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 12.1 | Analytics on the activation funnel, with consent | T1 | Analytics dashboard or event schema showing signup → activation → retention steps instrumented, gated by the consent mechanism (11.2) | No funnel instrumented at all, or events fired before consent is captured |
| 12.2 | Onboarding and empty states designed | T1 | Screenshots or component code for first-run onboarding and each major empty state (no data yet, no results, error state) | New user lands on a blank screen with no guidance; empty states show a raw "[]" or broken layout |
| 12.3 | Transactional emails actually deliver | T1 | Test send log showing delivery (not just "sent") for signup/reset/receipt emails, from the real sending domain | Emails "sent" successfully in logs but land in spam or bounce because sender auth (SPF/DKIM/DMARC) isn't set up |
| 12.4 | Help docs / FAQ published | T1 | Live help center or FAQ page URL covering the top known questions | No docs exist beyond what's in the UI; every question becomes a support ticket |
| 12.5 | Pricing and billing live, if the product is paid | T1 | Working checkout flow and pricing page reflecting the actual plan structure, tested end to end | Pricing page shows numbers that don't match what checkout actually charges, or checkout is stubbed/untested |
| 12.6 | Feedback loop in place | T2 | In-product feedback widget, survey, or a monitored channel with a documented review cadence | No mechanism for users to report problems or ideas short of finding a support email |
| 12.7 | Kill switch for problematic features | T2 | Feature flag or config toggle that can disable a specific feature in production without a full redeploy, exercised at least once | Only way to disable a broken feature is to roll back the entire deploy or ship a hotfix |

**Right-sizing notes.**
- T1 covers what a first real user needs on day one — a working funnel, onboarding, deliverable email, docs, and (if paid) accurate billing (12.1–12.5). Skipping these is what makes a launch feel unfinished even when the backend is solid.
- Feedback loop and kill switches (12.6, 12.7) are T2: worth having before GA scale, not blocking for a small beta where the team is talking to every user directly.
- Don't confuse this domain with domain 13 — this is the product surface itself; domain 13 is the organizational muscle around it.
