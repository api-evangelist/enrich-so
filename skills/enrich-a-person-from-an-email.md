---
name: enrich-a-person-from-an-email
description: Resolve a professional profile, and optionally a phone number, from a single email address using the Enrich API — without overspending credits.
api: Enrich Person Enrichment API
provider: enrich-so
base_url: https://dev.enrich.so/api/v3
operations:
  - reverseLookup
  - phoneLookup
  - getWalletBalance
generated: '2026-08-14'
method: generated
source: openapi/_original/enrich-so-v3-harvested-openapi.yml
---

# Enrich a person from an email address

Turn one email address into a professional profile — name, headline, current company,
position history, education — and, only when it is worth 500 credits, a phone number.

## Before you start

- Authenticate with `x-api-key: sk_...` on every request (or `Authorization: Bearer sk_...`).
- Every call is metered against one prepaid credit balance. Read the price before you
  call: reverse lookup is **10 credits**, phone lookup is **500 credits** — fifty times
  more. Never call the phone lookup speculatively.
- There is **no idempotency key**. A retried POST is a second billable lookup.

## Steps

### 1. Check the balance (free)

`getWalletBalance` — `GET /wallets/balance`

Returns `data.balance`. Do this once at the start of a run, not per record. If you are
about to enrich N people, you need at least `N * 10` credits for profiles alone.

### 2. Look up the profile

`reverseLookup` — `POST /reverse-lookup/lookup`

```json
{ "email": "jane@example.com" }
```

**10 credits, refunded when nothing is found.**

Read the answer from the body, not the status code:

- `data.found === true` → you have a profile, and `meta.creditsUsed` is 10.
- `data.found === false` → **HTTP 200, not 404**, and `meta.creditsUsed` is 0. This is a
  successful call that found nothing and charged nothing. Do not treat it as an error and
  do not retry it — the answer will not change, and results are cached for 7 days anyway.

Always record `meta.requestId`. It is the only trace identifier Enrich issues, it appears
only in the body (there is no `X-Request-Id` header), and support will ask for it.

### 3. Decide whether a phone number is worth 500 credits

`phoneLookup` — `GET /reverse-lookup/phones?email=jane@example.com`

Accepts `email` **or** `linkedin` — at least one is required.

**500 credits, refunded when no number is found.** Gate this behind an explicit business
rule. Enriching 1,000 people costs 10,000 credits for profiles and 500,000 credits for
phones; on the Growth pack (100,000 credits for $49/mo) the phone pass alone is five
months of plan.

### 4. Handle the errors that actually happen

Every error is RFC 9457 Problem Details, `application/problem+json`, with a `type` URI
under `https://dev.enrich.so/errors/`:

- **402 `insufficient-credits`** — read the `shortfall` extension member; it tells you
  exactly how many credits to top up. Nothing was charged.
- **429 `rate-limit-exceeded`** — honour `Retry-After` (seconds), then back off
  exponentially with jitter. Pace against `X-RateLimit-Remaining` so you never get here.
- **401 `unauthorized`** — the key is missing, malformed, disabled or revoked.
- **500 / 503** — retry with backoff.

## When to use the bulk path instead

Above roughly a hundred records, stop looping. `bulkReverseLookup`
(`POST /reverse-lookup/bulk-lookup`) accepts up to **100,000 emails** in one request and
counts as a **single** call against your rate limit. See
`skills/run-a-bulk-enrichment-job.md`.
