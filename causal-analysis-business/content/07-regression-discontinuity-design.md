# Regression Discontinuity Design

## Overview
Regression discontinuity design exploits situations where treatment is assigned based on whether a numeric score falls above or below a specific cutoff. Units just above and just below the cutoff are nearly identical in all respects except that one group received the treatment and the other did not. By comparing outcomes for these units near the threshold, analysts can estimate a causal effect that is almost as credible as a randomized experiment. This method is powerful because the cutoff creates a quasi-random assignment mechanism.

---

## Why It Matters
Many business and policy decisions involve clear thresholds: credit score cutoffs for loan approval, performance score cutoffs for bonuses, or eligibility cutoffs for government programs. Regression discontinuity lets analysts use these existing cutoffs as natural experiments. It provides highly credible causal estimates without requiring deliberate randomization, making it one of the most persuasive quasi-experimental methods available.

## Key Principles
- The cutoff must create a sharp or fuzzy discontinuity in the probability of receiving treatment
- Units just above and just below the cutoff should be comparable in all observable and unobservable characteristics
- Individuals must not be able to precisely manipulate their score to land on a preferred side of the cutoff
- The causal estimate applies locally to units near the cutoff and may not generalize to units far from it

## Key Terms
| Term | Definition |
|------|------------|
| **Running Variable** | The numeric score or measure that determines treatment assignment based on whether it crosses the cutoff |
| **Cutoff** | The threshold value of the running variable that determines who receives the treatment |
| **Sharp Design** | A regression discontinuity where crossing the cutoff perfectly determines treatment status with no exceptions |
| **Fuzzy Design** | A regression discontinuity where crossing the cutoff increases the probability of treatment but does not guarantee it |

## Use Case
A bank approves small business loans for applicants with credit scores at or above 650 and denies those below, allowing analysts to compare business outcomes for applicants just above and just below the threshold to estimate the causal effect of receiving the loan.

## Scenario
> A software company awards performance bonuses to salespeople who hit at least 100 percent of their quarterly quota. A salesperson at 99 percent is nearly identical in ability and effort to one at 101 percent, yet only the latter receives the bonus. By comparing retention and next-quarter performance for salespeople just above and just below the cutoff, the company estimates whether the bonus itself causes improved future performance or longer tenure.

## Examples
- A university admits students with entrance exam scores above a threshold, and researchers compare graduation rates for students just above and below the cutoff to estimate the causal effect of attending that university
- An e-commerce platform offers free shipping on orders above fifty dollars, and analysts compare return rates for orders just above and below the threshold to see if free shipping causally affects returns

---

## Audited Appendix

# Regression Discontinuity Design

Regression discontinuity design exploits situations where treatment is assigned based on whether a numeric score falls above or below a specific cutoff. Units just above and just below the cutoff are nearly identical except one group received the treatment. This provides almost-experimental causal estimates.

**Key Principles:**
- Cutoff must create a sharp or fuzzy discontinuity in treatment probability
- Units just above and below the cutoff should be comparable
- Individuals must not be able to precisely manipulate their score
- The causal estimate applies locally to units near the cutoff (local average treatment effect)

**Key Terms:** Running Variable, Cutoff, Sharp Design, Fuzzy Design

**Use Case:** Bank approves small business loans for credit scores ≥650. Comparing business outcomes for applicants just above vs just below gives causal effect of receiving the loan.

**Scenario:** Software company awards performance bonuses to salespeople who hit ≥100% of quarterly quota. Salesperson at 99% is nearly identical to one at 101% in ability/effort. Comparing retention and next-quarter performance for people just above and below the cutoff estimates whether the bonus causes improved performance.

