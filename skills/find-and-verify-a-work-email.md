---
name: find-and-verify-a-work-email
description: Find a professional email from a name and company domain with the Enrich API, then verify it is deliverable before you send — for one contact or half a million.
api: Enrich Email Finder API
provider: enrich-so
base_url: https://dev.enrich.so/api/v3
operations:
  - findEmail
  - validateEmail
  - batchFindEmails
  - batchValidateEmails
generated: '2026-08-14'
method: generated
source: openapi/_original/enrich-so-v3-harvested-openapi.yml
---

# Find and verify a work email

Two endpoints, in this order, do the whole job: find the address, then prove it is
deliverable. Running them in the other order — or skipping the second — is how a bounce
rate happens.

## Cost shape

| Step | Operation | Credits |
|---|---|---|
| Find | `findEmail` | 10 (not charged when `found` is false) |
| Verify | `validateEmail` | 1 (not charged when the result is risky) |

Verification costs a tenth of finding. Validate everything; it is the cheapest call in the
API.

## Steps

### 1. Find the address

`findEmail` — `POST /email-finder`

```json
{ "firstName": "Jane", "lastName": "Doe", "domain": "example.com" }
```

All three fields are required. `domain` is the company domain (`figma.com`), not a URL and
not a company name.

The response carries `data.email` and `data.confidence` (`high` / …). Treat `confidence`
as a routing signal, not a guarantee — it is Enrich's belief about a pattern match, and it
is not the same thing as a mailbox existing.

If no address is found, you get **HTTP 200** with `found: false` and `meta.creditsUsed: 0`.
Not a 404. Do not retry it.

### 2. Verify it is deliverable

`validateEmail` — `POST /email-validation`

```json
{ "email": "jane.doe@example.com" }
```

Read all five fields, not just `status`:

- `status` — `valid` / `invalid` / risky.
- `subStatus` — the reason, e.g. `no_mx_record`. This is what you log.
- `freeEmail` — a Gmail/Outlook address, not a company mailbox.
- `disposable` — a burner domain. Never sequence these.
- `catchAll` — the domain accepts everything, so `valid` here means "the domain will not
  bounce it", **not** "this person exists". Route `catchAll: true` addresses to a
  lower-confidence track.

### 3. At scale, batch both steps

Above a hundred contacts, use the batch pair — each takes up to **500,000** items and
counts as **one** request against your rate limit:

- `batchFindEmails` — `POST /email-finder/batch`, body `{ "leads": [ { "firstName", "lastName", "domain" } ], "webhookUrl": "…" }`
- `batchValidateEmails` — `POST /email-validation/batch`, body `{ "emails": [ … ], "webhookUrl": "…" }`

Both reserve the full estimated cost on submit and settle on the first results fetch,
refunding the excess. Poll every 5–10 seconds; polling is free. Full mechanics in
`skills/run-a-bulk-enrichment-job.md`.

### 4. Errors

RFC 9457 problem details on every failure. The two that matter here:

- **402 `insufficient-credits`** — for a batch this fires at submit, because the whole
  reservation is taken up front. The `shortfall` member tells you the exact top-up.
- **429 `rate-limit-exceeded`** — honour `Retry-After`. Bulk submit endpoints are limited
  far below the global rate: 1 req/sec on Free, 3 on Growth, 5 on Scale, 10 on Pro.

## Do not skip verification

Enrich holds no contact database of its own — results are assembled from upstream sources
at call time. A found address is a strong inference, not an observation. One credit per
address is the cheapest insurance in this API.
