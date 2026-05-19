# Customer Churn ML — API & Explainability

End-to-end project that trains a churn classifier on the Telco Customer Churn dataset, explains predictions with SHAP and LIME, audits subgroup fairness, and serves predictions through a FastAPI endpoint.

## Project structure

```
customer-churn-ml-api-explainability/
├── data/
│   └── telco_churn.csv
├── notebook/
│   ├── 01_churn_classification.ipynb       # EDA, preprocessing, train + evaluate, save model
│   └── 02_explainability_fairness.ipynb    # SHAP, LIME, gender / SeniorCitizen fairness
├── models/
│   └── churn_model.pkl                     # Best sklearn Pipeline (preprocessor + classifier)
├── apps/
│   ├── __init__.py
│   ├── main.py                             # FastAPI app: /predict, /health
│   └── schema.py                           # Pydantic input/output schemas
├── requirements.txt
├── Dockerfile
├── README.md
└── report.md
```

## Quick start

1. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

2. **Train the model** — open `notebook/01_churn_classification.ipynb` and run all cells. This writes `models/churn_model.pkl`.

3. **Explore explainability** — open `notebook/02_explainability_fairness.ipynb`.

4. **Run the API**

   ```bash
   uvicorn apps.main:app --reload --port 8000
   ```

   Then open <http://localhost:8000/docs> for the auto-generated Swagger UI.

   Sample request:

   ```bash
   curl -X POST http://localhost:8000/predict \
     -H "Content-Type: application/json" \
     -d '{
       "gender": "Female", "SeniorCitizen": 0, "Partner": "Yes", "Dependents": "No",
       "tenure": 1, "PhoneService": "No", "MultipleLines": "No phone service",
       "InternetService": "DSL", "OnlineSecurity": "No", "OnlineBackup": "Yes",
       "DeviceProtection": "No", "TechSupport": "No", "StreamingTV": "No",
       "StreamingMovies": "No", "Contract": "Month-to-month",
       "PaperlessBilling": "Yes", "PaymentMethod": "Electronic check",
       "MonthlyCharges": 29.85, "TotalCharges": 29.85
     }'
   ```

5. **Run with Docker**

   ```bash
   docker build -t churn-api .
   docker run -p 8000:8000 churn-api
   ```

## Dataset

[Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) — 7,043 customers, 21 columns, binary `Churn` target.

## Models

Two scikit-learn `Pipeline` models are trained inside `01_churn_classification.ipynb`:

- Logistic Regression
- Random Forest (200 trees)

Both wrap a shared `ColumnTransformer` (StandardScaler for numeric, OneHotEncoder for categorical) so the persisted artifact is self-contained — the API never has to re-implement preprocessing.

## Deliverables

- `notebook/01_churn_classification.ipynb`
- `notebook/02_explainability_fairness.ipynb`
- `models/churn_model.pkl`
- `apps/main.py`, `apps/schema.py`
- `report.md`
- `README.md`
- `Dockerfile`
