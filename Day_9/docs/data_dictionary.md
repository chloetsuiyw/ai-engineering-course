# Data Dictionary - Session 09 Pipeline Tuning Dataset

| Column | Type | Role | Leakage / use note |
|---|---|---|---|
| `request_id` | object | Identifier | Exclude from modelling |
| `request_channel` | object | Candidate feature | No, if available at triage |
| `service_area` | object | Candidate feature | No, if available at triage |
| `request_type` | object | Candidate feature | No, if available at triage |
| `customer_segment` | object | Candidate feature | No, if available at triage |
| `priority_at_submission` | object | Candidate feature | No, if available at triage |
| `request_age_hours_at_triage` | float64 | Candidate feature | No, if available at triage |
| `previous_tickets_90d` | int64 | Candidate feature | No, if available at triage |
| `open_items_for_team` | int64 | Candidate feature | No, if available at triage |
| `staff_available` | int64 | Candidate feature | No, if available at triage |
| `attachments_count` | int64 | Candidate feature | No, if available at triage |
| `has_clear_description` | int64 | Candidate feature | No, if available at triage |
| `historical_team_delay_rate` | float64 | Candidate feature | No, if available at triage |
| `requester_tenure_months` | float64 | Candidate feature | No, if available at triage |
| `day_of_week` | object | Candidate feature | No, if available at triage |
| `sla_breach_risk` | int64 | Target label | No - target, not a feature |
| `post_resolution_hours_DO_NOT_USE` | float64 | Post-outcome field | Yes - exclude from features |
| `final_status_DO_NOT_USE` | object | Post-outcome field | Yes - exclude from features |

The target is `sla_breach_risk`. Columns ending in `DO_NOT_USE` are intentionally included to practise leakage exclusion.
