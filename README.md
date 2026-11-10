# 🧬 Elastic Net Machine Learning for Circulating Biomarker Discovery in Osteoporosis

### 🤖 Logistic Regression | Cox Proportional Hazards | Multiple Linear Regression | OPUS Cohort

**Author:** David Carro Vázquez, PhD  
**Research affiliation:** Department of Orthopedic Surgery, University of California, San Francisco (UCSF)  
**Programming language:** R / R Markdown  
**Research areas:** Machine Learning | Osteoporosis | Biomarker Discovery | microRNA | Bone Turnover Markers | Fracture Prediction | Survival Analysis | Biostatistics

---

## 📖 Project Overview

This repository documents an R-based computational framework developed to investigate the predictive value of circulating molecular biomarkers for osteoporotic fractures, bone mineral density (BMD), longitudinal bone loss, and related musculoskeletal outcomes.

The analyses are based on the **Osteoporosis and Ultrasound Study (OPUS)** cohort and integrate established clinical predictors with circulating microRNAs (miRNAs) and bone turnover markers (BTMs).

The computational framework combines conventional statistical regression with **Elastic Net regularization**, enabling biomarker selection from correlated molecular predictors and evaluation of their incremental predictive contribution beyond clinical baseline models.

Three complementary regression approaches are included:

- 🩺 **Logistic regression:** Prediction of incident vertebral and nonvertebral fractures.
- 📈 **Multiple linear regression:** Prediction of continuous musculoskeletal and biochemical outcomes, including baseline BMD, longitudinal BMD change, grip strength, and selected bone metabolism markers.
- ⏱️ **Cox proportional hazards regression:** Prediction of time to incident nonvertebral fracture, incorporating follow-up duration and censoring.

The principal objective is to determine whether circulating molecular biomarkers improve predictive performance beyond established clinical risk factors.

### 🧬 Biomarker Integration Strategy

The framework investigates three molecular biomarker configurations:

1. **miRNAs only:** Circulating microRNA expression ratios.
2. **BTMs only:** Circulating biochemical markers of bone metabolism.
3. **miRNAs + BTMs:** Combined molecular predictors from both biomarker categories.

The logistic and Cox regression frameworks support all three biomarker configurations.

The multiple linear regression framework evaluates miRNAs and BTMs separately, without a combined miRNA + BTM model.

---

## 🎯 Research Objectives

1. Identify circulating miRNA signatures associated with osteoporotic fracture risk and quantitative musculoskeletal phenotypes.
2. Investigate the predictive contribution of circulating bone turnover markers.
3. Determine whether miRNAs and BTMs provide complementary predictive information when combined.
4. Apply Elastic Net regularization to select informative biomarkers from high-dimensional and correlated molecular predictors.
5. Evaluate whether selected biomarkers improve prediction beyond established clinical risk factors.
6. Compare predictive performance across binary, continuous, and time-to-event outcomes.
7. Assess biomarker selection stability across repeated training and testing partitions.
8. Develop a reusable computational framework for molecular biomarker discovery and clinical prediction.

---

## 🧪 Study Cohort and Molecular Biomarkers

### 🔹 OPUS Cohort

The analyses use data from the **Osteoporosis and Ultrasound Study (OPUS)**, comprising approximately **1,128 postmenopausal women aged 55–80 years**.

The dataset includes:

- Clinical and demographic characteristics.
- Bone mineral density measurements.
- Circulating microRNA expression profiles.
- Biochemical markers of bone metabolism.
- Longitudinal information on incident osteoporotic fractures.
- Musculoskeletal and biochemical phenotypes.

The cohort provides a framework for investigating associations between circulating molecular markers, skeletal health, and fracture outcomes.

### 🔹 1. Circulating MicroRNAs (miRNAs)

Serum microRNAs were measured using the osteomiR platform, profiling 19 candidate miRNAs.

The analytical framework incorporates pairwise miRNA expression ratios to investigate relative molecular expression patterns and identify potentially informative biomarker combinations.

**Main analytical steps:**

