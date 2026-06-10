# Classification Summary - Session 07

## Models compared
| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Dummy baseline | 0.707 | 0.707 | 1.000 | 0.828 |
| Random forest | 0.676 | 0.747 | 0.818 | 0.781 |
| Logistic regression | 0.658 | 0.811 | 0.673 | 0.735 |
| Decision tree | 0.627 | 0.791 | 0.642 | 0.708 |

## Chosen model
Random Forest — best ROC score and strongest balance of precision and recall.

## Threshold decision
Threshold 0.30 selected to maximise recall (0.92), minimising missed SLA breaches.

## Responsible AI note
Model should be checked for fairness across regions and customer segments. 
Class imbalance (70% breaches) may affect minority class performance. 
Human review recommended before any automated action.
