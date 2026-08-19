---
name: openmercantil-risk-screening
description: >-
  Pull documentary risk signals for a Spanish company — sanctions list matches,
  AEAT defaulter listing, embargoes, insolvency proceedings, regulator actions
  and CNMV disclosures — from public sources via OpenMercantil. Use for
  compliance, KYC pre-screening, counterparty checks or OSINT. Never for credit
  scoring.
api: OpenMercantil Risk Signals API
base_url: https://openmercantil.es
auth: none (anonymous); optional X-API-Key with scope companies:read
generated: '2026-08-14'
method: generated
source: openapi/openmercantil-risk-signals-api-openapi.yml, openapi/openmercantil-companies-api-openapi.yml
operations:
  - getCompanyBySlugRiskSignals
  - getCompanyBySlugSanctions
  - getCompanyBySlugAeatMoroso
  - getCompanyBySlugEmbargoes
  - getCompanyBySlugCnmv
  - getCompanyBySlugSources
---

# Screen a Spanish company for documentary risk signals

## Read this before you use the output

These are **documentary signals from public sources**, not a risk rating. The
provider states plainly:

- OpenMercantil does **not** perform credit scoring. The "Indicador documental"
  is an educational algorithmic estimate over public documentary signals, not a
  regulated financial rating.
- A match on an international list (sanctions, ICIJ) **may be homonymy** and does
  not by itself imply an infringement.
- Insolvency proceedings shown may already be concluded, archived or in a final
  phase — the date and state must be verified at source.
- Embargo records may not reflect later resolutions.

For due diligence with legal effect, direct the user to the official source or
an accredited provider. Say so in the answer; do not present these as findings
of fact.

## Step 1 — Resolve the company

```
GET /api/v1/search?q={name or CIF}&limit=5      # getSearch
```

Take the exact CIF match. Never construct a slug.

## Step 2 — Pull the signals

```
GET /api/v1/company/{slug}/risk-signals          # getCompanyBySlugRiskSignals
GET /api/v1/company/{slug}/sanctions             # getCompanyBySlugSanctions
GET /api/v1/company/{slug}/aeat-moroso           # getCompanyBySlugAeatMoroso
GET /api/v1/company/{slug}/embargoes             # getCompanyBySlugEmbargoes
GET /api/v1/company/{slug}/cnmv?limit=50         # getCompanyBySlugCnmv
```

`risk-signals` is the aggregate view across AEPD, CNMC, insolvency, AEAT
defaulters and CENDOJ citations. The others are the per-source detail. CNMV
returns listed-issuer disclosures with a `notice_url` constrained by schema to
a cnmv.es host — follow it for the official record.

Check which sources actually answered for this subject:

```
GET /api/v1/company/{slug}/sources               # getCompanyBySlugSources
```

## Step 3 — Distinguish "no signal" from "not checked"

This is the part agents get wrong.

| Response | Meaning | What to say |
|---|---|---|
| `200` with empty results | Source was queried, nothing matched | "No records found in {source}" |
| `404` | Neutral — absent, natural-person, or quarantined identity | "Not resolvable in OpenMercantil" |
| `503 projection_unavailable` | Fail-closed outage | "Could not be checked" — **never** "clean" |
| `503 legal_layer_unavailable` | Source withheld on licensing grounds | "Not published by OpenMercantil" |

A `503` is UNKNOWN. Reporting an unchecked source as a clean result is the
single most damaging error available in this workflow. Do not cache 503s; they
carry `Cache-Control: no-store`.

## Step 4 — Court decisions

Judgments are **not** exposed. CENDOJ is kept as a citation index only —
metadata plus a link to the official source, per CGPJ Reglamento 3/2010. If the
user wants the text of a ruling, send them to the official CENDOJ search.

## Step 5 — Rate limits and attribution

Free tier is 60 req/min and 200 req/day per IP; the five calls above spend five
of them per subject. Honour `Retry-After` on `429`. Read
`X-Data-Sources` and `X-Attribution-Required` and attribute accordingly —
upstream source terms prevail over OpenMercantil's own CC BY 4.0.

## Corrections

If the user believes a record is wrong, the provider runs a rectification
channel at <https://openmercantil.es/correcciones> with a stated 48–72 hour
response time. Offer it rather than arguing the record.
