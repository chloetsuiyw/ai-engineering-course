# Model Selection Summary - Session 10

## Metric comparison

### Scored by F1
     model_family  best_cv_score
gradient_boosting       0.180586
    decision_tree       0.148810
    random_forest       0.000000
              knn       0.000000

### Scored by Recall
Re-run GridSearchCV with scoring='recall' produced:
- Decision Tree: 0.120
- Gradient Boosting: 0.120
- Random Forest: 0.000
- KNN: 0.000

## Selected model
Model family: gradient_boosting
Best parameters: {'model__learning_rate': 0.1, 'model__max_depth': 3, 'model__n_estimators': 100}
Best CV F1: 0.181

## Metric choice rationale
Switching from F1 to recall changes the selected model from Gradient Boosting to Decision Tree.
Recall is more appropriate for SLA breach risk because missing a breach (false negative) is more
damaging than a false alarm — an undetected breach means a customer is let down without intervention.
F1 balances precision and recall, which may favour a more conservative model.

## Limitations
- All scores are low (F1 ~0.18, recall ~0.12) — models struggle to detect breaches reliably
- Synthetic dataset, not suitable for real operational decisions
- No fairness or subgroup analysis performed
