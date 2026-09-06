# Project 1: CRISP-DM 回归与分类实践（房价回归 + 慢性肾病分类）

## Goal
Produce a runnable Python project + a filled-in Word report (实验_基于CRISP-DM的回归与分类数据挖掘实践.docx) covering two full CRISP-DM pipelines: house-price regression and CKD classification. Fill in only Section 3 (实验过程及结果) and Section 4 (实验总结) — sections 1–2 are already written.

## Data (already in `data/`)
- `train.csv` (1460 rows, 80 features + `SalePrice`) — Kaggle house price train set
- `test.csv` (1459 rows, 80 features, no target)
- `sample_submission.csv` (Id, SalePrice) — submission format
- `kidney_disease.csv` (400 rows, 25 features + `classification` target: `ckd`/`notckd`)
  - Note: many numeric columns loaded as object due to stray whitespace/typos in raw CSV (e.g. `\t?`) — must clean before casting to float.
  - Many missing values across almost all columns.

## Folder structure to create
```
proj1_crispdm/
  data/                  # 4 csvs (copy from uploads)
  notebooks/ or src/
    01_house_price_eda.py
    02_house_price_preprocess.py
    03_house_price_model.py
    04_ckd_eda.py
    05_ckd_preprocess.py
    06_ckd_model.py
  outputs/
    figures/             # heatmaps, plots (png)
    metrics.json
    submission.csv        # for house price test set (matches sample_submission format)
  report/
    template_requirements.md   # formatting rules extracted from template docx
    report_draft.md            # section 3 & 4 content, later pasted into docx
```

## Task A — House Price Regression
1. **EDA**: shape, dtypes, missing % per column, target distribution (SalePrice — note skew, consider log1p transform), correlation of numeric features with SalePrice.
2. **Preprocessing**:
   - Numeric: impute median for missing (e.g. LotFrontage, MasVnrArea, GarageYrBlt).
   - Categorical: impute mode or "None" for features where NA is meaningful (e.g. Alley, PoolQC, Fence, FireplaceQu — NA means "does not have this feature").
   - Outlier check: GrLivArea vs SalePrice (known Kaggle outliers, e.g. GrLivArea > 4000 with low price).
   - Encode categoricals: one-hot for nominal, ordinal mapping for quality scales (Ex/Gd/TA/Fa/Po).
   - Scale numeric features (StandardScaler) for models sensitive to scale.
3. **Feature engineering**: Pearson correlation heatmap (top ~20 features vs SalePrice), drop highly collinear/redundant features, optionally create TotalSF = TotalBsmtSF+1stFlrSF+2ndFlrSF.
4. **Modeling**: baseline Linear Regression, then Ridge/Lasso, then a tree ensemble (RandomForestRegressor or XGBoost/LightGBM). Use train/validation split (or KFold CV) on train.csv.
5. **Evaluation**: RMSE, MAE, R² on validation; report log-scale RMSE since Kaggle scores that way.
6. **Output**: predict on test.csv, write outputs/submission.csv matching sample_submission.csv format.

## Task B — CKD Classification
1. **EDA**: shape, dtypes, missing % per column (this dataset has substantial missingness), class balance of `classification` (ckd vs notckd).
2. **Preprocessing**:
   - Clean stray characters/whitespace in numeric-looking object columns (pcv, wc, rc) before casting to numeric.
   - Impute missing: median for numeric, mode for categorical (or KNNImputer as a comparison method — nice for the report's "compare preprocessing methods" requirement).
   - Encode binary categoricals (rbc, pc, pcc, ba, htn, dm, cad, appet, pe, ane) as 0/1.
   - Encode target: ckd=1, notckd=0.
   - Standardize numeric features.
3. **Feature engineering**: correlation heatmap of numeric features vs target (or point-biserial), feature importance from a tree model, select top features.
4. **Modeling**: baseline Logistic Regression, then RandomForestClassifier or SVM. Use stratified train/test split (small dataset — consider 5-fold CV).
5. **Evaluation**: accuracy, precision, recall, F1, ROC-AUC, confusion matrix.

## Task C — Comparison write-up (report requirement #7)
Write a short comparison table/paragraph: how CRISP-DM stages, preprocessing choices, feature selection, modeling, and evaluation metrics differ between the regression and classification task. (Claude will draft this text — see report/report_draft.md.)

## Report formatting rules (from 数据挖掘实验报告_模板及要求.docx)
- Cover page: 题目/学院/专业班级/姓名/学号/完成时间, no header/page number.
- TOC own page, "目录" 黑体小二 centered; headings numbered 1 / 1.1 / 1.1.1.
- Chapter titles (一级标题) start new page, centered, 黑体小二号.
- Body text: 宋体小四号 (Chinese) / Times New Roman (non-Chinese), 1.25 line spacing, first-line indent 2 chars.
- Tables: caption above, centered, 宋体小五号加粗, numbered by chapter (表2.1...). Figures: caption below, same style, numbered by chapter (图2.1...).
- Page numbers centered in body; header = experiment title; not on cover/TOC.
- Every code block / figure / table needs accompanying explanatory text.

## Deliverables checklist
- [ ] `data/` populated, all 4 CSVs load cleanly
- [ ] House price: EDA + cleaning + heatmap + ≥2 models + metrics + submission.csv
- [ ] CKD: EDA + cleaning + heatmap + ≥2 models + metrics (incl. confusion matrix)
- [ ] Comparison section (regression vs classification across CRISP-DM stages)
- [ ] report/report_draft.md written in Chinese, ready to paste into docx Section 3 & 4
- [ ] Figures exported as PNG to outputs/figures/ for embedding in the Word doc
- [ ] Final docx assembled following template formatting rules (Claude will do this step directly, not Kilo Code, since it needs the docx skill)

## Notes for Kilo Code
- Use pandas, numpy, matplotlib/seaborn, scikit-learn (add xgboost only if available).
- Keep each script runnable standalone (`python src/0X_....py`), saving intermediate artifacts to outputs/.
- Prefer simple, well-commented code since it must be pasted as "含注释的源代码" into the report.
- Random seed = 42 everywhere for reproducibility.
