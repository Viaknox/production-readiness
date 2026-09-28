# 01 · Secrets & config

**Scope.** How secrets and environment configuration are stored, separated, and rotated across dev, staging, and prod.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 1.1 | No secrets in code or git history, checked with gitleaks/trufflehog over full history | T1 | Scanner run output (CI job link or local run log) showing zero findings, with scan date | Assistant hardcoded an API key while iterating, then "removed" it in a later commit that still leaves it in history |
| 1.2 | `.env` is git-ignored and a `.env.example` is present | T1 | `.gitignore` entry plus `.env.example` file path in the repo | `.env` committed early in the project and never removed, or `.env.example` missing so new devs copy real secrets around |
| 1.3 | Production secrets live in the platform's secret store, not in code or CI YAML | T1 | Screenshot or CLI listing of the platform's secret manager (Vercel/Railway/Supabase env vars, etc.) showing the keys in use | Secrets pasted directly into CI workflow files or into the hosting dashboard's plaintext build command |
| 1.4 | Separate keys for dev, staging, and prod | T1 | Env var listing per environment showing distinct key values/IDs | Same API key and DB reused across all environments because it was faster to set up once |
| 1.5 | Rotation plan exists and names who can rotate each secret | T2 | Runbook or doc link naming the rotation procedure and the owner per secret type | No one knows which keys are even live, so nothing gets rotated after launch |
| 1.6 | Leaked-key response steps documented | T2 | Doc link with the exact revoke/rotate/notify steps for a leaked key | No plan exists; a leaked key would be discovered only when the vendor bill spikes or the vendor disables it |

**Right-sizing notes.**
- At T1, the bar is just "no leak, keys separated, `.env` handled" — a solo founder can do this in an afternoon.
- Rotation plans and leaked-key runbooks (1.5, 1.6) become mandatory once there's a team or paying users at T2, since a single owner rotating everything ad hoc doesn't scale.
- Don't demand a full secrets-management platform (Vault, KMS policies) for a T1 beta — the platform's built-in secret store is enough until T3 compliance requirements kick in.
