# 2. Data harmonisation

Two standardisation tracks run in parallel. They are not alternatives: the aim is to have analysis-ready data either way and to compare the two outputs.

## Track A: Manual CSV standardisation (complete)

- All three sources (LVCT, IDI, DGH) were transformed into CSV files that follow a **shared data dictionary**, with variables aligned across sites.
- Each site produces a repeated-measures file with 84 columns.
- This track is the **input to the current survival analysis**. It is also the fallback if the OMOP route has problems and the comparator for it.

TODO: link or add the data dictionary (`docs/data-dictionary.csv`).

## Track B: OMOP CDM ETL (in progress)

- One ETL pipeline covers **IDI and LVCT**. DGH was already OMOP-standardised.
- Status: the IDI and LVCT sources are joined and the pipeline is at the **concept-mapping** stage.
- Why it matters: OMOP is the long-term interoperable format, but getting OMOP data into an analysis-ready survival shape inside DataSHIELD is the uncertain step.

TODO: link the OMOP ETL repository or add it as a subfolder.

## Challenges logged

1. LVCT data quality and inconsistency.
2. Manual standardisation of three sites against one dictionary.
3. Survival-analysis preparation, plus building a single OMOP ETL for two sources.
