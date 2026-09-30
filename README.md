# Predicting National Cybersecurity Readiness from Socioeconomic Indicators

**Master's Thesis Project — Ayumi Hierl**

A machine learning study investigating whether **national cybersecurity readiness** can be predicted from socioeconomic indicators such as human capital, economic development, education, and government expenditure.

The project combines **World Bank socioeconomic data** with the **2020 Global Cybersecurity Index (GCI)** from the International Telecommunication Union (ITU).

Four regression models were developed and compared:

* Linear Regression
* Generalized Additive Model (GAM)
* Support Vector Regression (SVR)
* XGBoost

The analysis includes nested cross-validation, hyperparameter tuning, synthetic data augmentation, subgroup error analysis, statistical testing, and SHAP-based explainability.

---

## Research Question

> **To what extent can national cybersecurity readiness be predicted from socioeconomic indicators?**

The study examines whether nonlinear machine learning models provide meaningful improvements over a classical linear baseline.

---

## Dataset

The final dataset combines:

* **World Bank World Development Indicators (WDI)**
* **World Bank Human Capital Index (HCI)**
* **ITU Global Cybersecurity Index 2020**

### Target

**Global Cybersecurity Index (GCI) 2020** — a 0–100 measure of national cybersecurity performance.

### Predictors

Socioeconomic indicators covering:

* Human capital
* GDP per capita (PPP)
* Education
* Government expenditure
* Industry structure
* Capital formation
* Inflation
* Trade
* Unemployment

**Final dataset:** 177 countries and 13 predictors.

---

## Methodology

```text
Data Collection
      ↓
Data Integration
      ↓
Exploratory Data Analysis
      ↓
Feature Selection & Preprocessing
      ↓
Data Augmentation
      ↓
Nested Cross-Validation
      ↓
Hyperparameter Tuning
      ↓
Model Evaluation
      ↓
Error & SHAP Analysis
```

Preprocessing included iterative imputation, Yeo-Johnson transformations, standardization, and multicollinearity reduction.

A **Gaussian Copula** was also investigated for synthetic data augmentation, expanding the training-validation data from 141 to 282 observations while keeping the test set untouched.

Models were evaluated using:

* MAE
* RMSE
* R²
* Repeated cross-validation
* Statistical significance tests
* Bootstrap confidence intervals

---

## Results

### Test Set Performance

| Model             |       R² |       MAE |      RMSE |
| ----------------- | -------: | --------: | --------: |
| Linear Regression |     0.57 |     18.55 |     23.18 |
| GAM               |     0.58 |     18.60 |     22.70 |
| SVR               |     0.50 |     21.17 |     24.93 |
| **XGBoost**       | **0.62** | **18.36** | **21.56** |

XGBoost achieved the strongest test-set performance, but its improvement over the simpler models was relatively small and accompanied by a larger training-validation gap.

This suggests that **model complexity provides limited additional value for this small cross-country dataset**.

### Data Augmentation

Gaussian Copula augmentation particularly affected SVR and XGBoost performance. For XGBoost, test MAE decreased from **18.36 to 17.13**.

---

## Income Group Analysis

Prediction errors were compared across World Bank income groups.

For XGBoost:

| Income Group        | Mean MAE |
| ------------------- | -------: |
| Low income          |    17.98 |
| Lower-middle income |    22.72 |
| Upper-middle income |    19.49 |
| High income         |    11.98 |

**Lower-middle-income countries showed the highest prediction errors**, suggesting greater heterogeneity that was not fully captured by the available socioeconomic indicators.

---

## SHAP Explainability

SHAP analysis of XGBoost identified the following as the strongest contributors:

1. Human Capital Index
2. GDP per capita (PPP)
3. Secondary school enrollment
4. Industry share of GDP
5. Tertiary enrollment
6. Government expenditure

The results highlight **human capital and economic development** as important predictors of national cybersecurity readiness.

---

## Main Findings

* Socioeconomic indicators can explain a meaningful portion of variation in national cybersecurity readiness.
* XGBoost achieved the strongest test performance, but simpler models remained competitive.
* Prediction accuracy varied substantially across income groups.
* Human capital and GDP per capita were the most influential predictors in the SHAP analysis.
* The results indicate predictive relationships, **not causal effects**.

---

## Limitations & Future Work

Key limitations include:

* Small dataset of 177 countries
* Single GCI edition (2020)
* XGBoost overfitting
* Limited observations in the low-income group
* Conceptual overlap between HCI and education variables
* Synthetic data cannot replace additional real-world observations

Future work could focus on:

* Longitudinal datasets across multiple GCI editions
* Country- or income-group-specific models
* Additional governance and institutional indicators
* Alternative augmentation methods
* Causal and longitudinal analysis

---

## Technical Skills

**Machine Learning:**
Linear Regression, GAM, SVR, XGBoost, hyperparameter optimization

**Evaluation:**
Nested cross-validation, repeated k-fold CV, MAE, RMSE, R², statistical testing, bootstrap confidence intervals

**Data Science:**
API data collection, data integration, EDA, imputation, feature selection, transformation, augmentation

**Explainable AI:**
SHAP, feature importance, nonlinear effect analysis

**Tools:**
Python, pandas, NumPy, scikit-learn, XGBoost, SHAP

---

## Reproducibility

The project was implemented in Python using publicly available World Bank and ITU data.

The repository contains the code for data processing, modeling, evaluation, visualization, and explainability analysis.

---

## Author

**Ayumi Hierl**
Master's Thesis Project

*Predicting National Cybersecurity Readiness from Socioeconomic Indicators*

**Research areas:** Cybersecurity · Socioeconomics · Machine Learning · Explainable AI
