# 11 · Legal & trust

**Scope.** The legal and compliance surface a product exposes to real users — policies, consent, vendor agreements, accessibility, and clean use of the product's name and dependencies.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 11.1 | Terms of Service and Privacy Policy match actual data flows | T1 | Published Terms/Privacy Policy pages, dated, describing the data actually collected and shared (cross-checked against the profile's data-types list) | Boilerplate policy generated once and never updated to reflect what the product actually does (e.g., doesn't mention the LLM vendor data is sent to) |
| 11.2 | Cookie consent shown where required (EU/UK) | T1 | Consent banner/config live on the site, gating non-essential cookies until accepted | No consent mechanism at all, or one that sets tracking cookies before consent is given |
| 11.3 | DPAs in place with vendors processing personal data | T3 | Signed Data Processing Agreement on file for each vendor that touches personal data | Vendor added and wired up with no one confirming a DPA exists or is even offered |
| 11.4 | Subprocessor list published and kept current | T3 | Public subprocessor list page or doc, dated, matching the actual vendor list from the integration inventory | No subprocessor list, so a B2B customer's security review stalls when they ask for one |
| 11.5 | Accessibility target set (WCAG 2.2 AA) and a basic audit done | T2 | Automated audit report (e.g., axe, Lighthouse a11y) plus a documented target, dated | No accessibility target set; product has never been run through even an automated checker |
| 11.6 | Open-source license compliance checked | T1 | License-scan output (e.g., license-checker, FOSSA) showing no copyleft/incompatible licenses in the dependency tree, or a documented exception | Dependency pulled in with an AGPL or similarly viral license with no one having looked at what it requires |
| 11.7 | Trademark / name clearance done for the product name | T1 | Trademark search result (e.g., USPTO TESS or equivalent) and domain/registry check, dated | Product ships and markets under a name nobody checked for conflicts, risking a forced rebrand post-launch |

**Right-sizing notes.**
- T1 covers the basics every public product needs on day one: real policies, consent where required, license hygiene, and name clearance (11.1, 11.2, 11.6, 11.7) — these are cheap to get right early and expensive to fix after users have signed up under the wrong terms.
- DPAs and a published subprocessor list (11.3, 11.4) wait for T3 — they matter once enterprise customers run security reviews, not for an early beta.
- Full regulated-data legal analysis (HIPAA, PCI, COPPA, GDPR specifics) lives in module M7, not here; this domain is the baseline every product needs regardless of regulation.
