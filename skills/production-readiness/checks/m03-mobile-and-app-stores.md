# M3 · Mobile & app stores

**Scope.** Requirements for shipping and staying live on Apple App Store and Google Play, plus cross-platform mobile release hygiene.

**Switched on when.** The product ships an iOS and/or Android app distributed through app stores.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence. Every evidence cell here must include a vendor doc URL + date checked, since store rules change yearly.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 3.1 | (Apple) App Review Guidelines followed | T1 | Apple App Review Guidelines URL + date checked, mapped against the app's actual behavior | App built against an old mental model of the guidelines, never re-checked before submission |
| 3.2 | (Apple) Privacy nutrition labels match real data collection | T1 | App Store Connect privacy label screenshot + vendor doc URL + date checked, compared to actual SDK data collection | Labels copied from a template and don't match what the app's SDKs actually collect |
| 3.3 | (Apple) Privacy manifest incl. third-party SDKs | T1 | Privacy manifest file contents + Apple doc URL + date checked | Third-party SDKs (analytics, ads, crash reporting) omitted from the manifest |
| 3.4 | (Apple) In-app account deletion if accounts can be created | T1 | Screenshot of the in-app deletion flow + Apple doc URL + date checked | Account creation exists in-app but deletion only works by emailing support |
| 3.5 | (Apple) Sign in with Apple rule when offering third-party login | T1 | Login screen showing Sign in with Apple alongside other providers + Apple doc URL + date checked | Google/Facebook login offered without the required Sign in with Apple option |
| 3.6 | (Apple) IAP rules for digital goods | T1 | Store listing/receipt code showing Apple IAP used for digital goods + Apple doc URL + date checked | Digital subscription sold via an external payment link, risking rejection |
| 3.7 | (Apple) TestFlight external testing | T2 | TestFlight build/testing group config + Apple doc URL + date checked | App never run through TestFlight before a production submission |
| 3.8 | (Apple) Export compliance | T1 | Export compliance declaration in App Store Connect + Apple doc URL + date checked | Encryption usage declaration skipped or answered incorrectly |
| 3.9 | (Google Play) Current target API level deadline met | T1 | Play Console target API level + Google's current deadline doc URL + date checked | App still targets an API level past Google's enforcement deadline |
| 3.10 | (Google Play) Data safety form accurate | T1 | Play Console Data safety form + Google doc URL + date checked, compared to actual data collection | Form filled out once at first submission and never updated as SDKs changed |
| 3.11 | (Google Play) Closed-testing requirement for new personal developer accounts | T1 | Play Console testing track status + Google doc URL + date checked | New developer account skips the mandatory closed test before production access |
| 3.12 | (Google Play) Play App Signing and upload-key custody | T1 | Play Console signing config + record of who holds the upload key | Upload key held by one departed contractor with no recovery plan |
| 3.13 | (Google Play) Account deletion web link | T1 | Play Store listing showing the required account-deletion web link + Google doc URL + date checked | Play listing missing the mandatory deletion link, risking listing removal |
| 3.14 | (Both) Crash reporting wired up | T1 | Crash reporting dashboard (e.g., Crashlytics, Sentry) showing live mobile events | Crash reporting SDK added but never verified to actually report a real crash |
| 3.15 | (Both) Forced/soft update mechanism for breaking API changes | T2 | Code/config showing a version-gate or forced-update prompt | Old app versions keep hitting a retired API with no way to force an upgrade |
| 3.16 | (Both) Deep/universal links | T2 | Deep link config (associated domains / app links) tested against a real URL | Deep links configured but untested, so marketing links open the wrong screen or a browser |
| 3.17 | (Both) Push credentials owned by the company account | T1 | Push cert/key stored under the company's developer account, not a personal one | Push credentials tied to a personal Apple/Google developer account |
| 3.18 | (Both) Store listing assets, age rating, support URL, privacy URL | T1 | Store listing screenshot showing all fields filled and correct | Placeholder support URL or missing privacy URL left in the live listing |
| 3.19 | (Both) Review-rejection buffer in the launch plan | T1 | Launch plan/calendar showing days (not hours) of buffer before the announced date | Launch date set assuming same-day store approval, with no fallback if rejected |

**Right-sizing notes.**
- Apple/Google policy items move fast — re-verify the vendor doc URL + date checked on every re-run, not just at first launch.
- TestFlight (3.7) and deep-link polish (3.16) can wait for T2; anything touching account deletion, privacy disclosure, or payment rules (3.2–3.6, 3.9–3.13) is a launch blocker because it risks outright store rejection or removal.
- A single-platform app (iOS-only or Android-only) drops the other platform's rows to N/A, not GAP.
