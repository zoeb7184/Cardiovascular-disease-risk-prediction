# 🫀 Cardiovascular Disease Risk Prediction

> End-to-end ML classification pipeline predicting heart disease risk from CDC BRFSS 2022 survey data — 308,854 records, 18 features, 4 models compared.

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)](https://python.org)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3-orange?style=flat-square&logo=scikit-learn)](https://scikit-learn.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## Results at a Glance

| Model | Accuracy | F1 Score | AUC-ROC |
|---|---|---|---|
| **Logistic Regression** | 0.745 | **0.611** | **0.836** ✅ |
| Decision Tree (Entropy) | 0.719 | 0.595 | 0.825 |
| Decision Tree (Gini) | 0.719 | 0.594 | 0.823 |
| Random Forest | 0.734 | 0.607 | 0.835 |

> **Why not 92% accuracy?** The dataset has a severe 11.4:1 class imbalance. Raw accuracy is misleading — a model that always predicts "No Disease" scores 91.9% without learning anything. AUC-ROC is the meaningful metric here.

---

## Dataset

| Property | Detail |
|---|---|
| Source | [CDC BRFSS 2022 Survey](https://www.cdc.gov/brfss/) |
| Records | 308,854 |
| Features | 18 (behavioral, demographic, clinical) |
| Target | `Heart_Disease` (binary) |
| Imbalance | 91.9% Negative / 8.1% Positive |

**Feature categories:**
- **Lifestyle:** Exercise, Smoking History, Alcohol & Dietary Consumption
- **Clinical:** BMI, Diabetes, Arthritis, Skin Cancer, Other Cancer, Depression
- **Demographic:** Age, Sex, Height, Weight
- **Self-reported:** General Health, Checkup Frequency

---

## Project Structure

```
├── CVD_Risk_Prediction.ipynb    # Main notebook (EDA → preprocessing → modeling → evaluation)
├── CVD_cleaned.csv              # Preprocessed dataset
└── README.md
```

---

## Methodology

### 1. EDA
- Distribution analysis of all 18 features split by heart disease status
- Correlation heatmap
- Class imbalance visualization

### 2. Preprocessing
| Step | Method |
|---|---|
| Binary encoding | `Yes/No → 1/0` |
| Ordinal encoding | Ordered integer mapping (health, checkup, age, diabetes severity) |
| Class balancing | Undersampling majority to 3:1 ratio + `class_weight='balanced'` |
| Feature scaling | `StandardScaler` (fit on train only — no data leakage) |

### 3. Models
- Logistic Regression (linear baseline)
- Decision Tree — Entropy criterion
- Decision Tree — Gini criterion
- Random Forest (ensemble, 100 trees)

### 4. Evaluation
- Accuracy, F1, AUC-ROC on held-out 20% test set
- Confusion matrices for all 4 models
- ROC curve comparison
- Random Forest feature importance ranking

---

## Key Findings

**Top predictors of cardiovascular disease risk:**

| Rank | Feature | Importance |
|---|---|---|
| 1 | Age Category | 36.7% |
| 2 | General Health (self-rated) | 24.5% |
| 3 | Diabetes | 9.4% |
| 4 | Arthritis | 8.8% |
| 5 | Smoking History | 4.1% |

Age and self-rated general health together account for **61% of predictive power**, suggesting that simple, low-cost survey inputs are highly informative for cardiovascular risk screening.

---

## How to Run

```bash
git clone https://github.com/zoeb7184/cvd-risk-prediction.git
cd cvd-risk-prediction

pip install -r requirements.txt

jupyter notebook CVD_Risk_Prediction.ipynb
```

---

## Limitations & Future Work

- [ ] **SMOTE oversampling** — test vs. current undersampling approach
- [ ] **Hyperparameter tuning** — GridSearchCV / Optuna for all models
- [ ] **XGBoost / LightGBM** — gradient boosting comparison
- [ ] **Streamlit deployment** — real-time risk calculator web app
- [ ] **SHAP values** — local feature explanations per patient

---

## Author

**Zoeb Ali Khan**  
M.Sc. Data Science · Universität Bielefeld, Germany  
[LinkedIn](https://linkedin.com/in/zoeb-ali-khan) · [GitHub](https://github.com/zoeb7184)
