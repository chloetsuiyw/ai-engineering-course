# Session 06 - Supervised Learning and Regression

## Objective
Train and evaluate a salary regression model and compare it with a baseline predictor.

## Dataset
Synthetic classroom salary dataset. No personal data. Not for real compensation decisions.

## Models compared
- DummyRegressor baseline (predicts mean salary for every employee)
- LinearRegression pipeline (with StandardScaler and OneHotEncoder)

## Metrics

| Model | MAE (£) | RMSE (£) | R² |
|---|---|---|---|
| Baseline: mean predictor | 10,844 | 13,581 | 0.00 |
| Linear regression | 4,600 | 5,928 | 0.81 |

## Key finding
The linear regression model significantly outperforms the baseline, reducing the average prediction error from £10,844 to £4,600 per person. With an R² of 0.81, the model explains 81% of salary variation using 13 features, making it suitable for broad workforce budget planning.

## Responsible-use note
This model should not be used for individual pay decisions. If trained on real historical data, it may encode existing gender or ethnicity pay gaps, perpetuating historical biases rather than correcting them. A fairness audit across protected characteristics would be required before any real deployment.
