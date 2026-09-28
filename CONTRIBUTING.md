# Contributing

Thanks for helping make AI-built products safer to ship.

**Where things live**
- `skills/production-readiness/SKILL.md` — the skill. Workflow, hard rules, tiers, domain and module definitions.
- `skills/production-readiness/checks/` — one file per domain (`core-NN-*.md`) and per module (`mNN-*.md`). Each row: check · required tier · evidence that satisfies · common gap.
- `scorecard/` — the printable one-page self-check, generated from the check files. If you change a check, regenerate the scorecard so the two never drift.
- `adapters/` — thin pointers for Cursor, Codex, Copilot and Gemini CLI. They must not duplicate the skill; they load it.

**The one rule for every contribution:** a check must say what evidence satisfies it. "Confirm that backups work" is not a check. "Restore log with timestamp and restore duration" is.

**Proposing a new module** — open an issue first with: the profile condition that switches it on, 5–12 checks in the standard table, and the tier each is required at. Modules are for things that only some products have (payments, app stores); anything every product needs belongs in a core domain.

**Vendor rules** (app stores, OAuth, payment, email senders) change every year. A PR that cites one must include the vendor doc URL and the date checked.

**Style** — plain English, sentence case, US spelling, no hype. No emojis in check files.

By contributing you agree your code is MIT and your documentation is CC BY 4.0.
