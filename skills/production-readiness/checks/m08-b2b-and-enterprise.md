# M8 · B2B & enterprise

**Scope.** What enterprise buyers expect beyond the core product — tenant isolation, identity federation, audit, and contractual controls.

**Switched on when.** The product serves B2B or enterprise customers.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 8.1 | Tenant isolation tested (cross-tenant access test) | T1 | A dated test attempting cross-tenant access, with the result showing it's blocked | Row-level filtering added in application code but never actually tested against a cross-tenant request |
| 8.2 | SSO (SAML/OIDC) and SCIM at T3 | T3 | Working SSO login test + SCIM provisioning/deprovisioning test against an IdP | SSO advertised on the pricing page but not actually implemented or tested |
| 8.3 | Audit log export | T2 | Export function/API producing an audit log a customer admin can download | Audit events logged internally but with no way for a customer to export them |
| 8.4 | Roles/permissions model | T1 | Roles/permissions config or code showing distinct roles enforced server-side | Every user in a tenant has the same implicit admin access |
| 8.5 | Data export | T2 | Working data-export function covering the customer's own data | No self-serve way for a customer to get their data out |
| 8.6 | Security questionnaire pack (architecture, subprocessors, pen test, policies) | T3 | A ready-to-send pack containing architecture diagram, subprocessor list, pen test summary, and security policies | Every enterprise deal stalls while the pack is assembled from scratch |
| 8.7 | Uptime SLA and credits | T2 | Published SLA terms with defined credit remedies | Uptime SLA promised in a contract with no defined credit process behind it |

**Right-sizing notes.**
- Tenant isolation (8.1) and a real roles model (8.4) are T1 — a cross-tenant leak is a launch blocker regardless of how small the customer base is.
- SSO/SCIM (8.2) and the full security questionnaire pack (8.6) are true T3 items — don't build them ahead of an actual enterprise deal requiring them.
- Audit export, data export, and SLA terms (8.3, 8.5, 8.7) are the T2 middle ground — expected once the product has paying business customers, even before enterprise contracts.
