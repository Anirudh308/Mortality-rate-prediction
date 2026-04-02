# Mortality-rate-prediction
ICU mortality prediction using Random Forest, XGBoost and Logistic Regression on the eICU Collaborative Research Database

Predicting ICU patient mortality from the first 24 hours of admission data using 
the eICU Collaborative Research Database.

## Results

| Model | CV AUC | Test AUC |
|---|---|---|
| Logistic Regression | 0.829 ± 0.040 | 0.856 |
| Random Forest | 0.876 ± 0.031 | **0.882** |
| XGBoost | 0.873 ± 0.027 | 0.878 |

Best model: **Random Forest — AUC 0.882**, consistent with published 
eICU benchmarks (0.82–0.88).

## Project Overview

Dataset: eICU Collaborative Research Database v2.0
Cohort: 1,000 patients (500 survivors, 500 non-survivors)
Feature window: First 24 hours of ICU admission only
Features: 71 (vital signs + lab biomarkers + demographics)
Models: Logistic Regression, Random Forest, XGBoost
Explainability: SHAP values (global + per-patient)

## Pipeline
```
Stage 1 → Data extraction & balanced cohort construction
Stage 2 → Feature engineering (time series → flat feature matrix)
Stage 3 → Preprocessing (imputation, encoding, scaling, train/test split)
Stage 4 → Model training with 5-fold cross-validation
Stage 5 → Evaluation (AUC-ROC, confusion matrix, SHAP)
```

## Key Methodological Decisions

**24-hour temporal constraint**: All features restricted to first 1,440 minutes
  of admission to prevent data leakage and ensure clinical validity
**Median imputation**: Chosen over mean for robustness to ICU outliers
**Balanced sampling**: Addresses 93% / 7% class imbalance in raw eICU data
**Data leakage correction**: Initial full-stay models scored AUC > 0.98 —
  identified as leakage and corrected by enforcing the temporal constraint

## Tech Stack

 Python 3.12, Google Colab
 pandas, NumPy, scikit-learn, XGBoost, SHAP
 matplotlib, seaborn, joblib

## Data Access

This project uses the **eICU Collaborative Research Database**, which requires 
a data use agreement and CITI training to access.

Request access at: https://eicu-crd.mit.edu/gettingstarted/access/

The data files are not included in this repository in compliance with the 
eICU data use agreement.

## How to Run

1. Complete the eICU data use agreement and download the database
2. Upload the files to Google Drive at the path:
   `/MyDrive/eicu-database/`
3. Open `icu_mortality_prediction.ipynb` in Google Colab
4. Run cells in order from top to bottom
5. Outputs are saved to `/MyDrive/eicu-database/scaled/`

## Author

Anirudh Sharma — Institute of Engineering and Technology Lucknow — 2026
