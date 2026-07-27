# Southern Company (southern-company)

Southern Company is an Atlanta-headquartered energy holding company and one of the largest producers of electricity in the United States, serving approximately 9 million electric and natural gas customers through Alabama Power, Georgia Power, Mississippi Power, Southern Power, Southern Company Gas (Atlanta Gas Light, Nicor Gas, Virginia Natural Gas, Chattanooga Gas), Southern Nuclear, PowerSecure, Southern Linc and Southern Telecom. It sits at the vertically-integrated regulated-utility layer of the value chain — it owns generation, transmission and distribution, operates its own balancing authority rather than belonging to an ISO/RTO, and runs a FERC-approved bid-based energy auction for wholesale power in the Southeast. Its API posture is honestly closed on both sides of the sector's two-speed split. There is no consumer data mandate in Alabama, Georgia or Mississippi and Southern Company does not implement Green Button Download My Data or Connect My Data, is not listed by the Green Button Alliance, and publishes no ESPI endpoint — a customer can only export their own interval data as a spreadsheet after logging into My Power Usage, and a third party gets billing history only through a signed paper release form. On the market side the FERC-required auction clearing prices and weighted-average hour-ahead transaction prices are posted as public web pages, but they are JavaScript-rendered HTML with no CSV, no feed and no API behind them. A production Apigee API gateway is live at api.southernco.com and developer.southernco.com resolves behind an Imperva edge, so the platform machinery exists internally, but no proxy, no specification and no documentation are published to anyone outside the company.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/southern-company/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/southern-company/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Utilities
- Electricity
- Gas
- Grid
- Smart Metering
- Nuclear
- Energy Markets
- Renewables

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

No public, documented APIs were found. Southern Company publishes no developer portal, no API reference, and no machine-readable API specification of any kind.

## Energy Data Posture

- **Home market:** United States
- **Mandate regime:** none — no US federal or state consumer energy-data mandate applies to Southern Company's service territories (Alabama, Georgia, Mississippi for electricity; Georgia, Tennessee, Illinois, Virginia for gas)
- **Mandate status:** none — not `green-button-voluntary` either, because no voluntary adoption was found. No Southern Company entity appears on the Green Button Alliance certification page, and no Download My Data or Connect My Data affordance exists on any probed property
- **Data standard:** no standard reference found — no Green Button/ESPI, CDR, IEEE 2030.5, OpenADR, OCPP/OCPI or IEC CIM reference on any public surface
- **Consumer data API:** no — a third party obtains billing history only via a signed paper "Release of Billing History to Third Party" form; customers export their own interval data to a spreadsheet from the login-walled My Power Usage portal
- **Market data open:** no — FERC-required auction clearing prices and weighted-average hour-ahead transaction prices are posted anonymously as web pages, but those pages are Adobe AEM chrome with no CSV, XLS, JSON, feed or API behind them. Southern Company is its own balancing authority, not an ISO/RTO
- **Access gate:** customer-account-required — no signup, no application, no keys, no sandbox, no partner program
- **Auth model:** none published. `/.well-known/openid-configuration` returns 404 on both `www.southerncompany.com` and `customerservice2.southerncompany.com`. Customer portals use a session/JWT flow issued by `webauth.southernco.com`, which is a web-application login, not a developer auth model

## Notable Findings

- **A live gateway with nothing on it.** `api.southernco.com` answers every probed path with the Apigee Edge fault `messaging.adaptors.http.flow.ApplicationNotFound` — a production API management platform with no published proxy. `developer.southernco.com` resolves but returns an Imperva bot-challenge 503 and never serves content, so it is not recorded as a developer portal.
- **A homonym trap.** Georgia Power's "Developers Portal" is for real-estate and construction developers — rate schedules, meter base pickup, wiring approval. It has no API, no data feed and no developer keys.
- **The only programmatic access is unofficial.** A community Node.js library reverse-engineers the customer login flow against `webauth.southernco.com` and `customerservice2.southerncompany.com`. It proves internal APIs exist; it is not a published API and is deliberately excluded from `apis.yml`.
- **EIX is unverified.** A third-party vendor page claims a "Southern Company Energy Information eXchange (EIX)" API platform is in development. No Southern Company source, host or documentation for it was found. A vendor page is not an implementation.

Full probe log with HTTP status for every URL is in [review.yml](review.yml).

## Artifacts

Enrichment round 2026-07-27. Every artifact below records what was probed, including the absences — nothing here is inferred.

- [well-known/southern-company-well-known.yml](well-known/southern-company-well-known.yml) — 22 `/.well-known/` probes across 5 hosts, **0 documents found**. `webauth.southernco.com` answers the OIDC and OAuth discovery paths with an HTTP 302 into an ASP.NET `/FriendlyError.html`, not with metadata. No `WellKnown` pointer is wired, because there is no catalog to point at.
- [security/southern-company-domain-security.yml](security/southern-company-domain-security.yml) — TLS/HSTS for five hosts and DNSSEC/CAA/SPF/DMARC for both registrable domains. Every host presents the same shared Imperva DV certificate (`CN=imperva.com`); HSTS `max-age` is inconsistent across the estate (86,400s on the API gateway, 31,536,000s on the corporate site); no DNSSEC and no CAA on either domain; SPF and DMARC `p=reject` on both.
- [conformance/southern-company-conformance.yml](conformance/southern-company-conformance.yml) — the standards a US utility of this size could adopt, each evaluated on probe evidence. Green Button/ESPI, IEEE 2030.5, OpenADR, OCPP/OCPI, IEC CIM, OAuth 2.0, OIDC, RFC 9116 and RFC 9727 all read `false`. The one `true` is the FERC market-disclosure obligation — met with HTML, not with data.
- [packages/southern-company-packages.yml](packages/southern-company-packages.yml) — **zero official SDKs** in any registry, and no GitHub organization. Two community npm libraries are recorded with `official: false`.
- [llms/southern-company-llms.txt](llms/southern-company-llms.txt) — generated agent-facing summary; Southern Company serves no `llms.txt` of its own (404).

No `openapi/`, `asyncapi/`, `graphql/`, `mcp/`, `skills/`, `authentication/`, `scopes/`, `errors/` or `lifecycle/` artifacts exist, because there is no contract, event surface, auth model or lifecycle policy published to derive them from. No vulnerability-disclosure programme and no trust centre were found (`vdp=none trust=none`).

## Common Properties

- [Website](https://www.southerncompany.com/)
- [About](https://www.southerncompany.com/about.html)
- [Blog](https://www.southerncompany.com/newsroom.html)
- [Support](https://customerservice2.southerncompany.com/CustService/Overview?mnuOpco=GPC)
- [Login](https://customerservice2.southerncompany.com/)
- [Contact](https://www.southerncompany.com/contact-us.html)
- [Privacy Policy](https://www.southerncompany.com/privacy-statement.html)
- [Terms of Service](https://www.southerncompany.com/terms-and-conditions.html)
- [Investors](https://investor.southerncompany.com/)
- [Careers](https://southerncompany.jobs/)
- [Sustainability](https://www.southerncompany.com/sustainability.html)
- [Reports](https://www.southerncompany.com/solutions/sustainability/data-downloads-reports.html)
- [LinkedIn](https://www.linkedin.com/company/southern-company)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