**Examples:**
- University admissions by entrance exam score — compare graduation rates for students just above/below cutoff
- E-commerce platform offers free shipping on orders above $50 — compare return rates for orders just above/below threshold

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|------|--------------------------|----------------------------|
| Running Variable (Forcing Variable) | The numeric score or metric that determines whether a unit receives treatment. Must be continuous and measurable. | In IT product settings, this could be a user's activity score, credit score, or usage metric. The quality of the RD estimate depends entirely on how well this variable is measured and how resistant it is to gaming. |
| Cutoff (Threshold) | The specific value of the running variable above or below which treatment is assigned. Creates a discontinuous jump in treatment probability. | Setting the cutoff is a policy decision with direct causal implications. Moving a software license threshold from 10 to 15 seats changes which customers receive enterprise support — and RD quantifies that effect. |
| Sharp RD Design | A design where crossing the cutoff deterministically switches treatment from 0 to 1. Everyone above gets treated; everyone below does not. | Most applicable in rule-based systems: SLA tier assignment, quota-based bonuses, automated approval workflows. The causal estimate is the most credible of any quasi-experimental design. |
| Fuzzy RD Design | A design where crossing the cutoff increases (but does not guarantee) the probability of treatment. Compliance is imperfect. | Common in enterprise contexts where human override exists — e.g., a credit score threshold triggers a recommendation, but relationship managers can override it. Requires IV-style estimation (LATE, not ATT). |
| Local Average Treatment Effect (LATE) | The causal effect of the treatment estimated specifically for units near the cutoff — not for the entire population. | A critical limitation: findings from the margin cannot be extrapolated to customers far from the cutoff. An AI lead cannot use RD results from borderline users to justify a policy shift for power users. |
| Bandwidth | The window of the running variable on either side of the cutoff used in estimation. Narrower windows increase internal validity; wider windows increase statistical power. | Choosing bandwidth is one of the most consequential analytical decisions. Too wide: you include units that are not comparable. Too narrow: you run out of data. Optimal bandwidth selection (e.g., Imbens-Kalyanaraman) should be reported in any consulting deliverable. |
| Manipulation Test (McCrary Test) | A diagnostic that checks whether the density of the running variable is smooth at the cutoff, or whether there is a suspicious spike indicating that units gamed their scores to receive treatment. | If salespeople can round up their quota attainment, or developers can inflate code commit counts near performance review cycles, the core comparability assumption breaks down. Always visualize and test the density. |
| Continuity Assumption | The requirement that all potential confounders change smoothly at the cutoff — only treatment jumps discontinuously. | This is the central identifying assumption and cannot be directly tested. Placebo tests at fake cutoffs and covariate balance checks provide indirect evidence. Violating this makes the RD estimate meaningless. |
| Polynomial Order | The degree of the polynomial regression fit on either side of the cutoff used to model the relationship between running variable and outcome. | Higher-order polynomials can overfit and produce spurious discontinuities. Modern best practice (Gelman & Imbens, 2019) recommends local linear or at most quadratic fits, not cubic or higher. |
| Donut RD | A variant that excludes observations very close to the cutoff to address precise manipulation concerns. | Useful in consulting engagements where there is evidence of gaming right at the threshold. Removing the donut hole and testing whether the discontinuity persists is a robustness check. |

---

## Frameworks & Mental Models

### Mental Model 1: The Comparability Window

The core logic of RD is that near the cutoff, treatment assignment is as good as random. The further you move from the cutoff, the less valid this assumption becomes.

```
OUTCOME
  |
  |                                        * * *
  |                              * * * * *
  |                    * * * * *                  <-- treated units (above cutoff)
  |          * * * * *
  |        *
  |      * |<-- DISCONTINUITY: causal effect
  |    *   |
  |  *     |
  |*       |  * * *
  |        |*       * * * * *
  |        |                   * * * * * * * * *  <-- control units (below cutoff)
  |        |
  +--------+----------------------------------------> RUNNING VARIABLE
           ^
         CUTOFF
         
  |<----->|  Bandwidth: the estimation window
  
  The jump at the cutoff = estimated causal effect (LATE)
```

### Mental Model 2: Sharp vs. Fuzzy Design

```
SHARP RD                           FUZZY RD

P(Treatment)                       P(Treatment)
1.0 |          **********          1.0 |
    |          *                       |              * * * * *
0.5 |          *                   0.7 |          * *
    |          *                       |        * *
0.0 |**********                    0.3 |* * * *
    +----------+------->               +--------+-------->
             Cutoff                           Cutoff

Treatment jumps from 0 to 1        Treatment probability jumps
deterministically                  but not to certainty

Estimation: OLS on either side     Estimation: IV/2SLS
                                   (cutoff as instrument)
Effect: ATE near cutoff            Effect: LATE (compliers only)
```

### Mental Model 3: The Bandwidth-Bias-Variance Tradeoff

```
          |<---------------------- Full data range ---------------------->|
          
  Bias    [LOW BIAS                                              HIGH BIAS]
          [                    WIDE BANDWIDTH                            ]
          
  Variance[HIGH VARIANCE][                                               ]
          [  NARROW BW  ]

Optimal Bandwidth:
          
  MSE     |        *
  (Mean   |      *   *
  Sq Err) |    *       *
          |  *           *
          |*               * * * * * * * * (plateaus at high variance)
          +--+-----------------------------------> Bandwidth
             ^
          Optimal BW
          (Imbens-Kalyanaraman or cross-validation)

Practitioner rule: start with IK-optimal BW, report results at 0.5x, 1x, 2x as robustness check.
```

