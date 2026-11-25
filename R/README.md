# R scripts

Scripts will be added here. Planned structure:

| Script | Purpose | Docs |
|--------|---------|------|
| `01_prepare_survival_data.R` | Harmonised CSV → counting-process and interval-censored files per site | [03](../docs/03-survival-data-preparation.md) |
| `02_centralized_analysis.R` | Baseline pooled analyses (reference results) | [05](../docs/05-analysis-plan.md) |
| `03_federated_analysis.R` | DataSHIELD login, assignment, dsSurvival models, SLMA | [05](../docs/05-analysis-plan.md) |
| `04_compare.R` | Side-by-side comparison tables | [06](../docs/06-centralized-vs-federated-comparison.md) |

Conventions:
- Read paths come from `config.yml` or environment variables. Never hard-code site data paths.
- Never commit Opal credentials. Use `.Renviron` (git-ignored).
