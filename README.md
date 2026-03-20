# 🫁 LRI Risk Prediction in Chadian Children Under Five

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![Data](https://img.shields.io/badge/Data-DHS_Chad_2014-green)](https://dhsprogram.com/)
[![ML](https://img.shields.io/badge/ML-XGBoost%20%7C%20LightGBM%20%7C%20CatBoost-orange)](https://scikit-learn.org/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()

> **Lower Respiratory Infection (LRI) is one of the leading causes of death in children under five in Chad.**  
> This project builds a machine learning pipeline to predict LRI risk at the individual child level — enabling  
> targeted health interventions where resources are most scarce.

---

## 🌍 Why This Matters

Chad has one of the highest child mortality rates in the world. LRI alone accounts for a significant share of
under-five deaths, yet healthcare infrastructure remains severely limited outside N'Djamena.

**The core question this project answers:**  
*"Given a child's demographic profile, household conditions, and nutritional status — how likely are they  
to develop a Lower Respiratory Infection?"*

Answering this with data can help NGOs, ministries of health, and field workers **prioritize interventions**
before a child gets critically ill.

---

## 📊 Dataset

- **Source**: [DHS Program — Chad Standard DHS 2014](https://dhsprogram.com/data/dataset/Chad_Standard-DHS_2014.cfm)
- **File**: Children's Recode (KR) — household survey of mothers and children under 5
- **Size**: National representative sample across all regions of Chad
- **Key Variables**: Child age/sex, nutritional indicators (WHZ, BMI), mother's education, household wealth,
  access to healthcare, vaccination status, water/sanitation conditions

---

## 🔬 Methodology

The pipeline is designed to be **leak-free and reproducible**:
```
Raw DHS Data
    ↓
Target Construction  (H31, H31B, H31C columns → binary LRI label)
    ↓
Train/Test Split  (Stratified 70/30 — split BEFORE any feature engineering)
    ↓
Feature Screening  (Drop >60% missing | T-test + Chi-Square selection)
    ↓
Preprocessing  (Median/mode imputation | dummy encoding | "Don't know" handling)
    ↓
SMOTE Balancing  (Synthetic oversampling on training set ONLY)
    ↓
Model Benchmarking  (8+ algorithms evaluated)
    ↓
Evaluation  (Accuracy, Recall, Precision — with focus on Recall for health context)
```

---

## 🤖 Models Benchmarked

| Model | Notes |
|---|---|
| Logistic Regression | Baseline |
| Decision Tree | Interpretability |
| Random Forest | Ensemble baseline |
| **XGBoost** | Best overall performance |
| **LightGBM** | Fast, competitive accuracy |
| CatBoost | Strong on categorical features |
| SVM | Tested with scaled features |
| KNN | Distance-based baseline |

---

## 📌 Key Findings

- **Nutritional status** (Weight-for-Height Z-score) is the strongest individual predictor of LRI risk
- **Mother's BMI** shows significant correlation — maternal health directly impacts child vulnerability  
- **Household wealth index** and **access to clean water** are among the top socioeconomic risk factors
- **Ensemble tree models** (XGBoost, LightGBM) consistently outperform linear models on this high-dimensional survey data
- SMOTE improved recall for the minority (positive LRI) class significantly without data leakage

---

## 🚀 How to Run
```bash
# 1. Clone the repo
git clone https://github.com/Derio001/lri-prediction-chad.git
cd lri-prediction-chad

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm catboost imbalanced-learn

# 3. Add the DHS dataset (requires free DHS program registration)
# Place chad_dhs_kr.csv in the project root

# 4. Run the full pipeline
python Mahamat_LRI_CHAD.py

# Or explore interactively
jupyter notebook Mahamat_LRI_Chad.ipynb
```

> **Note on Data Access**: The DHS dataset requires a free registration at [dhsprogram.com](https://dhsprogram.com).
> Chad 2014 KR recode is publicly available upon request.

---

## 📁 Project Structure
```
lri-prediction-chad/
│
├── Mahamat_LRI_Chad.ipynb      # Full analysis notebook (EDA → modeling → evaluation)
├── Mahamat_LRI_CHAD.py         # Clean script version of the pipeline
├── verify_data.py              # Diagnostic: check target distribution
├── extract.py                  # Utility: extract code cells from notebooks
└── README.md
```

---

## 🔭 Future Work

- [ ] Incorporate 2023/2024 DHS data when available for Chad
- [ ] Add regional/geographic disaggregation (Sahel vs. southern regions)
- [ ] Build a lightweight Streamlit dashboard for field worker use
- [ ] Extend to other child health outcomes (malnutrition, malaria, diarrheal disease)
- [ ] Explore transfer learning from similar DHS datasets (Niger, Mali, Sudan)

---

## 👤 Author

**Mahamat Hanga Derio**  
M.Tech Data Science — Christ University, Bangalore  
Chadian national | Focused on data-driven solutions for Sub-Saharan African health & development

📬 Open to collaboration with NGOs, research institutions, and public health organizations  
🔗 [GitHub Profile](https://github.com/Derio001)

---

## 📄 Citation

If you use this work, please cite:
```
Mahamat Hanga Derio (2024). LRI Risk Prediction in Chadian Children Under Five.
GitHub. https://github.com/Derio001/lri-prediction-chad
```

---

*This project is part of a broader effort to apply data science for public health impact in Chad and the Lake Chad Basin region.*
