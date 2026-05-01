# Medicare Payment Gap Analysis — Massachusetts Providers

Analysis of standardized Medicare payment gaps among 37,708 Massachusetts
providers using the 2023 CMS Medicare Physician & Other Practitioners dataset.
Four statistical methods are applied: multiple linear regression (MLR),
one-way ANOVA, logistic regression, and bootstrap/permutation tests.

The full report is available in `docs/medicare_payment_gap_ma.pdf`.
---

## Data Source

**CMS Medicare Physician & Other Practitioners — By Provider (2023)**  
https://data.cms.gov/provider-summary-by-type-of-service/medicare-physician-other-practitioners

The raw data file is not tracked in this repository due to size. Download the
2023 dataset from the link above and place it in `data/raw/` before running
the preprocessing script.

---

## Repository Structure

```
├── data/
│   ├── raw/          # CMS source file (gitignored)
│   └── processed/    # ma_providers_preprocessed.rds (output of 01_preprocessing)
├── docs/
│   └── figures/      # All figures referenced in the report
├── output/           # Knitted Rmd outputs
├── R/
│   ├── 01_preprocessing.Rmd
│   └── 02_analysis.Rmd
├── info6105_medicare_payment_gap_analysis.Rproj
└── README.md
```

---

## Reproducing the Analysis

1. Download the raw CMS file and place it in `data/raw/`
2. Open `info6105_medicare_payment_gap_analysis.Rproj` in RStudio
3. Knit `R/01_preprocessing.Rmd` — this filters to Massachusetts providers,
   engineers all derived variables, and writes `data/processed/ma_providers_preprocessed.rds`
4. Knit `R/02_analysis.Rmd` — this runs all four research questions and
   writes figures to `docs/figures/`

All random procedures use `set.seed(6105)`.

---

## Methods Overview

| Research Question | Method | n |
|---|---|---|
| RQ1: Predictors of payment gap magnitude | Multiple Linear Regression + Quantile Regression | 37,708 / 3,752 |
| RQ2: Specialty differences | Welch's ANOVA + Games-Howell + Kruskal-Wallis | 22,753 |
| RQ3: High-gap classification | Logistic Regression | 28,556 |
| RQ4: Dual-eligibility gap | Bootstrap + Permutation Tests | 28,556 |

---

## Environment

```
R version 4.4.x
Key packages: tidyverse, quantreg, glmnet, pROC, boot, rstatix, car, ggrepel
```
