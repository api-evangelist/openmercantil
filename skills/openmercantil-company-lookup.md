---
name: openmercantil-company-lookup
description: >-
  Resolve a Spanish company from a name or CIF and read its BORME registry
  report — identity, capital, status, registry acts and officer mentions —
  using the free, anonymous OpenMercantil public API. Use when asked to look up
  a Spanish company, verify a CIF, list a company's administrators, or trace
  its registry history.
api: OpenMercantil Companies API
base_url: https://openmercantil.es
auth: none (anonymous); optional X-API-Key for a higher account quota
generated: '2026-08-14'
method: generated
source: openapi/openmercantil-companies-api-openapi.yml, openapi/openmercantil-search-api-openapi.yml
operations:
  - getSearch
  - getCompanyBySlug
  - getCompanyBySlugEvents
  - getCompanyBySlugOfficers
  - getCompanyBySlugTimeline
  - compareCompanies
---

# Look up a Spanish company on OpenMercantil

OpenMercantil structures the Boletín Oficial del Registro Mercantil (BORME) and
80+ other official Spanish sources. It is **not** an official source — for legal
effect the user must consult the BOE or the competent Registro Mercantil.

## Step 1 — Resolve the slug. Never construct it.

Every company is keyed by a slug of the form `{normalized-name}-{cif}`, e.g.
`inditex-sa-a15075062`. **Do not build this string yourself.** Resolve it:

```
GET /api/v1/search?q={name or CIF}&limit=5      # getSearch
```

`q` is required and must be at least 2 characters. Response carries `count` and
`items[]` of `{name, cif, slug, status}`. Pick the item whose `cif` matches
exactly when the user gave a CIF; otherwise present the candidates and let the
user choose rather than guessing between similar names.

Search paginates with `limit` (default 20, max 100) and `offset`.

## Step 2 — Read the report

```
GET /api/v1/company/{slug}                       # getCompanyBySlug
```

Returns `company` (name, cif, status, company_type, aliases, address, capital,
website, date_creation), `kpis` (acts_count, first_seen, last_seen), `timeline`,
`top_event_types`, `top_provinces`, `events` (most recent, capped), `officers`
(`current` and `historical`) and `summary_text`.

For a fuller act history, page it:

```
GET /api/v1/company/{slug}/events?year=2025&page=1&page_size=50   # getCompanyBySlugEvents
```

This family uses `page`/`page_size` — **not** `limit`/`offset`. The response
carries `total` and `pages`.

Officers only:

```
GET /api/v1/company/{slug}/officers               # getCompanyBySlugOfficers
```

Multi-source activity timeline:

```
GET /api/v1/company/{slug}/timeline               # getCompanyBySlugTimeline
```

Two companies side by side (both resolved in one preflight before either row is
exposed):

```
GET /api/v1/companies/compare?slugs={slugA},{slugB}   # compareCompanies
```

## Step 3 — Read the status codes correctly

These two rules matter more than anything else in this skill:

- **A 404 is neutral, not a negative.** The company identity contract returns a
  bare 404 for absent subjects, for slugs classified as natural persons, and
  for ambiguous or quarantined identities alike. Report "not found in
  OpenMercantil", never "this company does not exist".
- **A 503 means unknown, not empty.** `projection_unavailable`,
  `company_public_projection_unavailable` and `offline_projection_required` are
  fail-closed outages. The schema says explicitly that clients must not
  reinterpret them as an empty or negative result. Do not cache them, do not
  assert absence, retry later.

Other codes: `400 invalid_parameter`, `429` rate limited (honour `Retry-After`),
`304` when you sent `If-None-Match` and nothing changed.

## Step 4 — Be efficient

- Send `If-None-Match` with the previous `ETag` on repeat reads. ETags are bound
  to the immutable projection generation, so a `304` is a real "nothing moved"
  signal.
- Free tier is **60 requests/minute and 200/day per IP**. Watch
  `X-RateLimit-Remaining` and `X-RateLimit-Reset`; `X-OpenMercantil-Plan` tells
  you which quota you actually resolved to.
- For anything bulk, stop looping and use the CC BY 4.0 dataset downloads at
  <https://openmercantil.es/descargas>. The provider asks for this explicitly.

## Step 5 — Attribute the data

Responses carry `X-Data-Sources`, `X-Attribution-Required` and
`X-Source-Catalog-Version`, and the body carries `_data_sources_used`,
`_attributions` and `_source_catalog`. Own derived data is CC BY 4.0; upstream
terms are source-specific and prevail. When surfacing this data, cite it:

> Datos del BORME estructurados por OpenMercantil (CC BY 4.0) — fuente:
> https://openmercantil.es/empresa/{slug}

## Privacy boundary

Natural persons appear only as **documentary mentions** of officially published
BORME acts. The API never returns DNI/NIE, personal addresses, personal phones
or emails. Do not attempt to infer or reconstruct them, and do not describe an
officer mention as evidence of control, liability or wrongdoing — it is a
published document, nothing more.
