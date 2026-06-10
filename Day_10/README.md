# Session 10 - Tree, Ensemble and KNN Pipeline Tuning

## Project purpose
This project compares four classifier families — Decision Tree, Random Forest, Gradient Boosting, and KNN — for predicting SLA breach risk in a synthetic workplace service-request dataset. Each model is wrapped in a reusable Scikit-learn pipeline that combines preprocessing and tuning, making the workflow reproducible and leak-free.

## Dataset summary and target
Synthetic workplace service-request dataset with no personal data. Each row represents a service request submitted before the outcome is known.

**Target:** `sla_breach` — binary flag indicating whether the request breached its SLA.

## Pipeline design
All preprocessing is contained inside the pipeline to prevent data leakage from the test set.

- `ColumnTransformer` routes numeric and categorical columns to separate sub-pipelines
- **Numeric route:** median imputation → standard scaling
- **Categorical route:** most-frequent imputation → one-hot encoding (unknown categories ignored)
- A candidate classifier is appended and tuned end-to-end using `GridSearchCV` with 5-fold stratified cross-validation

## Cross-validation metric and results

### Scored by F1
     model_family  best_cv_score
gradient_boosting       0.180586
    decision_tree       0.148810
    random_forest       0.000000
              knn       0.000000

### Selected model
Selected model family: gradient_boosting
Best parameters: {'model__learning_rate': 0.1, 'model__max_depth': 3, 'model__n_estimators': 100}
Best CV score: 0.181

## Limitations and responsible use
- Synthetic classroom dataset — not for real operational decisions
- Low CV and holdout scores indicate limited reliability without further feature engineering
- No subgroup or fairness analysis performed
- No production monitoring or drift detection in place

## How to run
pip install -r requirements.txt
jupyter notebook notebooks/Session_10_Practical_Activity.ipynb
