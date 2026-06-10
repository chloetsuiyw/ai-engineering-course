# Homework and Mini-Task - Session 09

## Task
Commit a tuned Scikit-learn pipeline notebook to GitHub with a README.

## Required deliverables
1. Executed notebook that runs end-to-end.
2. Pipeline using `ColumnTransformer` for numeric and categorical columns.
3. GridSearchCV or RandomizedSearchCV with a clearly stated scoring metric.
4. Metrics table for the selected tuned model.
5. README explaining purpose, data, features used, search space, best parameters, metric result, limitations and how to run the notebook.
6. GitHub commit with a clear message such as `Add tuned pipeline notebook for SLA breach model`.

## Marking criteria
- Correct pipeline structure: 25%
- Sensible search space and scoring metric: 20%
- Cross-validation without preprocessing leakage: 20%
- Clear interpretation of best parameters and metrics: 15%
- README and GitHub submission quality: 20%

## Responsible caveat
Do not claim deployment-readiness. State that the dataset is synthetic and that real deployment would require governance review, monitoring, subgroup performance checks and confirmation that all features are available at prediction time.
