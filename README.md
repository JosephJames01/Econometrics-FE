# UK Household Savings Determinants — Panel Econometric Analysis

Applied econometrics project investigating the determinants of UK household 
savings behaviour using panel data methodology in R.

## Overview

Balanced panel dataset of 90 individuals observed across 6 time periods 
(2016–2021), N=540. Two-way fixed effects regression estimated to control 
for unobserved individual heterogeneity and common time shocks.

## Methodology

### Model Specification
- Two-way fixed effects (entity + time) via `plm::within`
- Three-way interaction terms: `income × family × gender`
- Polynomial specification testing (linear vs. cubic income)
- All inference via HC1 heteroskedasticity-robust clustered standard errors (`vcovHC`)

### Hypothesis Tests
| Test | Statistic | p-value | Decision |
|------|-----------|---------|----------|
| Polynomial (cubic vs. linear) | F(2,425) = 0.789 | 0.455 | Linear retained |
| Time FE joint significance (2%) | F(5,432) = 3.523 | 0.004 | Time FE confirmed |

### Policy Evaluation
Pre-post first-differences estimator (2016→2017) to isolate the effect 
of a government savings incentive. Individual FE differenced out; intercept 
captures uniform policy shock: **£2,924 estimated savings increase**.

### Prediction
Manual FE prediction via extracted `fixef()` components:

ŷ = α_i + λ_t + Xβ̂ → £51,973

for: income=£35k, male, no children, cat owner, education sector,
household_size=2, prev_savings=£5k

## Key Results

| Variable | β | p-value | Significance |
|----------|---|---------|--------------|
| income | 0.734 | 0.006 | ** |
| prev_savings | −0.139 | <0.001 | *** |
| petCat | 9,551 | 0.016 | * |
| industryManufacturing | 2,200 | 0.038 | * |

## Stack
R — plm, AER, sandwich (vcovHC), stargazer, ggplot2, psych, readxl
## Data
`panel_savings_1.csv` — simulated panel dataset (seed: 300362)

## Module
BEEM011 Applied Econometrics — University of Exeter, MSc Financial Technology

