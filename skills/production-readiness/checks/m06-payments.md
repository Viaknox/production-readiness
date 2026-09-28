# M6 · Payments

**Scope.** How the product takes money — checkout, webhook-driven state, refunds, tax, and reconciliation.

**Switched on when.** The product processes payments.

**Scoring.** Every item is PASS, GAP, N/A or UNKNOWN. PASS needs evidence — a file path, config, CI run, dashboard or doc link. A README claim is not evidence.

| # | Check | Required at | Evidence that satisfies | Common gap in AI-built products |
|---|---|---|---|---|
| 6.1 | Hosted checkout to minimize PCI scope | T1 | Checkout integration code/screenshot showing a hosted payment page (not a custom card form) | Custom card-entry form built in-house, pulling the whole app into PCI scope |
| 6.2 | Webhook-driven state (never trust client redirect) | T1 | Order/fulfillment code showing state changes driven by a verified webhook, not the browser redirect | Order marked "paid" the moment the browser hits a success URL, before the webhook confirms it |
| 6.3 | Idempotent fulfillment | T1 | Fulfillment code showing an idempotency key/check preventing duplicate fulfillment | A retried webhook double-fulfills an order (double-ships, double-grants access) |
| 6.4 | Refunds, disputes, dunning | T1 | Refund/dispute handling code or dashboard showing a working flow for each | Refunds and chargebacks handled manually with no automated flow or tracking |
| 6.5 | Tax collection per region | T2 | Tax config/vendor (e.g., Stripe Tax) dashboard showing tax collected per applicable region | Tax not collected in regions where it's legally required |
| 6.6 | Test clock/sandbox covered | T1 | Test-mode transactions/test clock runs covering subscription lifecycle events | Subscription renewal/cancellation logic never tested against a simulated clock |
| 6.7 | Revenue reconciliation | T2 | Reconciliation process/report matching payment provider records to internal ledger | No process ties provider payouts back to what the app's database thinks was charged |

**Right-sizing notes.**
- Items 6.1–6.4 and 6.6 are T1 because a payment bug directly costs users or the business money — these need to be solid before any real transaction runs.
- Tax collection (6.5) and reconciliation (6.7) can mature at T2 as transaction volume and regional reach grow.
- A product using a fully hosted billing platform (e.g., Stripe Billing) may already satisfy several of these by default — confirm with a dashboard screenshot rather than assuming.
