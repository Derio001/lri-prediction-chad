# Chad Child Health: Predicting Lower Respiratory Infection (LRI)

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![DHS Data](https://img.shields.io/badge/Data-DHS_KR-green)](https://dhsprogram.com/data/dataset/Chad_Standard-DHS_2014.cfm?flag=0)
[![Machine Learning](https://img.shields.io/badge/ML-Classification-orange)](https://scikit-learn.org/)

This project develops a machine learning pipeline to predict **Lower Respiratory Infection (LRI)** in children under five in Chad, utilizing the Demographic and Health Survey (DHS) Children's Recode (KR) dataset. The goal is to identify key risk factors and build a predictive model to assist in health interventions.

## Project Overview

Lower Respiratory Infection remains a leading cause of childhood mortality in sub-Saharan Africa. This repository implements an end-to-end data science workflow—from raw data cleaning and target construction to advanced class-imbalance handling (SMOTE) and model evaluation.

### Key Features
- **Curated Target Construction**: Logic-based LRI labeling using `H31`, `H31B`, and `H31C` survey columns.
- **Informed Undersampling**: Removing low-quality survey records (high NaN counts in negative cases).
- **Statistical Feature Selection**: T-tests for numerical signficance and Chi-Square tests for categorical importance.
- **Automated Preprocessing**: Handling "Don't know" responses, median/mode imputation, and dummy encoding.
- **SMOTE Balancing**: Addressing class imbalance by generating synthetic positive cases.
- **Multi-Model Benchmarking**: Support for 8+ algorithms including XGBoost, LightGBM, CatBoost, and Random Forest.

## Technologies
- **Core**: Python, Pandas, NumPy
- **ML Frameworks**: Scikit-Learn, XGBoost, LightGBM, CatBoost, Imbalanced-learn (SMOTE)
- **Visualization**: Matplotlib, Seaborn

## Project Structure
- `Mahamat_LRI_CHAD.ipynb`: Main analysis and experimentation notebook.
- `Mahamat_LRI_CHAD.py`: Cleaned Python script version of the full pipeline.
- `chad_dhs_kr.csv`: The primary dataset (DHS KR recode for Chad).
- `verify_data.py`: Quick diagnostic script for checking target distribution.
- `extract.py`: Utility script to extract code cells from Jupyter notebooks.

## How to Run

1. **Install Dependencies**:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm catboost imbalanced-learn
   ```

2. **Prepare Data**:
   Ensure `chad_dhs_kr.csv` is in the project root.

3. **Run the Pipeline**:
   ```bash
   python Mahamat_LRI_CHAD.py
   ```

## Methodology & Insights
The project follows a rigorous pipeline to avoid data leakage:
1. **Cleaning**: Dropping rows with missing primary labels.
2. **Splitting**: Stratified 70/30 Train/Test split *before* any feature selection or imputation.
3. **Screening**: Dropping columns with >60% missing values.
4. **Balancing**: SMOTE is applied strictly to the training set to prevent leakage.
5. **Evaluation**: Models are evaluated using Accuracy, Recall, and Precision to account for class imbalance.

### Key Findings
- Nutritional indicators (like Weight-for-Height Z-score) and mother's BMI show significant correlation with LRI susceptibility.
- Ensemble tree models (XGBoost/LightGBM) consistently outperform linear models in handling the high-dimensional survey data.

---
*Created as part of a Health Analytics study focused on Chad.*
