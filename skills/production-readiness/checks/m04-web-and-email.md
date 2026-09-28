# M4 · Web & email

**Scope.** The public website's domain/discoverability hygiene and the email pipeline's deliverability and compliance.

**Switched on when.** The product has a public website and/or sends email to users.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 4.1 | Custom domain, DNS owned by company account, registrar lock + auto-renew | T1 | Registrar dashboard showing the domain under a company account with lock and auto-renew on | Domain registered under a founder's personal account with auto-renew off |
| 4.2 | SEO basics (titles, sitemap, robots, OG tags) if discoverability matters | T2 | Page source/sitemap.xml/robots.txt showing titles, sitemap, robots directives, and OG tags present | Client-only rendered app has no crawlable titles, sitemap, or OG tags |
| 4.3 | 404/500 pages | T1 | Screenshot/test of a broken URL and a forced server error showing branded pages, not a stack trace | Default framework error page leaks stack traces to real users |
| 4.4 | Email sender auth SPF, DKIM, DMARC and one-click unsubscribe for bulk mail (current Gmail/Yahoo sender rules checked) | T1 | DNS records for SPF/DKIM/DMARC + one-click unsubscribe header, plus vendor doc URL + date checked against current Gmail/Yahoo rules | Bulk mail sent with no DMARC record, so it lands in spam or gets bulk-sender throttled |
| 4.5 | Bounce/complaint handling | T1 | Email provider dashboard/webhook showing bounces and complaints processed (suppression list updated) | Bounced addresses keep getting emailed, hurting sender reputation |
| 4.6 | Separate transactional vs marketing streams | T2 | Email provider config showing distinct sending domains/streams for transactional vs marketing mail | A marketing blast suppression issue also blocks password-reset emails |

**Right-sizing notes.**
- Sender authentication (4.4) and bounce handling (4.5) are T1 because a bad sender reputation can silently kill transactional email (password resets, receipts) — the kind of failure users notice immediately.
- SEO polish (4.2) and stream separation (4.6) can wait until T2 unless organic discovery or marketing volume is already part of the launch plan.
- Re-check the Gmail/Yahoo bulk-sender rules (4.4) on every re-run; they've changed before and will again.
