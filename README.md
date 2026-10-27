# Factors Associated with Cognitive Processing Speed Among U.S. Adults Aged 60 and Older

## Project Overview

This project examines factors associated with cognitive processing speed among U.S. adults aged 60 years and older using data from the National Health and Nutrition Examination Survey (NHANES), 2011–2014.

The analysis investigates associations between cognitive processing test performance and age, sex, educational attainment, history of stroke, and depressive symptoms.

## Research Question

How are age, sex, education, stroke history, and depressive symptoms associated with cognitive processing test performance among U.S. adults aged 60 and older?

## Data Sources

The analysis combines data from two NHANES survey cycles:

- [NHANES 2011–2012: Cognitive Functioning (CFQ_G)](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2011/DataFiles/CFQ_G.htm)
- [NHANES 2013–2014: Cognitive Functioning (CFQ_H)](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2013/DataFiles/CFQ_H.htm)

Additional datasets provide demographic information, medical history, and depressive symptom scores.

| Dataset | 2011–2012 | 2013–2014 | Purpose |
|---|---|---|---|
| Cognitive functioning | `CFQ_G.xpt` | `CFQ_H.xpt` | Cognitive test scores |
| Demographics | `DEMO_G.xpt` | `DEMO_H.xpt` | Age, sex, education, survey design |
| Medical conditions | `MCQ_G.xpt` | `MCQ_H.xpt` | Stroke history |
| Depression questionnaire | `DPQ_G.xpt` | `DPQ_H.xpt` | PHQ-9 score |

The raw data files are stored in the project folder and are required to reproduce the analysis. They are publicly available from the U.S. Centers for Disease Control and Prevention (CDC).

**Study population:** U.S. adults aged 60 years and older  
**Survey period:** 2011–2014  
**Final analytical sample:** 2,936 participants

## Outcome and Explanatory Variables

### Outcome variable

- `CFDDS`: Digit Symbol Substitution Test score, used as a measure of performance on a cognitive processing task.

### Explanatory variables

- Age in years
- Sex
- Educational attainment
- Self-reported history of stroke
- Depressive symptom score measured using the Patient Health Questionnaire-9 (PHQ-9)

The primary model uses female participants, participants with 9th–11th grade education, and participants without a history of stroke as reference categories.

## Methods

The analysis included:

- Preparation and combination of two NHANES survey cycles
- Data-quality checks and missing-data assessment
- Construction of the PHQ-9 score
- Exploratory data analysis and descriptive visualizations
- Survey-weighted linear regression accounting for NHANES weights, strata, and primary sampling units
- Supplementary age-by-education interaction analysis
- Residual and influence diagnostics, including multicollinearity checks
- Cross-checking the primary regression estimates using R's `survey` package

The two survey cycles were combined using the four-year examination weight, calculated as `WTMEC2YR / 2`.

The primary model includes age, sex, education, stroke history, and PHQ-9 score. The supplementary model adds age-by-education interaction terms.

The final complete-case sample contained 2,936 participants. Both regression models used the same sample.

## Results: Primary Model

The primary survey-weighted linear regression model included 2,936 participants.

| Variable | Coefficient | 95% Confidence Interval | p-value |
|---|---:|---:|---:|
| Age (years) | −0.904 | −0.996 to −0.811 | <0.001 |
| Male vs. female | −5.293 | −6.265 to −4.320 | <0.001 |
| College graduate or above | +16.462 | 14.180 to 18.744 | <0.001 |
| High school graduate/GED | +6.640 | 5.023 to 8.257 | <0.001 |
| Less than 9th grade | −11.348 | −14.155 to −8.541 | <0.001 |
| Some college or associate degree | +12.065 | 10.253 to 13.878 | <0.001 |
| History of stroke: yes vs. no | −5.419 | −7.666 to −3.172 | <0.001 |
| PHQ-9 score | −0.611 | −0.807 to −0.416 | <0.001 |

*Education coefficients are relative to the 9th–11th grade reference category. All coefficients are adjusted for the other variables in the model.*

### Interpretation

After adjustment for the other included variables:

- **Age:** Each additional year of age was associated with an estimated 0.90-point lower cognitive processing score.
- **Sex:** Male participants had scores approximately 5.29 points lower than female participants.
- **Education:** Participants with a college degree or higher had scores approximately 16.46 points higher than participants in the 9th–11th grade reference category.
- **Stroke history:** Participants reporting a history of stroke had scores approximately 5.42 points lower than participants reporting no history of stroke.
- **Depressive symptoms:** Each additional PHQ-9 point was associated with an estimated 0.61-point lower cognitive processing score.

All explanatory variables in the primary model were statistically associated with the outcome at p < 0.001.

