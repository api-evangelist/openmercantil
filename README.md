# OpenMercantil (openmercantil)

OpenMercantil is an independent public-data API for Spanish company intelligence. It indexes the Boletin Oficial del Registro Mercantil (BORME) and cross-references it with 29+ public sources (CNMV, OEPM, PLACSP, BDNS, OpenSanctions, CCAA gazettes, CNMC, CENDOJ and more) to expose company search, structured company reports, registry event timelines, officer records, CNAE sector navigation, daily summaries, public-procurement rankings, a v1.4 cross-source trust score, and CSV/JSON exports. The public REST API is free, requires no API key, and is rate-limited per IP. The project is informational and does not replace official Registro Mercantil certificates.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/openmercantil/refs/heads/main/apis.yml)

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
- **Modified:** 2026-05-16

## APIs

### OpenMercantil Public API

Public JSON REST API exposing Spanish company search, company reports, registry event timelines, officer records, person reports, daily BORME summaries, CNAE sector navigation, public-procurement rankings, cross-source trust scores, geocoding, exports, integrated public-data source status and service health. Versioned under `/api/v1/`, no API key required, ~60 req/min/IP rate limit on the anonymous tier, with `X-RateLimit-*` and `Retry-After` headers signaling capacity.

#### Properties

- [OpenAPI](openapi/openmercantil-openapi.yml)
- [Documentation](https://openmercantil.es/api/documentacion)
- [Upstream OpenAPI](https://openmercantil.es/openapi.json)
- [APIs.json](https://openmercantil.es/apis.json)

## Common Properties

- [Website](https://openmercantil.es/)
- [API Documentation](https://openmercantil.es/api/documentacion)
- [APIs.json](https://openmercantil.es/apis.json)
- [Pricing](https://openmercantil.es/precios)
- [Terms Of Use](https://openmercantil.es/terminos-de-uso)
- [Support](https://openmercantil.es/soporte)
- [Downloads](https://openmercantil.es/descargas)
- [GitHub](https://github.com/PabloCirre/OpenBorme)

## Artifacts

### JSON Schema

- [Company Schema](json-schema/openmercantil-company-schema.json)
- [Event Schema](json-schema/openmercantil-event-schema.json)

### JSON Structure

- [Company Structure](json-structure/openmercantil-company-structure.json)

### JSON-LD

- [Context](json-ld/openmercantil-context.jsonld)

### Examples

- [Search Companies](examples/openmercantil-search-companies-example.json)
- [Get Company](examples/openmercantil-get-company-example.json)
- [Get Company Events](examples/openmercantil-get-company-events-example.json)
- [Health](examples/openmercantil-health-example.json)

### Rules

- [Spectral Ruleset](rules/openmercantil-rules.yml)

### Capabilities

- [Spanish Company Intelligence](capabilities/spanish-company-intelligence.yaml)

### Vocabulary

- [OpenMercantil Vocabulary](vocabulary/openmercantil-vocabulary.yml)

### Plans

- [Plans And Pricing](plans/openmercantil-plans-pricing.yml)

### Rate Limits

- [Rate Limits](rate-limits/openmercantil-rate-limits.yml)

### FinOps

- [FinOps Framework](finops/openmercantil-finops.yml)

## Maintainers

**FN:** OpenMercantil
**Email:** social@openmercantil.es

**FN:** Pablo Cirre
**URL:** https://github.com/PabloCirre
