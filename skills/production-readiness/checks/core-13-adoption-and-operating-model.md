# 13 · Adoption & operating model

**Scope.** Whether the people and process around the product will actually make it stick — the organizational half of readiness that most AI-built products skip, and the reason most launches stall after shipping rather than because the code failed.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence. In this domain, evidence must be a dated written artifact: a one-page decision doc, a calendar entry, a named approver list, or a feedback log — not a verbal agreement or an intention.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 13.1 | Success metric and pilot exit criteria written down before launch | T1 | A one-page doc, dated before launch, stating the metric, its target, the measurement method, and what moves the pilot to "scale" or "kill" | Launch happens with no written target, so the pilot runs indefinitely with no one able to say whether it's working ("pilot purgatory") |
| 13.2 | Documented release workflow with named approvers per risk tier and an agreed turnaround | T1 | A written workflow doc naming who approves low-risk vs. high-risk changes, plus a stated turnaround time (e.g., "high-risk: 2 approvers, 1 business day") | No documented approval path; every change either skips review or waits on whoever happens to be free, with no SLA on sign-off |
| 13.3 | Launch communication drafted: what's changing, what isn't, known limits | T1 | Dated launch-comms doc or email sent to affected users/stakeholders, stating what changes, what stays the same, and current known limitations | Product ships with no communication, so users discover new behavior (and its limits) by hitting them |
| 13.4 | First-user/champion group identified with a way to hear from them | T1 | Named list of first users/champions plus a specific channel or recurring touchpoint (calendar invite, Slack channel, standing call) to collect their input | "Early users" is an undefined, unnamed group with no dedicated way for their feedback to reach the team |
| 13.5 | In-product help, templates, or examples so users learn inside the tool | T2 | Screenshots or content files showing in-product guidance (tooltips, sample data, starter templates) shipped with the release, dated | Users are expected to learn the tool from a separate doc or a training session instead of the product itself |
| 13.6 | Feedback loop (user feedback + usage metrics) with a review cadence | T2 | A dated cadence doc or recurring calendar entry (e.g., 30/60/90 days, then quarterly) naming who reviews feedback and usage data, with at least one completed review logged | Feedback is collected somewhere but no one owns reviewing it on a schedule, so it never changes anything |
| 13.7 | Owner named for ongoing support as usage grows | T1 | Named individual or team documented as the ongoing owner, dated, distinct from (or explicitly overlapping with) the launch owner | Launch has an owner, but no one is designated to own the product once the original team moves to the next thing |

**Right-sizing notes.**
- This domain gets a row per item deliberately, even at T1 — shipped code with no operating model around it is the single most common reason AI-built launches stall, per the hard rule "shipped ≠ adopted."
- In-product learning aids and a scheduled feedback cadence (13.5, 13.6) are the two items that can wait for T2; everything else — success metric, approvers, launch comms, a named champion group, and an ongoing owner — is cheap to write down and should exist before launch at any tier.
- Reject verbal or implied answers here ("we all know who owns this") — if it isn't in a dated doc, calendar entry, or named list, score it GAP, not PASS.
