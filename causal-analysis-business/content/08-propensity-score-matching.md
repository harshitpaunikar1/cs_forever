# Propensity Score Matching

## Overview
Propensity score matching is a method that reduces selection bias in observational studies by pairing treated units with untreated units that have a similar probability of receiving the treatment. The propensity score summarizes multiple characteristics into a single number representing the likelihood of being treated. By comparing outcomes between matched pairs that had similar chances of receiving the treatment, analysts approximate what a randomized experiment would have shown. It is widely used when experiments are not feasible but rich background data is available.

---

## Why It Matters
In business, the people or units that receive a treatment, such as a training program, a marketing campaign, or a product upgrade, are rarely chosen at random. Those who opt in or are selected often differ systematically from those who do not. Propensity score matching addresses this by creating a balanced comparison, allowing analysts to draw more credible causal conclusions from the observational data companies already collect.

## Key Principles
- The propensity score is the estimated probability of receiving treatment given observed characteristics
- Matching on the propensity score balances the distribution of observed covariates between treated and untreated groups
- The method assumes that all important confounders are observed and included in the propensity score model
- Common support requires that there are untreated units with propensity scores similar to those of treated units; without overlap, matching fails

## Key Terms
| Term | Definition |
|------|------------|
| **Propensity Score** | The estimated probability that a unit receives the treatment, calculated from observed background characteristics |
| **Matching** | The process of pairing each treated unit with one or more untreated units that have similar propensity scores |
| **Common Support** | The range of propensity scores where both treated and untreated units exist, ensuring valid comparisons can be made |
| **Selection Bias** | Systematic differences between treated and untreated groups that arise because treatment assignment was not random |

## Use Case
A professional services firm wants to evaluate whether attending its leadership development program causes promoted employees to perform better, so it matches program attendees with non-attendees who had similar tenure, performance ratings, and department backgrounds.

## Scenario
> A health insurance company introduces a wellness program and wants to measure its effect on medical claims. Employees who enrolled tend to be younger and healthier, so a simple comparison would underestimate costs for non-enrollees. The analytics team estimates each employee's probability of enrolling based on age, salary, job role, and prior claims. They match each enrollee with a non-enrollee who had a nearly identical probability of joining. Comparing medical claims between these matched pairs provides a fairer estimate of the program's true causal effect.

## Examples
- A retail bank matches customers who received a credit limit increase with similar customers who did not, based on income, credit score, and account age, to estimate the causal effect on spending
- A technology company matches employees who used an internal mentorship platform with non-users of similar seniority and department to evaluate the platform's effect on promotion rates

---

## Audited Appendix

# Propensity Score Matching

