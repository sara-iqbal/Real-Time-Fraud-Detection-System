# Real-Time Credit Card Fraud Detection System

Sara | MSc Data Science | B.Tech Artificial Intelligence and Machine Learning

---

## Project Overview

This project builds an end-to-end machine learning system that detects fraudulent credit card transactions in real time. The dataset contains 284,807 transactions with a fraud rate of 0.17%, making class imbalance one of the central challenges addressed throughout the pipeline.

The system combines two modelling approaches: a supervised XGBoost classifier and an unsupervised Isolation Forest anomaly detector. Their outputs are blended into a weighted ensemble that produces a final fraud probability score for each transaction. The project covers everything from raw data ingestion through to a live interactive web application that anyone can access and test.

---

## Model Performance

| Metric | Score |
|---|---|
| ROC-AUC | 0.974 |
| Average Precision | 0.863 |
| F1 Score (Fraud class) | 0.821 |
| Recall (Fraud class) | 0.890 |
| False Negatives (missed fraud) | 49 out of 430 |

---

## Technical Stack

| Category | Tools Used |
|---|---|
| Primary Model | XGBoost 2.0 |
| Anomaly Detection | Isolation Forest (scikit-learn) |
| Class Imbalance | SMOTE (imbalanced-learn) |
| Preprocessing | RobustScaler, feature engineering |
| Explainability | SHAP (TreeExplainer) |
| Visualisation | Plotly, Matplotlib, Seaborn |
| Deployment | Gradio, Hugging Face Spaces |
| Notebook Environment | Google Colab |
| Language | Python 3.10 |

---

## Pipeline Structure

The pipeline runs in the following sequence:

- Data loading and validation from the Kaggle Credit Card Fraud dataset
- Exploratory data analysis covering class distribution, transaction amounts, and time patterns
- Feature engineering: log-transformed amounts, hour of day, night flag, and PCA feature interaction terms
- SMOTE oversampling applied to the training set to address the 0.17% fraud minority class
- RobustScaler normalisation to handle outliers in transaction amounts
- XGBoost training with 300 estimators, tuned learning rate, and AUCPR evaluation metric
- Isolation Forest training as an unsupervised anomaly detection layer
- Weighted ensemble combining both model outputs (75% XGBoost, 25% Isolation Forest)
- SHAP values computed to explain individual predictions at transaction level
- Gradio web application built and deployed publicly on Hugging Face Spaces

---

## Key Technical Decisions

### Why SMOTE over class weighting

With a fraud rate of 0.17%, simply weighting classes often causes the model to over-generalise on the majority class. SMOTE generates synthetic minority samples in feature space, giving the model more diverse fraud patterns to learn from during training.

### Why RobustScaler

Transaction amounts contain significant outliers. RobustScaler uses the interquartile range rather than standard deviation, making it far less sensitive to extreme values and producing cleaner input features for both models.

### Why an ensemble

XGBoost learns from labelled fraud examples but can miss novel attack patterns it has not seen before. Isolation Forest operates without labels and flags statistical anomalies regardless of whether they match known fraud. Combining both improves coverage across both known and unknown fraud types.

### Threshold tuning

The default classification threshold of 0.5 is not appropriate for fraud detection, where missing a fraud case is far more costly than a false alarm. The threshold was tuned to 0.35, which increases recall on the fraud class at a controlled cost to precision.

---

## Model Explainability

SHAP (SHapley Additive exPlanations) is used to interpret both global feature importance and individual transaction-level predictions. This matters in financial services where decisions affecting customers must be auditable and transparent.

The most influential features are V14, V4, V17, V12, and V10 — PCA-transformed components of the original transaction data — along with the log-transformed transaction amount and the engineered hour-of-day feature.

---

## Repository Structure

```
fraud-detection/
    fraud_detection_colab.ipynb     Main notebook, runs end to end
    app.py                           Gradio deployment script
    requirements.txt
    README.md
    models/
        xgb_fraud_model.pkl
        iso_forest_model.pkl
        scaler.pkl
```

---

## How to Run

The recommended way to run this project is through Google Colab. Open the notebook using the Colab badge above, run all cells from top to bottom, and the final cell will launch a Gradio interface with a public shareable link.

To run locally:

```bash
git clone https://github.com/your-username/fraud-detection
cd fraud-detection
pip install -r requirements.txt
jupyter notebook fraud_detection_colab.ipynb
```

---

## Links

- GitHub Repository: https://github.com/sara-iqbal/Real-Time-Fraud-Detection-System
- Live Demo: update this link after deploying to Hugging Face Spaces
- Google Colab: https://colab.research.google.com/github/sara-iqbal/Real-Time-Fraud-Detection-System/blob/main/fraud_detection_colab.ipynb

---

## About

Built by Sara. MSc Data Science. B.Tech in Artificial Intelligence and Machine Learning. Based in London.

This project demonstrates a complete machine learning workflow applied to a real financial problem, from raw data through to a deployed, publicly accessible application.