### Mental Model 4: Sorting and Gaming — The Threat Map

```
THREAT: Can units sort themselves across the cutoff?

                    CAN they KNOW the cutoff?
                    /                        \
                  YES                        NO
                  /                            \
    CAN they control their score?           Low manipulation risk
          /             \                   (proceed with RD)
        YES              NO
        /                  \
  HIGH RISK               MODERATE RISK
  (McCrary test            (test density;
  likely fails;             probably OK)
  consider Donut RD
  or abandon design)

IT Examples of HIGH RISK:
- Employees who know their KPI threshold can pad metrics at quarter-end
- Users who learn the free shipping threshold can adjust cart value
- Vendors aware of credit score cutoff can coach applicants to hit it

IT Examples of LOW RISK:
- Algorithm-assigned quality scores that users cannot observe
- Automated system health scores computed on encrypted telemetry
- Regulatory FICO cutoffs where exact formula is proprietary
```

---

## Formulas, Thresholds & Rules of Thumb

### Core RD Estimator (Sharp Design)

```
tau_RD = lim_{x -> c+} E[Y | X = x]  -  lim_{x -> c-} E[Y | X = x]

Where:
  tau_RD = estimated causal effect (LATE at cutoff c)
  Y      = outcome variable
  X      = running variable
  c      = cutoff value
  x -> c+ = limit from above (treated side)
  x -> c- = limit from below (control side)
```

**Context:** This is estimated in practice by fitting separate regression lines on each side of the cutoff within the chosen bandwidth and computing the gap at the cutoff. The result is an estimate of the jump in outcome attributable to the treatment.

---

### Local Linear Regression Specification

```
Y_i = alpha + tau * D_i + beta_1*(X_i - c) + beta_2*D_i*(X_i - c) + epsilon_i

Where:
  D_i    = 1 if X_i >= c (treatment indicator)
  tau    = estimated discontinuity (causal effect)
  beta_1 = slope of regression line for control units
  beta_2 = additional slope change for treated units (interaction)
  c      = cutoff (centering the running variable)
```

**Context:** The interaction term allows the slope to differ on each side of the cutoff. This is standard best practice. Forcing the same slope on both sides introduces misspecification bias.

---

### Fuzzy RD via 2SLS

```
Stage 1: D_i = pi_0 + pi_1*(1[X_i >= c]) + gamma*(X_i - c) + v_i
Stage 2: Y_i = alpha + tau_fuzzy * D_hat_i + delta*(X_i - c) + epsilon_i

tau_fuzzy = Jump in outcome at cutoff / Jump in treatment probability at cutoff
          = (lim E[Y|X->c+] - lim E[Y|X->c-]) / (lim E[D|X->c+] - lim E[D|X->c-])
```

**Context:** In consulting contexts where compliance is imperfect (e.g., a credit policy that can be overridden), the Fuzzy RD estimate is the LATE for compliers only — those who were induced into treatment by crossing the threshold. Always report the first-stage jump to demonstrate instrument relevance.

---

### Bandwidth Selection — Imbens-Kalyanaraman Rule

```
h_IK = C_K * sigma * n^(-1/5)

Where:
  C_K   = kernel-specific constant (triangular kernel commonly used)
  sigma = estimated standard deviation of outcome
  n     = sample size

Rule of Thumb: Report results at h_IK, 0.5 * h_IK, and 2 * h_IK.
If estimates are stable across bandwidths, confidence in the finding increases.
```

---

### Sample Size / Power Rule of Thumb

```
Minimum observations near cutoff:
  - For detectable effects of ~0.2 SD: need ~400 units per side within bandwidth
  - For detectable effects of ~0.5 SD: need ~70 units per side within bandwidth
  - For detectable effects of ~0.1 SD: need ~1500+ units per side within bandwidth

RD is less statistically efficient than a true RCT by a factor of ~3-5x
because it only uses observations near the cutoff.
```

**Context:** In enterprise SaaS with thin margins near a pricing threshold, RD may be underpowered. Consider whether a pilot RCT is more feasible before investing in observational analysis.

---

### McCrary Density Test (Manipulation Check)

```
H0: density of X is continuous at cutoff c
H1: there is a discontinuous jump in density at c (evidence of manipulation)

Practical threshold: p < 0.05 suggests manipulation
Visual check: histogram of running variable should be smooth at cutoff
```

