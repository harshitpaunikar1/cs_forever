# Regression Analysis for Causal Inference

## Overview
Regression analysis estimates the relationship between a dependent variable and one or more independent variables by fitting a mathematical model to observed data. When used for causal inference, it attempts to isolate the effect of a specific variable by statistically controlling for other factors that might influence the outcome. Regression is one of the most widely used tools in business analytics. However, it only supports causal claims when the right variables are included and key assumptions are met.

---

## Why It Matters
Businesses rarely have the luxury of running experiments for every decision. Regression allows analysts to use observational data they already have to estimate causal effects, provided they account for confounding factors. It is the workhorse of applied economics and business analytics, powering everything from pricing models to workforce planning.

## Key Principles
- Including relevant control variables helps isolate the causal effect of the variable of interest by holding other influences constant
- Omitted variable bias occurs when an important confounder is left out of the model, distorting the estimated effect
- The relationship modeled must reflect the actual data-generating process; a misspecified model produces misleading results
- Regression on observational data can suggest causation but requires strong assumptions that must be justified and tested

## Key Terms
| Term | Definition |
|------|------------|
| **Dependent Variable** | The outcome being studied, whose variation the model tries to explain |
| **Independent Variable** | A factor included in the model as a potential driver or control for the dependent variable |
| **Omitted Variable Bias** | Distortion in estimated effects caused by leaving out a variable that is correlated with both the treatment and the outcome |
| **Control Variable** | A variable included in the regression not because its effect is of primary interest but to account for its confounding influence |

## Use Case
A hotel chain uses regression to estimate whether its loyalty program increases repeat bookings after controlling for customer demographics, travel frequency, and price sensitivity.

## Scenario
> A consumer electronics company wants to know if increasing warranty length causes higher customer satisfaction scores. The analytics team runs a regression on survey data, controlling for product category, purchase price, and customer age. The results show a statistically significant positive relationship between warranty length and satisfaction. However, the team recognizes that unobserved factors like brand loyalty could still bias the estimate, so they flag the finding as suggestive rather than definitive.

## Examples
- A retailer regresses store revenue on advertising spend, foot traffic, local income levels, and competitor proximity to estimate the causal return on advertising
- An HR department uses regression to assess whether a training program improves employee performance after controlling for tenure, education, and prior performance ratings

---

## Audited Appendix

# Regression Analysis for Causal Inference
**Course:** Applied Methods for Causal Analysis in Business
**Module:** Content / Regression Analysis for Causal Inference
**Audited on:** 2026-04-18
**Audited by:** A10
**Source files reviewed:** `causal-analysis-business/content/04-regression-causal-inference.md`

---

## 1. Topic Snapshot
Regression estimates the relationship between a dependent variable (Y) and one or more independent variables (X) by fitting a model to observed data; in a causal lens, it attempts to isolate the effect of a focal X by holding other relevant factors constant through statistical control. It is the workhorse of applied econometrics and business analytics precisely because randomised experiments are infeasible for most everyday decisions (pricing, warranty length, loyalty programs, training spend). However, regression only licenses causal claims when the specification reflects the true data-generating process (DGP) — i.e., all relevant confounders are included, functional form is correct, and error terms behave well; otherwise the coefficient is a biased descriptive slope, not a causal effect.

---

## 2. Jargon & Terminology

