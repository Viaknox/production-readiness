# M1 · Integrations you consume

**Scope.** Every third-party API, SDK, or platform the product depends on to function — production accounts, quotas, auth, webhooks, and exit terms.

**Switched on when.** The product consumes any third-party API, webhook, SSO provider or marketplace.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 1.1 | Production account/keys (not sandbox) and who owns the account | T1 | Vendor dashboard showing a live/production key in use, plus the named account owner | App is still running on the founder's personal sandbox key with no production account created |
| 1.2 | Rate limits & quotas vs expected peak | T1 | Vendor plan/quota page compared against expected peak request volume, dated | Nobody has checked the vendor's rate limit against launch-day traffic |
| 1.3 | Pricing ceiling & alerts | T1 | Vendor billing dashboard showing a spend cap or alert threshold configured | Usage-based vendor with no spend alert, so a traffic spike becomes a surprise invoice |
| 1.4 | Auth type and token refresh | T1 | Code/config showing token refresh handling and the auth type used (API key, OAuth, mTLS) | Long-lived token hardcoded with no refresh path, so it silently expires in production |
| 1.5 | Webhook signature verification, replay protection, idempotent handlers, retry/backoff and dead-letter | T1 | Webhook handler code showing signature check, replay/idempotency guard, and a dead-letter path | Webhook endpoint trusts payloads unsigned, or replays double-process the same event |
| 1.6 | API version pinned + deprecation watch (subscribed to changelog) | T2 | Config/lockfile showing a pinned API version and a changelog subscription (email/RSS/Slack) | Integration calls an unversioned or "latest" endpoint that can break without warning |
| 1.7 | Timeout + circuit breaker + user-visible fallback | T1 | Code showing a request timeout, breaker/backoff logic, and what the user sees when the vendor is down | A slow vendor call hangs the whole request with no timeout, taking the app down with it |
| 1.8 | Vendor status page subscribed | T2 | Screenshot/config showing subscription to the vendor's status page or incident feed | Nobody finds out the vendor is down until users start complaining |
| 1.9 | ToS allows your use (resale, AI training, scraping) | T1 | Vendor ToS section quoted/linked confirming the specific use case is allowed | Vendor data reused in a way its ToS actually forbids (e.g., training a model on it) |
| 1.10 | Exit plan — you own your data/prompts/config and can export them, contract has no multi-year lock without break clauses | T2 | Export mechanism tested + contract clause confirming no unbreakable multi-year lock | No documented way to get data out if the vendor relationship ends |
| 1.11 | Data residency/DPA | T3 | Signed DPA and a stated data residency region from the vendor | Personal data sent to a vendor with no DPA in place |
| 1.12 | OAuth app verification/review requirements (e.g., Google sensitive/restricted scopes, Microsoft publisher verification, Slack/Zoom app review) — verify current rules live | T1 | Vendor doc URL + date checked, plus the app's current verification/review status | App ships using unverified OAuth scopes that get throttled or blocked at scale |

**Use.** Copy this table once per vendor and name the vendor in the file name (m01-<vendor>.md).

**Right-sizing notes.**
- Score one vendor sheet at a time — a product with five integrations needs five short sheets, not one sprawling table.
- Items 1.1–1.5 and 1.7/1.9/1.12 are T1 because a vendor outage, unsigned webhook, or ToS violation can hurt users or the business immediately; the rest wait until the product has more operational maturity or contractual exposure.
- Don't chase every vendor to the same depth — spend the most scrutiny on vendors that touch money, auth, or user data.