---

### Placebo Cutoff Test

```
Re-run the RD at a "fake" cutoff above and below the true cutoff.
Expected result: NO significant discontinuity at placebo cutoffs.

If discontinuities appear at multiple cutoffs, the design may be invalid
or the outcome has a non-linear relationship with the running variable.
```

---

## Do / Don't

### DO

1. **Do visualize the data first.** Plot the running variable against the outcome with a scatter plot and overlaid regression lines. Visual inspection is not optional — it reveals non-linearities, outliers, and whether the discontinuity is credible before you run a single regression.

2. **Do run the McCrary density test on the running variable.** In any IT or consulting setting where employees, users, or vendors might be aware of the threshold, manipulation is a real risk. Publish the test statistic and p-value in your deliverable.

3. **Do report results across multiple bandwidths.** Always show the estimate at the IK-optimal bandwidth, half the bandwidth, and double the bandwidth. Stability across these is your primary robustness argument to a skeptical CFO or board.

4. **Do use local linear (or at most quadratic) polynomial fits.** Gelman and Imbens (2019) showed convincingly that high-order polynomials produce spurious discontinuities. Stick to low-order fits and let bandwidth selection carry the flexibility.

5. **Do check covariate balance at the cutoff.** Run the same RD specification using pre-treatment covariates (demographics, historical behavior) as outcomes. No covariate should show a significant jump at the cutoff. This is indirect evidence for the continuity assumption.

6. **Do account for the local nature of the estimate.** The RD LATE applies to units near the cutoff. Explicitly communicate to stakeholders that the finding does not generalize to users far above or far below the threshold.

7. **Do consider the Donut RD if manipulation near the cutoff is suspected but not conclusive.** Excluding the narrow band immediately around the cutoff and testing whether the effect persists is a credible robustness check.

8. **Do test for heterogeneous effects within the bandwidth.** Split the sample by user segment, industry vertical, or tenure. The LATE may differ dramatically across subgroups, and that information drives differentiated product or policy decisions.

9. **Do document the policy rule clearly.** The entire validity of RD rests on the cutoff being a real, binding rule. If the cutoff is fuzzy due to organizational discretion, design a Fuzzy RD with proper IV estimation from the start.

10. **Do use the triangular kernel by default.** It weights observations closer to the cutoff more heavily, which is consistent with the local comparability logic and is the standard in peer-reviewed econometrics.

### DON'T

1. **Don't extrapolate findings beyond the cutoff neighborhood.** If a $50 free-shipping threshold causes a 5% increase in order completion for orders between $45–$55, you cannot assume the same effect holds for a $100 threshold. This is one of the most common misapplications in product analytics.

2. **Don't use high-order polynomials to fit the regression.** Cubic and quartic polynomials are statistically tempting but methodologically flawed. They can generate false discontinuities purely through overfitting noise far from the cutoff.

3. **Don't ignore the manipulation threat.** In quota-based systems, enterprise procurement, or user-facing score displays, the assumption that units cannot sort around the cutoff is frequently violated. Treat this as guilty until proven innocent.

4. **Don't confuse RD with regression adjustment.** RD identifies causal effects through the discontinuity in treatment assignment, not through controlling for the running variable in a linear model. Adding more controls to a standard regression does not replicate RD logic.

5. **Don't apply RD when the cutoff is soft or negotiated.** If there is organizational flexibility to place borderline cases above or below the cutoff (e.g., a manager can override an automated loan denial), the Sharp RD assumption is violated. Use Fuzzy RD or a different design.

6. **Don't treat the bandwidth decision as arbitrary.** Choosing a bandwidth that happens to produce a significant result — and not reporting sensitivity — is p-hacking. Pre-register your bandwidth selection rule or use algorithmic selection and report all robustness checks.

7. **Don't forget that LATE ≠ ATE.** Decision-makers often ask "what would happen if we applied this policy to everyone?" RD cannot answer that. Explicitly manage this expectation in consulting deliverables and product reviews.

8. **Don't ignore measurement error in the running variable.** If the running variable is measured with substantial noise, the effective cutoff is blurred. Classical measurement error in the running variable attenuates the RD estimate toward zero.

9. **Don't use RD when the cutoff changes over time without modeling it.** If a credit score threshold was 650 in Q1 and 680 in Q2, pooling data without time fixed effects or separate estimation will produce a biased estimate.

10. **Don't skip the placebo test.** Testing the same specification at a non-cutoff value is among the cheapest and most persuasive robustness checks available. Its absence from a consulting presentation signals analytical inexperience.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: Sales Performance Bonus and Next-Quarter Revenue

