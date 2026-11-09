# Elastic-Net-ML-biomarker-discovery-UCSF-collaboration-OPUS-data
R-based machine learning framework integrating Elastic Net regularization with logistic, Cox proportional hazards, and linear regression to identify circulating microRNA biomarkers associated with fracture risk, time-to-fracture, and bone mineral density in the OPUS cohort.

# 🧬 Elastic Net Machine Learning for Circulating Biomarker Discovery in Osteoporosis

### 🤖 Logistic Regression | Cox Proportional Hazards | Multiple Linear Regression | OPUS Cohort

**Author:** David Carro Vázquez, PhD  
**Research affiliation:** Department of Orthopedic Surgery, University of California, San Francisco (UCSF)  
**Programming language:** R / R Markdown  
**Research areas:** Machine Learning | Osteoporosis | Biomarker Discovery | microRNA | Bone Turnover Markers | Fracture Risk Prediction | Survival Analysis | Biostatistics

---

## 📖 Project Overview

This repository documents an R-based computational framework developed to investigate the predictive value of circulating molecular biomarkers for osteoporotic fractures, bone mineral density (BMD), longitudinal bone loss, and related musculoskeletal outcomes.

The analyses are based on the **Osteoporosis and Ultrasound Study (OPUS)** cohort and integrate clinical predictors with circulating microRNAs (miRNAs) and bone turnover markers (BTMs).

The computational framework combines conventional regression methods with **Elastic Net regularization**, enabling biomarker selection from correlated molecular predictors and evaluation of their incremental predictive contribution beyond established clinical variables.

Three complementary regression approaches are implemented or planned:

- 🩺 **Logistic regression:** Prediction of incident vertebral and nonvertebral fractures.
- 📈 **Multiple linear regression:** Prediction of continuous musculoskeletal and biochemical outcomes, including baseline BMD, BMD change, grip strength, and selected bone metabolism markers.
- ⏱️ **Cox proportional hazards regression:** Prediction of time to incident nonvertebral fracture.

The principal objective is to determine whether circulating biomarkers improve predictive performance beyond clinical baseline models.

### Biomarker Integration Strategy

The framework investigates three molecular biomarker configurations:

1. **miRNAs only:** Circulating microRNA expression ratios.
2. **BTMs only:** Circulating biochemical markers of bone metabolism.
3. **miRNAs + BTMs:** Combined molecular predictors from both biomarker categories.

The logistic and Cox regression frameworks evaluate all three biomarker configurations.

The multiple linear regression framework evaluates miRNAs and BTMs separately, without a combined miRNA + BTM model.

---

## 🎯 Research Objectives

1. Identify circulating miRNA signatures associated with osteoporotic fracture risk and quantitative musculoskeletal phenotypes.
2. Investigate the predictive contribution of circulating bone turnover markers.
3. Determine whether miRNAs and BTMs provide complementary predictive information when combined.
4. Apply Elastic Net regularization to select informative biomarkers from high-dimensional and correlated molecular predictors.
5. Evaluate whether selected biomarkers improve prediction beyond established clinical risk factors.
6. Compare predictive performance across binary, continuous, and time-to-event outcomes.
7. Assess the stability of biomarker selection across repeated training and testing partitions.
8. Develop a reusable computational framework for molecular biomarker discovery and clinical prediction.

---

## 🧪 Study Cohort and Molecular Biomarkers

### 🔹 OPUS Cohort

The analyses use data from the Osteoporosis and Ultrasound Study (OPUS), comprising approximately **1,128 postmenopausal women aged 55–80 years**.

The dataset includes clinical characteristics, bone mineral density measurements, circulating molecular biomarkers, and longitudinal information on incident osteoporotic fractures.

The cohort provides a framework for investigating relationships between circulating molecular markers, skeletal health, and fracture outcomes.

### 🔹 1. Circulating MicroRNAs (miRNAs)

Serum microRNAs were measured using the osteomiR platform, which profiles 19 candidate miRNAs.

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

