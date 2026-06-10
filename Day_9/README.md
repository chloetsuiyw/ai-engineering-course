# SLA Breach Risk Predictor

## Purpose
Predict whether a workplace request is at risk of breaching SLA using 
a tuned Scikit-learn pipeline.

## Dataset
Synthetic workplace dataset (workplace_pipeline_tuning_dataset.csv). 
Not real data — do not use for production decisions.

## Features Used
All columns except identifiers (request_id) and leakage columns 
(those ending in DO_NOT_USE).

## Pipeline Structure
- Numeric features: median imputation → StandardScaler
- Categorical features: most-frequent imputation → OneHotEncoder
- Models tuned: Logistic Regression (GridSearchCV), 
  Random Forest (RandomizedSearchCV)

## Scoring Metric
ROC-AUC — chosen because it evaluates ranking ability across all 
thresholds without assuming a fixed decision point.

## Best Parameters
Logistic Regression: C=0.5, class_weight=balanced  
Random Forest: n_estimators=100, max_depth=6, min_samples_split=10, 
min_samples_leaf=2, class_weight=balanced

## Results
Both models required class_weight=balanced, confirming class imbalance 
in the dataset. Random Forest marginally outperformed Logistic 
Regression with a recall of 0.681.

## Limitations
- Dataset is synthetic, not real workplace data
- Not deployment-ready without governance review and monitoring
- Subgroup performance and fairness not checked

## How to Run
1. Install dependencies: pip install -r requirements.txt
2. Open Session_09_Practical_Activity.ipynb in Jupyter
3. Run all cells from top to bottom