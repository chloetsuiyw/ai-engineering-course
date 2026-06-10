# Session 07 - Classification Models

## Objective
Train binary and multiclass classifiers, inspect predicted probabilities, evaluate confusion matrices and tune a decision threshold.

## Dataset
Synthetic workplace service request dataset (`workplace_service_classification_dataset.csv`). No personal data.

## Models trained
| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Dummy baseline | 0.707 | 0.707 | 1.000 | 0.828 |
| Random forest | 0.676 | 0.747 | 0.818 | 0.781 |
| Logistic regression | 0.658 | 0.811 | 0.673 | 0.735 |
| Decision tree | 0.627 | 0.791 | 0.642 | 0.708 |

## Key results
Random Forest was selected as the best model based on ROC score and balanced precision/recall. The dummy baseline was excluded despite high F1 as it has no real discriminative power (ROC = 0.5).

## Threshold decision
A threshold of 0.30 was chosen to prioritise recall (0.92), minimising missed SLA breaches. In this context, a false negative (missing a real breach) is more costly than a false positive.

## Responsible AI note
- Class imbalance (~70% breach cases) may bias the model toward over-predicting breaches
- Performance should be checked across regions and customer segments for fairness
- Model predictions should be reviewed by a human before any automated action is taken

## Files
- `notebooks/` — main Colab notebook
- `data/` — dataset CSV
- `reports/` — threshold tradeoff table and classification summary
- `visuals/` — confusion matrix and probability distribution charts
