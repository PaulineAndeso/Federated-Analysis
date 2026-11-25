# 1. Study overview

## Background

Multi-country HIV analyses usually use one of three approaches:

- **Centralized:** individual-level data are pooled in one place. This is the most flexible approach, but it needs cross-border data transfer.
- **Site-specific:** each site analyses its own data. Data stay local, but the approach depends on local capacity and makes iterative work hard.
- **Federated:** the analysis goes to the data. Commands run remotely and only aggregate outputs that pass disclosure checks are returned.

DataSHIELD with Opal servers provides the federated approach. The dsSurvival package adds Cox models, proportional-hazards checks and privacy-preserving survival curves.

Earlier DataSHIELD comparisons of federated and centralized analysis used synthetic data (Jégou et al., 2024). This study runs the comparison on **routine HIV programme data** for **survival and competing-risks outcomes**.

## Sites

| Site | Country | Notes |
|------|---------|-------|
| LVCT Health | Kenya | Most data cleaning was needed (quality and consistency issues). Restricted to ART initiation from 2020. |
| IDI | Uganda | Included in the OMOP ETL track. |
| DGH | Cameroon | Already OMOP-standardised. Descriptives only for the VL suppression analysis. |

## Outcomes

| Outcome | Definition | Competing event |
|---------|-----------|-----------------|
| VL suppression | Time from ART initiation to first documented VL suppression (<1000 copies/mL or undetectable) | Death |
| Mortality | Time from ART initiation to death | — |

## Design decisions

- **Complete-case analysis.**
- **Primary VL endpoint:** first *documented* suppression (observed test date). The interval-censored fit is a sensitivity analysis; see [03](03-survival-data-preparation.md).
- Centralized R outputs are the reference that DataSHIELD outputs are compared against.

## Related work

- Mental-health federated analysis (IWHOD poster): DataSHIELD + OMOP CDM across Iganga, Kagando and Kilifi HDSS.
- Training example: [Federated-Analysis-using-DataSHIELD-I](https://aphrc-dse.github.io/Federated-Analysis-using-DataSHIELD-I/).
