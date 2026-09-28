# 04 · Data & backups

**Scope.** How data is protected across backup, migration, environment separation, retention, and encryption.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 4.1 | Automated backups run on a schedule, and a restore has actually been tested | T1 | Backup config path, timestamp of last successful backup, and a dated restore-drill log with the actual restore time | Backups enabled on the platform default but never once restored, so nobody knows if they even work |
| 4.2 | Point-in-time recovery where the database supports it | T2 | DB config/dashboard showing PITR enabled and its retention window | Only full nightly snapshots kept, so any mid-day mistake loses up to a day of data |
| 4.3 | Migrations are backward-compatible (expand → migrate → contract) | T1 | Migration files or PR history showing the expand/migrate/contract pattern for a recent schema change | Migration generated as a single destructive `ALTER`/drop that breaks the running app mid-deploy |
| 4.4 | Staging uses no raw production PII | T1 | Staging data-seeding script or anonymization config, dated | Prod database dumped straight into staging for "realistic" testing |
| 4.5 | Retention and deletion path actually deletes across DB, storage, logs, and vendors | T1 | Deletion job code/log showing it touches DB, object storage, log pipeline, and any downstream vendor | Account "deletion" only soft-deletes the DB row; files in storage and vendor copies (email, analytics) remain |
| 4.6 | Encryption at rest and in transit confirmed by default settings | T1 | Hosting/DB dashboard setting or config showing encryption at rest and TLS in transit | Assumed "the platform handles it" with no one having actually checked the setting |

**Right-sizing notes.**
- T1 already requires a proven restore and a real deletion path — these are the two data checks most often skipped because they only bite after something goes wrong.
- Point-in-time recovery (4.2) is the one item that waits for T2; nightly backups are fine for a low-scale beta.
- Full data-residency/DPA and regulated-data controls (PHI/PCI/GDPR specifics) live in module M7, not here — don't fold those into a core-domain review.
