## Production readiness (Viaknox kit)

When asked to "run production readiness" or to assess whether the product is ready to ship:

- Follow `skills/production-readiness/SKILL.md` step by step (profile → evidence → assess → deliver). Do not skip Step 0.
- Use `skills/production-readiness/checks/*.md` as the item list. Each row states the tier it is required at and the evidence that satisfies it.
- Every item is PASS / GAP / N/A / UNKNOWN. PASS requires evidence you actually inspected. A README claim is not evidence.
- Write the results to `readiness/scorecard.md` (template: `skills/production-readiness/templates/scorecard.md`) and `readiness/backlog.md` (one entry per gap, template: `templates/gap-ticket.md`).
- Verify app-store, OAuth, payment and email-sender rules against current vendor documentation before citing them; record URL + date checked.
- Do not modify product code during the assessment. Report; do not fix.
