# 07 · CI/CD & release

**Scope.** How code moves from commit to production safely, and how a bad release gets undone.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 7.1 | Required checks on main: lint, typecheck, tests, secret scan, dependency audit | T1 | CI config showing these as required (blocking) checks, plus a recent passing run | CI runs tests but doesn't block merge on failure, so red builds still ship |
| 7.2 | Preview or staging environment exists | T1 | Deploy config/dashboard showing a preview or staging environment distinct from prod | Every change deploys straight to prod because a preview/staging env was never set up |
| 7.3 | One-click rollback proven to work | T1 | A dated log/screenshot of an actual rollback performed (not just a documented button) | Rollback documented in theory but never exercised, and it fails the first time it's needed |
| 7.4 | Feature flags for risky features | T2 | Feature-flag config/dashboard showing a risky feature gated behind a flag | Risky feature shipped live to 100% of users with no kill switch if it misbehaves |
| 7.5 | Migrations run safely as part of deploy | T1 | Deploy pipeline config showing migration step ordering and failure handling | Migrations run manually and separately from deploy, so app and schema can drift out of sync |
| 7.6 | Release notes/changelog maintained | T2 | Changelog file or release-notes doc with dated entries | No record of what shipped when, making incident correlation guesswork |
| 7.7 | Branch protection enabled on main | T1 | Repo settings screenshot showing branch protection rules (required reviews/checks) | Anyone can push directly to main, bypassing CI and review entirely |

**Right-sizing notes.**
- T1 needs the release safety net proven, not just configured: required CI checks, a preview env, safe migration ordering, branch protection, and a rollback that has actually been exercised once.
- Feature flags and a maintained changelog (7.4, 7.6) are T2 additions once there's a team and paying users who need predictable, reversible releases.
- Don't over-engineer this for a beta with multi-stage approval gates — per the anti-patterns, a heavy release-governance process on a beta is as much a gap as no process at all.
