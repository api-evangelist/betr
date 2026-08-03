# Betr

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Betr (Betr Holdings, Inc.) is a Miami-based real-money gaming and sports media company founded in 2022 by Joey Levy and Jake Paul on a $50M Series A. It operates a consumer "real money gaming super app" spanning **Betr Picks** (real-money pick'em daily fantasy sports), a **micro-betting sportsbook** (launched in Ohio in January 2023), a **social sportsbook** and **social casino**, **Betr Arcade**, and **Betr Media**.

- Website: https://www.betr.app
- Help center: https://help.betr.app/en/
- Secondary-market listing (harvest source): https://forgeglobal.com/betr_stock/

## API posture

**Betr is business-to-consumer and publishes no public developer API program.** The 2026-07-31
enrichment pass ran full contract discovery against every Betr host and found no OpenAPI, Swagger,
AsyncAPI, GraphQL SDL, MCP server or A2A agent card. Every probe and its HTTP status is recorded in
`apis.yml` under `x-contract-discovery` and in `well-known/betr-well-known.yml`.

| Host | Result |
|---|---|
| `api.betr.app` | Live private backend (Symfony). Anonymous requests return HTTP 500 / 403. No contract. |
| `stage1-backoffice-api-docs.betr.app` | Real staging back-office API docs host, HTTP 403 on every path (internal). |
| `www.betr.app` | Webflow site. `/llms.txt` = 200 (harvested). All `/.well-known/*` = 404. |
| `picks.betr.app` | SPA catch-all — HTTP 200 HTML for every path; all 200s rejected as false positives. |
| `help.betr.app` | Intercom help center. `/llms.txt` = 200 (harvested). `security.txt` = 200 but is **Intercom's** vendor policy. |

## Artifacts

| Path | Type | Method |
|---|---|---|
| `llms/betr-llms.txt` | LLMsTxt | searched — verbatim from https://www.betr.app/llms.txt |
| `llms/betr-help-center-llms.txt` | LLMsTxt | searched — verbatim from https://help.betr.app/llms.txt |
| `well-known/betr-well-known.yml` | (no pointer) | probed — records that Betr publishes **no** first-party `/.well-known/` document |
| `well-known/betr-help-center-intercom-security.txt` | (no pointer) | probed — Intercom's vendor `security.txt`, saved for the record, **not** attributed to Betr |
| `security/betr-domain-security.yml` | DomainSecurity | probed — TLS/HSTS per host, DNSSEC/CAA/SPF/DMARC for `betr.app` |
| `conformance/betr-conformance.yml` | Conformance | searched — observable standards posture + regulatory/responsible-gaming surface |

No `SecurityTxt`, `Security`, `WellKnown` or `Compliance` pointer is emitted: the only `security.txt`
found belongs to Intercom (`Canonical: app.intercom.com`), no first-party `/.well-known/` document
exists, and Betr publishes no trust center or certification page. Recording those would credit Betr
with a posture it does not have.
