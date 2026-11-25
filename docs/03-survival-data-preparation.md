# 3. Survival data preparation

Implemented in R (`dplyr`, `readr`). All columns are read as character to keep precision, and only the working columns are converted to numeric.

## Steps

1. **Drop degenerate rows** where `start_day == stop_day == 0`.
2. **Kenya:** keep patients who started ART in 2020 or later.
3. **Normalise categorical levels:** replace slashes and spaces with underscores so factor levels are safe to use in DataSHIELD.
4. **First event only:** drop rows after a patient's first VL suppression.
5. **Write two output shapes per site:**

| File | Shape | Key columns |
|------|-------|-------------|
| Counting-process (at-risk) | Multiple rows per patient | `start_day`, `stop_day`, event |
| Interval-censored | One row per patient | `left_bound`, `right_bound`, `event` |

Collapsing to one row per patient is required for any interval-censored analysis, because each patient contributes a single interval.

## Finding: most VL "intervals" are left-censored

In testing, **86% of Kenya** and **92% of Uganda** patients had already suppressed at their first VL test after ART initiation. This makes them left-censored rather than genuinely interval-censored.

| Method | Median time to suppression |
|--------|---------------------------|
| Turnbull NPMLE / Weibull AFT (interval-censored) | 1–5 days. This reflects the testing schedule, not biology. |
| Right-endpoint Kaplan–Meier | Kenya 266 days, Uganda 190 days |

**Decision:** the primary analysis uses the observed test date (time to first *documented* suppression). The interval-censored fit is a **sensitivity analysis**. Results should be described as time to documented suppression, because they depend on the testing schedule.

## Scripts

TODO: add to `R/`
- `R/01_prepare_survival_data.R`