- Import circulating miRNA expression data.
- Generate or import pairwise miRNA ratios.
- Perform quality control and missing-value assessment.
- Identify candidate molecular predictors.
- Evaluate individual miRNA ratios.
- Apply Elastic Net regularization for multivariable biomarker selection.
- Integrate selected miRNA ratios into clinical prediction models.

### 🔹 2. Bone Turnover Markers (BTMs)

The analyses incorporate circulating biochemical markers associated with bone formation, resorption, and mineral metabolism.

**Investigated markers include:**

- **Osteocalcin (OC):** Marker associated with bone formation.
- **Procollagen type I N-terminal propeptide (PINP/P1NP):** Marker of type I collagen formation.
- **C-terminal telopeptide of type I collagen (CTX):** Marker of bone resorption.
- **Parathyroid hormone (PTH):** Hormone involved in calcium homeostasis and bone metabolism.

These markers provide complementary information about bone remodeling processes.

### 🔹 3. Clinical Baseline Predictors

Clinical baseline models incorporate outcome-specific combinations of:

- Age.
- Body mass index (BMI).
- Total hip BMD.
- Lumbar spine BMD.
- Prevalent vertebral or nonvertebral fracture history.
- Additional clinical or technical covariates where applicable.

The exact clinical baseline model is defined separately for each outcome.

**All biomarker-augmented models are evaluated relative to their corresponding clinical baseline models.**

---

## ⚙️ Shared Computational Analysis Framework

The three regression pipelines follow a common analytical strategy, adapted to the statistical characteristics of each outcome.

### 🔹 1. Data Import and Preprocessing

The workflow imports clinical and molecular biomarker datasets and prepares them for statistical analysis.

**Main analytical steps:**

- Import clinical and biomarker data from Excel files.
- Define outcome variables and mandatory baseline predictors.
- Identify candidate miRNA and BTM predictors.
- Evaluate missing observations.
- Remove invalid or noninformative biomarker columns.
- Convert categorical variables into appropriate data types.
- Prepare outcome-specific analytical datasets.
- Generate numerical predictor matrices.
- Standardize molecular predictors where required.

The Cox implementation additionally validates participant identifiers, fracture event coding, and follow-up durations.

### 🔹 2. Construction of Clinical Baseline Models

For each clinical outcome, a baseline model is constructed using established clinical predictors without the molecular biomarkers under investigation.

These baseline models provide the reference for evaluating incremental biomarker performance.

The same outcome-specific clinical predictor definition is retained when comparing molecular biomarker configurations.

### 🔹 3. Individual Biomarker Screening

Candidate molecular biomarkers are evaluated individually by adding them to the corresponding clinical baseline model.

**Main analytical steps:**

- Fit the baseline regression model.
- Add each candidate biomarker individually.
- Estimate biomarker-associated regression coefficients.
- Calculate statistical significance.
- Compare baseline and biomarker-augmented models.
- Rank candidate biomarkers.
- Generate screening summary tables.

The specific effect estimates and performance metrics depend on the regression family.

### 🔹 4. Elastic Net Feature Selection

Elastic Net combines L1 and L2 regularization to identify informative predictors while controlling model complexity.

The workflow uses the `glmnet` framework for regularized regression.

**Principal hyperparameters:**

- **Alpha (α):** Controls the balance between LASSO and Ridge regularization.
- **Lambda (λ):** Controls the overall strength of regularization.
- **Cross-validation folds:** Used to optimize regularization parameters within training data.

Elastic Net is applied to select informative molecular biomarkers from potentially correlated predictor sets.

In the Cox implementation, mandatory clinical predictors are retained without penalization using `penalty.factor = 0`.

### 🔹 5. Biomarker Model Configurations

Three molecular biomarker configurations are considered.

**Model A — miRNAs only**

Clinical baseline predictors are combined with selected circulating miRNA ratios.

**Model B — BTMs only**

Clinical baseline predictors are combined with selected bone turnover markers.

**Model C — miRNAs + BTMs**

Clinical baseline predictors are combined with selected biomarkers from both molecular categories.

Model C is included in the logistic regression framework and supported by the Cox regression framework, but is not evaluated in the multiple linear regression workflow.