**Course:** Causal Analysis for Business
**File:** 08 — Propensity Score Matching
**Industry Lens:** IT / AI / Product / Consulting
**Connects to:** [01-causal-vs-correlation.md](01-causal-vs-correlation.md) | [02-randomized-controlled-trials.md](02-randomized-controlled-trials.md) | [03-difference-in-differences.md](03-difference-in-differences.md) | [05-instrumental-variables.md](05-instrumental-variables.md) | [07-regression-discontinuity.md](07-regression-discontinuity.md)

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|------|--------------------------|---------------------------|
| Propensity Score | The estimated probability that a unit (person, firm, product user) receives the treatment, given its observed characteristics. Modeled via logistic regression or ML classifiers. | Reduces a multi-dimensional covariate adjustment problem to a single number, enabling tractable matching and balance assessment. |
| Selection Bias | The distortion that arises when the treated group differs from the control group in ways that also affect the outcome — making naive comparisons misleading. | In tech, users who adopt a new feature are almost never identical to those who don't; ignoring this inflates perceived treatment effects. |
| Matching | The process of pairing each treated unit with one or more untreated units that have a nearly identical propensity score (or covariate profile). | Creates a pseudo-control group that mirrors the treated group, enabling apples-to-apples outcome comparison without a true experiment. |
| Common Support (Overlap) | The region of propensity scores where both treated and untreated units exist. Units outside this region cannot be matched and must be excluded. | Generalizing results beyond the common support is invalid; in product analytics, heavy users often fall outside common support with casual users. |
| Balancing Property | The statistical property that, conditional on the propensity score, the distribution of observed covariates is identical across treated and untreated groups. | Confirms the matching worked; validated via standardized mean differences (SMDs) before outcome analysis. |
| Standardized Mean Difference (SMD) | The difference in covariate means between treated and untreated groups, divided by a pooled standard deviation. Benchmark: SMD < 0.1 after matching signals good balance. | Used to declare matching successful; auditors and peer reviewers inspect SMD plots ("love plots") as proof of covariate balance. |
| Average Treatment Effect on the Treated (ATT) | The causal effect of treatment for those who actually received it — the estimand PSM most naturally delivers, as matched controls are chosen to mirror the treated. | Answers the operational question: "Did our program work for the people who went through it?" More actionable than ATE in targeted rollouts. |
| Caliper | A maximum allowable distance between propensity scores of matched pairs. Tighter calipers improve balance but reduce the matched sample size. | A caliper of 0.2 standard deviations of the logit propensity score is a widely used rule of thumb; too loose a caliper reintroduces bias. |
| Nearest-Neighbor Matching | The simplest matching algorithm: each treated unit is paired with the untreated unit whose propensity score is closest (with or without replacement). | Easy to implement but sensitive to caliper width and replacement choice; with replacement improves balance but inflates variance. |
| Kernel Matching | A weighted matching approach where each treated unit is compared to a weighted average of all untreated units, with higher weights given to closer propensity scores. | Increases efficiency by using all control observations but requires bandwidth tuning; preferred for large datasets common in SaaS analytics. |
| Covariate | A pre-treatment variable (feature) included in the propensity score model because it is a potential confounder — i.e., it predicts both treatment and outcome. | Including post-treatment variables as covariates introduces collider bias and invalidates the analysis; variable selection requires domain knowledge. |
| Ignorability / Unconfoundedness | The assumption that, conditional on observed covariates, treatment assignment is independent of potential outcomes. Also called "no hidden bias." | PSM is only as valid as this assumption; unobserved confounders (e.g., employee motivation) can silently invalidate the entire analysis. |

---

## Frameworks & Mental Models

### Framework 1 — The PSM Pipeline

PSM is a multi-stage workflow. Each stage has a failure mode that can silently corrupt results.

```
+------------------+     +---------------------+     +-------------------+
|  1. DESIGN       |     |  2. ESTIMATE         |     |  3. MATCH         |
|                  |     |                      |     |                   |
| Identify:        | --> | Logistic regression  | --> | Nearest-neighbor  |
| - Treatment T    |     | (or GBM, RF) of      |     | / Kernel / Radius |
| - Outcome Y      |     | P(T=1 | X)           |     | matching          |
| - Covariates X   |     |                      |     | Apply caliper     |
| (pre-treatment   |     | Output: propensity   |     | Exclude off-      |
|  only)           |     | score p_hat for each |     | support units     |
+------------------+     +---------------------+     +-------------------+
          |                                                    |
          v                                                    v
+------------------+     +---------------------+     +-------------------+
|  4. ASSESS       |     |  5. ESTIMATE EFFECT  |     |  6. REPORT        |
|  BALANCE         |     |                      |     |                   |
| SMD < 0.1?       | --> | Compare Y between    | --> | ATT ± SE          |
| Love plot        |     | matched T=1, T=0     |     | Sensitivity test  |
| Overlap check    |     | (t-test, regression) |     | (Rosenbaum bounds)|
| If fail: re-spec |     |                      |     | Generalizability   |
| covariate model  |     |                      |     | caveat            |
+------------------+     +---------------------+     +-------------------+
```

### Framework 2 — Selection Bias Anatomy in Tech/Product

```
         OBSERVED WORLD (no PSM)
         ========================

  TREATED group         CONTROL group
  (used new feature)    (did not use)
  ┌──────────────┐      ┌──────────────┐
  │ Power users  │      │ Casual users │
  │ High tenure  │      │ Low tenure   │
  │ B2B segment  │      │ B2C segment  │
  │ Outcome: +35%│      │ Outcome: +5% │
  └──────────────┘      └──────────────┘
         ↓
  Naive estimate: 35% - 5% = +30% lift (BIASED — confounders differ)

         AFTER PSM
         =========

  TREATED (matched)     MATCHED CONTROLS
  ┌──────────────┐      ┌──────────────┐
  │ Power users  │  ←→  │ Power users  │
  │ High tenure  │      │ High tenure  │
  │ B2B segment  │      │ B2B segment  │
  │ Outcome: +35%│      │ Outcome: +28%│
  └──────────────┘      └──────────────┘
         ↓
  PSM estimate: 35% - 28% = +7% lift (LESS BIASED — comparable groups)
```