## Supplementary Analysis: Age-by-Education Interaction

A supplementary survey-weighted regression model examined whether the association between age and cognitive processing scores differed across education groups.

| Variable | Coefficient | 95% Confidence Interval | p-value |
|---|---:|---:|---:|
| Age (years) | −0.689 | −0.983 to −0.394 | <0.001 |
| Male vs. female | −5.202 | −6.162 to −4.241 | <0.001 |
| College graduate or above | +40.654 | 15.997 to 65.310 | 0.003 |
| High school graduate/GED | +9.196 | −15.255 to 33.648 | 0.442 |
| Less than 9th grade | −24.333 | −55.941 to 7.274 | 0.124 |
| Some college or associate degree | +37.730 | 14.400 to 61.061 | 0.003 |
| History of stroke: yes vs. no | −5.399 | −7.595 to −3.204 | <0.001 |
| PHQ-9 score | −0.595 | −0.787 to −0.404 | <0.001 |
| Age × college graduate or above | −0.348 | −0.687 to −0.008 | 0.045 |
| Age × high school graduate/GED | −0.035 | −0.381 to 0.312 | 0.836 |
| Age × less than 9th grade | +0.181 | −0.254 to 0.616 | 0.396 |
| Age × some college or associate degree | −0.368 | −0.697 to −0.038 | 0.030 |

*In the interaction model, education main-effect coefficients represent differences at age zero under the model's current parameterization. They should not be interpreted as meaningful education-group differences among older adults. The age coefficient represents the age association in the reference education group.*

A joint Wald test indicated that the four interaction terms were statistically significant overall: F(4, 20) = 5.319, p = 0.0044.

| Model metric | Primary model | Interaction model |
|---|---:|---:|
| R² | 0.406 | 0.411 |
| Adjusted R² | 0.404 | 0.409 |
| AIC | 23,422.74 | 23,407.67 |

The interaction model showed improved fit, although the increase in explained variance was modest. The main-effects model remains the primary model because it is simpler to interpret. The interaction model is presented as supplementary analysis.

## Descriptive Visualizations

The project includes three descriptive plots:

- `stroke_history_score.png` — cognitive processing scores by stroke history
- `age_cognitive_score.png` — cognitive processing scores by age
- `education_level_score.png` — cognitive processing scores by education level

These plots are unweighted and are used for exploratory purposes. The regression models account for the complex NHANES survey design.

## Limitations

- **Cross-sectional design:** The analysis uses data collected during 2011–2014. It cannot establish causal relationships or measure within-person cognitive decline over time.
- **Outcome measurement:** The Digit Symbol Substitution Test measures performance on a specific cognitive task. It is not a comprehensive assessment of cognition or a diagnosis of dementia.
- **Complete-case analysis:** Participants with missing PHQ-9, stroke-history, or education data were excluded. This may introduce selection bias if missingness is related to the variables being studied.
- **Residual confounding:** Other factors associated with cognitive performance may not be accounted for in the models.
- **Descriptive visualizations:** The descriptive plots are unweighted, whereas the regression models account for the complex NHANES survey design.
- **Model assumptions:** The primary model assumes a linear association between age and the outcome. The supplementary model examines whether that association differs by education group.
- **Generalizability:** The findings describe older U.S. adults surveyed in 2011–2014 and may not generalize to younger populations, other countries, or current populations.

## Tools and Technologies

- Python
- pandas
- NumPy
- Polars
- SciPy
- statsmodels
- matplotlib
- seaborn
- `svy` for survey-weighted analysis
- R and the `survey` package for cross-checking the primary regression model

## Project Files

The project folder contains:

- The Jupyter notebook: `nhanes_cognitive_processing_analysis.ipynb`
- Raw NHANES data files required for the analysis
- Three descriptive visualization files listed above

The notebook contains the data preparation, exploratory analysis, regression models, diagnostics, and interpretation.

## Reproducibility

To reproduce the analysis:

1. Download the NHANES datasets listed in the Data Sources section.
2. Place the raw files in the location expected by the notebook, or update the file paths.
3. Install the Python packages imported by the notebook.
4. Run the notebook from beginning to end.
5. To reproduce the R cross-check, install R and the `survey` package and ensure the notebook can locate the R executable.

The analysis uses the same complete-case sample for the primary and supplementary regression models.

## Conclusion

In this analysis of NHANES 2011–2014 data, age, sex, educational attainment, stroke history, and depressive symptoms were associated with performance on the Digit Symbol Substitution Test among U.S. adults aged 60 and older.

A supplementary analysis found evidence that the age association varied across some education groups. These results describe adjusted cross-sectional associations and should not be interpreted as causal effects or evidence of individual cognitive decline.