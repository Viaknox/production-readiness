# 02 · Identity & access

**Scope.** How users and admins authenticate, how requests are authorized, and how access is limited and logged.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 2.1 | Auth uses a proven provider or well-reviewed library, not hand-rolled crypto | T1 | Dependency/config showing the auth provider or library (Auth.js, Clerk, Supabase Auth, etc.) and its version | A generated login flow that hashes passwords with a custom scheme or rolls its own JWT signing |
| 2.2 | Server-side authorization on every data route (IDOR, missing tenant filters, permissive RLS) | T1 | Code path or RLS policy per data route, plus a passing IDOR/cross-tenant test | Frontend hides a button but the API route still returns or accepts any user's data because the check was never added server-side |
| 2.3 | Session/token lifetimes and revocation are defined | T1 | Config showing token TTL and a revocation/logout-everywhere path that actually invalidates sessions | Tokens issued with no expiry, or a "logout" that only clears the client cookie |
| 2.4 | Rate limits on login, signup, password reset, and OTP endpoints | T1 | Rate-limit config or middleware for each of those routes, with the limits stated | Auth endpoints wide open, so a bot can brute-force or spam OTP codes at will |
| 2.5 | MFA available/required for admin accounts | T2 | Admin auth config or provider setting showing MFA enforced | Admin panel protected by the same single-factor password as any regular user |
| 2.6 | Service accounts and API keys follow least privilege | T2 | IAM policy or key-scope config showing scoped, non-admin permissions per service account | One shared "god mode" service key used by every background job and integration |
| 2.7 | Admin actions are logged | T2 | Log entries or audit-log config capturing who did what admin action and when | Admin panel changes data with no record of which admin made the change |

**Right-sizing notes.**
- T1 needs solid auth and authorization fundamentals (2.1–2.4) — this is where most vibe-coded apps fail first, especially IDOR and missing tenant filters.
- MFA for admins, least-privilege service accounts, and admin action logging (2.5–2.7) matter once there's real operational risk at T2, not for a small closed beta.
- Full SSO/SCIM (domain M8, B2B/enterprise) is a T3 add-on, not a core requirement here — don't gate a beta launch on it.