### 🔹 6. Conventional Regression Model Refitting

Selected biomarkers are incorporated into conventional regression models alongside mandatory clinical predictors.

This enables estimation of interpretable regression coefficients and comparison of clinical baseline models with biomarker-augmented models.

**Effect estimates depend on the regression family:**

- Logistic regression: Odds ratios (OR).
- Multiple linear regression: Regression coefficients (β).
- Cox regression: Hazard ratios (HR).

Statistical inference following data-driven biomarker selection is interpreted cautiously because selection can introduce bias.

### 🔹 7. Repeated Train/Test Evaluation

The supplied regression workflows use repeated training and testing partitions to evaluate predictive performance.

The implementations specify:

- **50 random train/test splits.**
- **70% training / 30% testing.**
- Consistent partitions for model comparisons within each analysis.
- Biomarker selection using training observations.
- Predictive performance evaluation using held-out observations.

The logistic regression framework incorporates class-imbalance handling within training data.

The Cox regression framework uses event-stratified splits without class balancing.

### 🔹 8. Model Performance and Biomarker Stability

Predictive performance is evaluated using metrics appropriate to each outcome type.

The framework also examines biomarker selection frequencies across repeated partitions to investigate selection stability.

Repeated-split performance estimates provide internal validation but do not replace external validation in an independent cohort.

---

## 🩺 Pipeline 1: Logistic Regression — Incident Osteoporotic Fractures

### 🎯 Research Objective

To identify circulating molecular biomarkers that improve prediction of incident osteoporotic fractures beyond established clinical risk factors.

### 🧪 Clinical Outcomes

Two binary outcomes are investigated:

1. **Incident vertebral fracture.**
2. **Incident nonvertebral fracture.**

### 🧬 Biomarker Model Comparisons

Four predictive model configurations are evaluated.

| Model | Predictors |
|---|---|
| Baseline | Clinical predictors only |
| Baseline + miRNAs | Clinical predictors + selected miRNA ratios |
| Baseline + BTMs | Clinical predictors + selected bone turnover markers |
| Baseline + miRNAs + BTMs | Clinical predictors + selected miRNAs and BTMs |

The combined model investigates whether the two molecular biomarker categories provide complementary predictive information.

### 🤖 Statistical and Machine-Learning Methods

The logistic regression workflow incorporates:

- Binary logistic regression using `glm()`.
- Individual biomarker screening.
- Training-set class-imbalance handling.
- Elastic Net logistic regression using `glmnet`.
- Cross-validation for regularization tuning.
- Selection of biomarkers with nonzero coefficients.
- Conventional logistic regression refitting.
- Comparison of baseline and biomarker-augmented models.
- Repeated train/test evaluation.
- Biomarker selection stability analysis.

### 📊 Model Evaluation

The workflow evaluates:

- **ROC-AUC:** Discrimination between participants with and without incident fractures.
- **ΔAUC:** Improvement or deterioration relative to the baseline model.
- **Net Reclassification Improvement (NRI):** Changes in risk classification at specified thresholds.
- **Odds ratios (OR):** Association estimates for selected biomarkers.
- **Statistical significance:** Regression and model-comparison tests.
- **FDR-adjusted p-values:** Multiple-testing adjustment where implemented.
- **Biomarker selection frequency:** Stability across repeated partitions.

The logistic implementation includes NRI evaluation using risk thresholds of 0.10 and 0.20.

### 📂 Generated Outputs

- Individual biomarker screening tables.
- Elastic Net-selected biomarker combinations.
- Logistic regression coefficient summaries.
- Odds ratios and statistical significance values.
- ROC-AUC comparisons.
- NRI results.
- Repeated-split performance summaries.
- Biomarker selection stability tables.

---

## 📈 Pipeline 2: Multiple Linear Regression — Continuous Musculoskeletal Outcomes

### 🎯 Research Objective

To investigate associations between circulating molecular biomarkers and continuous musculoskeletal or biochemical outcomes, and evaluate whether molecular predictors improve performance beyond clinical baseline models.

### 🧪 Investigated Outcomes

