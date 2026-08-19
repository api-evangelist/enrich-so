---
name: build-a-lead-list-without-overspending
description: Use the Enrich Lead Finder to size an audience for free, preview it for free, and pay only for the contacts you actually reveal — with the field-level cost control most integrations miss.
api: Enrich Lead Finder API
provider: enrich-so
base_url: https://dev.enrich.so/api/v3
operations:
  - countLeads
  - searchLeads
  - revealLeads
  - getRevealJob
  - unlockNames
  - createSavedSearch
  - exportLeads
  - getExportJob
  - downloadExportJob
generated: '2026-08-14'
method: generated
source: openapi/_original/enrich-so-v3-harvested-openapi.yml
---

# Build a lead list without overspending

Lead Finder is the one Enrich product where cost is almost entirely under your control.
Counting is free. Searching previews are free. Saving searches is free. Polling is free.
You pay at exactly one moment — reveal — and how much you pay depends on a single optional
array most integrations never send.

## The free path

### 1. Size the audience

`countLeads` — `POST /lead-finder/count`

```json
{ "filters": { … } }
```

**Free. No credits.** Returns the total matching your filters. Iterate on filters here
until the number looks right — never by running searches.

`excludeFilters` narrows further, but only across a limited set of text fields
(`personHeadline`, `companyHeadline`, `aboutUs`, …).

### 2. Preview the matches

`searchLeads` — `POST /lead-finder/search`

```json
{ "filters": { … }, "page": 1, "pageSize": 100 }
```

Returns combined person + organization + insights rows. **Last names are masked by
default** in search results.

Search has a free tier and a paid tier, and a pager that ignores the boundary will start
spending without saying so:

- **Free:** the first 3 pages **or** 75 results per search, whichever comes first, and 50
  free searches per month (a search = a unique filter combination; paging or re-running
  the same search does not consume another one).
- **Paid, from page 4:** **1 credit per result returned**, up to a maximum of 40 pages.

Limits: `pageSize` is 1–100, and the offset cap `(page - 1) × pageSize` must stay under
500. You cannot page endlessly through a large result set — narrow the filters or export
instead.

### 3. Save the filter set

`createSavedSearch` — `POST /lead-finder/saved` — free. `listSavedSearches`
(`GET /lead-finder/saved`) and `deleteSavedSearch` (`DELETE /lead-finder/saved/{id}`) are
free too. Only the owner can delete their own saved search.

`getFilterOptions` (`GET /lead-finder/filter-options`) and `suggestCompanyNames`
(`GET /lead-finder/suggest`) are also free — use them to build the filter UI rather than
hard-coding country/department/industry values.

## The paid path — and the field that controls it

### 4. Reveal only what you need

`revealLeads` — `POST /lead-finder/reveal`

```json
{
  "leads": [ … ],
  "fields": ["email"]
}
```

`leads` is capped at **25 per call**. `fields` is optional — **and omitting it is the most
expensive thing you can do in this API.**

| `fields` | Cost per lead |
|---|---|
| `["email"]` | 10 credits |
| `["phone"]` | 525 credits |
| omitted (default: `["email","phone"]`) | 535 credits |

Revealing 1,000 leads costs **10,000 credits** with `fields: ["email"]` and **535,000
credits** on the default. That is a 53× difference produced by one array. Send it
explicitly, every time, even when you want both.

Cached reveals are free — re-revealing a lead you already paid for does not charge again.

### 5. Poll the reveal job

`getRevealJob` — `GET /lead-finder/reveal-jobs/{jobId}`

Reveal is asynchronous: `revealLeads` returns a `jobId` in under 100ms and the credits are
charged **inside the worker**. That has one consequence you must code for — **insufficient
credits fail the job asynchronously; there is no synchronous 402.** A 202 from
`revealLeads` does not mean you could afford it. Poll `getRevealJob` every 2 seconds until
`status` is `completed` or `failed`, and treat `failed` as a possible billing failure.

**Polling is always free.** `listRevealJobs` (`GET /lead-finder/reveal-jobs`) lists the
last 30 days.

### 6. Unmask names separately

`unlockNames` — `POST /lead-finder/unlock-names` — **1 credit per lead**, up to 100 leads
per call. Search results mask last names; this is the cheap way to unmask a shortlist
without revealing contact details.

### 7. Export

`exportLeads` (`POST /lead-finder/export`) returns a `jobId`. Poll
`getExportJob` (`GET /lead-finder/export-jobs/{jobId}`), then stream the file with
`downloadExportJob` (`GET /lead-finder/export-jobs/{jobId}/download`), which returns
`text/csv` with `Content-Disposition`.

The CSV endpoints are the only ones that report billing in **response headers** —
`X-Credits-Used` and `X-Credits-Refunded` — because a CSV body has no `meta` object. If
you track spend by parsing `meta.creditsUsed`, you will miss export costs entirely.

A completed export can expire: `410 Gone` on download means re-submit the job.

## Sequence that costs the least

1. `countLeads` → free, iterate on filters
2. `searchLeads` → free preview
3. `unlockNames` on the shortlist → 1 credit each
4. `revealLeads` with `fields: ["email"]` on the shortlist only → 50 credits each
5. `getRevealJob` until complete → free
