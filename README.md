# Betr

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