**Bone Mineral Density**

- Baseline total hip BMD.
- Baseline lumbar spine BMD.

**Longitudinal Bone Mineral Density Change**

- Change in total hip BMD.
- Change in lumbar spine BMD.

**Musculoskeletal Function**

- Grip strength.

**Biochemical Measurements**

- Osteocalcin (OC).
- PINP.
- PTH.
- CTX.

### 🧬 Biomarker Model Comparisons

Three model configurations are evaluated:

| Model | Predictors |
|---|---|
| Baseline | Outcome-specific clinical predictors |
| Baseline + miRNAs | Clinical predictors + selected miRNA ratios |
| Baseline + BTMs | Clinical predictors + selected BTMs |

**The linear regression workflow does not evaluate a combined miRNA + BTM model.**

The miRNA-only and BTM-only analyses are conducted separately for the relevant continuous outcomes.

When a biochemical marker is itself the outcome, the predictor set must exclude that outcome to avoid self-prediction.

### 🤖 Statistical and Machine-Learning Methods

- Multiple linear regression using `lm()`.
- Individual biomarker screening.
- Elastic Net regression using the Gaussian family.
- Cross-validation for regularization tuning.
- Selection of informative molecular predictors.
- Conventional linear regression refitting.
- Comparison of baseline and biomarker-augmented predictions.
- Repeated training and testing partitions.
- Biomarker selection stability analysis.

### 📊 Model Evaluation

The workflow evaluates:

- **R²:** Proportion of test-set outcome variation explained relative to the test-set mean.
- **RMSE:** Root mean squared prediction error.
- **MAE:** Mean absolute prediction error.
- **Regression coefficients (β):** Estimated associations between predictors and continuous outcomes.
- **Model comparison statistics:** Assessment of incremental biomarker contributions.
- **Residual diagnostics:** Evaluation of regression assumptions where applicable.
- **Selection frequency:** Stability of biomarker identification across repeated splits.

### 📂 Generated Outputs

- Individual biomarker screening results.
- Elastic Net-selected predictor sets.
- Regression coefficient tables.
- Model comparison statistics.
- RMSE, MAE, and R² summaries.
- Repeated-split predictive performance estimates.
- Biomarker selection stability summaries.

---

## ⏱️ Pipeline 3: Cox Proportional Hazards Regression — Time to Incident Nonvertebral Fracture

### 🎯 Research Objective

To identify circulating molecular biomarkers associated with time to incident nonvertebral fracture and evaluate whether their inclusion improves survival prediction beyond established clinical risk factors.

Unlike logistic regression, which models fracture occurrence as a binary outcome, Cox proportional hazards regression incorporates follow-up duration and censoring information.

### 🧪 Clinical Outcome and Data Preparation

**Primary outcome:** Time to incident nonvertebral fracture.

The analysis incorporates:

- Follow-up duration, measured in months.
- Incident nonvertebral fracture status (0 = censored, 1 = event).
- Mandatory clinical baseline predictors.
- Circulating microRNA ratios.
- Bone turnover markers.

The Cox workflow performs:

- Complete-case filtering.
- Validation of participant identifiers.
- Verification of binary fracture event coding.
- Validation of follow-up duration.
- Identification of nonpositive follow-up times.
- Removal of all-zero biomarker columns.
- Molecular predictor standardization.
- Preparation of survival outcome and predictor matrices.

Records with nonpositive follow-up times are explicitly identified and either excluded with an audit file or cause execution to stop, depending on the configured setting.

### 🧬 Biomarker Model Comparisons

The Cox framework supports four model configurations:

| Model | Predictors |
|---|---|
| Baseline | Mandatory clinical predictors |
| Baseline + miRNAs | Clinical predictors + circulating miRNA ratios |
| Baseline + BTMs | Clinical predictors + bone turnover markers |
| Baseline + miRNAs + BTMs | Clinical predictors + both biomarker categories |

These configurations allow evaluation of the incremental prognostic contribution of individual biomarker categories and their combination.

The Cox script processes the candidate biomarker columns supplied in the input dataset. Each molecular configuration therefore requires an appropriately prepared input dataset.