### Framework 3 — The Unconfoundedness Threat Map

```
                     VARIABLES
                         |
         +---------------+---------------+
         |               |               |
   PRE-TREATMENT    POST-TREATMENT    UNOBSERVED
   COVARIATES       VARIABLES        CONFOUNDERS
   (include in      (NEVER include   (threat to
    PS model)        in PS model)     validity)
         |               |               |
    Adjusts for    Would introduce   Cannot be
    confounding    collider bias     controlled
                                     by PSM
                                         |
                                  Rosenbaum
                                  Sensitivity
                                  Analysis
                                  (tests how
                                   fragile
                                   results are)
```

### Framework 4 — Estimand Choice Map

```
  Question: Who is the target population for inference?

  "Did the program work            "Would the program work
   for participants?"               for everyone?"
         |                                |
         ATT                             ATE
   (Average Treatment             (Average Treatment
    Effect on Treated)              Effect)
         |                                |
   PSM naturally                   Harder with PSM;
   delivers this                   IPW / AIPW better
         |
   Most consulting
   engagements ask
   for ATT
```

---

## Formulas, Thresholds & Rules of Thumb

### 1. Propensity Score Estimation

**Logistic regression model:**

```
logit[P(T=1 | X)] = β₀ + β₁X₁ + β₂X₂ + ... + βₖXₖ
p̂ᵢ = 1 / (1 + exp(−(β₀ + β₁X₁ᵢ + ... + βₖXₖᵢ)))
```

- Context: X must include all pre-treatment confounders. In SaaS product analytics, typical covariates include account age, plan tier, prior NPS score, industry vertical, and number of active users in prior quarter.
- ML alternatives (gradient boosting, random forests) can model nonlinear relationships but require regularization to avoid overfitting propensity scores.

### 2. Nearest-Neighbor Matching Distance

```
Distance(i, j) = | p̂ᵢ − p̂ⱼ |   (on raw probability scale)
or
Distance(i, j) = | logit(p̂ᵢ) − logit(p̂ⱼ) |   (preferred: logit scale)
```

- Context: The logit scale spreads scores near 0 and 1, reducing "crowding" at extremes common when treatment prevalence is low (e.g., < 10% of users adopt a beta feature).

### 3. Caliper Width Rule of Thumb

```
Caliper = 0.2 × SD(logit(p̂))
```

- Context (Austin, 2011): Calipers tighter than 0.1 SD may discard too many treated units; looser than 0.25 SD often fails to eliminate bias. For enterprise software rollouts, typical logit SD is 1.0–1.5, yielding calipers of 0.20–0.30.

### 4. Standardized Mean Difference (SMD)

```
SMD = (X̄_treated − X̄_control) / √[(SD²_treated + SD²_control) / 2]
```

- Threshold: SMD < 0.1 (10%) is the widely accepted criterion for covariate balance post-matching. Values between 0.1–0.2 warrant caution. Values > 0.2 indicate matching failure; re-specify the propensity score model.
- Context: In AI product launches, SMD is reported for every covariate in a balance table presented to product leadership before any outcome analysis begins.

### 5. Average Treatment Effect on the Treated (ATT)

```
ATT = E[Y(1) − Y(0) | T=1]
    ≈ (1/N_T) Σᵢ∈T [Yᵢ − Ŷᵢ(0)]
```

where Ŷᵢ(0) is estimated from the matched control unit(s).

- Context: If ATT = +12% reduction in support tickets, the interpretation is: "Among employees who participated in the training, participation caused a 12% reduction in support escalations on average."

### 6. Rosenbaum Sensitivity Parameter (Γ)

```
Γ = odds of treatment for unit i / odds of treatment for unit j
  (when i and j have identical observed covariates)
```

