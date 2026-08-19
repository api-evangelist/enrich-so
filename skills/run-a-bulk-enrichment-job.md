---
name: run-a-bulk-enrichment-job
description: Submit, poll and settle a large Enrich batch job — the reserve-and-settle credit model, the free polling loop, and the retry trap that can reserve your balance twice.
api: Enrich Email Verification API
provider: enrich-so
base_url: https://dev.enrich.so/api/v3
operations:
  - batchValidateEmails
  - getEmailValidationBatchStatus
  - getEmailValidationBatchResults
  - bulkReverseLookup
  - getBulkLookupStatus
  - getBulkLookupResults
  - getWalletBalance
generated: '2026-08-14'
method: generated
source: openapi/_original/enrich-so-v3-harvested-openapi.yml
---

# Run a bulk enrichment job

Every Enrich bulk product — email validation, email finder, reverse lookup, phone finder,
IP-to-company, company followers — uses the same three-step shape: **submit → poll →
fetch results**. Learn it once and it applies to all of them. The example below uses email
validation; substitute the operation names for any other product.

## The credit model you must understand first

Bulk billing is **reserve-and-settle**:

1. **Submit** — the FULL estimated cost (`itemCount × creditCostPerItem`) is deducted from
   your balance immediately, before any work happens.
2. **Process** — asynchronous. **Polling is free.**
3. **Settle** — on the first results fetch after the job reaches a terminal status, you
   are charged only for successfully processed items, and the reserved excess is refunded.

Settlement is idempotent: fetching results repeatedly will not charge you twice.

## Steps

### 1. Size the reservation

`getWalletBalance` — `GET /wallets/balance`

A 10,000-email validation batch reserves 10,000 credits (1/email). A 10,000-item **phone**
bulk job reserves **5,000,000** credits (500/item). Check the balance against the
reservation, not against the expected hit rate — Enrich takes the full amount up front and
gives the difference back later.

### 2. Submit

`batchValidateEmails` — `POST /email-validation/batch`

```json
{
  "emails": ["a@example.com", "b@example.com"],
  "webhookUrl": "https://api.yourapp.com/webhooks/enrich"
}
```

Limits: up to **500,000** emails per request for validation, email finder, phone finder
and IP-to-company; up to **100,000** for reverse lookup.

Returns `data.batchId` — a 24-character hex string — plus `meta.creditsReserved` and
`meta.creditsPerItem`.

> **The retry trap.** Submit is **not idempotent**. There is no `Idempotency-Key` header.
> If the request times out and you blind-retry, you may reserve the full cost a second
> time and run two jobs. On a timeout, do not retry — poll for the job instead, or check
> `GET /wallets/transactions` for the reservation before resubmitting.

### 3. Poll for progress (free)

`getEmailValidationBatchStatus` — `GET /email-validation/batch/{batchId}`

Returns `status` (`queued` → `processing` → `completed` | `failed`), `totalItems`,
`processedItems` and `progress` (0–100).

Poll every **5–10 seconds**. Not in a tight loop — status calls are free in credits but
they are not free against your rate limit, and bulk endpoints carry the tightest limits in
the API (1 req/sec on Free, 10 req/sec on Pro).

### 4. Fetch and page the results

`getEmailValidationBatchResults` — `GET /email-validation/batch/{batchId}/results?page=1&limit=1000`

Page-number pagination: `page` (default 1), `limit` (default 100, **max 1000**). The
response carries `page`, `limit`, `total` and `totalPages` — walk until `page === totalPages`.

This first call after a terminal status is the settlement point. Read `meta.creditsUsed`
and `meta.creditsRemaining` to confirm the refund landed.

### 5. Or skip polling entirely — use the webhook

Pass `webhookUrl` on submit and Enrich POSTs your endpoint:

- once **per item** as each one completes, and
- **exactly once** when the whole job finishes.

Two warnings before you turn this on:

- **Volume.** Per-result callbacks are 1:1 with items. A 500,000-email batch will POST
  your endpoint 500,001 times.
- **No signature.** Enrich publishes no signing secret and no HMAC header for any of its
  ten callbacks, and the payloads carry names, work emails and phone numbers. Use an
  unguessable per-job `webhookUrl`, and treat the body as a notification — re-fetch from
  the results endpoint before trusting the data.

See `asyncapi/enrich-so-webhooks.yml` for the full event catalogue and the event-name
inconsistency (eight events use a `webhook:` prefix; the two completion events do not).

## The same shape, other products

| Product | Submit | Poll | Results |
|---|---|---|---|
| Email Validation | `batchValidateEmails` | `getEmailValidationBatchStatus` | `getEmailValidationBatchResults` |
| Email Finder | `batchFindEmails` | `getEmailFinderBatchStatus` | `getEmailFinderBatchResults` |
| Reverse Lookup | `bulkReverseLookup` | `getBulkLookupStatus` | `getBulkLookupResults` |
| Phone Finder | `createPhoneBulkJob` | `getPhoneBulkJobStatus` | `getPhoneBulkJobResults` |
| IP to Company | `batchIpToCompany` | `getIpToCompanyBatchStatus` | `getIpToCompanyBatchResults` |
