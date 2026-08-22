# OpenMercantil (openmercantil)

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

OpenMercantil is an independent public-data API for Spanish company intelligence. It indexes the Boletin Oficial del Registro Mercantil (BORME) and cross-references it with 29+ public sources (CNMV, OEPM, PLACSP, BDNS, OpenSanctions, CCAA gazettes, CNMC, CENDOJ and more) to expose company search, structured company reports, registry event timelines, officer records, CNAE sector navigation, daily summaries, public-procurement rankings, a v1.4 cross-source trust score, and CSV/JSON exports. The public REST API is free, requires no API key, and is rate-limited per IP. The project is informational and does not replace official Registro Mercantil certificates.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Open Data
- Spain
- Company Data
- Business Registry
- BORME
- Public Records
- Spanish Companies
- CIF
- CNAE
- Public Procurement
- PLACSP
- CNMV
- OEPM
- BDNS
- OpenSanctions
- Public-Interest Data
- Spanish Open Data
- REST API
- JSON
- CSV
- Geocoding
- Trust Score
- Registry Timeline
- Daily Summary

## Timestamps

- **Created:** 2026-05-09
- **Modified:** 2026-05-19

## APIs

### OpenMercantil Public API

Public JSON REST API exposing Spanish company search, company reports, registry event timelines, officer records, person reports, daily BORME summaries, CNAE sector navigation, public-procurement rankings, cross-source trust scores, geocoding, exports, integrated public-data source status and service health. Versioned under /api/v1/, no API key required, ~60 req/min/IP rate limit on the anonymous tier, with X-RateLimit-* and Retry-After headers signaling capacity.

- **Human URL:** [https://openmercantil.es/api/documentacion](https://openmercantil.es/api/documentacion)
- **Base URL:** `https://openmercantil.es`

#### Tags

- Search
- Companies
- Persons
- Daily
- Export
- Sectors
- Score
- Sources
- Contracts
- Network
- Geocode
- Stats
- Billing
- System

#### Properties

- [OpenAPI](openapi/openmercantil-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/openmercantil.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/openmercantil.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [OpenAPI](https://openmercantil.es/openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://openmercantil.es/api/documentacion)
- [A P Is J S O N](https://openmercantil.es/apis.json)

## Common Properties

- [Website](https://openmercantil.es/)
- [Documentation](https://openmercantil.es/api/documentacion)
- [A P Is J S O N](https://openmercantil.es/apis.json)
- [Pricing](https://openmercantil.es/precios)
- [Terms of Service](https://openmercantil.es/terminos-de-uso)
- [Support](https://openmercantil.es/soporte)
- [Downloads](https://openmercantil.es/descargas)
- [Git Hub Project](https://github.com/PabloCirre/OpenBorme)
- [JSON Schema](json-schema/openmercantil-company-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/openmercantil-event-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/openmercantil-company-structure.json)
- [J S O N L D Context](json-ld/openmercantil-context.jsonld)
- [Example](examples/openmercantil-search-companies-example.json)
- [Example](examples/openmercantil-get-company-example.json)
- [Example](examples/openmercantil-get-company-events-example.json)
- [Example](examples/openmercantil-health-example.json)
- [Spectral Ruleset](rules/openmercantil-rules.yml)
- [Vocabulary](vocabulary/openmercantil-vocabulary.yml)
- [Plans](plans/openmercantil-plans-pricing.yml)
- [Rate Limits](rate-limits/openmercantil-rate-limits.yml)
- [Fin Ops](finops/openmercantil-finops.yml)
- [L L Ms Txt](https://openmercantil.es/llms.txt)

## Maintainers

**FN:** OpenMercantil
**Email:** social@openmercantil.es
**FN:** Pablo Cirre
**URL:** https://github.com/PabloCirre
