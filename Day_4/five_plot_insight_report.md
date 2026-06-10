# Five Plot Insight Report - Session 04 EDA

## Data Story

This analysis explores a workplace training dataset of employees across multiple departments and regions, with the goal of understanding what drives training completion.

**What we found:**
Assessment scores are broadly normally distributed, suggesting most employees reach a similar level of understanding by the end of the course. However, scores vary noticeably by department, indicating that some teams may face greater challenges or receive less support during training.

The correlation heatmap revealed that engagement score and assessment score are among the strongest numerical predictors of whether an employee completes training. Employees who completed training consistently showed higher engagement scores, pointing to motivation and involvement as key factors in success.

Completion rates also differ substantially across departments. Some departments achieve close to full completion while others lag significantly behind, which has direct implications for how training programmes are designed and resourced.

**What this means for the business:**
Departments with low completion rates should be prioritised for additional manager support or adjusted training formats. Engagement appears to be an earlier signal of risk — identifying low-engagement employees early could allow for timely intervention before dropout occurs.

**Limitations:**
This dataset is a training sample and may not fully represent the organisation. Patterns observed here should be validated on a larger or more recent dataset before driving policy decisions.

---

## Modelling Hypotheses

**Features that may help a model predict `completed_training`:**

1. `engagement_score` — consistently higher among completers, likely a strong predictor of dropout risk.
2. `assessment_score` — correlates with completion, suggesting performance during the course reflects likelihood of finishing.
3. `manager_support_score` — employees with more managerial backing may be more likely to complete training.

**Feature that may cause leakage:**

- `completion_days` — this records how many days it took to complete the course, meaning it is only recorded *after* someone has already completed training. Including it in a model would leak the target variable and produce misleadingly high accuracy.