### 🔬 1. Individual Biomarker Cox Regression

Candidate biomarkers are evaluated individually by adding each molecular predictor to the mandatory clinical baseline model.

The analysis uses:

- Cox proportional hazards regression using `survival::coxph()`.
- Breslow approximation for tied event times.
- 50 stratified train/test partitions.
- 70% training and 30% testing observations.
- Stratification according to fracture event status.
- Conventional Cox regression without class balancing.

For each biomarker, the workflow estimates:

- Regression coefficient and standard error.
- Hazard ratio (HR).
- 95% confidence interval for the hazard ratio.
- Wald z-statistic and p-value.
- Harrell's C-index on held-out observations.
- Change in C-index relative to the baseline model.
- Nested partial-likelihood ratio test.
- Training AIC and BIC.
- Proportional hazards diagnostics.

The individual biomarker screening threshold is configurable and is set to **p < 0.10** in the supplied implementation.

### 🤖 2. Elastic Net Cox Regression

The workflow applies Elastic Net regularization using `glmnet` with the Cox survival family.

**Hyperparameter optimization:**

| Parameter | Configuration |
|---|---|
| Alpha (α) | 0.05–1.00 |
| Alpha increment | 0.05 |
| Cross-validation folds | 5, 10, 20 |
| Lambda selection | `lambda.min` |
| Cross-validation criterion | Concordance |
| Training/test splits | 50 |
| Training proportion | 70% |
| Testing proportion | 30% |

Internal cross-validation folds are stratified by fracture event status.

**Mandatory clinical predictors are included without penalization** using `penalty.factor = 0`, while candidate molecular biomarkers are subject to regularization.

This preserves the mandatory clinical predictors while allowing Elastic Net to select additional molecular biomarkers.

### 📊 3. Baseline and Biomarker-Augmented Model Comparison

The machine-learning baseline is fitted using Ridge-regularized Cox regression with mandatory clinical predictors.

Biomarker-augmented Elastic Net models are evaluated using the same training and testing partitions.

Model comparisons include:

- Baseline C-index.
- Biomarker-augmented C-index.
- Change in C-index (ΔC-index).
- Cross-validated concordance.
- Selected regularization parameters.
- Number and identity of selected molecular predictors.

The C-index is calculated using `survival::concordance()`, accounting for the direction of Cox linear risk scores.

### 🔁 4. Repeated Train/Test Validation

The analysis uses **50 stratified random train/test splits**, with 70% of observations assigned to training and 30% to testing.

The same partitions are reused across:

- Individual biomarker screening.
- Elastic Net modeling.
- Conventional Cox regression refitting.

The workflow summarizes predictive performance across repeated partitions, including:

- Mean C-index.
- Mean ΔC-index.
- Variation across random splits.
- Empirical 2.5th–97.5th percentile performance ranges.
- Biomarker selection frequencies.

These empirical ranges describe variability across repeated partitions and are not independent-sample confidence intervals.

### 🧬 5. Biomarker Selection and Stability Assessment

Elastic Net identifies molecular predictors with nonzero fitted coefficients.

The workflow records selected variables across combinations of:

- Random training/test splits.
- Alpha values.
- Cross-validation fold configurations.

Biomarker selection frequencies are calculated to evaluate consistency of molecular predictor identification.

For individual biomarker screening, the script defines a robustness threshold requiring:

- Statistical significance in at least **80% of the 50 splits**.
- Positive mean improvement in C-index relative to the clinical baseline model.

This corresponds to at least 40 significant splits.

Selection stability is interpreted as an internal measure of consistency rather than evidence of external validation.

### 📈 6. Conventional Cox Regression Refitting

Following Elastic Net feature selection, selected biomarker combinations are refitted using conventional Cox proportional hazards regression alongside mandatory clinical predictors.

The refitted models provide interpretable estimates including:

- Regression coefficients.
- Hazard ratios.
- Standard errors.
- Wald z-statistics.
- P-values.
- Confidence intervals.
- FDR-adjusted p-values.
- Model comparison statistics.