| # | Term | Plain Meaning | Business Signal | IT/AI/Product/Consulting Example |
|---|------|---------------|-----------------|----------------------------------|
| 1 | Linear Regression (OLS) | Fit line minimising squared residuals | Baseline estimator | PM regresses NPS on feature adoption |
| 2 | Dependent Variable (Y) | Outcome being explained | KPI | Churn, ARR, CSAT |
| 3 | Independent Variable (X) | Predictor / treatment | Lever | Price, onboarding hours |
| 4 | Coefficient β | Marginal effect of X on Y | Causal slope (if clean) | β_price = −0.8% churn per $1 |
| 5 | Intercept α | Y when all X = 0 | Baseline level | Churn when usage = 0 |
| 6 | Residual ε | Unexplained component | Model slack | Noise + omitted factors |
| 7 | R² | % variance explained | Fit quality | 0.42 on SaaS cohort |
| 8 | Adjusted R² | R² penalised for #regressors | Parsimony check | Prefer when adding controls |
| 9 | Standard Error (SE) | Sampling uncertainty of β̂ | Precision | Smaller SE → tighter CI |
| 10 | t-statistic | β̂ / SE | Significance test | |t| > 1.96 → p < 0.05 |
| 11 | p-value | Prob. of t given H0 | Decision proxy | 0.03 flagged |
| 12 | 95% CI | β ± 1.96·SE | Range of plausible effects | [−1.2%, −0.4%] |
| 13 | Multicollinearity (VIF) | Xs correlated | Unstable β | VIF > 5 concern |
| 14 | Heteroscedasticity | Non-constant error variance | Biased SE | White / Breusch-Pagan test |
| 15 | Autocorrelation | Errors correlated over time | Inflated t | Durbin-Watson ≈ 2 |
| 16 | Endogeneity | cov(X, ε) ≠ 0 | Biased β | Price set by demand shock |
| 17 | Omitted Variable Bias (OVB) | Missing confounder biases β | False causal claim | Brand loyalty unobserved |
| 18 | Control Variable | Covariate held constant | Confounder proxy | Tenure, segment |
| 19 | Confounder | Causes both X and Y | Creates spurious slope | Seasonality → ad & revenue |
| 20 | Instrumental Variable (IV) | Predicts X, not Y directly | Fix endogeneity | See 06-instrumental-variables |
| 21 | Fixed Effects (FE) | Entity/time dummies | Remove time-invariant bias | Cohort FE for churn |
| 22 | Random Effects | Entity effect ~ distribution | Assumes no corr w/ X | Hausman test |
| 23 | Cluster-Robust SE | SE accounting for intra-group correlation | Honest inference | Cluster by customer |
| 24 | Difference-in-Differences | Pre/post × treat/control | Quasi-experimental | See 05-DiD |
| 25 | Regression Discontinuity | Cutoff-based ID | Local causal | Scholarship threshold |
| 26 | Propensity Score | Prob(T=1|X) | Matching/weighting | See 08-PSM |
| 27 | Specification Curve | β across all defensible specs | Robustness map | Simonsohn et al. 2020 |
| 28 | Generalisation | Fit vs out-of-sample | Overfit/underfit | Holdout R² drop |

---

## 3. Frameworks & Matrices

### 3.1 OLS -> Causal Claim Ladder
**Purpose:** Choose the weakest assumption strong enough to support the claim; every rung costs more data / design.

```
Rung  Method              Key Assumption                     Cost
-----------------------------------------------------------------
1     Correlation         None (descriptive)                 Free
2     OLS + controls      Conditional independence (CIA)     Cheap
3     Fixed effects       No time-varying confounder         Panel data
4     Instrumental vars   Valid + relevant instrument        Hard
5     DiD                 Parallel trends                    Pre-periods
6     RDD                 Continuity at cutoff               Running var
```
**Components:** method, identifying assumption, data ask, falsification test.
**Worked example (AI Product):** Churn study starts at rung 2 (OLS w/ usage, plan, tenure); moves to rung 3 (cohort FE) after brand-era confound detected; rung 4 (IV = free-trial lottery) if endogeneity remains.
**Trigger:** Any time a stakeholder says "so the feature *caused* retention" — locate the claim on the ladder before signing off.

### 3.2 Assumption Stack (Gauss-Markov + Causal Overlay)
**Purpose:** Pre-flight checklist before reporting β as causal.