**Trigger:** A SaaS company's Head of Revenue Operations questions whether the quarterly performance bonus (awarded to salespeople hitting ≥100% of quota) actually drives incremental revenue in the following quarter, or whether it merely rewards those who were already on an upward trajectory.

**Analysis:**
- Running variable: Q3 quota attainment percentage (continuous)
- Cutoff: 100% quota attainment
- Outcome: Q4 individual revenue generated
- Bandwidth: IK-optimal = ±8 percentage points around 100%
- Covariates checked for balance: years of tenure, deal size, territory, product line
- McCrary test: p = 0.31 — no evidence of manipulation
- Sharp RD estimate: tau = +$42,000 in Q4 revenue (SE = $11,000, p < 0.001)

**Decision:** The bonus causes a statistically significant lift of ~$42K in next-quarter revenue. The effect is largest for mid-tenure salespeople (3–7 years). The VP of Sales recommends preserving the bonus structure and testing a tiered bonus for those reaching 110% and 120%.

**Result:** Policy retained. A/B test of tiered bonus initiated in Q1 following year. RD result used as anchor in board presentation on compensation effectiveness.

**Anti-Example:** A junior analyst fits a 4th-degree polynomial across the full range of quota attainment (60% to 150%) and reports no discontinuity, concluding the bonus "has no effect." The finding is an artifact of overfitting — the polynomial absorbs the discontinuity into curvature. The correct approach is local linear regression within the bandwidth.

---

### Scenario 2: Enterprise Tier Upgrade and Feature Adoption

**Trigger:** A B2B product team wants to know whether automatically upgrading users to the Enterprise tier when their monthly active users (MAU) exceed 500 causes higher feature adoption, or whether larger teams naturally adopt more features regardless of tier.

**Analysis:**
- Running variable: peak MAU in the prior month (continuous, measured at account level)
- Cutoff: 500 MAU
- Treatment: automatic upgrade to Enterprise tier (unlocks SSO, advanced analytics, dedicated CSM)
- Outcome: 90-day feature adoption score (0–100 index)
- Bandwidth: IK-optimal = ±60 MAU
- Manipulation check: IT verifies that MAU count is server-side, not client-reported — low gaming risk. McCrary p = 0.58.
- Fuzzy RD required: 12% of accounts just above 500 MAU were manually held at Pro tier by sales for contractual reasons. First stage: probability of upgrade jumps from 0.11 to 0.87 at cutoff.
- Fuzzy RD estimate (2SLS): tau_fuzzy = +14.3 points on adoption score (SE = 3.1)

**Decision:** The Enterprise upgrade causes a meaningful lift in feature adoption. The CSM assignment (part of the Enterprise tier) is identified through qualitative interviews as the primary mechanism. Product team recommends lowering the MAU threshold to 350 to expand CSM coverage.

**Result:** Threshold lowered. Six-month follow-up shows adoption score improvements consistent with the RD estimate. Incremental CSM cost offset by expansion revenue from higher-adoption accounts.

**Anti-Example:** A product manager runs a simple comparison of feature adoption between Pro and Enterprise users across the full MAU range, finds a 25-point difference, and concludes the Enterprise tier "dramatically improves adoption." This confounds tier with account size — larger accounts that earned Enterprise status have more resources and incentive to adopt features regardless of tier. The naive estimate is nearly double the causal estimate.

---

### Scenario 3: AI Model Quality Gate and Deployment Velocity

**Trigger:** An AI platform team wants to evaluate whether enforcing a mandatory quality gate (models must achieve ≥0.85 F1 score on a holdout set to receive auto-deployment) improves post-deployment production accuracy, or whether it merely delays deployment for models that would have performed well anyway.

**Analysis:**
- Running variable: F1 score on validation holdout (continuous, 0–1 scale)
- Cutoff: 0.85 F1
- Treatment: auto-deployment vs. manual review queue (models below 0.85 enter a 2-week human review before deployment)
- Outcome: 30-day production accuracy (F1 on live traffic)
- Time period: 18 months of model deployment logs, N = 340 models
- Bandwidth: IK-optimal = ±0.04 F1 units (N = 87 models within window)
- McCrary test: p = 0.04 — marginal evidence of manipulation. Investigation reveals ML engineers were retraining models until they barely exceeded 0.85. Donut RD applied: exclude models within ±0.005 of cutoff.
- Donut RD estimate: tau = +0.032 F1 in production (SE = 0.009, p < 0.01)

