Project for ML Aging
# Predicting Cardiovascular Disease Using Machine Learning

A comparative evaluation of Logistic Regression, Naive Bayes, and Random Forest models to predict cardiovascular disease risk from routine clinical measurements, with a focus on model interpretability, robustness, and fairness — completed as part of the *ML for Aging & Longevity* course, Sommersemester 2025.

## Overview

This project uses medical examination data to classify whether a patient has cardiovascular disease. Beyond just optimizing accuracy, the analysis compares three models across interpretability, robustness to outliers, computational cost, and fairness — with the goal of identifying a model suitable for real-world clinical deployment, not just a leaderboard score.

## Dataset

- **Source:** [Kaggle — Cardiovascular Disease dataset](link-to-your-kaggle-source)
- **Size:** ~70,000 patient records
- **Target:** `cardio` (binary — presence/absence of cardiovascular disease)
- **Features (11 total):**
  - *Objective:* age, height, weight, gender
  - *Examination:* systolic/diastolic blood pressure, cholesterol, glucose
  - *Subjective (self-reported):* smoking, alcohol intake, physical activity

## Approach

1. **Missing data handling** — investigated patterns of missingness (`missingno`), applied multiple imputation via `miceforest` / `IterativeImputer`
2. **Outlier treatment** — cleaned implausible values in `weight`, blood pressure fields
3. **Feature engineering** — e.g. converting age from days to years, discretizing blood pressure into ordinal bins for Naive Bayes
4. **Modeling** — trained and tuned Logistic Regression, Naive Bayes, and Random Forest
5. **Evaluation** — compared models on accuracy, recall, train/test generalization gap, interpretability, robustness, and computational cost
6. **Fairness analysis** — examined class imbalance (gender, lifestyle features) and its implications for underrepresented subgroups

## Results
All three models showed similar accuracy and recall with minimal train/test gap, indicating no overfitting. **Random Forest** was selected as the final model for its higher accuracy/recall and robustness to noise, despite being the least interpretable and most computationally expensive.

## Key Findings

- **Interpretability vs. performance tradeoff:** Logistic Regression offers the clearest explanations (coefficients, odds ratios) — valuable for clinical trust — while Random Forest trades transparency for better handling of non-linear relationships.
- **Fairness considerations:** The dataset shows significant gender imbalance and skews toward healthy lifestyles (non-smokers, non-drinkers, physically active). These imbalanced features tend to contribute less to final predictions after feature selection, but this reduces interpretability of *why* a subgroup may be under-served rather than eliminating the underlying risk — correlated features can still encode bias indirectly.
- **Deployment simplicity:** The final model requires only two key inputs (systolic blood pressure and cholesterol level), making it easy to integrate into clinical workflows — though this simplicity also limits opportunities to audit or correct subgroup-specific errors.

## Limitations

- Missing documentation on original data collection process and consent (Kaggle-sourced) — unclear GDPR compliance
- Demographic imbalance (gender, lifestyle factors) may limit generalizability
- Population/region of origin not fully disclosed, limiting applicability to broader populations

## Future Work

- Incorporate additional features (e.g. BMI, computed from height/weight)
- More extensive hyperparameter tuning across patient subgroups
- Collect more demographically diverse data to reduce
