# Enrich (enrich-so)

Enrich (enrich.so) is a person and company data enrichment API for B2B go-to-market, sales, and web intelligence teams. From a single REST interface it resolves a professional profile from an email address (reverse email lookup), finds and verifies professional email addresses, finds mobile and phone numbers, resolves a company and geolocation from an IP address, scrapes LinkedIn company followers, and searches a lead-finder database of people and organizations for contact discovery and lead enrichment.

**Access model:** Commercial, closed-source SaaS — there is no self-hostable component. Access requires an Enrich account and an API key (prefixed `sk_`) created in the dashboard at `https://dash.enrich.so/dashboard/api-keys`, passed via the `x-api-key` header or as an `Authorization: Bearer` token. Every endpoint shares the base URL `https://dev.enrich.so/api/v3` and is metered against a prepaid credit balance; unsuccessful ("not found") lookups are refunded. New accounts receive a one-time grant of free credits.

**Grounding note:** The single-lookup endpoints below, their HTTP methods, and their credit costs are confirmed from the live Enrich documentation. The batch / progress / results sub-paths are modeled on Enrich's documented submit → poll → results pattern and are flagged as modeled in `openapi/enrich-so-openapi.yml` and `review.yml`; reconcile them against the current docs before code generation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/enrich-so/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/enrich-so/refs/heads/main/apis.yml)

## Tags

- Data Enrichment
- Contact Discovery
- Web Intelligence
- B2B Data
- Lead Enrichment
- Email Finder
- Email Verification
- Phone Numbers
- LinkedIn
- Reference Data

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Enrich Person Enrichment API

Reverse email lookup that returns a person's professional profile — name, headline, current company, position history, education, and skills — from just an email address, with a matching batch endpoint for bulk enrichment. Confirmed endpoint `POST /reverse-lookup/lookup` at 10 credits per successful lookup (not charged when no profile is found).

- **Human URL:** [https://doc.enrich.so/look-up-a-professional-profile-by-email-27483203e0](https://doc.enrich.so/look-up-a-professional-profile-by-email-27483203e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Person Enrichment
- Contact Discovery
- Reverse Email Lookup
- LinkedIn
- Web Intelligence

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/look-up-a-professional-profile-by-email-27483203e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Enrich Email Finder API

Finds a person's professional email address from their first name, last name, and company domain, with a batch variant plus progress and results endpoints. Confirmed endpoint `POST /email-finder` at 10 credits per successful find (not charged when `found` is false).

- **Human URL:** [https://doc.enrich.so/find-a-professional-email-27483195e0](https://doc.enrich.so/find-a-professional-email-27483195e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Email Finder
- Contact Discovery
- B2B Data

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/find-a-professional-email-27483195e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Enrich Email Verification API

Validates a single email address for deliverability, returning a status of valid, invalid, or risky along with confidence, mail provider, and catch-all domain detection, plus a batch validation flow. Confirmed endpoint `POST /email-validation` at 1 credit per request (not charged when the result is risky).

- **Human URL:** [https://doc.enrich.so/validate-a-single-email-27483191e0](https://doc.enrich.so/validate-a-single-email-27483191e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Email Verification
- Deliverability
- Data Quality

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/validate-a-single-email-27483191e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Enrich Phone Finder API

Finds phone and mobile numbers associated with a person from their email address or LinkedIn profile URL, with a bulk variant plus progress and results endpoints. Confirmed endpoint `GET /reverse-lookup/phones` at 500 credits per successful lookup (not charged when no numbers are found).

- **Human URL:** [https://doc.enrich.so/find-phone-numbers-27483199e0](https://doc.enrich.so/find-phone-numbers-27483199e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Phone Numbers
- Mobile Finder
- Contact Discovery

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/find-phone-numbers-27483199e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Enrich Company Intelligence API

Company-level web intelligence — resolve a company, organization, and geolocation from an IPv4/IPv6 address (`POST /ip-to-company`, 100 credits, results cached 7 days), scrape LinkedIn company followers asynchronously with filtering by location, title, department, and seniority (`POST /company-follower`), find employees at a company, and suggest company names.

- **Human URL:** [https://doc.enrich.so/resolve-company-from-ip-35511038e0](https://doc.enrich.so/resolve-company-from-ip-35511038e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Company Enrichment
- Web Intelligence
- B2B Data
- IP Intelligence
- LinkedIn

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/resolve-company-from-ip-35511038e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Enrich Lead Finder API

Lead-finder search across a database of people and organizations with roughly 135 filter fields (person attributes, firmographics, and technology stack), lead counting and estimation, saved searches, and asynchronous reveal/enrich of contact email and phone. Confirmed endpoints `POST /lead-finder/search` (first 3 pages / 75 results free, then 1 credit per result) and `POST /lead-finder/reveal` (50 credits email, 525 phone, 575 both).

- **Human URL:** [https://doc.enrich.so/search-leads-28165853e0](https://doc.enrich.so/search-leads-28165853e0)
- **Base URL:** `https://dev.enrich.so/api/v3`

#### Tags

- Lead Enrichment
- Prospecting
- Contact Discovery
- B2B Data
- ICP

#### Properties

- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [API Reference](https://doc.enrich.so/search-leads-28165853e0)
- [OpenAPI](openapi/enrich-so-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/enrich-so.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/enrich-so.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Authentication](authentication/enrich-so-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/enrich-so)
- [Website](https://www.enrich.so)
- [Documentation](https://doc.enrich.so/introduction-1951028m0)
- [Plans](plans/enrich-so-plans-pricing.yml)
- [Rate Limits](rate-limits/enrich-so-rate-limits.yml)
- [Fin Ops](finops/enrich-so-finops.yml)
- [Blog](https://www.enrich.so/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
