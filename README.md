# Wage Determinants by Age, Sex, Education, and Occupation

## Research question

How are individual wage-salary income levels associated with age, sex, education, and the average wage of a worker's occupation? The project uses an ordinary least squares (OLS) regression as an exploratory analysis rather than a causal study.

## Data source and usage permissions

The analysis was developed for CISC7204 using public-use microdata from the IPUMS USA Current Population Survey Annual Social and Economic Supplement (CPS-ASEC) and American Community Survey (ACS) extracts. Please obtain the authorized extracts directly from IPUMS USA and follow the IPUMS terms of use and citation requirements before reproducing the analysis. The raw and individual-level merged data are intentionally not included in this public repository because the assignment requires avoiding restricted or personal data uploads.

The notebook expects the following local input files, which are not committed here:

- `cps_00001.csv`
- `usa_00001.csv`

## Methods and tools

- Python 3
- pandas and NumPy for loading, cleaning, weighting, aggregation, and merging
- statsmodels for OLS regression
- Matplotlib for visualizations
- Occupation-level weighted average wages are calculated from ACS records using `PERWT` and then merged to CPS records using `OCC`.
- Records with missing wage code `999999`, non-positive wages, or no matched occupation-level wage are excluded from the regression sample.

## Key findings

The model estimates the relationship between `INCWAGE` and `AGE`, `SEX`, `EDUC`, and `occ_mean_wage`. The coefficient chart indicates which estimated associations are statistically significant at the 5% level in this exploratory specification. The observed-versus-fitted plot and residual plot provide visual checks of model fit and show that wage variation is substantial and that a simple linear model does not explain all individual differences.

Exact numerical results depend on the authorized data extracts and should be regenerated locally by running the notebook.

## Limitation

The OLS results show associations, not causal effects. Wage distributions are highly skewed, and the model does not fully address factors such as work experience, hours worked, industry, geography, selection into employment, or nonlinear and interaction effects. Residual patterns also suggest that model assumptions may not hold uniformly.

## How to run the analysis

1. Obtain the authorized CPS-ASEC and ACS extracts from IPUMS USA and place `cps_00001.csv` and `usa_00001.csv` in the working directory.
2. Create and activate a Python environment.
3. Install dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

4. Open and run `CISC7204-Assgn01-MC631173-PreliminaryProjectProposal.ipynb` from top to bottom.
5. The notebook generates the intermediate files `acs_2024_occ_avg_wage.csv` and `merged_cps_acs.csv`, then saves the visualizations in the project directory.

## Repository contents

- `CISC7204-Assgn01-MC631173-PreliminaryProjectProposal.ipynb` - analysis notebook
- `requirements.txt` - Python dependencies
- `reg_coef_bar.png` - regression coefficient visualization
- `observed_vs_fitted.png` - observed versus fitted wage visualization
- `residual_fitted.png` - residual diagnostic visualization
- `.gitignore` - excludes notebook checkpoints, local system files, and common secret files