The analyses incorporate circulating biochemical markers associated with bone formation, resorption, and bone metabolism.

**Investigated markers include:**

- **Osteocalcin (OC):** Marker associated with bone formation.
- **Procollagen type I N-terminal propeptide (PINP/P1NP):** Marker of type I collagen formation.
- **C-terminal telopeptide of type I collagen (CTX):** Marker of bone resorption.
- **Parathyroid hormone (PTH):** Hormone involved in calcium homeostasis and bone metabolism.

These biomarkers provide complementary information about bone remodeling processes.

### 🔹 3. Clinical Baseline Predictors

Clinical baseline models incorporate outcome-specific combinations of:

- Age.
- Body mass index (BMI).
- Total hip BMD.
- Lumbar spine BMD.
- Prevalent vertebral or nonvertebral fracture history.
- Additional clinical or technical covariates where applicable.

The exact baseline model is defined separately for each outcome.

**All biomarker-augmented models are compared against their corresponding clinical baseline models.**

---

## ⚙️ Shared Computational Analysis Framework

The regression pipelines follow a common analytical strategy, adapted to the statistical properties of each outcome.

### 🔹 1. Data Import and Preprocessing

The workflow imports clinical and molecular biomarker datasets and prepares them for statistical analysis.

**Main analytical steps:**

- Import clinical and biomarker data from Excel files.
- Define outcome variables and baseline predictors.
- Identify candidate miRNA and BTM predictors.
- Evaluate missing observations.
- Remove invalid or noninformative biomarker columns.
- Convert categorical variables into appropriate data types.
- Prepare outcome-specific analytical datasets.
- Generate numerical predictor matrices.
- Standardize molecular predictors where required.

### 🔹 2. Construction of Clinical Baseline Models

For each clinical outcome, a baseline model is constructed using established clinical predictors without the molecular biomarkers under investigation.

These baseline models provide the reference for evaluating incremental biomarker performance.

The same outcome-specific baseline definition is retained when comparing molecular biomarker configurations.

### 🔹 3. Individual Biomarker Screening

Candidate molecular biomarkers are evaluated individually by adding them to the corresponding baseline clinical model.

**Main analytical steps:**

- Fit baseline regression models.
- Add candidate biomarkers individually.
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
- **Cross-validation folds:** Used to optimize the regularization parameters within the training data.

Elastic Net is applied to select informative molecular biomarkers from potentially correlated predictor sets.

### 🔹 5. Biomarker Model Configurations

Three biomarker configurations are considered across the project.

**Model A — miRNAs only**

Clinical baseline predictors are combined with selected circulating miRNA ratios.

**Model B — BTMs only**

Clinical baseline predictors are combined with selected bone turnover markers.

**Model C — miRNAs + BTMs**

Clinical baseline predictors are combined with selected biomarkers from both molecular categories.

Model C is evaluated in the logistic regression analyses and is planned for the Cox regression analyses, but not in the multiple linear regression workflow.

### 🔹 6. Regression Model Refitting

Selected biomarkers can be incorporated into conventional regression models alongside mandatory clinical predictors.

This allows estimation of interpretable regression coefficients and comparison of clinical baseline models with biomarker-augmented models.

**Effect estimates depend on the regression family:**

- Logistic regression: Odds ratios.
- Multiple linear regression: Regression coefficients.
- Cox regression: Hazard ratios.

Statistical inference following data-driven biomarker selection is interpreted cautiously because selection may introduce bias.

### 🔹 7. Repeated Train/Test Evaluation

The logistic and linear regression implementations use repeated training and testing partitions to assess predictive performance.

The supplied scripts specify:

- 50 random train/test splits.
- 70% training / 30% testing.
- Consistent partitions for comparisons within each analysis.
- Biomarker selection using training observations.
- Predictive performance evaluation using held-out observations.

The logistic regression implementation also incorporates class-imbalance handling within the training data.

The test-set event distribution is preserved.

