# Session 05 - Feature Engineering Fundamentals

## Objective
Engineer features for a churn dataset and compare a baseline feature set against an engineered feature set using a logistic regression model.

## Dataset
Synthetic workplace churn dataset with safe pre-prediction fields and intentionally leaky post-outcome fields for exclusion practice.

## Methods
- Baseline feature set using raw safe input columns
- Engineered feature set with date, ratio, interaction, binning, and text-derived features
- Logistic regression comparison using the same train/test split and metrics
- Leakage review to exclude post-outcome columns

## Key findings
1. The baseline model achieved a ROC-AUC of 0.82 with 13 features before encoding
2. The engineered feature set used 28 features but scored a lower ROC-AUC of 0.78, suggesting some added features introduced noise rather than signal
3. Precision and recall both dropped with the engineered set, indicating that more features do not always improve model performance — feature selection would be a useful next step

## Leakage exclusions
- cancellation_reason
- account_closed_date
- retention_offer_after_churn