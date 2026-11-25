# 6. Centralized vs federated comparison

## What is compared

| Dimension | What to check |
|-----------|---------------|
| Descriptives | Counts and summaries match, apart from suppressed cells |
| Country-level models | Estimates should agree exactly (same data, same model) |
| Pooled estimates | SLMA (federated) vs pooled model (centralized) |
| Survival / incidence curves | Effect of privacy-preserving smoothing on the curves |
| Disclosure controls | Which outputs were blocked or modified, and whether conclusions changed |
| Model diagnostics | What can and cannot be checked under federation |
| Effort | Data preparation and deployment burden |

## Findings recorded so far (manuscript draft 3)

- Country-level models agree exactly, as expected.
- A small discrepancy (**0.012 on the log SHR scale**) between meta-analysis and pooled modelling comes from the pooling method, not from the federation.
- Disclosure controls were inconsistent: the Uganda marital-status **table** was suppressed, but the variable was still allowed in the **model**.
- Privacy-preserving smoothing changes the shape of survival and incidence curves.
- Model-checking diagnostics are limited under federation.

## Open items

- [ ] Confirm whether the three country datasets were hosted on a single Opal server for the comparison
- [ ] Decide whether to report the parallel OMOP CDM pipeline
- [ ] Add a results table template to `outputs/`