The Cox regression validation strategy will be documented after its implementation is finalized.

### 🔹 8. Model Performance and Biomarker Stability

Predictive performance is evaluated using metrics appropriate to the outcome type.

The framework also examines biomarker selection frequencies across repeated partitions to investigate selection stability.

Repeated-split performance estimates provide internal validation but do not replace external validation in an independent cohort.

---

## 🩺 Pipeline 1: Logistic Regression — Incident Osteoporotic Fractures

### Research Objective

To identify circulating molecular biomarkers that improve the prediction of incident osteoporotic fractures beyond established clinical risk factors.

### Clinical Outcomes

Two binary outcomes are investigated:

1. **Incident vertebral fracture.**
2. **Incident nonvertebral fracture.**

### Biomarker Model Comparisons

Four predictive model configurations are evaluated.

| Model | Predictors |
|---|---|
| Baseline | Clinical predictors only |
| Baseline + miRNAs | Clinical predictors + selected miRNA ratios |
| Baseline + BTMs | Clinical predictors + selected bone turnover markers |
| Baseline + miRNAs + BTMs | Clinical predictors + selected miRNAs and BTMs |

The combined model investigates whether the two molecular biomarker categories provide complementary predictive information.

### Statistical and Machine-Learning Methods

- Binary logistic regression using `glm()`.
- Individual biomarker screening.
- Training-set class-imbalance handling.
- Elastic Net logistic regression using `glmnet`.
- Cross-validation for regularization tuning.
- Selection of biomarkers with nonzero coefficients.
- Conventional logistic regression refitting.
- Comparison of baseline and biomarker-augmented models.

### Model Evaluation

The workflow evaluates:

- **ROC-AUC:** Discrimination between participants with and without incident fractures.
- **ΔAUC:** Improvement or deterioration relative to the baseline model.
- **Net Reclassification Improvement (NRI):** Changes in risk classification at specified thresholds.
- **Odds ratios (OR):** Association estimates for selected biomarkers.
- **Statistical significance:** Regression and model-comparison tests.
- **FDR-adjusted p-values:** Multiple-testing adjustment where implemented.
- **Biomarker selection frequency:** Stability across repeated data partitions.

The supplied logistic implementation includes NRI evaluation using risk thresholds of 0.10 and 0.20.

### Generated Outputs

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

### Research Objective

To investigate associations between circulating molecular biomarkers and continuous musculoskeletal or biochemical outcomes, and evaluate whether molecular predictors improve performance beyond clinical baseline models.

### Investigated Outcomes

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

### Biomarker Model Comparisons

Three model configurations are evaluated:

| Model | Predictors |
|---|---|
| Baseline | Outcome-specific clinical predictors |
| Baseline + miRNAs | Clinical predictors + selected miRNA ratios |
| Baseline + BTMs | Clinical predictors + selected BTMs |

**The linear regression workflow does not evaluate a combined miRNA + BTM model.**

The miRNA-only and BTM-only analyses are conducted separately for the relevant continuous outcomes.

When a biochemical marker is itself the outcome, the predictor set must be defined to avoid including the outcome as its own predictor.

### Statistical and Machine-Learning Methods

- Multiple linear regression using `lm()`.
- Individual biomarker screening.
- Elastic Net regression using the Gaussian family.
- Cross-validation for regularization tuning.
- Selection of informative molecular predictors.
- Conventional linear regression refitting.
- Comparison of baseline and biomarker-augmented predictions.

### Model Evaluation

The workflow evaluates:

- **R²:** Proportion of test-set outcome variation explained relative to the test-set mean.
- **RMSE:** Root mean squared prediction error.
- **MAE:** Mean absolute prediction error.
- **Regression coefficients (β):** Estimated associations between predictors and continuous outcomes.
- **Model comparison statistics:** Assessment of incremental biomarker contributions.
- **Residual diagnostics:** Evaluation of regression assumptions where applicable.
- **Selection frequency:** Stability of biomarker identification across repeated splits.

