# Estimating the Effect of Email Acquisition on Customer Revenue using Propensity Score Matching

**Quasi-experimental analysis (Python) estimating whether Email acquisition causes higher customer revenue than other acquisition channels**, using Propensity Score Matching (PSM) on observational e-commerce data.

## Business question

*Does acquisition via the Email channel lead to higher customer revenue than other acquisition channels?*

## Why Propensity Score Matching?

Users in this dataset were not randomly assigned to acquisition channels — a simple comparison of average revenue between Email and Non-Email users would be biased, since users acquired through different channels may differ systematically (e.g. more engaged users may self-select into email signup). Propensity Score Matching reduces this selection bias by matching each Email user to a Non-Email user with a similar estimated probability of being acquired through Email, based on observed pre-treatment characteristics.

## Method

1. **Feature engineering** — aggregated raw order, session, and demographic data into a user-level feature table
2. **Propensity score model** — logistic regression estimating each user's probability of Email acquisition, using only pre-treatment demographic covariates (age, gender, country, state) to avoid post-treatment bias
3. **Common support check** — verified sufficient overlap in propensity scores between treatment and control groups before matching
4. **1:1 nearest-neighbour matching** — matched ~4,995 Email users to ~4,995 comparable Non-Email users
5. **Covariate balance check** — confirmed matching meaningfully reduced observed differences between groups
6. **ATT estimation** — Average Treatment Effect on the Treated, based on matched-pair revenue differences
7. **Paired t-test** — significance testing appropriate for 1:1 matched pairs

## Key finding

The estimated ATT was **−$1.34** (Email users generated slightly less revenue than matched Non-Email users), but the effect was **not statistically significant** (p = 0.61; 95% CI: −$6.51 to $3.83, which includes zero). Based on the observed data, there is no statistically significant evidence that Email acquisition affects customer revenue.

## Limitations

- **Observational data** — treatment assignment was not randomized, so causal conclusions cannot be established with certainty
- **Unobserved confounding** — PSM only adjusts for variables included in the propensity model; factors like purchase intent, prior marketing exposure, or browsing behaviour were not available and may still confound the result
- **Limited covariates** — only demographic characteristics were used, deliberately restricted to pre-treatment variables to avoid post-treatment bias, at the cost of a thinner covariate set
- The result should be interpreted as an **adjusted association**, not definitive causal evidence

## Tools

Python — pandas, scikit-learn (LogisticRegression, NearestNeighbors), scipy (paired t-test), matplotlib, seaborn

## Data

`bigquery-public-data.thelook_ecommerce` (Google Cloud public dataset), used via local CSV exports (`users`, `orders`, `order_items`, `products`, `inventory_items`, `distribution_centers`, `events`).
