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