**Decision:** The quality gate causes a 3.2 percentage point improvement in production accuracy for models near the 0.85 threshold. The finding is robust to the exclusion of potentially manipulated models. The AI Lead recommends retaining the gate and adding a secondary check at 0.90 for models deployed in customer-facing products.

**Result:** Gate retained. Tiered gate implemented: 0.85 for internal tools, 0.90 for customer-facing. Manipulation concern addressed by making the F1 score computation fully automated and opaque to engineers until after code freeze.

**Anti-Example:** The AI platform team observes that models that passed the gate have higher production accuracy on average and concludes "the gate works." This is selection bias — models that barely passed the gate are not compared to models that barely failed it; instead, high-scoring models (far above 0.85) are being compared to rejected models. The RD estimate is 3.2 points; the naive comparison inflates the estimate to 11 points by mixing in the easiest cases.

---

## Practitioner Playbook

**Step-by-step guide for applying RD in IT/AI/Product/Consulting contexts.**

1. **Identify the Policy Rule.** Confirm that treatment assignment is governed by a numeric threshold applied to a measurable running variable. Document the exact rule: who set it, when, and whether exceptions are granted. A rule that exists on paper but is overridden in practice requires Fuzzy RD or a different design.

2. **Obtain and Validate the Running Variable.** Extract the running variable from the authoritative system of record. Verify continuity: it must be a numeric scale without rounding artifacts that cluster units at round numbers near the cutoff (a common problem with manually entered scores). Check the distribution visually.

3. **Run the McCrary Density Test.** Before any outcome analysis, test whether the density of the running variable is smooth at the cutoff. Plot a histogram with narrow bins. Compute the McCrary (2008) test statistic. If p < 0.05, document the manipulation concern and decide whether to proceed with Donut RD, Fuzzy RD, or abandon the design.

4. **Define the Outcome and Measurement Window.** Specify the outcome variable and the time window over which it is measured post-treatment. Be precise: "30-day retention" and "90-day retention" can yield different estimates if the treatment effect fades. The measurement window should be pre-specified, not chosen after inspecting results.

5. **Select the Bandwidth.** Use the Imbens-Kalyanaraman algorithm (available in R's `rdrobust` package or Python's `rdd` library) to compute the optimal bandwidth. Record this value. You will use it as your primary specification and report results at 0.5x and 2x as robustness checks.

6. **Check Covariate Balance.** For each available pre-treatment covariate (tenure, segment, historical behavior), run the same RD specification with that covariate as the outcome. No covariate should show a significant discontinuity at the cutoff. Failure indicates a violation of the continuity assumption — document and investigate.

7. **Fit the Local Linear Model.** Estimate the RD using local linear regression (polynomial order = 1) with a triangular kernel within the optimal bandwidth. If using a software package, confirm defaults: `rdrobust` in R uses triangular kernel and IK bandwidth by default. Report the point estimate, standard error, confidence interval, and p-value.

8. **Determine Sharp vs. Fuzzy.** If treatment probability jumps from 0 to 1 at the cutoff, proceed with the Sharp estimate. If compliance is imperfect, implement 2SLS with the cutoff indicator as the instrument. Report the first-stage F-statistic to confirm instrument relevance (F > 10 minimum; F > 20 preferred).

9. **Run Placebo Tests.** Repeat the RD specification at two false cutoffs: one above and one below the true cutoff, at locations with sufficient data. You should find no statistically significant discontinuity. If you do, investigate whether there are additional threshold-based policies or non-linearities in the outcome function.

10. **Conduct Bandwidth Sensitivity Analysis.** Present results in a coefficient plot showing the estimated effect as the bandwidth varies from very narrow to very wide. A flat line indicates robustness. A rapidly changing estimate suggests the result is sensitive to bandwidth choice and should be interpreted with caution.

11. **Test for Heterogeneous Effects.** Stratify the analysis by key subgroups: customer segment, product line, geography, tenure band. The LATE at the cutoff may differ across groups, and these differences are often more actionable than the average estimate. Report subgroup estimates with appropriate multiple-testing corrections.

12. **Communicate the Local Nature of the Finding.** In all deliverables — slide decks, memos, dashboards — explicitly label the estimate as "effect for units near the cutoff" not "effect for all units." Provide a range of the running variable to which the finding applies. Pre-empt the extrapolation mistake by showing a visual of where the bandwidth sits in the overall distribution.

