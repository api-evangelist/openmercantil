---
name: openmercantil-procurement-watch
description: >-
  Search Spanish public procurement (PLACSP) notices by buyer, supplier, CPV
  sector, province, amount or deadline, and tie awards back to the winning
  company's registry record. Use when asked which public contracts a Spanish
  company has won, what tenders are open in a sector or region, or who the top
  suppliers to a public body are.
api: OpenMercantil Public Procurement API
base_url: https://openmercantil.es
auth: none (anonymous); optional X-API-Key with scope tenders:read for account quota
generated: '2026-08-14'
method: generated
source: openapi/openmercantil-public-procurement-api-openapi.yml
operations:
  - searchTenders
  - getTender
  - getTenderStats
  - listTenderSuppliers
  - getCompanyBySlugContracts
  - getCompanyBySlugGrants
---

# Track Spanish public procurement with OpenMercantil

PLACSP notices and awards, structured with typed monetary amounts. Grants come
from BDNS through the same company routes.

## Search the notice index

```
GET /api/v1/tenders?q=&cpv=&phase=&province=&buyer_nif=&supplier_cif=
    &open_only=&amount_kind=&min_amount_eur=&max_amount_eur=
    &published_from=&published_to=&limit=&cursor=      # searchTenders
```

Every parameter is optional. Useful combinations:

- Open tenders in a sector: `cpv={code}&open_only=1`
- Everything a company won: `supplier_cif={CIF}`
- Everything a public body bought: `buyer_nif={NIF}`
- Value band: `amount_kind=...&min_amount_eur=...&max_amount_eur=...`
- Date window: `published_from=YYYY-MM-DD&published_to=YYYY-MM-DD`

This endpoint is **cursor-paginated** (`cursor`), unlike company search which is
`limit`/`offset`. Follow the returned cursor; do not compute offsets.

A `422 unsupported_filter_combination` means each filter is individually legal
but the pair has no safe indexed combination. Drop one filter or move to the
bulk datasets — do not retry the same combination.

## Read one notice

```
GET /api/v1/tenders/{key}                       # getTender
```

Returns `TenderNotice` with `buyer` and (when awarded) `supplier` as
`TenderParty`, plus typed `amounts` (`TenderMoney`) and lots. A `TenderParty`
carries `company_slug` when the party resolved to a company — follow it into the
company routes to get the registry record.

## Aggregates

```
GET /api/v1/tenders/stats                       # getTenderStats
GET /api/v1/tenders/suppliers?limit=50          # listTenderSuppliers
```

`getTenderStats` carries `geography` and a `data_quality` block. Read
`data_quality` before quoting a figure — it is there because coverage is not
uniform.

## From the company side

```
GET /api/v1/company/{slug}/contracts?limit=50   # getCompanyBySlugContracts
GET /api/v1/company/{slug}/grants?limit=50      # getCompanyBySlugGrants
```

Resolve `{slug}` through `GET /api/v1/search` first — never construct it. Grants
are BDNS subsidy records, a different source from PLACSP contracts; keep them
labelled separately when reporting.

## Caveats you must carry into the answer

- **Only legal persons are exposed as suppliers.** Natural-person suppliers are
  withheld for GDPR reasons, so a supplier list is not exhaustive.
- **Contract modifications are not included.** An award amount is the published
  award, not the final settled cost.
- A `503` on any procurement route is fail-closed: unknown, not zero.
- Honour `Retry-After` on `429`. Free tier is 60/min, 200/day per IP.

## Attribution

Cite PLACSP as the origin and OpenMercantil as the structuring layer, with the
canonical URL, e.g. `https://openmercantil.es/licitacion/{slug}-{key}`. Check
`X-Attribution-Required` on the response.