These estimates are exploratory because biomarker selection and conventional regression refitting use overlapping training observations.

### 🩺 7. Proportional Hazards Diagnostics

The workflow evaluates the proportional hazards assumption using `survival::cox.zph()`.

Diagnostics include:

- Global proportional hazards tests.
- Biomarker-specific proportional hazards tests.
- Recording diagnostic p-values across repeated partitions.

The workflow also checks for nonconvergent models, nonfinite coefficients, and invalid covariance estimates.

Models that fail specified validity checks are excluded from the corresponding results and recorded for review.

### 📂 8. Generated Outputs

The Cox pipeline generates:

- Individual biomarker screening results.
- Hazard ratios and coefficient summaries.
- Baseline and biomarker-augmented C-index comparisons.
- Elastic Net hyperparameter evaluation tables.
- Selected biomarker combinations.
- Biomarker selection-frequency summaries.
- Conventional Cox regression refitting results.
- Proportional hazards diagnostics.
- Failed-model and data-exclusion logs.
- Interactive HTML tables.
- Excel reports and diagnostic visualizations.

### 🔬 Interpretation

The Cox regression pipeline extends the OPUS biomarker-discovery framework from binary fracture prediction to time-to-event analysis.

Its primary purpose is to determine whether circulating miRNAs, BTMs, or their combination improve prediction of time to incident nonvertebral fracture beyond mandatory clinical predictors.

The framework incorporates regularized biomarker selection, repeated internal validation, conventional Cox regression refitting, and proportional hazards diagnostics.

Results should be interpreted as internally validated exploratory findings until independently replicated.

---

## 📊 Comparison of the Three Regression Pipelines

| Characteristic | Logistic Regression | Multiple Linear Regression | Cox Regression |
|---|---|---|---|
| Outcome type | Binary | Continuous | Time to event |
| Main outcomes | Vertebral and nonvertebral fractures | BMD, BMD change, grip strength, biochemical traits | Time to nonvertebral fracture |
| Regression family | Binomial | Gaussian | Cox |
| Regularization | Elastic Net | Elastic Net | Elastic Net |
| miRNAs only | Yes | Yes | Supported |
| BTMs only | Yes | Yes | Supported |
| miRNAs + BTMs | Yes | No | Supported |
| Repeated splits | 50 | 50 | 50 |
| Training/test ratio | 70/30 | 70/30 | 70/30 |
| Class imbalance handling | Training only | Not applicable | No class balancing |
| Main effect estimates | Odds ratios | Regression coefficients | Hazard ratios |
| Main prediction metrics | AUC, ΔAUC, NRI | R², RMSE, MAE | C-index, ΔC-index |
| Additional diagnostics | Model comparison tests | Residual diagnostics | Proportional hazards tests |
| Biomarker stability | Selection frequencies | Selection frequencies | Selection frequencies |

---

## 🧰 Technologies and R Packages

### 🤖 Machine Learning and Statistical Modeling

- `glmnet`
- `caret`
- `rsample`
- `tidymodels`
- `lmtest`

### 🩺 Clinical Prediction and Survival Analysis

- `survival`
- `pROC`
- `broom`
- Base R statistical functions

### 🔄 Data Processing

- `dplyr`
- `readxl`
- `writexl`
- `reshape2`

### 📈 Visualization and Reporting

- `ggplot2`
- `knitr`
- `kableExtra`
- `DT`
- `htmltools`

Package requirements vary between the three analytical workflows.

---

## 📂 Repository Structure

```text
Elastic-Net-ML-biomarker-discovery-UCSF-collaboration-OPUS-data/
│
├── README.md
├── LICENSE
│
├── Logistic_Regression.Rmd
├── Linear_Regression.Rmd
└── Cox_Regression.Rmd
```

The filenames above are illustrative and should be replaced with the actual filenames used in the repository.

Each workflow contains the corresponding data preparation, statistical modeling, machine-learning procedures, and reporting sections.

If the uploaded files contain executable R Markdown code chunks, their `.Rmd` extensions should be retained.

---

## ▶️ Reproducibility and Usage

