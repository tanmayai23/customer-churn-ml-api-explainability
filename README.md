# Customer Churn Classification Project

## Project Title
**Supervised Classification Model for Customer Churn Prediction**

## Project Overview

This project builds and evaluates a supervised machine learning classification model to predict customer churn using the Telco Customer Churn dataset.

The objective is to identify customers who are likely to leave a telecom service provider. The project includes data preprocessing, exploratory data analysis, model training, model comparison, cross-validation, evaluation metrics, visualizations, and final model saving.

Two machine learning algorithms were compared:

1. Logistic Regression
2. Random Forest Classifier

Based on the final evaluation, **Logistic Regression** was selected as the best-performing model.

---

## Goal

Build and evaluate a supervised classification model for predicting customer churn.

The project satisfies the following requirements:

- Data preprocessing
- Train/test split
- Cross-validation
- Comparison of at least two algorithms
- Evaluation using:
  - Accuracy
  - Precision
  - Recall
  - F1 Score
  - ROC-AUC
- Notebook with code, plots, and metrics
- Short report summarizing model selection and results

---

## Dataset

The project uses the **Telco Customer Churn dataset**.

### Dataset Details

- Total records: **7,043**
- Total columns before preprocessing: **21**
- Target variable: **Churn**
- Problem type: **Binary Classification**

### Target Classes

| Class | Meaning |
|---|---|
| No | Customer did not churn |
| Yes | Customer churned |

### Class Distribution

| Class | Percentage |
|---|---|
| No Churn | 73.5% |
| Churn | 26.5% |

The dataset is imbalanced because the number of non-churn customers is much higher than churn customers.

---

## Project Structure

```text
customer-churn-classification/
│
├── 01_churn_classification.ipynb
├── churn_classification_project_report.docx
├── churn_model.pkl
├── README.md
└── data/
    └── telco_churn.csv
