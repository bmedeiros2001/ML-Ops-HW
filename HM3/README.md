# ML Ops Homework 3 – AutoML Comparison

## Overview

This assignment compares two AutoML frameworks—H2O AutoML and FLAML—for predicting `total_lift` from athlete data.

Two feature sets were tested:
- All features (6 total)
- Top 3 selected features

Results are compared to models developed in HW1 and HW2, focusing on validation performance and training time.

---

## Tools Used

- H2O AutoML
- FLAML
- Jupyter Notebook

---

## Evaluation Metrics

- R² (coefficient of determination)
- RMSE (root mean squared error)
- Training time (total and best model)

---

## Summary of Results

| Framework | Features | R²     | RMSE   | Training Time |
|-----------|----------|--------|--------|----------------|
| H2O       | All      | 0.6946 | 152.91 | 174.29 s       |
| H2O       | Top 3    | 0.6081 | 173.23 | 160.17 s       |
| FLAML     | All      | 0.6951 | 152.79 | 300.18 s       |
| FLAML     | Top 3    | 0.6362 | 166.89 | 299.98 s       |

AutoML models performed better than earlier models in terms of R² and RMSE, especially using all features. However, training time was longer.

---

## Platform Comparison

| Platform | Interface | Code Level |
|----------|-----------|------------|
| H2O      | Python API | Low-code   |
| FLAML    | Python API | Low-code   |

Both platforms required minimal manual tuning.
