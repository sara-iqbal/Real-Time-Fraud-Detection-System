# 🏦 Real-Time Credit Card Fraud Detection System

> **Portfolio Project for JP Morgan** | Built by Sara  
> MSc Data Science | BSc Artificial Intelligence & Machine Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_LINK_HERE)
[![Hugging Face Spaces](https://img.shields.io/badge/🤗-Live%20Demo-yellow)](YOUR_HF_SPACES_LINK)
[![Python](https://img.shields.io/badge/Python-3.10+-blue)](https://python.org)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.0-orange)](https://xgboost.readthedocs.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 📌 Business Problem

JP Morgan processes **millions of credit card transactions daily**. Even a 0.1% fraud rate represents hundreds of millions in losses annually. This project builds a **production-grade, real-time fraud detection system** that flags suspicious transactions with high precision while minimising false positives that frustrate legitimate customers.

---

## 🏗️ Architecture

```
Raw Transaction Data
        ↓
Feature Engineering (Time, Amount, PCA interactions)
        ↓
SMOTE Oversampling (handles 0.17% fraud imbalance)
        ↓
┌─────────────────────┐    ┌─────────────────────────┐
│   XGBoost (75%)     │    │  Isolation Forest (25%) │
│ Supervised Learner  │    │  Anomaly Detection      │
└─────────────────────┘    └─────────────────────────┘
        ↓                            ↓
        └──────── Ensemble ──────────┘
                    ↓
          Fraud Probability Score
                    ↓
         🚨 FRAUD / ✅ LEGITIMATE
```

---

## 📊 Results

| Metric | Score |
|--------|-------|
| ROC-AUC | **0.974** |
| Avg Precision | **0.863** |
| F1 Score (Fraud) | **0.821** |
| Recall (Fraud) | **0.89** |

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| ML Models | XGBoost, Isolation Forest |
| Imbalanced Data | SMOTE (imbalanced-learn) |
| Explainability | SHAP |
| Visualisation | Plotly, Matplotlib, Seaborn |
| Deployment | Gradio, Hugging Face Spaces |
| Language | Python 3.10 |

---

## 🚀 Quick Start

### Run in Google Colab (Recommended)
Click the **Open in Colab** badge above — no setup needed!

### Run Locally
```bash
git clone https://github.com/YOUR_USERNAME/fraud-detection-jpmorgan
cd fraud-detection-jpmorgan
pip install -r requirements.txt
jupyter notebook fraud_detection_colab.ipynb
```

---

## 📁 Project Structure

```
fraud-detection-jpmorgan/
│
├── fraud_detection_colab.ipynb  # Main notebook (end-to-end)
├── app.py                        # Gradio deployment app
├── requirements.txt
├── README.md
└── models/
    ├── xgb_fraud_model.pkl
    ├── iso_forest_model.pkl
    └── scaler.pkl
```

---

## 🔍 Key Techniques

- **SMOTE**: Handles extreme class imbalance (0.17% fraud rate)
- **Ensemble Learning**: Combines supervised XGBoost with unsupervised Isolation Forest
- **SHAP Values**: Explains *why* each transaction was flagged (critical for compliance)
- **RobustScaler**: Handles outliers in transaction amounts
- **Feature Engineering**: Time-of-day, log-amount, PCA feature interactions

---

## 💼 Relevance to JP Morgan

- Real-time scoring infrastructure mirrors JP Morgan's fraud pipeline
- SHAP explainability supports regulatory compliance (model transparency)
- Ensemble approach mirrors industry best practice for high-stakes financial decisions
- Threshold tuning balances fraud catch rate vs. customer experience

---

## 👩‍💻 Author

**Sara** | Data Scientist based in London  
MSc Data Science | BSc Artificial Intelligence & Machine Learning  

*This is Project 1 of 4 in my JP Morgan Data Science Portfolio.*

---

## 📄 License
MIT License — feel free to use and build on this work.
