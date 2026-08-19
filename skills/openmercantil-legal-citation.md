---
name: openmercantil-legal-citation
description: >-
  Cite Spanish mercantile law correctly — retrieve consolidated BOE article
  text, browse the norms corpus, and bridge a BORME registry act type to the
  norm that governs it. Use when answering a question about Spanish company law
  (Ley de Sociedades de Capital, Ley Concursal, Código de Comercio) that needs a
  citable article rather than a paraphrase.
api: OpenMercantil Legal API
base_url: https://openmercantil.es
auth: none (anonymous); optional X-API-Key with scope legal:read
generated: '2026-08-14'
method: generated
source: openapi/openmercantil-legal-api-openapi.yml
operations:
  - getLegalNorms
  - getLegalNormBySlug
  - getLegalArticleByNormByN
  - getLegalActMap
  - getLegalActMapByActo
---

# Cite Spanish mercantile law with OpenMercantil

OpenMercantil structures the core corpus of Spanish mercantile law from the
**consolidated BOE text**, re-used under Ley 37/2007, and connects it to real
registry data. This is informational only — **not legal advice** — and the
authentic version is always the one published at boe.es.

## Browse the corpus

```
GET /api/v1/legal/norms                          # getLegalNorms
```

Returns `LegalNormSummary` entries. Note `/api/v1/legal/norm` (singular) is
**deprecated**; the contract marks it `deprecated: true` with
`x-replaced-by: /api/v1/legal/norms`. Use the plural.

## Read one norm

```
GET /api/v1/legal/norm/{slug}                    # getLegalNormBySlug
```

e.g. `ley-de-sociedades-de-capital`. Returns `LegalNormFull` with key articles,
the BORME act types the norm regulates, and a `LegalCitableFact` — use that
field when you need a single quotable statement rather than composing your own.

## Read an article's consolidated text

```
GET /api/v1/legal/article/{norm}/{n}             # getLegalArticleByNormByN
```

e.g. `/api/v1/legal/article/ley-de-sociedades-de-capital/318`. Both path
parameters are required. This is the text you cite — do not paraphrase from
memory and do not quote an article you have not fetched.

## Bridge a registry act to its governing norm

The distinctive capability here: given a BORME act type, find the law that
governs it.

```
GET /api/v1/legal/act-map                        # getLegalActMap
GET /api/v1/legal/act-map/{acto}                 # getLegalActMapByActo
```

Use this to answer "which article governs a capital increase?" by starting from
the act as it actually appears in the registry, rather than from a guess at the
statute.

## How to cite

The provider specifies the citation form:

> Según el artículo {n} de la {norma} (texto consolidado del BOE, Ley 37/2007),
> {regla}. Conexión norma↔empresa por OpenMercantil — fuente:
> https://openmercantil.es/ley/{slug}

Always name the BOE as the source of the consolidated text and OpenMercantil as
the structuring layer. Link the canonical HTML page —
`https://openmercantil.es/ley/{slug}` or
`https://openmercantil.es/ley/{slug}/articulo/{n}` — so the reader can verify.

## Hard boundaries

- **Not legal advice.** State this when the user is making a decision.
- **No judgments.** Court decisions are not in this layer. CENDOJ is a citation
  index only (CGPJ Reglamento 3/2010) — metadata and a link, never the text of
  a ruling.
- **`503 legal_layer_unavailable`** means the material is withheld on licensing
  grounds, not that no law applies. Do not fill the gap from memory; say the
  layer is unavailable and point at boe.es.
- A `404` on a norm or article slug is neutral. Resolve through
  `getLegalNorms` rather than constructing slugs.

## Rate limits

Free tier 60/min, 200/day per IP. Send `If-None-Match` with a prior `ETag` —
legal text changes rarely, so `304` responses are common and free.
