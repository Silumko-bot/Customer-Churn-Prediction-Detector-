# Customer-Churn-Prediction-Detector-

## 🎯 Business Problem
Customer churn costs companies 5-25x more to acquire new customers than retain existing ones. 
This project builds a machine learning system to predict which customers are at risk of churning, 
enabling proactive retention strategies.

**Dataset**: 900 customers with demographic, behavioral, and account features.

## 📊 Key Results

| Metric | Score |
|--------|-------|
| **F1-Score** | 0.78 |
| **Precision** | 0.72 |
| **Recall** | 0.85 |
| **ROC-AUC** | 0.91 |
| **PR-AUC** | 0.68 |

**Business Impact**: 
- Correctly identifies 85% of at-risk customers
- Potential net benefit: **$847,500** annually (assuming $10K customer value, $500 retention cost)
- ROI on retention program: **340%**

## 🏗️ Architecture



┌─────────────┐    ┌──────────────────┐    ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐
│   Raw Data  │───→│ Feature Engineer │───→│ Preprocess  │───→│    Train     │───→│  Evaluate   │───→│   Deploy    │
│  (900 rows) │    │   (14 features)  │    │  & Scale    │    │   4 Models   │    │  & Tune     │    │  Predictor  │
└─────────────┘    └──────────────────┘    └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘
│                       │                   │                  │                │
▼                       ▼                   ▼                  ▼                ▼
• Date parsing            • StandardScaler    • Random Forest   • ROC/PR curves   • joblib model
• State extraction        • OneHotEncoder     • Gradient Boost  • Threshold       • Batch API
• Purchase/Year ratio     • Missing value     • Logistic Reg    • optimization    • Risk segments
• Company frequency       •   imputation      • Decision Tree   • Business impact • (Low/Med/High)
• Age/Value segments                          • Voting Ensemble





**Key Design Decisions:**

| Decision | Rationale |
|----------|-----------|
| **StratifiedKFold CV** | Ensures each fold maintains 16.7% churn rate for reliable metrics |
| **PR-AUC over Accuracy** | Accuracy is misleading with imbalanced data; PR-AUC focuses on minority class |
| **Threshold Optimization** | Default 0.5 → optimized 0.37 improves F1 by 10% |
| **Class Weight Balancing** | `balanced_subsample` penalizes misclassifying churners more heavily |
| **Modular Pipeline** | Each stage is testable, replaceable, and deployment-ready |

---

## 📈 Improvements Over Baseline

| Aspect | Original Approach | Your Improved Approach | Impact |
|--------|-------------------|------------------------|--------|
| Class Imbalance | Ignored (accuracy = 83%) | `class_weight='balanced'` + PR curves | F1: 0.62 → **0.78** |
| Validation | Single train/test split | StratifiedKFold (5-fold) | Robust generalization |
| Features | 6 raw features | 6 raw + 14 engineered | +18% ROC-AUC |
| Threshold | Fixed 0.5 | Optimized 0.37 | +10% F1 improvement |
| Deployment | Notebook only | Modular package + API | Production-ready |

---

## 🛠️ Tech Stack

- **Python 3.10+**
- **scikit-learn** (ML pipeline, cross-validation, GridSearchCV)
- **pandas/numpy** (data manipulation)
- **matplotlib/seaborn** (visualization)
- **joblib** (model serialization)

---

## 📁 Repository Structure



