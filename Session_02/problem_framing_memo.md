# Problem Framing Memo — Service Request Triage

## Problem Statement
When a service request is submitted, predict whether it will be resolved on time, so the team can prioritise support for at-risk cases.

## Target
`resolved_on_time`: 1 if the case was resolved on time, 0 otherwise.

## Safe Features
`submitted_date`, `channel`, `service_area`, `customer_type`, `postcode_area`, `priority_flag`, `previous_cases`

## Leakage Exclusions
`days_open`, `updates_count`, `assigned_team`, `late_status_2024`, `satisfaction_score`, `case_id`

These columns are excluded because they are either only known after the case closes (`days_open`, `satisfaction_score`), accumulate during the case (`updates_count`), are effectively the target itself (`late_status_2024`), or carry no predictive signal (`case_id`). `assigned_team` is excluded as it may not be determined at the point of submission.

## Split Strategy
Use a time-based split on `submitted_date`: oldest 60% for training, next 20% for validation, newest 20% for test. A random split must be avoided here — it would allow future data to leak into training.

## Success Metrics
- **Recall** for at-risk cases (predicted `resolved_on_time = 0`): the priority metric, since missing a case that will fail is a real service harm
- **Precision** for at-risk cases: kept in check to avoid overwhelming teams with false alarms
- **Slice checks** by `service_area` and `channel`: overall accuracy can hide uneven performance across groups

## Top 3 Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Leakage from post-resolution columns | High | High | Remove `days_open`, `late_status_2024`, `satisfaction_score` before training |
| Unfair prioritisation by postcode area | Medium | High | Test performance by `postcode_area`; consider aggregating or excluding it |
| Target encodes historic service delays, not true risk | Medium | Medium | Review the target definition with operations and frontline staff before training |