- Threshold interpretation: Γ = 1 means no hidden bias. Γ = 1.5 means results hold even if an unobserved confounder increased odds of treatment by 50%. Γ = 2 is considered a moderately robust result. Below Γ = 1.3, results are fragile and require strong caveats.
- Context: For consulting deliverables presented to CFOs, always report the Γ at which the p-value crosses 0.05; this communicates how much unobserved confounding would overturn the finding.

### 7. Sample Size After Matching

```
Effective N ≈ N_treated × (match_ratio / (1 + match_ratio)) × 2
```

- Rule: Plan for 20–40% sample loss from caliper exclusions plus off-support trimming. For a study with 500 treated users, target at least 1,500–2,000 untreated users in the raw data to have adequate control pool.

---

## Do / Don't

### Do

1. **Include all relevant pre-treatment confounders** in the propensity score model. In IT consulting contexts, this means pulling CRM data, prior usage logs, firmographic data, and historical performance metrics — not just what is convenient.
2. **Use the logit of the propensity score** (not the raw probability) as the distance metric for matching, especially when propensity scores cluster near 0 or 1.
3. **Apply a caliper** to exclude poor matches. Document the caliper width and justify it relative to the 0.2 × SD(logit p̂) rule of thumb.
4. **Produce a balance table and love plot** before any outcome analysis. Report SMD for every covariate, both before and after matching. SMD < 0.1 is required before proceeding.
5. **Assess common support** by overlaying propensity score distributions of treated and untreated. Trim or exclude units outside the overlap region and document what share of the treated sample was excluded.
6. **Run a Rosenbaum sensitivity analysis** and report the Γ threshold. This is the minimum required step to communicate robustness to unobserved confounding — non-negotiable in HBS-style case write-ups.
7. **Clarify the estimand** (ATT vs. ATE) and state which population the results generalize to. In product analytics, ATT answers "Did the feature help adopters?" — which is the primary business question.
8. **Pair PSM with regression adjustment** on the matched sample (double-robust estimation or bias-corrected matching) to reduce residual imbalance bias, especially with continuous treatments or rich covariate spaces.
9. **Document exclusions and their justification** in a methods appendix. Regulators, internal audit functions, and replication reviewers will inspect this; in BFSI and healthcare tech, this is a compliance requirement.
10. **Communicate uncertainty honestly**: PSM yields causal estimates only under unconfoundedness. If that assumption is suspect, frame findings as "suggestive evidence" rather than definitive causal claims.

### Don't

1. **Don't include post-treatment variables** as covariates in the propensity score model. Variables measured after treatment assignment introduce collider bias and invalidate the balancing property. In product analytics, do not include metrics collected during or after the feature rollout period.
2. **Don't skip the balance check** and proceed directly to outcome comparison. An unbalanced matched sample does not support causal inference; it is just a biased observational study with extra steps.
3. **Don't use PSM when common support is thin or absent**. If 60% of treated units have no plausible control match, PSM results reflect a non-representative subset and should not drive business decisions.
4. **Don't overfit the propensity score model**. A model that perfectly predicts treatment (AUC near 1.0) produces propensity scores near 0 or 1 for everyone, making matching impossible. The goal is balance, not prediction accuracy.
5. **Don't treat PSM as equivalent to an RCT**. PSM controls only for observed confounders. Unobserved confounders (e.g., employee ambition, customer intent-to-churn) can still bias results. Always pair with sensitivity analysis.
6. **Don't generalize ATT results to the untreated population** without justification. ATT estimates the effect for those who received treatment; extrapolating to non-participants requires additional assumptions.
7. **Don't match on variables that are proxies for treatment** (instruments or post-treatment mediators). Matching on mediators blocks the causal path and biases the estimate toward zero.
8. **Don't report only the matched-sample outcome comparison**. Also report: (a) covariate balance table, (b) sample sizes before and after matching, (c) share excluded from common support, (d) sensitivity Γ. Omitting these signals methodological naivety.
9. **Don't use PSM for very high-dimensional covariate spaces** without dimensionality reduction. With 50+ covariates, a simple logistic regression propensity model may be mis-specified; consider regularized models or entropy balancing instead.
10. **Don't present PSM results without an honest discussion of unconfoundedness**. For board-level or client deliverables, name the specific unobserved variables that could confound results and explain why you believe they are not driving the finding.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1 — Enterprise SaaS: Effect of Customer Success Manager (CSM) Assignment on Retention