The analytical framework is implemented in R and organized into outcome-specific workflows.

To reproduce an analysis:

1. Install R and the required CRAN or Bioconductor packages.
2. Obtain the relevant OPUS clinical and biomarker datasets through authorized access.
3. Configure the input and output directories.
4. Specify the clinical outcome and mandatory baseline predictor variables.
5. Select the molecular biomarker configuration.
6. Configure random seeds, cross-validation folds, and Elastic Net hyperparameters.
7. Execute preprocessing and individual biomarker screening.
8. Perform Elastic Net feature selection.
9. Refit the corresponding conventional regression model.
10. Evaluate predictive performance relative to the clinical baseline model.
11. Review statistical summaries and biomarker selection results.

The supplied scripts contain dataset-specific column indices and local file paths that may require adaptation before execution in another computational environment.

The original analyses cannot be reproduced without access to appropriately formatted OPUS datasets.

---

## 🔒 Data Availability and Research Ethics

This repository is intended to share computational methods rather than participant-level OPUS data.

Clinical records, individual-level molecular measurements, and restricted research datasets are not included.

Reproduction of the original analyses requires appropriate data access and compatible input datasets.

Researchers may adapt the computational methods to other clinical or molecular datasets, subject to applicable data-use agreements and software licensing conditions.

---

## ⚠️ Methodological Considerations

- **Predictive modeling versus causality:** Elastic Net performs regularized prediction and variable selection; it does not establish causal relationships.
- **Internal validation:** Repeated train/test splits assess performance variability but do not replace external validation.
- **Post-selection inference:** Statistical inference following data-driven biomarker selection may be affected by selection bias.
- **Biomarker stability:** Selection frequencies describe consistency across evaluated data partitions rather than independent replication.
- **Preprocessing:** The supplied Cox implementation uses global biomarker scaling before data splitting. This can introduce information leakage; training-only scaling is recommended for a more rigorous predictive validation design.
- **Multiple testing:** The Cox individual-screening implementation calculates FDR adjustment within fitted models. This should not be interpreted as controlling the false discovery rate across all screened biomarkers.
- **Class imbalance:** Training-set weighting or resampling in logistic regression can influence predicted probability calibration.
- **Survival analysis:** Cox regression requires appropriate handling of censoring and assessment of proportional hazards assumptions.
- **Performance generalizability:** Predictive performance may vary across populations, measurement platforms, and clinical settings.

The computational framework is intended for exploratory research and methodological development rather than direct clinical decision-making.

---

## 👨‍🔬 Author and Scientific Contributions

**David Carro Vázquez, PhD**

Computational bioinformatics researcher specializing in machine learning, molecular biomarker discovery, transcriptomics, and statistical modeling of biomedical datasets.

This repository documents computational work involving:

- Integration of clinical and molecular predictors.
- Development of outcome-specific clinical baseline models.
- Individual biomarker screening.
- Elastic Net regularization and hyperparameter optimization.
- Logistic regression for incident fracture prediction.
- Multiple linear regression for continuous musculoskeletal outcomes.
- Cox proportional hazards regression for time to nonvertebral fracture.
- Evaluation of miRNA-only and BTM-only predictive models.
- Investigation of combined miRNA + BTM models for fracture outcomes.
- Repeated training and testing procedures.
- Evaluation of incremental predictive performance.
- Biomarker selection stability assessment.
- Statistical diagnostics, reporting, and visualization.

The computational work was developed in the context of OPUS cohort research and scientific collaborations associated with the University of California, San Francisco.

---

## 📜 License

This repository is distributed under the terms specified in the `LICENSE` file.

If the repository uses the MIT License, users may reuse, modify, and distribute the licensed code subject to its conditions.

The license applies to the released code and does not grant access to restricted clinical datasets or third-party proprietary materials.

---

## 📬 Citation and Contact

**David Carro Vázquez, PhD**

GitHub: https://github.com/davicarro

For scientific inquiries, methodological questions, or research collaborations, please contact the repository author through GitHub.

If these computational methods contribute to published research, users are encouraged to cite the corresponding scientific publication in addition to acknowledging the software repository.