13. **Recommend Follow-on Research.** RD identifies whether the treatment works at the margin. Pair with qualitative interviews to understand the mechanism. Consider an RCT to estimate the ATE across the full population if the policy decision extends beyond the cutoff neighborhood.

14. **Archive the Analytical Decisions.** Document bandwidth selection rationale, polynomial order, kernel choice, and all robustness checks in an appendix. This is not optional in consulting or regulated environments — analytical transparency is part of the deliverable.

---

## Content Critique & Depth Gaps

### What the Source Material Covers Well
The source provides an intuitive setup for RD, identifies the key design variants (Sharp/Fuzzy), and offers concrete business use cases. The loan and sales bonus scenarios are accessible entry points.

### Critical Gaps for IIM/HBS MBA Depth

**1. No Treatment of Identification Assumptions Formally.**
The continuity assumption is named but not operationalized. A rigorous treatment would state: "E[Y(0) | X = x] and E[Y(1) | X = x] must both be continuous in x at the cutoff." Without this, practitioners cannot reason about what would need to be true for the estimate to be valid — or precisely what would invalidate it.

**2. Bandwidth as a Research Design Choice Is Absent.**
The source mentions bandwidth implicitly (units "just above and below") but does not address the methodological literature on bandwidth selection. The Imbens-Kalyanaraman (2012) optimal bandwidth selector and the Calonico-Cattaneo-Titiunik (CCT, 2014) bias-corrected estimator are the empirical standard. No practitioner-level audit is complete without them.

**3. Polynomial Order Debate Is Missing.**
The source implies that one simply fits regression lines on each side, but does not alert readers to the Gelman-Imbens (2019) critique of high-order polynomials — a widely cited and practically important warning that has changed default practice in the field.

**4. Geographic and Time-Based RD Are Not Discussed.**
Geographic RD (exploiting administrative boundaries as quasi-random cutoffs) and time-series RD (interrupted time series at a policy change date) are major extensions used extensively in policy consulting and product analysis. Their omission limits applicability.

**5. Multiple Cutoffs and Kink Designs Are Absent.**
Regression Kink Design (RKD), where the slope rather than the level of treatment changes at the cutoff, is increasingly used in IT contexts (e.g., tiered pricing structures). Multiple cutoffs (e.g., three support tiers) enable variance reduction through pooling. Neither is mentioned.

**6. Mechanism Identification Is Ignored.**
RD estimates the reduced-form effect of crossing the cutoff but cannot distinguish between different channels through which the treatment operates (e.g., whether a bonus works through motivation, retention of high performers, or signaling). The source does not discuss mediation analysis or qualitative follow-on as complements.

**7. The External Validity Problem Is Understated.**
The LATE limitation is mentioned once but not explored. The MBA curriculum should confront: Can we generalize from the margin to the mean? What assumptions are required? What happens if we move the cutoff? These are exactly the policy questions a consultant will face.

**8. Practical Power Analysis Is Missing.**
RD requires substantially more data than a comparably powered RCT. The source provides no guidance on whether an RD is feasible for a given dataset size — a critical pre-analysis consideration for product teams working with thin margins near threshold values.

**9. Software Implementation Is Not Referenced.**
Practitioners need to know: `rdrobust` (R and Stata), `rdd` (Python), and the suite of CCT diagnostic tools. Pointing students toward reproducible implementation reduces errors in applied work.

**10. Ethical Dimensions of Cutoff-Based Policies Are Not Raised.**
Cutoffs in credit, hiring, or product access have distributional consequences. Who is clustered just below the cutoff? Are these populations systematically disadvantaged? RD estimates the effect of the policy but not its fairness — an important dimension in regulated industries and responsible AI contexts.

---

## Quick-Recall Card

