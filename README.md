# Centralized vs Federated Survival Analysis of Routine HIV Data

Documentation and code for comparing **centralized** and **federated (DataSHIELD)** survival analyses of harmonized routine HIV programme data from three sites:

| Country  | Data source | Role in analysis |
|----------|-------------|------------------|
| Kenya    | LVCT Health | Full analysis |
| Uganda   | IDI (Infectious Diseases Institute) | Full analysis |
| Cameroon | DGH (Douala General Hospital) | Descriptives only for VL suppression analysis |

Part of the APHRC proof-of-federation work (DSWB consortium). It builds on the completed mental-health federated analysis (DataSHIELD + OMOP CDM).

## Research questions

1. **Time from ART initiation to viral-load (VL) suppression**, with death treated as a competing event.
2. **Time to death** after ART initiation.

The cohort is patients initiating ART from 2020 onwards. The comparison asks whether federated analysis gives the same estimates as pooled centralized analysis. It also asks whether DataSHIELD disclosure controls (small-cell suppression, modified survival curves) change the conclusions that would be drawn.

## Workflow

```
Site raw data (LVCT, IDI, DGH)
        │
        ▼
[1] Harmonisation ──── Track A: manual CSV standardisation against shared data dictionary
        │              Track B: OMOP CDM ETL (parallel; see docs/02)
        ▼
[2] Survival data preparation (R) ── counting-process + interval-censored files per site
        │
        ├──────────────► [3a] Centralized analysis in R (baseline / reference results)
        │
        ▼
[3b] Upload to Opal ──► DataSHIELD + dsSurvival federated analysis
        │
        ▼
[4] Comparison: descriptives, survival estimates, model coefficients, disclosure-control effects
```

## Repository layout

```
├── docs/
│   ├── 01-study-overview.md
│   ├── 02-data-harmonisation.md
│   ├── 03-survival-data-preparation.md
│   ├── 04-opal-datashield-setup.md
│   ├── 05-analysis-plan.md
│   └── 06-centralized-vs-federated-comparison.md
├── R/                    # analysis scripts (to be added; see R/README.md)
├── docker/rock-survival/ # Rock server image with dsSurvival
├── data/                 # NOT tracked: no patient-level data in this repo
└── outputs/              # aggregate, disclosure-safe outputs only
```

## Data governance

**This repository contains no individual-level data.** `data/` is git-ignored. Only aggregate, non-disclosive outputs belong in `outputs/`. Each site's data stays under its own data-sharing and data-protection terms: Kenya Data Protection Act 2019, Uganda Data Protection and Privacy Act 2019, and the applicable Cameroon law.

## Status

| Stage | Status |
|-------|--------|
| CSV harmonisation (Track A), 3 sites | Complete |
| OMOP ETL (Track B), IDI + LVCT | In progress |
| Survival data preparation (R) | Complete |
| Centralized baseline analysis | Complete |
| Opal + dsSurvival deployment | Local test instance; TODO: confirm final state |
| Federated analysis + comparison | Manuscript draft 3 (Discussion written) |

## Team

APHRC Data Science team. TODO: add contributors and acknowledgements (David for R configuration support, Letisha for review of transformed datasets).

## Citation

TODO: add the manuscript citation once submitted.