**Trigger:** A B2B SaaS company (ARR: $200M) wants to know whether assigning a dedicated CSM to mid-market accounts causes higher renewal rates. The challenge: CSMs are assigned based on account size, product complexity, and perceived churn risk — all of which also predict renewal.

**Analysis:**
- Treatment: Dedicated CSM assigned (T=1) vs. pooled CSM support (T=0)
- Outcome: 12-month contract renewal (binary)
- Covariates: ARR at assignment, product tier, number of active seats, integrations deployed, support tickets in prior 6 months, NPS score, industry vertical, account age
- Propensity score estimated via logistic regression; logit-scale caliper of 0.20 × SD applied
- Balance check: All 8 covariates achieve SMD < 0.08 post-matching
- Common support: 94% of treated accounts are within support region; 6% excluded (very large enterprise accounts with no comparable controls)

**Decision:**
- ATT = +11 percentage points in renewal rate (matched t-test, p < 0.001)
- Γ sensitivity analysis: result holds up to Γ = 1.7 (unobserved confounder would need to increase odds of CSM assignment by 70% to overturn the finding)
- Decision: Expand dedicated CSM coverage to all mid-market accounts above $50K ARR

**Result:**
- Pilot expansion quarter: renewal rate improved by 9 percentage points vs. prior year cohort, closely consistent with the PSM estimate; revenue impact approximately $4M in retained ARR.

**Anti-Example:**
- The sales ops team initially proposed comparing renewal rates across the entire CSM-assigned vs. non-assigned book of business (naive comparison). This showed a +28pp difference — more than double the causal estimate — because the largest, most stable accounts were disproportionately CSM-assigned. Acting on the naive figure would have led to CSM hiring projections triple the justified level, wasting $2M+ in headcount budget on an overstated effect.

---

### Scenario 2 — AI/Product: Effect of In-App AI Writing Assistant on User Engagement

**Trigger:** A productivity SaaS product team launches an AI writing assistant. After 60 days, the data team observes that users who activated the assistant have 2.3× higher weekly active usage. The VP of Product wants to claim causation in the board deck.

**Analysis:**
- Treatment: AI assistant activated within first 14 days of account creation (T=1)
- Outcome: Weekly Active Days at Day 60
- Covariates: Plan tier, prior-14-day login frequency (pre-activation), number of documents created in first week, team size, industry, device type (mobile/desktop), onboarding flow completed (Y/N)
- Gradient boosting model used for propensity score estimation (AUC: 0.74; avoids overfitting — checked via cross-validation)
- Caliper: 0.20 × SD(logit p̂) = 0.18
- Balance: 7 of 7 covariates at SMD < 0.10 post-matching; prior-14-day login frequency was the most critical balancing variable (early adopters of AI tool were inherently more engaged)

**Decision:**
- ATT = +0.8 weekly active days (vs. naive 2.3× suggesting +3.1 days)
- PSM-adjusted effect is modest but statistically significant (p = 0.002); Γ = 1.4
- Decision: AI assistant drives genuine but moderate engagement lift; product team deprioritizes aggressive AI upsell and instead invests in improving AI quality to increase effect size

**Result:**
- Avoids overstating ROI in board deck; product roadmap focuses on AI quality improvements; 2-quarter follow-up shows improved effect size (+1.4 WAD) after AI quality sprint — consistent with hypothesis.

**Anti-Example:**
- Using the raw 2.3× figure, the original marketing brief proposed pricing the AI tier at $40/user/month premium based on projected engagement-to-conversion assumptions. PSM revealed the true incremental effect was 74% smaller, implying the premium was justified only at $12–15/user/month. Proceeding with $40 pricing would have caused significant churn among price-sensitive SMB accounts.

---

### Scenario 3 — IT Consulting: Effect of Agile Training Program on Project Delivery Time

**Trigger:** A global IT consulting firm runs a 3-day Agile certification training for delivery teams. Six months later, HR wants to show the training reduced project overruns. Teams that attended were predominantly from larger, more mature accounts — which also tend to have more structured delivery processes.

