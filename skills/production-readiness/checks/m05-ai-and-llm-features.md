# M5 · AI & LLM features

**Scope.** How the product's AI/LLM features are made reliable, safe, cost-controlled, and honest with users.

**Switched on when.** The product includes AI/LLM features.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 5.1 | Provider abstraction or gateway with fallback model | T2 | Code/config showing a model gateway or abstraction layer with a configured fallback model | Hardcoded calls to one model/provider with no fallback if it's down or deprecated |
| 5.2 | Timeouts and retry on 429/5xx | T1 | Code showing a request timeout and retry logic on rate-limit/server errors | A slow or rate-limited model call hangs the request indefinitely |
| 5.3 | Structured output validated by schema (Zod/Pydantic) | T1 | Schema definition + validation code rejecting malformed model output | Model output parsed with raw string matching, breaking silently on format drift |
| 5.4 | Eval set of real cases run in CI before prompt/model changes | T2 | CI job running an eval set against prompt/model changes, with pass/fail history | Prompt changes shipped straight to production with no regression check |
| 5.5 | Prompt-injection defenses where the model reads untrusted content or can call tools (least-privilege tools, human confirm for destructive actions) | T1 | Tool-permission config showing least-privilege scoping and a human-confirm step before destructive actions | Model can call a delete/send-money tool directly from untrusted input with no confirmation |
| 5.6 | Per-user and global cost caps | T1 | Billing/usage dashboard or code showing enforced per-user and global spend caps | One user (or a prompt loop) can run up unlimited LLM spend |
| 5.7 | PII handling and provider data-retention settings | T1 | Provider dashboard/config showing data-retention/zero-retention settings and PII handling policy | Sensitive user data sent to a model provider with default (long) retention never reviewed |
| 5.8 | Model deprecation dates tracked | T2 | Tracking doc/calendar entry listing each model's announced deprecation date | Production still calling a model version past its provider-announced sunset date |
| 5.9 | AI disclosure to users where required | T1 | UI screenshot showing an AI-generated content disclosure where required | AI-generated content shown with no disclosure where one is expected |
| 5.10 | Brand/quality guardrails on generated output (banned terms, tone checks, human review tiered by risk) | T1 | Guardrail config/code showing banned-term filtering, tone checks, and a review tier by risk level | Generated output ships straight to users/customers with no content guardrail |
| 5.11 | UI tells users the limits ("verify facts", sources shown for claims) | T1 | UI screenshot showing a limits disclaimer and/or sources cited for factual claims | Model output presented as authoritative with no caveat or source shown |
| 5.12 | Prompt/model changes tested first in a sandbox on historical/sample data, then rolled out to a small share of traffic before everyone | T2 | Rollout config/log showing a staged rollout percentage and sandbox test results before full traffic | New prompt or model pushed to 100% of users the same day it was written |
| 5.13 | Scheduled (e.g., semiannual) model/vendor review | T2 | Calendar entry or doc showing a recurring model/vendor review cadence | Model/vendor choice never revisited after initial launch |

**Right-sizing notes.**
- Items that directly protect users or money — timeouts (5.2), output validation (5.3), injection defenses (5.5), cost caps (5.6), PII/retention (5.7), disclosure (5.9), guardrails (5.10), and limits messaging (5.11) — are T1 and worth fixing before any real users touch the feature.
- Eval-in-CI, staged rollout, and vendor review (5.4, 5.12, 5.13) are operational maturity items that matter more once prompt/model changes happen regularly, so they land at T2.
- A single, low-risk AI feature (e.g., a text summarizer with no tool access) can skip the tool-permission half of 5.5 — mark that half N/A rather than GAP.
