# Enrich

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Enrich (enrich.so), operated by Enrich Labs, is a person and company data enrichment API for B2B go-to-market, sales, and web intelligence teams. From a single REST interface at https://dev.enrich.so/api/v3 it resolves a professional profile from an email address (reverse email lookup), finds and verifies professional email addresses, finds mobile and phone numbers, resolves a company and geolocation from an IP address, searches a lead-finder database of people and organizations, finds employees at a company, and scrapes LinkedIn company followers. Fifty-one operations across nine products, every one of them metered against a single prepaid credit balance and refunded when a lookup finds nothing. Every bulk product follows one submit/poll/results shape with reserve-and-settle billing, ten typed webhook callbacks, RFC 9457 problem details on every error, and official TypeScript and Go SDKs. Enrich also operates a first-party remote MCP server at mcp.enrich.so with OAuth 2.0 and dynamic client registration.

**Areas:** Data Enrichment · Contact Discovery · Web Intelligence · B2B Data · Lead Enrichment · Email Finder · Email Verification · Phone Numbers · People Search · IP Intelligence · LinkedIn · Reference Data

## Enrich on APIs.io

Everything profiled for Enrich is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/enrich-so/](https://apis.io/providers/enrich-so/)** — or go straight to one of the APIs or properties below.

### APIs (18)

- [Enrich Email Finder API](https://apis.io/apis/enrich-so/enrich-so-email-finder-api/) — Find a professional email from a first name, last name and company domain, single or in batches of up to 500,000 leads.
- [Enrich Lead Finder API](https://apis.io/apis/enrich-so/enrich-so-lead-finder-api/) — Search, count, reveal, enrich, unlock and export leads across people and organizations, with saved searches and asynchronous reveal and export jobs.
- [Enrich Phone Finder API](https://apis.io/apis/enrich-so/enrich-so-phone-finder-api/) — Find phone and mobile numbers for a person from an email address or profile URL, single or in bulk.
- [Enrich Teams API](https://apis.io/apis/enrich-so/enrich-so-teams-api/) — List team members and manage pending team invitations for the organization behind the API key.
- [Enrich People Search API](https://apis.io/apis/enrich-so/enrich-so-people-search-api/) — Find employees at a company and run cascading ICP (ideal customer profile) people searches.
- [Enrich Authentication API](https://apis.io/apis/enrich-so/enrich-so-authentication-api/) — The Authentication API from Enrich — 1 operation(s) for authentication.
- [Enrich Company Followers API](https://apis.io/apis/enrich-so/enrich-so-company-followers-api/) — The Company Followers API from Enrich — 7 operation(s) for company followers.
- [Enrich Company Followers/Count Estimation API](https://apis.io/apis/enrich-so/enrich-so-company-followers-count-estimation-api/) — The Company Followers/Count Estimation API from Enrich — 2 operation(s) for company followers/count estimation.
- [Enrich Email Validation API](https://apis.io/apis/enrich-so/enrich-so-email-validation-api/) — The Email Validation API from Enrich — 4 operation(s) for email validation.
- [Enrich API](https://apis.io/apis/enrich-so/enrich-so-enrich-api/) — The Enrich API from Enrich — 1 operation(s) for enrich.
- [Enrich IP to Company API](https://apis.io/apis/enrich-so/enrich-so-ip-to-company-api/) — The IP to Company API from Enrich — 4 operation(s) for ip to company.
- [Enrich Reverse Email Lookup API](https://apis.io/apis/enrich-so/enrich-so-reverse-email-lookup-api/) — The Reverse Email Lookup API from Enrich — 4 operation(s) for reverse email lookup.
- [Enrich Wallets API](https://apis.io/apis/enrich-so/enrich-so-wallets-api/) — The Wallets API from Enrich — 2 operation(s) for wallets.
- [Enrich Account API](https://apis.io/apis/enrich-so/enrich-so-account-api/) — Credit balance and transaction history.
- [Enrich Company Intelligence API](https://apis.io/apis/enrich-so/enrich-so-company-intelligence-api/) — IP-to-company resolution and LinkedIn company-follower scraping.
- [Enrich Email Verification API](https://apis.io/apis/enrich-so/enrich-so-email-verification-api/) — Validate email addresses for deliverability.
- [Enrich Person Enrichment API](https://apis.io/apis/enrich-so/enrich-so-person-enrichment-api/) — Reverse email lookup returning a person's professional profile.
- [Enrich Webhooks API](https://apis.io/apis/enrich-so/enrich-so-webhooks-api/) — The Webhooks API from Enrich — 0 operation(s) for webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Enrich So Webhooks](https://apis.io/asyncapis/enrich-so/enrich-so-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [enrich-so-mcp.yml](https://apis.io/servers/enrich-so/enrich-so-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Enrich So Agentic Access](https://apis.io/agentic-access/enrich-so/enrich-so-agentic-access/)

#### Collections (10)

Postman and Open Collection request collections.

- [Enrich API](https://apis.io/collections/enrich-so/open-enrich-so/)
- [Enrich Account API](https://apis.io/collections/enrich-so/open-enrich-so-account-api/)
- [Enrich Company Intelligence API](https://apis.io/collections/enrich-so/open-enrich-so-company-intelligence-api/)
- [Enrich Email Finder API](https://apis.io/collections/enrich-so/open-enrich-so-email-finder-api/)
- [Enrich Email Verification API](https://apis.io/collections/enrich-so/open-enrich-so-email-verification-api/)
- [Enrich Lead Finder API](https://apis.io/collections/enrich-so/open-enrich-so-lead-finder-api/)
- [Enrich People Search API](https://apis.io/collections/enrich-so/open-enrich-so-people-search-api/)
- [Enrich Person Enrichment API](https://apis.io/collections/enrich-so/open-enrich-so-person-enrichment-api/)
- [Enrich Phone Finder API](https://apis.io/collections/enrich-so/open-enrich-so-phone-finder-api/)
- [Enrich Teams API](https://apis.io/collections/enrich-so/open-enrich-so-teams-api/)

#### Overlays (9)

OpenAPI overlays, including conversational phrasing for each operation.

- [Enrich So Account Overlay](https://apis.io/overlays/enrich-so/enrich-so-account-overlay/)
- [Enrich So Company Intelligence Overlay](https://apis.io/overlays/enrich-so/enrich-so-company-intelligence-overlay/)
- [Enrich So Email Finder Overlay](https://apis.io/overlays/enrich-so/enrich-so-email-finder-overlay/)
- [Enrich So Email Verification Overlay](https://apis.io/overlays/enrich-so/enrich-so-email-verification-overlay/)
- [Enrich So Lead Finder Overlay](https://apis.io/overlays/enrich-so/enrich-so-lead-finder-overlay/)
- [Enrich So People Search Overlay](https://apis.io/overlays/enrich-so/enrich-so-people-search-overlay/)
- [Enrich So Person Enrichment Overlay](https://apis.io/overlays/enrich-so/enrich-so-person-enrichment-overlay/)
- [Enrich So Phone Finder Overlay](https://apis.io/overlays/enrich-so/enrich-so-phone-finder-overlay/)
- [Enrich So Teams Overlay](https://apis.io/overlays/enrich-so/enrich-so-teams-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Enrich So Authentication](https://apis.io/security/enrich-so/enrich-so-authentication/)
- [Enrich So Domain Security](https://apis.io/security/enrich-so/enrich-so-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Enrich So Scopes](https://apis.io/scopes/enrich-so/enrich-so-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Enrich So Plans Pricing](https://apis.io/plans/enrich-so/enrich-so-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Enrich So Rate Limits](https://apis.io/rate-limits/enrich-so/enrich-so-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Enrich So Finops](https://apis.io/finops/enrich-so/enrich-so-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.enrich.so)
- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [Getting started](https://doc.enrich.so/quickstart-1951029m0)
- [API reference](https://doc.enrich.so/api-reference-1951025m0)
- [Pricing](https://doc.enrich.so/credits-pricing-1951027m0)
- [Sign up](https://dash.enrich.so)
- [Blog](https://www.enrich.so/blog)
- [Terms of service](https://www.enrich.so/terms-of-service)
- [Privacy policy](https://www.enrich.so/privacy-policy)
- [GitHub](https://github.com/maximiseai)
- [Status](https://status.enrich.so)

## API Evangelist rating

**Kin Score 62.5** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 61.9 |
| Contract governance | 18.2 |
| Operational transparency | 73.7 |
| Developer ergonomics | 62.5 |
| Access clarity | 65.8 |

**Agent readiness 44.6** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/enrich-so/](https://apis.io/providers/enrich-so/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Enrich: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/enrich-so/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
