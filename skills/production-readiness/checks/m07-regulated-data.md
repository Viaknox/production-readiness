# M7 · Regulated data

**Scope.** Data types with their own legal regime — health, payment, children's, and regional privacy data.

**Switched on when.** The product handles PHI, PCI-regulated payment data beyond hosted checkout, children's data, EU/UK users, or California users.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 7.1 | PHI → HIPAA: BAA with every vendor touching PHI, access logging, minimum necessary | T3 | Signed BAAs for every vendor in the PHI data path + access log showing who viewed what PHI and when | A vendor (e.g., analytics, error tracking) receives PHI with no BAA in place |
| 7.2 | PCI beyond hosted checkout → SAQ scope | T2 | Current SAQ type identified and its required controls mapped against the actual card-data flow | Card data touches app servers/logs, but no one has determined which SAQ applies |
| 7.3 | Children → COPPA/age gating | T1 | Age-gate flow/config + parental consent mechanism where the product knowingly serves children | No age gate at all on a product likely to have under-13 users |
| 7.4 | EU/UK users → GDPR lawful basis, DSAR process, transfers | T1 | Documented lawful basis per processing purpose + a working DSAR intake process + transfer mechanism (e.g., SCCs) | No documented lawful basis for processing, and no way for a user to submit a data request |
| 7.5 | California → CCPA/CPRA | T1 | Privacy policy section covering CCPA/CPRA rights + a working "do not sell/share" or deletion request path | Privacy policy doesn't mention CCPA rights and there's no request-handling path |

**Note.** This module flags items for legal review. It does not give legal conclusions.

**Right-sizing notes.**
- COPPA, GDPR, and CCPA baseline obligations (7.3–7.5) apply as soon as the relevant users exist, even at T1 — the legal exposure doesn't wait for scale.
- HIPAA (7.1) and PCI-beyond-hosted-checkout (7.2) usually only bite once the product is handling real regulated volume under contract, so they land at T2/T3 — but flag them the moment PHI or raw card data is in scope at all, regardless of tier.
- Every row here is a "get this in front of legal/privacy" flag, not a pass/fail the skill can adjudicate on its own.
