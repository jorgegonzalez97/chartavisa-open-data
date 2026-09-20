---
license: cc-by-4.0
language:
  - en
pretty_name: Charta Visa Travel Authorization Data
tags:
  - travel
  - visa
  - immigration
  - government
  - time-series
size_categories:
  - n<1K
---

# Charta Visa Travel Authorization Data

Open data on travel authorizations (ESTA, UK ETA, ETIAS, Canada eTA, US B1/B2 visa): which nationality needs which product, the government fee in its own currency, validity, processing, the official government source for every row, the 2026 'Cost of Crossing Borders' report tables, and a monthly time series of U.S. visitor-visa interview wait times as published by the U.S. Department of State.

> Charta Visa is an independent private service, not a government website. Government fees are stated separately and paid to the authorities in full.

Published by [Charta Visa](https://chartavisa.com) — see the [research hub](https://chartavisa.com/research) for the reports built on this data and the [developer docs](https://chartavisa.com/developers) for the live API and MCP server. Licensed **CC BY 4.0** (see `LICENSE`). Machine-readable metadata: `croissant.json` (Croissant 1.0 / schema.org Dataset), `CITATION.cff`.

## Files

| File | Vintage | What it is |
|---|---|---|
| `visa-requirements.csv` / `.json` | 2026-06-01 | 386 rows — 195 nationalities × the destinations Charta Visa serves (US, UK, Canada, Schengen/ETIAS). Product, government fee + currency, service availability, processing, validity, and the **official government source URL for every row**. |
| `entry-cost-2026.csv` | 2026-06-01 | The tables behind [The Cost of Crossing Borders — 2026](https://chartavisa.com/research/cost-of-crossing-borders-2026): fee history per authorization and the per-nationality authorization burden in USD. Two sections, each with its own header row; `#` lines are comments. |
| `us-visa-wait-times/<asOf>.json` | monthly | One snapshot per U.S. Department of State vintage of the *Global Visa Wait Times* table (B1/B2 next-available appointment and average wait, per consular post). Files are never rewritten, so the folder is a time series. Latest: `2026-07-28.json` (241 posts, source last updated 2026-06-18). |
| `us-visa-wait-times/index.json` | — | Manifest of the snapshots above (asOf, source vintage, post count). |

Live copies of the current files are also served from the site: [visa-requirements.csv](https://chartavisa.com/api/research/visa-requirements.csv), [visa-requirements.json](https://chartavisa.com/api/research/visa-requirements), [entry-cost-2026.csv](https://chartavisa.com/api/research/entry-cost), [latest wait times](https://chartavisa.com/api/research/us-visa-wait-times).

## Method and honesty notes

- **Derived, not hand-typed.** Every row is generated from the same registry Charta Visa's website renders from (`VISA_REGISTRY`, the eligibility engine, and the per-product official-source map), by `scripts/export-datasets.mjs` in the app repository. If the site changes, the data changes with it.
- **Government fees are the authority's published fee**, in the authority's currency. Charta Visa's own service fee is never included in any file.
- **Wait times are transcribed, never estimated.** Non-numeric published values (`NA`, `< 0.5 Month`) keep their raw string and get `null` for the day count. Months are the Department's 30-day increments.
- **ETIAS is pre-launch** (`service_available = false`): the EU has not opened the portal; rows carry the announced fee and validity for reference.
- Files are deterministic (sorted rows, no generation timestamps), so a diff between two releases is a real data change.

## How to cite

Charta Visa (2026). *Charta Visa Travel Authorization Data* [Data set]. https://github.com/jorgegonzalez97/chartavisa-open-data (DOI: pending first Zenodo release)

A DOI is minted by Zenodo for every GitHub release of this repository (tags `data-YYYY-MM-DD`); cite the version DOI for the release you used, or the concept DOI for the series. `CITATION.cff` carries the same reference in machine-readable form (GitHub shows a *Cite this repository* button from it).

## Mirrors

- GitHub (source of the releases + DOI): https://github.com/jorgegonzalez97/chartavisa-open-data
- Hugging Face: https://huggingface.co/datasets/chartavisa/travel-authorization-data (`chartavisa/travel-authorization-data`)
- Kaggle: https://www.kaggle.com/datasets/jorgegonzalezl/travel-authorization-data

## Updates

Regenerated weekly and on every change to the underlying registries. The wait-times snapshot is refreshed monthly when the State Department republishes its table.

Questions or corrections: support@chartavisa.com · https://chartavisa.com/contact
