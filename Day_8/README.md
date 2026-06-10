# Session 08 - Model Evaluation and Cross-Validation

## Objective
Compare two classifiers using cross-validation and metrics aligned to business risk.

## Dataset
Synthetic service request dataset. Target: SLA breach risk (~43% breach rate).

## Models Compared
- Logistic Regression
- Random Forest

## Validation Strategy
5-fold stratified cross-validation on the training data (75% split), with a 
held-out test set (25%) reserved for final evaluation.

## Key Result
Logistic Regression is recommended. It achieved a higher recall (0.55 vs 0.41) 
than Random Forest, which matters most for this task as missing a real SLA breach 
directly impacts the customer.

## Limitations
- Data is synthetic and may not reflect real operational patterns
- Class imbalance (~43% breach rate) limits model confidence
- Subgroup fairness across regions and customer types has not been validated
- Real data validation and fairness audits would be required before deployment
