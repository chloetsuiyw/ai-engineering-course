# Feature Justification Report

Three additional features were engineered from the workplace churn dataset to improve the model's ability to identify customers at risk of leaving.

**Feature 1: late_payment_rate**

This feature divides the number of late invoices in the last six months by the customer's tenure in months. The business rationale is that payment friction means something very different depending on how long a customer has been with the company — two late payments in three months is far more concerning than two late payments over three years. This ratio gives the model a cleaner signal of payment behaviour relative to relationship length. The feature is safe from leakage as both invoices_late_6m and tenure_months are known before the prediction date. A governance caveat is that new customers have very low tenure values which can inflate the ratio significantly, so clipping the output at a sensible maximum should be considered.

**Feature 2: days_to_renewal**

This feature calculates how many days remain until a customer's next renewal date. Customers are most likely to churn at the point when their contract is up for renewal, as this is the natural decision moment. Giving the model visibility of how close each customer is to that window allows it to weight at-risk customers more appropriately. The renewal_month field is recorded in the system before prediction and is therefore leakage-free. The main caveat is that this feature is most meaningful for annual contracts. Monthly contract customers face a renewal decision every month, which reduces the signal value.

**Feature 3: satisfaction_x_support_load**

This interaction feature multiplies an inverted satisfaction score by the number of support tickets raised in the last 90 days. A high volume of support tickets alone does not necessarily indicate churn risk, as engaged, satisfied customers can be heavy support users. However, high ticket volume combined with low satisfaction is a strong warning sign. Combining them into a single term allows a logistic regression model to capture this joint effect without requiring a more complex model. Both inputs are pre-prediction so there is no leakage risk. The key caveat is that missing satisfaction scores are filled with a neutral value of 5, which is an assumption that should be revisited if the missingness is not random.