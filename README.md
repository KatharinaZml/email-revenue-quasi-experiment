# Estimating the effect of email acquisition on customer revenue using Propensity Score Matching (PSM)

This project examines the causal effect of email acquisition on customer revenue using a quasi-experimental approach with PSM on observational e-commerce data.

## 1. Business question

*Does acquisition via the email channel lead to higher customer revenue?*

## 2. Why PSM?

Users in this dataset were not randomly assigned to acquisition channels. Therefore, a simple comparison of average revenue between email and non-email users would be biased, since users acquired through different channels may differ systematically. For example, more engaged users may self-select into email signup). PSM reduces this selection bias by matching each email to a non-email users with a similar estimated probability of being acquired through email, based on observed pre-treatment characteristics.

## 3. Method

1. **Feature engineering**: Aggregated raw order, session and demographic data into a user level feature table
2. **Propensity score model**: Logistic regression was applied to  estimate each user's probability of email acquisition, using pre-treatment demographic covariates (age, gender, country, state) to avoid post-treatment bias
3. **Common support check**: Before matching, propensity scores between treatment and control groups were verified
4. **1:1 nearest-neighbour matching**: Matched email to non-email users on a 1:1 principle.
5. **Covariate balance check**: Validated this matching by observed differences between groups
6. **ATT estimation**:  Average Treatment Effect (ATE) on the treated, based on matched-pair revenue differences
7. **Paired t-test** : Significance testing appropriate for 1:1 matched pairs

## 4. Key finding

The estimated ATT was **−$1.34**. Specifically, email users generated slightly less revenue than matched non-email users. However,the effect was not statistically significant (p = 0.61; 95% CI: −$6.51 to $3.83, which includes zero). Consequently, there is no statistically significant evidence that email acquisition affects customer revenue.

## 5. Limitations

- **Observational data**: Treatment assignment was not randomised. This means causal conclusions cannot be established with certainty
- **Unobserved confounding** : PSM only adjusts for variables included in the propensity model. Factors such as purchase intent, prior marketing exposure, or browsing behaviour were not available and may still confound the result
- **Limited covariates**: Only demographic characteristics were used, deliberately restricted to pre-treatment variables to avoid post-treatment bias, at the cost of a thinner covariate set
-> The result should be interpreted as an adjusted association, not definitive causal evidence

## 6. Tools

Python — pandas, scikit-learn (LogisticRegression, NearestNeighbours), scipy (paired t-test), matplotlib / seaborn

## 7. Data

`bigquery-public-data.thelook_ecommerce` (Google Cloud public dataset), used via local CSV exports (`users`, `orders`, `order_items`, `products`, `inventory_items`, `distribution_centers`, `events`).
