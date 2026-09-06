# Data-Mining-Practice-Based-on-CRISP-DM-for-Regression-and-Classification
# CRISP-DM Experiment: Regression & Classification

A data mining practice notebook applying the full **CRISP-DM** (Cross-Industry
Standard Process for Data Mining) six-phase methodology to two classic tasks:

## Part 1 — House Price Prediction (Regression)
- **Dataset:** Kaggle House Prices (`train.csv`)
- **Goal:** Predict continuous `SalePrice` from property features
- **Pipeline:** missing-value imputation (median/mode), IQR-based outlier removal,
  log-transform of the skewed target, one-hot encoding, feature scaling
- **Models compared:** Linear Regression, Ridge, Random Forest, Gradient Boosting
- **Evaluation:** 5-fold CV RMSE, validation RMSE/MAE/R², residual analysis

## Part 2 — Chronic Kidney Disease Diagnosis (Classification)
- **Dataset:** Kidney Disease dataset (`kidney_disease.csv`)
- **Goal:** Binary classification (CKD vs. not-CKD) from clinical lab values
- **Pipeline:** text cleaning, numeric coercion, missing-value imputation,
  one-hot encoding, scaling
- **Models compared:** Logistic Regression, Random Forest, Gradient Boosting
- **Evaluation:** Accuracy, Precision, Recall, F1, ROC-AUC, confusion matrix, ROC curve
  (recall emphasized as clinically critical)

## Structure
Each task walks through all six CRISP-DM phases — Business Understanding, Data
Understanding, Data Preparation, Modeling, Evaluation, and Result Analysis — with
visualizations (missing-value plots, correlation heatmaps, feature importance,
model comparison bar charts) throughout.

**Tech stack:** pandas, numpy, scikit-learn, matplotlib, seaborn
