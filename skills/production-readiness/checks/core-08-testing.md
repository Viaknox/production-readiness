# 08 · Testing

**Scope.** Whether the tests that exist actually cover the paths that matter, not just a coverage percentage.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 8.1 | Tests on critical paths (auth, payments, data writes, permissions) over a coverage percentage | T1 | Test files covering each critical path, plus a CI run showing they pass | High overall coverage % from trivial generated tests while auth and payment paths have none |
| 8.2 | Integration tests run against a real database | T1 | CI job config showing tests run against a real (test) DB instance, not a mock | All tests mock the DB layer, so a real migration or query bug never surfaces before prod |
| 8.3 | E2E smoke tests on top user journeys, run post-deploy | T2 | CI/CD step showing E2E smoke tests triggered after each deploy, with a recent run link | E2E tests exist locally but nothing runs them automatically after a real deploy |
| 8.4 | Contract tests or recorded fixtures for external APIs | T2 | Contract test suite or recorded fixture files (e.g., VCR/nock cassettes) for each external API used | Tests hit the real third-party API sandbox inconsistently, or assume its response shape with no fixture to catch drift |

**Right-sizing notes.**
- T1 is about coverage of the paths that actually matter (auth, payments, writes, permissions) and testing against a real DB — a high coverage number on trivial code is not a pass.
- Automated E2E smoke and contract/fixture tests (8.3, 8.4) become mandatory at T2 once a deploy pipeline and external integrations are running in production continuously.
- For deeper code-level test-gap analysis, defer to `pm-ai-shipping:derive-tests` per this skill's reuse rule rather than re-deriving coverage manually here.
