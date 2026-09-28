# M9 · Marketplaces you publish into

**Scope.** Listings the product publishes into third-party marketplaces or app directories — Chrome Web Store, Slack/Teams/Zoom app directories, Shopify, MCP/plugin registries, and similar.

**Switched on when.** The product publishes a listing into one or more third-party marketplaces or app directories.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence. Every evidence cell here must include a vendor doc URL + date checked, since marketplace rules are verified live.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 9.1 | Listing requirements met | T1 | Marketplace listing requirements doc URL + date checked, compared field-by-field against the actual listing | Listing submitted against an outdated understanding of what the marketplace requires |
| 9.2 | Review timelines planned for | T2 | Marketplace's current stated review timeline doc URL + date checked, reflected in the launch calendar | Launch date set assuming same-day approval with no buffer for review |
| 9.3 | Permission justification documented | T1 | Permission-justification doc URL + date checked, plus the app's written justification for each requested permission | Broad permissions requested (e.g., "read all files") with no justification on file, risking rejection |
| 9.4 | Privacy disclosures accurate | T1 | Marketplace privacy disclosure doc URL + date checked, compared against the app's actual data practices | Privacy disclosure copied from a template and doesn't match what the app actually collects |

**Right-sizing notes.**
- Marketplace rules move at least as fast as app store rules — re-verify the vendor doc URL + date checked on every re-run, not just before first submission.
- Permission justification (9.3) and privacy disclosures (9.4) are the two most common causes of listing rejection or removal — treat them as launch blockers even for a small, low-traffic listing.
- A product listed in multiple marketplaces gets one row set per marketplace in the appendix, even though this file carries one generic table.