**Analysis:**
- Treatment: Team attended Agile training (T=1, N=320 teams) vs. did not attend (T=0, N=1,100 teams)
- Outcome: Project schedule variance (% overrun vs. planned timeline)
- Covariates: Team size, account revenue tier, prior delivery score, geographic region, project type (fixed-price vs. T&M), years of team experience, prior overrun rate (6 months pre-training)
- Propensity score via logistic regression; matching 1:2 (each treated team matched to 2 controls) with replacement; caliper = 0.20 SD
- Balance: Prior overrun rate and account revenue tier were primary confounders; SMD reduced from 0.31 and 0.28 (pre-match) to 0.07 and 0.06 (post-match)

**Decision:**
- ATT = −8.4 percentage points in schedule variance (teams that attended training had overruns 8.4pp lower than matched non-attendees)
- Γ = 1.6: unobserved confounder would need to increase odds of training attendance by 60% to overturn finding
- Decision: Firm mandates Agile training for all delivery teams; expected annual benefit modeled at $12M in avoided penalties and scope overruns

**Result:**
- Firm-wide mandate implemented; 18-month tracking shows −7.1pp overrun reduction across mandated cohort — within confidence interval of PSM estimate. Training program ROI validated.

**Anti-Example:**
- An initial cross-sectional regression by the HR analytics team (without PSM) showed only −2.1pp effect, because it failed to adequately control for non-linear interactions between account maturity and prior overrun rates. If HR had used the regression result, they would have underestimated the program's value and potentially discontinued it — sacrificing $12M in annual benefit.

---

## Practitioner Playbook

**Step-by-step guide for IT/AI/Product/Consulting teams implementing PSM**

1. **Define the causal question precisely.** State: (a) unit of analysis (user, team, account), (b) treatment definition with clear start/end dates, (c) outcome variable and measurement window, (d) target estimand (ATT or ATE). Write this as a one-paragraph study protocol before touching any data.

2. **Identify and assemble pre-treatment covariates.** Pull all variables that: (i) precede treatment assignment temporally, and (ii) plausibly predict both treatment uptake and the outcome. In SaaS product work, this typically requires joining behavioral logs, CRM data, support ticket history, and billing tables. Document the variable list with business justification for each.

3. **Screen for post-treatment contamination.** Audit each candidate covariate for its measurement date. Any variable measured after treatment begins must be excluded. Build a timeline diagram mapping variable measurement dates vs. treatment start date.

4. **Estimate the propensity score.** Default: logistic regression with all covariates from Step 2. Check model fit (Hosmer-Lemeshow or calibration plot). If AUC > 0.90, the model likely overfits or a covariate is a near-perfect predictor — investigate and adjust. For high-dimensional data (> 30 covariates), consider LASSO-regularized logistic regression or gradient boosting with cross-validation.

5. **Inspect the raw propensity score distribution.** Plot overlapping histograms of propensity scores for treated and control. Identify the common support region. Flag what fraction of treated units fall outside it. If > 15% of treated units lack common support, reconsider the study scope or population.

6. **Execute matching with caliper.** Use caliper = 0.20 × SD(logit p̂). Choose matching ratio (1:1, 1:2, or kernel) based on control pool size vs. treated pool size. For scarce controls (< 3:1 ratio), use kernel or radius matching. For abundant controls (> 5:1), 1:1 nearest-neighbor without replacement is efficient.

7. **Assess covariate balance.** Compute SMD for every covariate, before and after matching. Generate a love plot (dot plot of SMDs with a vertical reference line at 0.1). All covariates must achieve SMD < 0.10 post-matching. If any covariate fails, return to Step 4 and re-specify the propensity score model (add interaction terms, polynomial terms, or use a more flexible ML model).

8. **Re-check common support post-matching.** Confirm that matched controls are genuinely within the treated propensity score range. Remove any matched pairs where the control score falls outside the treated distribution.

9. **Estimate the treatment effect.** For 1:1 matched data: use a paired t-test or OLS regression on the matched dataset. For matched data with weights or kernel matching: use weighted regression. For binary outcomes: use logistic regression on matched pairs or risk-difference estimation. Always cluster standard errors by matched pair ID.

10. **Apply bias-corrected or doubly-robust adjustment.** Run a regression on the matched sample controlling for residual covariate imbalance (Abadie-Imbens bias-corrected matching estimator, or AIPW). This provides additional protection against the propensity score model being slightly mis-specified.

