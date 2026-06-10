# Data Quality Report — Session 03: UK Workplace Learning Dataset

## 1. Dataset Overview

| | Before Cleaning | After Cleaning |
|---|---|---|
| Rows | 620 | 600 |
| Columns | 14 | 16 |
| Missing cells | 139 | 11 |
| Exact duplicate rows | 20 | 0 |

The 2 additional columns after cleaning are `enrolment_date_parsed` and `enrolment_date_invalid_flag`.

---

## 2. Issues Identified

### Missing Values
| Column | Missing Count | % Missing |
|---|---|---|
| `prior_python_score` | 35 | 5.6% |
| `engagement_score` | 30 | 4.8% |
| `region` | 24 | 3.9% |
| `completion_days` | 18 | 2.9% |
| `department` | 18 | 2.9% |
| `manager_support_score` | 14 | 2.3% |

### Duplicate Rows
20 exact duplicate rows were identified, likely caused by data entry errors or system export issues.

### Type Errors
`support_tickets_last_30d` was stored as a string with values like `"3 tickets"` rather than a plain integer.

### Impossible Numeric Ranges
| Column | Valid Range | Invalid Values Found |
|---|---|---|
| `prior_python_score` | 0–100 | 6 (e.g. values of –10 and 125) |
| `engagement_score` | 0–100 | 5 |
| `course_minutes` | 0–480 | 6 |

### Inconsistent Category Labels
`department` contained variants such as `"Human Resources"`, `"human resources"`, and `"HR"` for the same group, and `"Information Technology"` alongside `"it"`.

### Invalid Dates
Some `enrolment_date` values could not be parsed as valid dates and were coerced to missing.

---

## 3. Cleaning Decisions

**Duplicates:** All 20 exact duplicate rows were removed. Exact duplicates add no information and can overweight certain records in a model.

**Type conversion:** The numeric part of `support_tickets_last_30d` was extracted using a regex and cast to float, preserving the data rather than discarding the column.

**Category standardisation:** All categorical columns were lowercased, stripped of whitespace, and known synonyms were mapped to a canonical label (e.g. `"human resources"` → `"hr"`). This prevents a model treating the same group as separate categories.

**Impossible ranges:** Out-of-range values were converted to `NaN` and flagged with a binary `_invalid_flag` column rather than deleting the row. This preserves the rest of the record's information while signalling to a model that the value was unreliable.

**Missing values:** Numeric columns were imputed with the column median. The median is more robust than the mean when outliers are present, as seen in `prior_python_score` (min –10, max 125 before cleaning). Categorical columns were filled with `"unknown"` to keep rows in the dataset. A binary `_missing_flag` column was added for each imputed column so a model can learn whether missingness itself carries signal.

**Dates:** Invalid dates were coerced to `NaN` and a flag column was created. The original `enrolment_date` column was kept alongside the parsed version for auditability.

---

## 4. Encoding and Scaling

**One-hot encoding** was applied to `department`, `region`, and `training_type`. These are nominal categories with no natural order, so label encoding would imply a false ranking.

**Z-score scaling** was applied to `prior_python_score`, `course_minutes`, `engagement_score`, and `support_tickets_last_30d`. Scaling brings features onto a comparable scale, which is important for distance-based models and gradient descent.

---

## 5. Bias, Leakage, and Signal Preservation

**Leakage risk:** `completion_days` records how long a learner took to finish a course. This value is only known after completion, so using it to predict `completed_on_time` would constitute leakage — the model would be trained on information unavailable at prediction time.

**Bias risk:** Filling missing values with `"unknown"` rather than deleting rows avoids the risk of systematically removing a particular group. Learners with missing scores may be less engaged or from departments with lower digital access; deleting those rows would make the cleaned dataset unrepresentative of the real population.

**Signal preservation:** No rows were deleted solely because of missing values. Invalid numeric values were flagged rather than causing row deletion. This keeps 600 of the original 620 rows (97%) available for modelling, with only the 20 genuine duplicates removed.
