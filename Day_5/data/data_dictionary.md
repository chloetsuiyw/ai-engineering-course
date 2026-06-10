# Data Dictionary - Workplace Churn Feature Engineering Dataset

| Column | Type | Description | Quality issue | Feature use | Leakage risk |
|---|---|---|---|---|---|
| customer_id | string | Synthetic customer identifier | No | Identifier only; do not model directly | Possible entity leakage if repeated across splits |
| signup_date | date string | Date customer started subscription | Yes after conversion | Can derive tenure/cohort/month | Safe if known at prediction time |
| last_login_date | date string | Most recent login before prediction date | Yes after conversion | Can derive days_since_login | Must ensure it is before prediction date |
| region | category | UK region | Yes | Can be one-hot encoded | Fairness and representation caveat |
| sector | category | Organisation sector | Yes | Can be one-hot encoded | May encode structural differences |
| plan_type | category | Subscription plan | Yes | Can be one-hot encoded | Safe if known before prediction |
| contract_type | category | Monthly or annual contract | Yes | Can be one-hot encoded | Safe if known before prediction |
| acquisition_channel | category | How customer was acquired | Yes | Can be encoded | Check small groups |
| monthly_fee_gbp | numeric | Current monthly subscription fee | Yes | Can be transformed or used in ratios | Safe if known at prediction |
| tenure_months | numeric | Months since signup | Yes | Can be binned or used in interactions | Safe if calculated at prediction date |
| usage_minutes_30d | numeric | Usage minutes in last 30 days | Some missing | Can create ratios and low-usage flags | Safe if window closes before prediction |
| active_days_30d | numeric | Number of active days in last 30 days | Yes | Can create usage per active day | Safe if window closes before prediction |
| support_tickets_90d | numeric | Support tickets in last 90 days | Yes | Can create support-load features | Safe if known before prediction |
| invoices_late_6m | numeric | Late invoices in last six months | Yes | Can indicate payment friction | Sensitive business handling |
| satisfaction_score | numeric | Recent customer survey score | Some missing | Can create low-satisfaction flag | Check response bias |
| renewal_month | numeric/category | Renewal month | Yes | Can create seasonal/cyclical feature | Safe if known |
| account_notes | text | Short account-management note | Some blank | Can derive keyword flags/length | Review personal data and minimisation |
| cancellation_reason | category | Reason recorded after churn | Yes but leaky | Exclude from model features | Target/future leakage |
| account_closed_date | date string | Closure date after churn | Yes but leaky | Exclude from model features | Future information |
| retention_offer_after_churn | category | Action after churn event | Yes but leaky | Exclude from model features | Future information |
| churned | binary target | Whether customer churned | Target | Do not use as input feature | Target variable |