11. **Run Rosenbaum sensitivity analysis.** Use the rbounds package (R) or equivalent. Report the Γ value at which the result would no longer be statistically significant at p < 0.05. For client deliverables, frame this as: "Our finding would be overturned only if an unobserved variable increased the odds of treatment assignment by [Γ−1]×100%."

12. **Document and present results with full transparency.** Deliverable must include: (a) balance table with before/after SMDs, (b) propensity score overlap plot, (c) sample sizes at each stage (raw → within-support → matched), (d) ATT estimate with confidence interval, (e) sensitivity Γ, (f) explicit statement of the unconfoundedness assumption and known threats to it.

13. **Flag generalizability constraints.** If common support excluded treated units (e.g., extreme power users, very large enterprise accounts), results apply only to the in-support subset. State this limitation explicitly in the executive summary and recommendations section.

14. **Design a validation step.** Where possible, identify a natural experiment or partial RCT data that can serve as an external validity check. In product analytics, A/B test results from adjacent features can calibrate the PSM estimate.

---

## Content Critique & Depth Gaps

### What the Source Material Covers Well
The source provides an accurate conceptual foundation: propensity score as a summary statistic, the matching logic, and the intuition behind balancing covariate distributions. The use cases (leadership development, wellness programs, credit limit increases, mentorship platforms) illustrate the concept accessibly.

### Gaps Requiring IIM/HBS MBA Depth

**1. Estimand Ambiguity**
The source does not distinguish between ATT, ATE, and ATC (Average Treatment Effect on the Control). For consulting deliverables, this distinction is critical: ATT answers "did our program work for participants?" while ATE answers "would it work if we rolled it out to everyone?" Misidentifying the estimand leads to incorrect policy recommendations.

**2. Failure Modes and Diagnostics**
The source omits the most common PSM failure modes: (a) propensity score model mis-specification, (b) near-positivity violations (thin common support), (c) matching on mediators. These are the errors that most frequently invalidate PSM studies in practice and are the first things a rigorous reviewer will check.

**3. Sensitivity Analysis**
Rosenbaum bounds — the standard method for quantifying robustness to unobserved confounding — are entirely absent. No credible causal inference study should be published or presented without this. The source's omission is a significant depth gap for anyone using PSM in professional contexts.

**4. Alternatives and When to Prefer Them**
PSM is not always the best quasi-experimental method. The source should compare PSM to: (a) Inverse Probability Weighting (IPW), which uses all data without discarding off-support controls, (b) Doubly Robust / AIPW estimators, which combine propensity score and outcome model for added robustness, (c) Coarsened Exact Matching (CEM), which matches directly on coarsened covariates without a propensity model. Knowing when to use each is core MBA-level decision-making.

**5. High-Dimensional Covariate Settings**
Modern IT/AI datasets routinely have hundreds of potential covariates. The source's implicit assumption of a small, hand-curated covariate set is anachronistic. Methods like LASSO-penalized propensity models, entropy balancing, and targeted maximum likelihood estimation (TMLE) are standard in data-science-heavy organizations.

**6. Temporal Dynamics**
PSM assumes stable treatment assignment. In SaaS and AI products, treatment (feature adoption) is ongoing and users switch in and out. Dynamic treatment effects require more sophisticated frameworks (Marginal Structural Models, sequential g-estimation) that the source does not acknowledge.

**7. Multiple Testing and Outcome Pre-Registration**
When multiple outcomes are tested after matching (e.g., retention, ARPU, NPS, support tickets), results must be corrected for multiple comparisons or pre-registered. The source makes no mention of this, risking p-hacking in practice.

**8. Software and Implementation**
No mention of implementation tools: MatchIt (R), Python's causalinference or CausalML packages, Stata's teffects psmatch, or commercial platforms like Databricks' causal inference libraries. MBA-level practitioners need to know the implementation landscape.

**9. Ethical and Fairness Considerations**
In HR analytics (leadership programs, promotions), PSM analyses that use demographic proxies as covariates risk encoding discriminatory patterns into the matched control group. The source does not address fairness implications, which are increasingly central to AI governance and responsible analytics.

---

## Quick-Recall Card

**Propensity Score Matching — At a Glance**