```
+--------------------------------------+
| Linearity in parameters              |
| Zero conditional mean E[ε|X]=0       |  <- causal crux (no OVB)
| No perfect multicollinearity         |
| Homoscedasticity Var(ε|X)=σ²         |
| Independent errors (no autocorr.)    |
| Normality of ε (inference only)      |
+--------------------------------------+
```
**Components:** assumption, diagnostic test, remedy, business-stakes column.
**Worked example (Consulting):** Retainer engagement audits ad-spend model — Breusch-Pagan flags heteroscedasticity → switch to HC3 robust SEs before boardroom read-out.
**Trigger:** Any regression headed into a decision doc > ₹1 cr impact.

### 3.3 OVB Diagnostic Worksheet
**Purpose:** Force the team to enumerate plausible omitted confounders and sign the bias.

```
Candidate Omitted z    | Sign(β_z on Y) | Sign(δ_kz: z~X) | Implied Bias Dir.
-----------------------+----------------+-----------------+-------------------
Brand loyalty          | +              | +               | UPWARD (overstates)
Seasonality            | +              | +               | UPWARD
Price promotion overlap| +              | -               | DOWNWARD
Salesforce push        | +              | +               | UPWARD
```
**Components:** z, hypothesised β_z, hypothesised δ, net bias direction, mitigation (proxy/FE/IV).
**Worked example (IT):** Warranty→satisfaction study: brand-loyalty z is unobserved, both signs positive → β_warranty is biased UP; label finding "suggestive, likely upper bound."
**Trigger:** Every observational regression presented as causal.

### 3.4 (Optional) Specification Curve
**Purpose:** Plot β̂ and CI across every defensible model spec; robust effects survive the curve.

```
β̂
 |           . . . .
 |        . .       . . .
 | . . . .                . .  <- majority negative, robust
 |________________________________
          spec 1 ... spec 128
```
**Trigger:** When reviewers will challenge "cherry-picked controls."

---

## 4. Formulas