- **What it is:** A quasi-experimental method that uses a numeric threshold to create near-random treatment assignment for units close to the cutoff.
- **Core assumption:** Everything changes smoothly at the cutoff except the probability of receiving treatment (continuity assumption).
- **Sharp design:** Crossing the cutoff fully determines treatment. Estimate with local linear OLS.
- **Fuzzy design:** Crossing the cutoff increases (but does not guarantee) treatment probability. Estimate with 2SLS using the cutoff indicator as an instrument.
- **What you estimate:** LATE — the causal effect of treatment for units near the cutoff only. Not generalizable to units far from the threshold.
- **Running variable:** The score that determines treatment. Must be continuous. Must resist precise manipulation.
- **Bandwidth:** The estimation window around the cutoff. Too narrow = high variance. Too wide = high bias. Use IK-optimal selection and report sensitivity.
- **Polynomial order:** Use local linear (order = 1). Avoid cubic or higher — they produce spurious discontinuities.
- **McCrary test:** Check that density of the running variable is smooth at the cutoff. A spike = manipulation = invalid design.
- **Placebo tests:** Run at fake cutoffs. No significant discontinuity should appear.
- **Covariate balance:** Pre-treatment covariates should NOT jump at the cutoff.
- **Donut RD:** Exclude the narrow band around the cutoff to handle suspected (but not conclusive) manipulation.
- **Common mistakes:** Extrapolating LATE to full population; using high-order polynomials; ignoring bandwidth sensitivity; skipping manipulation tests; confusing naive comparison with causal estimate.
- **IT/AI applications:** Sales quota bonuses, product tier thresholds, credit scoring policies, AI model quality gates, enterprise upgrade triggers, support SLA cutoffs.
- **Pair with:** Difference-in-Differences when you have panel data; Instrumental Variables when the cutoff is an instrument in a larger structural model; qualitative interviews to identify mechanisms.

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "For units right at the margin of this threshold, does crossing it actually cause the outcome we care about — or would those units have achieved the same result anyway?"

---

## Self-Audit Report

<!-- Self-Audit:
SECTION COMPLETION CHECK:
[x] Section 1 — Jargon Buster: 10 terms provided (minimum 8 required). All defined with IT/AI/Product/Consulting lens. Table format correct.
[x] Section 2 — Frameworks & Mental Models: 4 frameworks with ASCII diagrams. Covers core RD logic, Sharp vs Fuzzy, Bandwidth tradeoff, and Manipulation threat map.
[x] Section 3 — Formulas, Thresholds & Rules of Thumb: 6 formulas/rules provided with context. Covers Sharp estimator, local linear spec, Fuzzy 2SLS, IK bandwidth, power rules, McCrary test, placebo test.
[x] Section 4 — Do / Don't: 10 DOs and 10 DONTs (minimum 8 each required). All grounded in IT/AI/product/consulting practice.
[x] Section 5 — Metric-Driven Scenarios with Anti-Examples: 3 scenarios completed. Each has Trigger, Analysis, Decision, Result, and Anti-Example. Scenarios cover sales bonus, B2B product tier, and AI model quality gate.
[x] Section 6 — Practitioner Playbook: 14 numbered steps. Covers full end-to-end workflow from policy identification to archiving decisions.
[x] Section 7 — Content Critique & Depth Gaps: 10 gaps identified. Covers identification assumptions, bandwidth, polynomial order, geographic/time RD, kink designs, mechanisms, external validity, power, software, and ethics.
[x] Section 8 — Quick-Recall Card: Bullet format. Ends with exact phrase starting "As a PM/Consultant/AI Lead, the one question to answer with this framework is:".
[x] Section 9 — Self-Audit Report: This HTML comment.

INDUSTRY LENS VERIFICATION:
- All scenarios use IT/SaaS/AI/consulting contexts (sales tech, B2B product, AI deployment)
- No generic economics examples used without IT translation
- Jargon buster entries explicitly reference IT/product contexts

QUALITY CHECKS:
- File substantially exceeds 13 KB target
- No section omitted
- Placebo tests, McCrary test, bandwidth sensitivity all covered
- Sharp vs Fuzzy distinction made explicit with formulas
- LATE limitation prominently flagged in multiple sections
- Role-lens question in Section 8 starts with exact phrase "As a PM/Consultant/AI Lead"

CONNECTS TO:
- 01-correlation-vs-causation.md (foundational causal reasoning)
- 02-potential-outcomes-framework.md (LATE, ATE, ATT definitions)
- 04-instrumental-variables.md (Fuzzy RD uses IV/2SLS logic)
- 05-difference-in-differences.md (alternative quasi-experimental design)
- 06-propensity-score-matching.md (alternative observational design)
- 08-natural-experiments.md (RD as a form of natural experiment)

Worker ID: A3
File: 07-regression-discontinuity-design.md
Date written: 2026-04-18
Model: claude-sonnet-4-6
-->

---

**Connects to:**
- `01-correlation-vs-causation.md` — foundational distinction between association and causation
- `02-potential-outcomes-framework.md` — defines LATE, ATE, ATT used throughout this file
- `04-instrumental-variables.md` — Fuzzy RD estimation relies on IV/2SLS logic
- `05-difference-in-differences.md` — alternative quasi-experimental design for panel data
- `06-propensity-score-matching.md` — alternative observational design when no threshold exists
- `08-natural-experiments.md` — RD is a canonical form of natural experiment
