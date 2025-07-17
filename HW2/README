# HW2: Feature Store & ML Pipeline (Databricks)

This project implements a machine learning pipeline using a feature store on Databricks. The goal is to track model performance and carbon emissions across different feature versions and hyperparameters.

---

## Objective

- Use `athletes.csv` as the dataset.  
- Create two versions of features: `v1` (original) and `v2` (with feature engineering like BMI).  
- Train a Random Forest model with two sets of hyperparameters on both feature versions (4 runs total).  
- Track metrics (RMSE, R²) and carbon emissions using MLflow and CodeCarbon.  
- Compare results both quantitatively and qualitatively.  

---

## Tools

- Databricks (Free Community Edition)  
- Feature Store (for versioning)  
- MLflow (for experiment tracking)  
- scikit-learn (RandomForestRegressor)  
- CodeCarbon (for emissions)  
- SHAP (for feature importance)  

---

## Results Summary

| Feature Version | Parameters               | RMSE   | R²    | CO₂ Emissions (kg) |
|-----------------|---------------------------|--------|-------|--------------------|
| v1              | n=100, max_depth=5        | 176.66 | 0.59  | 0.000004           |
| v1              | n=200, max_depth=10       | 170.49 | 0.62  | 0.000000           |
| v2              | n=100, max_depth=5        | 172.49 | 0.61  | 0.000000           |
| v2              | n=200, max_depth=10       | 161.60 | 0.65  | 0.000000           |