### 4.1 OLS Estimator
β̂ = (X'X)^{-1} X'Y
**Threshold:** Needs X'X invertible (no perfect multicollinearity); n > k + a few.
**IT example:** Regress monthly churn on feature-usage, tenure, plan, segment (n=12k users, k=4) → β̂_feature = −0.008 (−0.8 pp per extra session/week).

### 4.2 Partial-Regression Coefficient
β_k = effect of X_k on Y holding X_{-k} constant (Frisch-Waugh-Lovell: regress X_k on other Xs → residual; regress Y on that residual).
**Threshold:** Interpret only if controls span the confounder set.
**Example:** β_training on performance after partialling out tenure + education + prior rating = 0.12 (12% lift).

### 4.3 Variance Inflation Factor
VIF_k = 1 / (1 − R_k²), where R_k² = R² of regressing X_k on all other Xs.
**Thresholds:** VIF > 5 watch; VIF > 10 serious multicollinearity.
**Example:** In ad-spend model, TV_spend and digital_spend co-move → VIF = 8 → combine into log-total or use ridge.

### 4.4 OVB Formula
Bias(β̂_k) = β_z · δ_{kz}
where β_z = true effect of omitted z on Y, δ_{kz} = coefficient from auxiliary regression of z on X_k (and other controls).
**Threshold:** If product |β_z · δ| exceeds 20% of β̂_k, claim is fragile.
**Example:** Warranty coef = +0.30; suspect brand-loyalty β_z ≈ +0.5, δ ≈ +0.4 → bias ≈ +0.20 → true effect plausibly +0.10 only.

### 4.5 Cluster-Robust SE (Liang-Zeger, 1986)
V_cluster = (X'X)^{-1} · Σ_g X_g' ε̂_g ε̂_g' X_g · (X'X)^{-1}
**Threshold:** Cluster at the level of treatment assignment; #clusters G ≥ 30 for asymptotics.
**Example:** Rolling out warranty policy at store level (G = 180 stores) → cluster SEs at store, not customer; naive SE understates by ~3×.

### 4.6 Elasticity (log-linear interpretation)
Elasticity = β · (X̄ / Ȳ); or directly β in log-log specs (d ln Y / d ln X).
**Threshold:** |elasticity| > 1 = elastic; < 1 = inelastic.
**Example:** Consulting pricing study: β_price = −0.0015, X̄ = $99, Ȳ = 0.08 churn → elasticity = −1.86 (highly elastic; a 10% price rise → ~18.6% churn lift).

---

## 5. Do vs Don't

| # | Do | Don't |
|---|------|--------|
| 1 | Draw a DAG before choosing controls | Throw every column into the model ("kitchen-sink") |
| 2 | Report β, SE, 95% CI, and n together | Report only p-values |
| 3 | Use cluster-robust SEs at assignment level | Use default OLS SEs for panel / nested data |
| 4 | Run a specification curve for key claims | Show only the best-looking spec |
| 5 | Label claims "suggestive" when OVB plausible | Call any significant β "the causal effect" |
| 6 | Test heteroscedasticity + autocorrelation | Assume i.i.d. errors with time-series data |
| 7 | Use fixed effects to sweep unit-invariant confounders | Add "controls" that are themselves outcomes (bad controls) |
| 8 | Cross-validate out-of-sample R² | Optimise in-sample R² by adding regressors |
| 9 | Pre-register specification for high-stakes decisions | Iterate specs until p < 0.05 (p-hacking) |
| 10 | Translate β into business units (₹, pp, elasticity) | Leave β in raw standardised form for execs |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI Product (Churn vs Feature Usage)
A PM at a B2B SaaS firm regresses monthly churn on feature-usage, tenure, plan, segment. Raw β = −1.2 pp/session. DAG reveals "customer success touches" as a likely confounder (CS reaches power-users more often, reduces churn). Team adds CS-touch count, cohort FE, and clusters SE by account → β shrinks to −0.5 pp. Specification curve across 64 defensible models shows 58 negative, median −0.4 pp → claim labelled robust-but-modest. Tools: Python `statsmodels` + `linearmodels` for FE, `econml` for heterogeneous effects, Jupyter on Snowflake, Papermill for reproducible runs.

### Scenario 2 — HR Analytics (Training → Performance)
Consulting team regresses annual performance rating on training hours controlling for tenure, education, prior rating. β = 0.12 (12% lift). Specification curve across alternative controls (manager FE, department FE, role level) yields β range [0.04, 0.14]; 95% of specs significant and positive. Recommendation: invest, but with heterogeneous-effect caveats — interactions show benefit concentrated in tenure < 3 years. Tools: R `plm` + `lfe` for FE, Stata for panel diagnostics, Looker for downstream dashboards.

### Scenario 3 — ANTI-EXAMPLE (Ad-Spend ROI Misclaim)
Marketing team regresses weekly revenue on ad-spend only. β = 2.3 → claims "₹1 of ads returns ₹2.30." Missing controls: seasonality (Diwali/EoSS), pricing promos, competitor stock-outs. After adding month FE, promo dummies, competitor index, and clustering SE at region, β collapses to 0.6. Prior over-claim led to a ₹14 cr over-budgeting in the next quarter — mis-allocation ≈ ₹14 cr when true causal lift is 0.6×. Lesson: ad-spend is endogenous (set in response to expected sales); use geo-holdout experiments or IV before scaling.

**Tooling summary:** Python (`statsmodels`, `linearmodels`, `econml`), R (`plm`, `lfe`, `fixest`), Stata; Jupyter notebooks on Snowflake/BigQuery; Looker & Mode for diagnostics dashboards; Papermill + dbt for reproducibility; DoubleML / EconML for ML-augmented causal estimates.

---

## 7. Implementation Playbook

1. **Draft DAG** of the causal question (focal X, Y, candidate confounders, mediators, colliders) in dagitty or whiteboard.
2. **Specify base model** Y = α + βX + γ·Controls + ε; pre-register in notebook header before pulling data.
3. **Pull + QC data** (missingness, outliers, leakage checks); stamp dataset hash in Snowflake.
4. **Fit OLS + diagnostics** (VIF, Breusch-Pagan, Durbin-Watson, residual plots) in `statsmodels`.
5. **Upgrade SEs** — cluster-robust at assignment level; re-run t-stats and CIs.
6. **Add Fixed Effects / alternative specs** — build specification curve (≥ 16 defensible specs) with `specr` (R) or custom loop.
7. **Stress-test OVB** using Oster (2019) δ/R²-max bounds or manual β_z·δ_kz worksheet.
8. **Translate & communicate** — convert β into ₹, pp, or elasticity; label claim on the Causal Claim Ladder; publish notebook + dashboard.

---

## 8. Content Quality Audit

**Covered well in source:** core definitions (dependent/independent var, OVB, control), intuitive hotel & electronics examples, caveat that observational regression only *suggests* causation.

**Underplayed / missing:**
- Formal OVB decomposition (β_z · δ_kz) with numeric bounds.
- Cluster-robust and heteroscedasticity-consistent standard errors.
- Fixed effects vs random effects (Hausman); panel data treatment.
- Specification curve analysis as a robustness-communication tool.
- DAG-guided control selection (good vs bad controls, colliders).
- Heterogeneous treatment effects via interaction terms or causal forests.
- Rigorous statement of identifying assumptions (CIA, SUTVA, overlap).

**Supplementary sources (≥5):**
1. Angrist, J. D. & Pischke, J.-S. (2008). *Mostly Harmless Econometrics*. Princeton UP.
2. Wooldridge, J. M. (2019). *Introductory Econometrics: A Modern Approach*, 7th ed. Cengage.
3. Cunningham, S. (2021). *Causal Inference: The Mixtape*. Yale UP.
4. Hernán, M. A. & Robins, J. M. (2020). *Causal Inference: What If* (online, Harvard).
5. Simonsohn, U., Simmons, J. P., & Nelson, L. D. (2020). "Specification Curve Analysis." *Nature Human Behaviour*, 4, 1208-1214.
6. Oster, E. (2019). "Unobservable Selection and Coefficient Stability." *JBES*, 37(2).

**Red flags in source material:**
- Uses the word "significant" without distinguishing statistical vs practical significance.
- No mention of standard-error choice (homoscedastic vs robust vs clustered).
- Hotel / electronics examples treat "controlling for demographics" as sufficient — risks licensing under-rigorous causal claims in classroom use.
- No guidance on what *not* to control for (colliders, post-treatment variables).

---

## 9. Quick-Recall Card
- Regression gives a *causal* β only when the specification reflects the DGP; otherwise it is a descriptive slope.
- OVB = β_z · δ_kz: enumerate omitted confounders and sign the bias before shipping the claim.
- Always upgrade SEs (robust + clustered) and run a specification curve for high-stakes decisions.
- Place every claim on the Causal Claim Ladder: OLS → FE → IV → DiD → RDD; the rung dictates the assumption burden.
- Translate β into ₹, pp, or elasticity — executives act on units, not coefficients.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: *Which confounders, if omitted, would flip the sign or halve the magnitude of my β — and have I controlled, fixed-effected, or instrumented them away before calling this causal?*

---

**Connects to:** [01-causation-vs-correlation.md](01-causation-vs-correlation.md), [05-difference-in-differences.md](05-difference-in-differences.md), [06-instrumental-variables.md](06-instrumental-variables.md), [08-propensity-score-matching.md](08-propensity-score-matching.md), [../business-analytics/08-regression-analysis-business.md](../business-analytics/08-regression-analysis-business.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [2 (expanded to 28 terms w/ IT lens), 3 (added Specification Curve + OVB worksheet), 4 (added cluster-robust + elasticity), 6 (added anti-example w/ ₹14 cr cost), 8 (added Oster + specification curve refs), 9 (role-lens question)]
Enrichments applied: [cross-course links; 6 supplements; anti-example w/ quantified cost; IT/AI/Product/Consulting tooling stack; role-lens question starting "As a PM/Consultant/AI Lead"]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A10
-->
