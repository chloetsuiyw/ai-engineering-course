### Model Evaluation Summary

**Intended use:** Early triage of service requests at risk of breaching SLA targets,
to support prioritisation decisions at the point of intake.

**Models compared:** Logistic Regression and Random Forest, both trained with
class_weight='balanced' to account for class imbalance.

**Validation strategy:** 5-fold stratified cross-validation on the training set
(75% of data), with a held-out test set (25%) reserved for a final sanity check.
Stratification ensured each fold preserved the original breach rate of ~43%.

**Metrics and rationale:**
| Metric    | Logistic Regression | Random Forest |
|-----------|-------------------|---------------|
| Accuracy  | 0.562             | 0.615         |
| Precision | 0.490             | 0.569         |
| Recall    | 0.546             | 0.408         |
| F1        | 0.515             | 0.473         |
| ROC-AUC   | 0.588             | 0.602         |

Recall is prioritised because missing a true SLA breach is more costly than a
false alarm — a missed breach affects the customer, while a false alarm only
triggers an unnecessary review.

**Limitations:** Data is synthetic and may not reflect real operational patterns.
Class imbalance (~43% breach rate) limits model confidence. Subgroup performance
across regions and customer types has not been validated. The feature
`updates_first_24h` carries timing risk if prediction is needed before 24 hours
have elapsed. Results must not be used in production without real data validation
and fairness checks.

**Responsible use note:** Before deployment, this model would require fairness
audits across protected characteristics, monitoring for data drift, and human
oversight of all high-stakes triage decisions.