### Generated Outputs

- Individual biomarker screening results.
- Elastic Net-selected predictor sets.
- Regression coefficient tables.
- Model comparison statistics.
- RMSE, MAE, and R² summaries.
- Repeated-split predictive performance estimates.
- Biomarker selection stability summaries.

---

## ⏱️ Pipeline 3: Cox Proportional Hazards Regression — Time to Incident Nonvertebral Fracture

### Research Objective

To investigate circulating molecular biomarkers associated with time to incident nonvertebral fracture and determine whether they improve survival prediction beyond established clinical risk factors.

Unlike logistic regression, which models fracture occurrence as a binary outcome, Cox regression incorporates follow-up duration and censoring information.

### Clinical Outcome

**Time to incident nonvertebral fracture.**

The analysis requires:

- Follow-up duration.
- Incident nonvertebral fracture status.
- Clinical baseline predictors.
- Circulating miRNA ratios.
- Bone turnover markers.

### Biomarker Model Comparisons

Four model configurations will be evaluated:

| Model | Predictors |
|---|---|
| Baseline | Clinical predictors only |
| Baseline + miRNAs | Clinical predictors + selected miRNA ratios |
| Baseline + BTMs | Clinical predictors + selected bone turnover markers |
| Baseline + miRNAs + BTMs | Clinical predictors + selected miRNAs and BTMs |

The combined model will investigate whether integrating miRNAs and BTMs improves time-to-fracture prediction beyond either biomarker category alone.

### Planned Statistical and Machine-Learning Methods

The intended analytical framework includes:

- Cox proportional hazards regression.
- Elastic Net regularization for survival outcomes.
- Cross-validation for regularization parameter optimization.
- Individual biomarker screening.
- Multivariable biomarker selection.
- Conventional Cox regression refitting.
- Comparison of baseline and biomarker-augmented survival models.
- Assessment of biomarker selection stability.
- Evaluation of proportional hazards assumptions.

### Planned Model Evaluation

Potential evaluation measures include:

- **Hazard ratios (HR):** Associations between biomarkers and fracture hazard.
- **Concordance index (C-index):** Discrimination of survival predictions.
- **Time-dependent ROC-AUC:** Discrimination at specified follow-up times.
- **Likelihood-ratio tests:** Comparison of nested Cox models.
- **Proportional hazards diagnostics:** Assessment of model assumptions.

The exact validation strategy, follow-up horizons, and reported metrics will be confirmed after the Cox script is finalized.

### Development Status

The Cox regression analysis is planned for time to incident nonvertebral fracture, using the three biomarker configurations described above.

Its final implementation and analytical results will be documented when the Cox script is available.

---

## 📊 Comparison of the Three Regression Pipelines

| Characteristic | Logistic | Multiple Linear | Cox |
|---|---|---|---|
| Outcome type | Binary | Continuous | Time to event |
| Main outcomes | Vertebral and nonvertebral fractures | BMD, BMD change, grip strength, biochemical traits | Nonvertebral fracture timing |
| Regression family | Binomial | Gaussian | Cox |
| Regularization | Elastic Net | Elastic Net | Planned Elastic Net |
| miRNAs only | Yes | Yes | Yes, planned |
| BTMs only | Yes | Yes | Yes, planned |
| miRNAs + BTMs | Yes | No | Yes, planned |
| Class imbalance handling | Training only | Not applicable | To be defined |
| Main effect estimates | Odds ratios | Regression coefficients | Hazard ratios |
| Main prediction metrics | AUC, ΔAUC, NRI | R², RMSE, MAE | C-index, time-dependent AUC (planned) |

---

## 🧰 Technologies and R Packages

### 🤖 Machine Learning and Statistical Modeling

- `glmnet`
- `caret`
- `rsample`
- `tidymodels`
- `lmtest`

### 🩺 Clinical Prediction and Model Evaluation

- `pROC`
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

Additional survival-analysis dependencies will be documented when the Cox pipeline is finalized.

