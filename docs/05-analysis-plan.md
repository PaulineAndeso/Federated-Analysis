# 5. Analysis plan

Each analysis runs twice: **centralized** (pooled individual-level data in R) and **federated** (DataSHIELD, data on Opal).

## Descriptive statistics

- Baseline characteristics by site. Cameroon is included here.
- Federated: `ds.table`, `ds.mean` and related functions. Some cells will be suppressed by disclosure control.

## Time to VL suppression (death as competing risk)

- Sites: Kenya, Uganda.
- Cumulative incidence of suppression by site.
- Regression for the competing-risks outcome. TODO: confirm the model used (Fine–Gray subdistribution hazard vs cause-specific Cox). The manuscript reports results on the log SHR scale.
- Primary endpoint: first documented suppression. Sensitivity analysis: interval-censored fit.

## Time to death

- Kaplan–Meier / survival curves by site.
- Cox proportional-hazards model. Check the PH assumption: a violation was noted in the Kenya data, so stratified models may be needed.

## Federated estimation

- **Study-level meta-analysis (SLMA):** site-specific estimates pooled by meta-analysis, e.g. `ds.coxph.SLMA`.
- Compare with **pooled** centralized models.

## Scripts

TODO: add to `R/`
- `R/02_centralized_analysis.R`
- `R/03_federated_analysis.R`