- PSM collapses multi-dimensional covariate adjustment into a single score: P(T=1|X)
- Core assumption: unconfoundedness — all important confounders are observed and included
- Estimate the score (logit regression or ML) → match treated to controls with similar scores → check balance → estimate outcome difference
- Common support is non-negotiable: matched pairs must overlap in propensity score space
- Success criterion for matching: SMD < 0.1 for every covariate in the balance table
- Caliper rule: 0.2 × SD(logit p̂); tighter improves balance, looser improves sample retention
- PSM most naturally delivers ATT — the effect for those who actually received treatment
- Rosenbaum Γ quantifies fragility to unobserved confounding; always report it; Γ < 1.3 is a weak result
- PSM ≠ RCT: unobserved confounders can still bias results; sensitivity analysis is mandatory, not optional
- Double-robustness: combine PSM with regression adjustment on matched sample for added protection
- In IT/AI/Product contexts, the three most common PSM mistakes are: (1) including post-treatment variables as covariates, (2) skipping the balance check, (3) not assessing common support
- Alternatives to consider: IPW when you want to use all data; CEM for exact coarsened matching; AIPW for doubly-robust estimation; Diff-in-Diff when temporal pre-post data is available
- For consulting deliverables: always state the estimand, always show the balance table, always report Γ, always name the unobserved confounders that could threaten validity

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "After matching on propensity scores and verifying covariate balance, what is the estimated causal effect of this intervention on our treated population, and how sensitive is that estimate to the presence of unobserved confounders?"

---

## Self-Audit Report

<!-- Self-Audit: 
  WORKER: A4
  TARGET FILE: 08-propensity-score-matching.md
  DATE: 2026-04-18

  SECTION COMPLETENESS CHECK:
  [PASS] Section 1 — Jargon Buster: 12 terms provided (minimum 8 required). All entries have Term, Plain-English Definition, and Why It Matters in Practice columns. Industry lens (IT/AI/Product/Consulting) applied throughout examples.
  [PASS] Section 2 — Frameworks & Mental Models: 4 frameworks provided, each with an ASCII diagram. Covers PSM pipeline, selection bias anatomy, unconfoundedness threat map, and estimand choice. Diagrams are text-art compliant.
  [PASS] Section 3 — Formulas, Thresholds & Rules of Thumb: 7 formula blocks with contextual explanation. Covers logistic model, distance metric, caliper rule, SMD formula and threshold, ATT definition, Rosenbaum Γ, and sample size planning.
  [PASS] Section 4 — Do / Don't: 10 Do items and 10 Don't items (minimum 8 each required). All grounded in IT/consulting/product/AI contexts.
  [PASS] Section 5 — Metric-Driven Scenarios with Anti-Examples: 3 full scenarios provided. Each contains Trigger → Analysis → Decision → Result → Anti-Example structure. Industries covered: B2B SaaS (CSM assignment), AI/Product (writing assistant engagement), IT Consulting (Agile training).
  [PASS] Section 6 — Practitioner Playbook: 14 numbered steps with operational detail. Covers full PSM workflow from problem definition to validation. IT/AI/Product implementation references included.
  [PASS] Section 7 — Content Critique & Depth Gaps: 9 distinct gaps identified. Covers estimand ambiguity, failure modes, sensitivity analysis, alternatives, high-dimensional settings, temporal dynamics, multiple testing, software, and ethics/fairness.
  [PASS] Section 8 — Quick-Recall Card: Bullet-point format. Final sentence begins exactly "As a PM/Consultant/AI Lead" as required. The role-lens question is specific and actionable.
  [PASS] Section 9 — Self-Audit Report: Present as HTML comment as required.

  CONNECTS TO LINKS: Present at top of file. Links to 5 related course files.
  MINIMUM SIZE: File is well above 13 KB threshold given section depth.
  INDUSTRY LENS: IT/AI/Product/Consulting lens applied consistently across all sections.
  ESTIMAND COVERAGE: ATT vs ATE distinction explicitly covered in multiple sections.
  SENSITIVITY ANALYSIS: Rosenbaum bounds covered in Formulas section, Do section, Playbook, Quick-Recall Card, and Content Critique.
  KNOWN RISKS: Unconfoundedness assumption explicitly named and caveated throughout; not presented as equivalent to RCT.

  VERDICT: All 9 mandatory sections present, all structural requirements met, industry lens consistent, minimum size exceeded. File is publication-ready.
-->
