# 03 · Edge & app security

**Scope.** The perimeter and application-layer defenses between untrusted traffic and your app and dependencies.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 3.1 | HTTPS enforced with HSTS | T1 | Hosting/DNS config or response header dump showing `Strict-Transport-Security` | HTTP left open as a fallback, or HSTS header never set |
| 3.2 | Security headers set (CSP, frame-ancestors, etc.) | T1 | Response header dump or middleware config listing the headers in place | Default framework headers only, no CSP, page embeddable in a hostile iframe |
| 3.3 | CORS is tight, not wildcard | T1 | CORS config showing an explicit allow-list of origins | `Access-Control-Allow-Origin: *` left in from local development |
| 3.4 | Input validation at every boundary | T1 | Schema validation code (Zod/Pydantic/etc.) at each API entry point | Model-generated endpoints trust request bodies directly with no schema check |
| 3.5 | File upload limits and type checks | T1 | Upload handler config showing max size and allowed MIME/type checks | Upload endpoint accepts any file type/size, opening a path to stored malware or storage abuse |
| 3.6 | SSRF guards on any URL-fetching feature | T1 | Code showing allow-listed hosts/IP-range blocking on server-side fetch calls | A "fetch this URL" or webhook-preview feature lets a user hit internal/cloud-metadata IPs |
| 3.7 | WAF or bot protection in front of the app | T2 | Config or dashboard screenshot of the WAF/bot-protection service in front of the app | Nothing in front of the origin beyond the hosting platform's defaults |
| 3.8 | Dependency scanning and lockfiles in place | T1 | Lockfile committed plus a dependency-audit CI run or dashboard | No lockfile, or `npm audit`/`pip-audit` never run, so vulnerable transitive deps ship silently |
| 3.9 | SAST running in CI | T2 | CI job config and a recent run link for the SAST tool | Static analysis never wired in; the AI-generated code has never been scanned for injection/XSS patterns |
| 3.10 | SBOM generated and license check run | T3 | SBOM file (CycloneDX/SPDX) and license-check report, both dated | No inventory of what's actually in the build, so an enterprise security questionnaire can't be answered |

**Right-sizing notes.**
- T1 already expects the perimeter basics (HTTPS/HSTS, headers, CORS, input validation, upload/SSRF guards, dependency scanning) — these are cheap to fix and catch most vibe-coded holes.
- WAF/bot protection and SAST in CI (3.7, 3.9) become worth the setup cost at T2 once there's real traffic and attack surface to defend.
- SBOM and license compliance (3.10) is overkill for a beta; treat it as a T3 gate tied to enterprise/regulated deals, not a launch blocker for early users.
