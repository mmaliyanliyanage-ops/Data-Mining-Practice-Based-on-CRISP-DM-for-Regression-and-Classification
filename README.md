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
<img width="945" height="790" alt="image" src="https://github.com/user-attachments/assets/e7ded929-c0b4-4018-9e48-82c6e8de932a" />
<img width="1188" height="390" alt="image" src="https://github.com/user-attachments/assets/ebb77237-fc5d-421a-bbd9-5e2f8eac2892" />
<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/532405c9-f30e-4b78-a871-0016dd4f4092" />
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/a89a6e51-fe9f-446f-962c-4406b67746f0" />
