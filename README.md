# OpenMercantil (openmercantil)

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
