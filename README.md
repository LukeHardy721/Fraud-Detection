# 🕵️‍♂️ Unsupervised Anomaly Detection for Credit Card Fraud

## 📌 Project Overview

This project explores **unsupervised anomaly detection** techniques for identifying fraudulent transactions in credit card data.

The key twist: although the dataset contains known fraud labels, the models are trained **without access to these labels**. Labels are **only used for final evaluation**, simulating a realistic fraud-detection scenario where fraud cases are unknown in advance.

I then benchmark the unsupervised methods against a supervised baseline.

---

## 🎯 Objectives

- Model fraud detection as an **anomaly detection problem** using only transaction features.
- Compare multiple **unsupervised algorithms** (Isolation Forest, Local Outlier Factor, One-Class SVM).
- Use the true labels **only after training** to assess detection performance.
- Visualise anomaly scores and fraud patterns.
- Demonstrate the limitations and strengths of unsupervised vs. supervised approaches.

---

## 📂 Dataset

- **Name:** [Credit Card Fraud Detection Dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions over 2 days
- **Fraud rate:** ~0.172% (492 frauds)
- **Features:**
  - `V1`–`V28`: PCA-transformed features (original features anonymised for privacy)
  - `Amount`: Transaction amount
  - `Time`: Seconds elapsed since first transaction
  - `Class`: Target variable (1 = Fraud, 0 = Non-fraud)

---

## 🛠️ Methods

### 1. **Data Preparation & EDA**
- Explore features
- Analyse relationships with target
- Drop the `Class` column before modeling.
- Standardised numerical features (`StandardScaler`).

### 2. **Unsupervised Models**
- Isolation Forest
- Local Outlier Factor (LOF)
- One-Class SVM

### 3. **Evaluation Metrics** (using hidden labels)
- ROC AUC
- Precision, Recall, F1-score
- Precision@K (top K% highest anomaly scores)
- Confusion matrix
- Fraud detection rate in top-ranked anomalies

### 4. **Supervised Benchmark**
- Gradient Boosting (`XGBoostClassifier`) trained with labels
- Compared performance to best unsupervised method

---

## 📊 Key Visualisations

- **Class distribution** (severe imbalance)
- **Transaction amount by class** (log scale)
- **Anomaly score histograms** (fraud vs. non-fraud)
- **Precision–Recall curves**

---

## 🚀 Results Summary

| Model                 | ROC AUC  | PR AUC | Precision@1% | Recall@1% |
|-----------------------|----------|--------|--------------|-----------|
| Isolation Forest      | 0.96     | 0.24   | 0.12         | 0.68      |
| Local Outlier Factor* | 0.95     | 0.51   | 0.14         | 0.84      |
| One-Class SVM         | 0.94     | 0.15   | 0.14         | 0.80      |
| **Supervised XGBoost**| **0.98** |**0.88**| **0.16**     | **0.91**  |

*Note that Local Outlier Factor (LOF) further achieved 0.82 recall with 0.28 precision at 0.5%, meaning that by reviewing 0.5% of transactions, we could catch 82% of fraudulent transactions. This is a 164x improvement on random guessing.
The supervised XGBoost model further achieved 0.91 recall with 0.31 precision at 0.5%, meaning that by reviewing 0.5% of transactions, we could catch 91% of fraudulent transactions. This is a 182x improvement on random guessing.

---

## 📂 Project Structure

```bash
fraud-detection/
├── data/                   # Raw and processed data (excluded via .gitignore)
├── notebooks/              # Jupyter notebooks for EDA, unsupervised modelling and supervised modelling
├── README.md
└── .gitignore