---

## 📂 Repository Structure

```text
ElasticNet-miRNA-Biomarker-Discovery-OPUS/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── Logistic_Regression.R
├── Linear_Regression.R
└── Cox_Regression.R
```

The filenames above are suggested names. They should be replaced with the actual uploaded filenames.

If the workflows contain executable R code chunks, Markdown explanations, and reporting configuration, retaining their `.Rmd` extensions is recommended.

---

## ▶️ Reproducibility and Usage

The analytical framework is implemented in R and organized into outcome-specific workflows.

To reproduce an analysis:

1. Install R and the required CRAN or Bioconductor packages.
2. Obtain the relevant OPUS clinical and biomarker datasets through authorized access.
3. Configure the input and output directories.
4. Specify the clinical outcome and baseline predictor variables.
5. Select the molecular biomarker configuration.
6. Configure the random seeds, cross-validation folds, and Elastic Net hyperparameter grid.
7. Execute preprocessing and individual biomarker screening.
8. Perform Elastic Net feature selection.
9. Refit the corresponding conventional regression model.
10. Evaluate predictive performance relative to the baseline model.
11. Review the generated statistical summaries and biomarker selection results.

The supplied scripts contain dataset-specific column indices and local file paths that may require adaptation before execution in another computational environment.

---

## 🔒 Data Availability and Research Ethics

The repository is intended to share computational methods rather than participant-level OPUS data.

Clinical records, individual-level molecular measurements, and restricted research datasets are not included.

Reproduction of the original analyses requires appropriate data access and compatible input datasets.

Researchers may adapt the computational methods to other clinical or molecular datasets, subject to applicable data-use agreements and software licensing conditions.

---

## ⚠️ Methodological Considerations

- Elastic Net performs regularized prediction and variable selection; it does not establish causality.
- Biomarker selection frequencies describe stability within the evaluated data partitions rather than independent replication.
- Repeated train/test splits provide internal validation but do not replace external validation.
- Statistical inference after data-driven biomarker selection may be affected by selection bias.
- Scaling and other learned preprocessing parameters should be estimated within training partitions to avoid information leakage.
- Class weighting or resampling can affect predicted probability calibration.
- Cox regression requires appropriate handling of censoring and assessment of proportional hazards assumptions.
- Predictive performance may vary across populations, measurement platforms, and clinical settings.

---

## 👨‍🔬 Author and Scientific Contributions

**David Carro Vázquez, PhD**

Computational bioinformatics researcher specializing in machine learning, molecular biomarker discovery, transcriptomics, and statistical modeling of biomedical datasets.

This repository documents computational work involving:

- Integration of clinical and molecular predictors.
- Development of outcome-specific baseline models.
- Individual biomarker screening.
- Elastic Net regularization and hyperparameter optimization.
- Logistic regression for incident fracture prediction.
- Multiple linear regression for continuous musculoskeletal outcomes.
- Development of a Cox survival-analysis framework for time to nonvertebral fracture.
- Evaluation of miRNA-only and BTM-only predictive models.
- Investigation of combined miRNA + BTM models for fracture outcomes.
- Repeated training and testing procedures.
- Evaluation of incremental predictive performance.
- Biomarker selection stability assessment.
- Statistical reporting and visualization.

The work was developed in the context of OPUS cohort research and scientific collaborations associated with the University of California, San Francisco.

---

## 📜 License

This repository is distributed under the terms specified in the `LICENSE` file.

If the repository uses the MIT License, users may reuse, modify, and distribute the licensed code subject to the license conditions.

The license applies to the released code and does not grant access to restricted clinical datasets or third-party proprietary materials.

---

## 📬 Citation and Contact

**David Carro Vázquez, PhD**

GitHub: https://github.com/davicarro

For scientific inquiries, methodological questions, or research collaborations, please contact the author through GitHub.

If these computational methods contribute to published research, users are encouraged to cite the corresponding scientific publication in addition to acknowledging the software repository.
