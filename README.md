# Understanding Birth Weight Variation in U.S. Birth Records

This repository contains the full code, report, and figures for a birth weight analysis based on historical U.S. natality records from the National Center for Health Statistics (NCHS). The project studies how birth weight varies at both the individual level and the subgroup level, with a focus on maternal and paternal characteristics, demographic structure, and heterogeneity across geographic and demographic strata.

## Project motivation

Birth weight is a clinically important early-life outcome and a useful lens for understanding population health differences. Rather than stopping at a single regression model, this project combines two complementary perspectives:

1. **Individual-level modeling** to study how birth weight changes with predictors such as infant sex, maternal age, paternal age, plurality, and birth order.
2. **Subpopulation-level heterogeneity analysis** to examine how estimated effects and outcomes vary across counties, years, sex, and maternal-race strata.

That combination makes the project both statistically rich and practically interpretable.

## Data

The analysis uses U.S. birth records released by the NCHS. The raw files are fixed-width natality records that were harmonized into tabular form using the preprocessing pipeline in `scripts/prep.py`.

Main data elements used in the analysis include:
- birth weight
- infant sex
- maternal age
- paternal age
- plurality
- birth order
- county and state identifiers
- year
- maternal race

## Methods

The repository includes code for both data preparation and statistical analysis.

### Individual-level analysis
- missingness exploration and complete-case analysis
- nonlinear age effects using polynomial and spline-style modeling
- Gamma GLM/GEE style modeling for positively skewed birth weight outcomes
- clustering-aware inference for grouped birth records

### Subpopulation heterogeneity analysis
- construction of county-year-sex-race strata
- subgroup summary statistics and empirical variability analysis
- z-score style calibration across subpopulations
- false discovery rate style screening for unusually large deviations
- heterogeneity summaries motivated by ICC-like reasoning

## Main findings

The report shows that birth weight variation is not explained by one factor alone. Several predictors have systematic associations with birth weight, and the strength of these patterns varies meaningfully across subpopulations. The subgroup analysis also shows substantial heterogeneity that would be hidden in a single pooled model.

## Repository structure

```text
birthweight_repo_package/
├── analysis/
│   ├── birthweight.ipynb
│   ├── birthweight.Rmd
│   ├── birthweight_meta.ipynb
│   └── birthweight_meta.Rmd
├── docs/
│   └── report.pdf
├── figures/
│   ├── Distribution of subgroup sample sizes.png
│   ├── FDR.png
│   ├── Hexbin.png
│   ├── ICC line.png
│   ├── scatter.png
│   └── stratum-specific Z-scores.png
├── scripts/
│   ├── prep.py
│   └── agg.py
├── data/
├── .gitignore
└── requirements.txt
```

## Reproducibility

### Python setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Download and preprocess raw natality files

```bash
python scripts/prep.py
```

This downloads and harmonizes selected NCHS natality files into the `data/` directory.

### Build aggregated subgroup summaries

```bash
python scripts/agg.py
```

### Run the analysis

Use either the notebooks or the R Markdown files in `analysis/` depending on your preferred workflow.

## Notes

- The original project was created in a course setting and has been reorganized here into a cleaner public-facing repository.
- The notebooks and report are included together so readers can connect the code to the statistical narrative.
- Large raw data files are not committed to the repository.

## Possible future improvements

- add a single environment lockfile for Python and R dependencies
- refactor notebooks into reusable analysis scripts
- add a small synthetic sample dataset for quick demonstration
- export final figures with consistent naming and captions

## Author

Hao-Chun Shih
