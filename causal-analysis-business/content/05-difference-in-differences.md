# Difference-in-Differences

## Overview
Difference-in-differences is a method that estimates causal effects by comparing the change in outcomes over time between a group that received a treatment and a group that did not. It calculates the difference in the before-and-after change for the treated group minus the same change for the control group. This double differencing removes biases from both time-invariant group differences and common time trends. It is especially useful when randomization is not possible but a clear before-and-after comparison exists.

---

## Why It Matters
Many business interventions, such as policy changes, new store openings, or regulation shifts, cannot be randomly assigned. Difference-in-differences lets analysts estimate causal effects from observational data by leveraging the timing of these interventions. It is one of the most trusted and frequently used methods in applied economics and program evaluation.

## Key Principles
- The parallel trends assumption requires that the treatment and control groups would have followed the same trajectory in the absence of the intervention
- The first difference removes permanent differences between the groups that do not change over time
- The second difference removes time trends that affect both groups equally
- Violations of parallel trends, such as one group already diverging before the treatment, invalidate the causal estimate

## Key Terms
| Term | Definition |
|------|------------|
| **Parallel Trends Assumption** | The requirement that the treatment and control groups would have experienced the same change over time if the treatment had not occurred |
| **Treatment Group** | The set of units that experienced the intervention or policy change being studied |
| **Pre-Treatment Period** | The time frame before the intervention was implemented, used to establish baseline trends |
| **Post-Treatment Period** | The time frame after the intervention, during which outcomes are measured for comparison |

## Use Case
A restaurant chain introduces a new tipping policy in its California locations and uses its Texas locations as a control group, comparing the change in average tip amounts before and after the policy in both states.

## Scenario
> A city government raises the minimum wage in January. Economists want to know if this caused employment to drop. They compare employment changes in the affected city from the year before to the year after the increase, against a neighboring city where the minimum wage stayed the same. Both cities had been trending similarly before the change. The difference in employment change between the two cities provides an estimate of the minimum wage effect.

## Examples
- A tech company rolls out a new onboarding program in its European offices and uses its unchanged Asian offices as a control to measure the effect on 90-day retention
- A retailer launches a loyalty rewards program in select regions and compares the change in repeat purchase rates against regions without the program

---

## Audited Appendix

# Difference-in-Differences

Difference-in-differences (DiD) estimates causal effects by comparing the change in outcomes over time between a treated group and a control group. It uses double differencing to remove biases from time-invariant group differences and common time trends. DiD is one of the most widely deployed quasi-experimental methods in applied economics, product analytics, and policy evaluation because it requires weaker assumptions than pure randomization while still producing credible causal estimates.

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|------|--------------------------|----------------------------|
| **Parallel Trends Assumption** | The treated and control groups would have moved in the same direction by the same amount if the treatment had never occurred. | The entire validity of the DiD estimate rests on this assumption. If it breaks down — e.g., one region was already growing faster before the intervention — your causal estimate is contaminated. |
| **Treatment Group** | The units (users, regions, offices, cohorts) that actually received the intervention or policy change. | Misclassifying who is treated inflates or deflates the estimate. In SaaS rollouts, partial adoption within a "treated" office is a common contamination source. |
| **Control Group** | The comparison units that did not receive the intervention and act as a counterfactual for what would have happened to the treated group. | Control groups must be plausibly similar in trajectory, not just in level. Choosing a control group that is geographically or structurally too different from the treated group undermines validity. |
| **Pre-Treatment Period** | The time window before the intervention is applied, used to establish baseline trends for both groups. | Longer pre-periods allow you to test parallel trends empirically. A single pre-period data point is almost always insufficient for credible DiD. |
| **Post-Treatment Period** | The time window after the intervention, during which outcomes are measured to detect the treatment effect. | Short post-periods may miss delayed or compounding effects; overly long post-periods risk contamination from other contemporaneous changes. |
| **First Difference** | The change in outcome over time for a single group (post minus pre). | Removes time-invariant unobserved heterogeneity within a group — e.g., a city's permanently higher cost of living is differenced away. |
| **Second Difference** | Subtracting the control group's first difference from the treated group's first difference. | Removes common time trends — e.g., macroeconomic seasonality or industry-wide shifts that affect both groups equally. |
| **Counterfactual** | What would have happened to the treated group in the absence of treatment — unobservable but approximated by the control group's trajectory. | Every causal claim in DiD is ultimately a claim about a counterfactual. Making this explicit helps stakeholders understand what assumption is being made. |
| **Staggered Adoption DiD** | A DiD design where different units receive treatment at different calendar times rather than all at once. | Common in product rollouts (feature flags, phased launches). Requires more sophisticated estimators (Callaway-Sant'Anna, Sun-Abraham) to avoid negative weighting bias. |
| **SUTVA (Stable Unit Treatment Value Assumption)** | The assumption that one unit's treatment does not affect another unit's outcome, and that the treatment is well-defined and uniform. | Violated in network products (Slack, LinkedIn) where treating one user changes the experience of their connections. Requires cluster-level randomization or network DiD corrections. |
| **Parallel Trends Test (Event Study)** | A pre-period visual and statistical test showing that treated and control groups had statistically indistinguishable trends before the intervention. | The single most important robustness check. In consulting deliverables, a clean event-study plot with non-significant pre-period coefficients is the standard evidence that DiD is credible. |
| **Anticipation Effect** | Changes in behavior that occur before the treatment is formally applied, because treated units knew it was coming. | Common in policy settings (minimum wage announcements) and enterprise software deployments (pre-launch behavioral change). Causes the "pre-period" to be contaminated, biasing the estimate toward zero or in the wrong direction. |

---

## Frameworks & Mental Models

### 1. The 2x2 DiD Core Identity

The fundamental DiD estimator can always be visualized as a 2x2 table:

```
                  PRE-PERIOD          POST-PERIOD         FIRST DIFFERENCE
                 ─────────────       ─────────────        ────────────────
TREATED GROUP  │   Y_T_pre     │     Y_T_post     │    ΔY_T = Y_T_post - Y_T_pre
               ├───────────────┼──────────────────┼────────────────────────────
CONTROL GROUP  │   Y_C_pre     │     Y_C_post     │    ΔY_C = Y_C_post - Y_C_pre
               └───────────────┴──────────────────┴────────────────────────────

DiD Estimate (ATT) = ΔY_T − ΔY_C
                   = (Y_T_post − Y_T_pre) − (Y_C_post − Y_C_pre)
```

Mental model: Think of the control group's change as your "noise cancellation track." You subtract it from the treated group's change to isolate the signal attributable to the intervention.

---

### 2. The Parallel Trends Mental Model

```
OUTCOME (Y)
    │
    │                                    ╱  ← Actual Treated Path
    │                                  ╱
    │                    ┌───────────╱
    │                    │    DiD Estimate (ATT)
    │                    │           {gap}
    │          ╱─────────┼─────────────────── ← Counterfactual Treated Path
    │        ╱           │                        (= control group slope)
    │      ╱             │
    │────╱               │
    │  ╱ (parallel pre)  │
    │╱                   │
    └────────────────────┼──────────────────────────────► TIME
                    TREATMENT
                     EVENT
```

The counterfactual (dashed line) is constructed by assuming the treated group would have continued at the same slope as the control group. The vertical gap between actual and counterfactual at the post-period is the ATT (Average Treatment Effect on the Treated).

---

### 3. Event-Study Framework (Staggered or Multi-Period DiD)

```
COEFFICIENTS (β_t)
     │
 0.3 ┤                                    ●
     │                                  ╱   ╲
 0.2 ┤                            ●  ╱       ●
     │                          ╱
 0.1 ┤                      ●─╱
     │                    ╱
 0.0 ┤──●────●────●────●──────────────────────────────  ← Null line
     │   (pre-period coefficients: all near zero = parallel trends hold)
-0.1 ┤
     └──┬────┬────┬────┬────┬────┬────┬────┬────►
       t-4  t-3  t-2  t-1  t=0  t+1  t+2  t+3  t+4
                             ↑
                         TREATMENT
```

Pre-period coefficients (t-4 through t-1) should be statistically indistinguishable from zero. Post-period coefficients (t+1 onward) reveal the dynamic treatment effect trajectory — whether the effect grows, decays, or is immediate.

---

### 4. Threat Taxonomy Map

```
                     ┌────────────────────────────────────┐
                     │        DiD VALIDITY THREATS        │
                     └──────────────┬─────────────────────┘
                                    │
          ┌─────────────────────────┼──────────────────────┐
          ▼                         ▼                       ▼
  ┌───────────────┐       ┌─────────────────┐     ┌────────────────────┐
  │  Parallel     │       │   Interference  │     │  Measurement /     │
  │  Trends       │       │   & Spillovers  │     │  Data Issues       │
  │  Violations   │       │                 │     │                    │
  ├───────────────┤       ├─────────────────┤     ├────────────────────┤
  │• Pre-existing │       │• SUTVA violated │     │• Outcome def       │
  │  divergence   │       │• Network effects│     │  change over time  │
  │• Differential │       │• Geographic     │     │• Differential      │
  │  seasonality  │       │  spillovers     │     │  attrition         │
  │• Anticipation │       │• Cross-shopping │     │• Compositional     │
  │  effects      │       │  contamination  │     │  shifts            │
  └───────────────┘       └─────────────────┘     └────────────────────┘
```

---

## Formulas, Thresholds & Rules of Thumb

### Core DiD Estimator

```
DiD = (Ȳ_treated,post − Ȳ_treated,pre) − (Ȳ_control,post − Ȳ_control,pre)
```

**Context:** This is the average treatment effect on the treated (ATT). It is unbiased under parallel trends + SUTVA. Use sample means for experimental settings; use regression for observational data with covariates.

---

### Regression Form of DiD

```
Y_it = α + β₁·Treated_i + β₂·Post_t + β₃·(Treated_i × Post_t) + ε_it

Where:
  β₁ = fixed baseline difference between groups (absorbed)
  β₂ = common time trend (absorbed)
  β₃ = DiD ESTIMATE (the causal effect of interest)
```

**Context:** In practice, always cluster standard errors at the group level (e.g., by office, by region, by user cohort) to account for within-group serial correlation. Bertrand, Duflo & Mullainathan (2004) show that failure to cluster leads to severe under-rejection of the null.

---

### Parallel Trends Pre-Test Rule

```
|β_pre_k| ≈ 0  for all k = {-K, ..., -2, -1}
p-value of joint F-test on pre-period coefficients > 0.10
```

**Context:** No statistical test can prove parallel trends hold in the post-period, but pre-period coefficient magnitude and joint significance provide strong suggestive evidence. If any pre-period coefficient is statistically significant at p < 0.05, treat DiD results with high skepticism.

---

### Minimum Detectable Effect (MDE) Rule of Thumb

```
MDE ≈ 2.8 × σ / √(n × T)

Where:
  σ = standard deviation of outcome
  n = number of units per group
  T = number of time periods
```

**Context:** DiD gains statistical power from both cross-sectional units and time periods. Adding 4x more time periods is equivalent to 4x more units for power purposes. Short panel datasets are frequently underpowered — a common failure in startup analytics.

---

### Variance Inflation from Clustering

```
Var_clustered ≈ Var_OLS × (1 + ρ × (m − 1))

Where:
  ρ = within-cluster outcome correlation
  m = average cluster size
```

**Context:** High intra-cluster correlation (ρ > 0.1) with large clusters (m > 20) can inflate standard errors by 5–10x relative to naive OLS. This is why DiD studies with few treated clusters (< 20) require wild cluster bootstrap or permutation inference instead of standard clustered SEs.

---

### Rule of Thumb: Minimum Clusters

```
Minimum: 20 clusters per treatment arm for asymptotic cluster SE validity
Preferred: 50+ clusters per arm
With < 10 clusters: use Fisher exact / permutation tests
```

**Context:** Product analytics teams running DiD on 5 treated cities and 5 control cities are operating in a regime where standard errors are unreliable. This is one of the most common errors in consulting-style causal work.

---

## Do / Don't

### DO

1. **Empirically test parallel trends** using a multi-period event study before reporting DiD results. Plot pre-period coefficients with confidence intervals as a mandatory exhibit in any stakeholder deck.

2. **Cluster standard errors at the unit of treatment assignment** (e.g., if treatment is at the regional level, cluster at the region level, not at the individual user level).

3. **Use multiple control groups** to triangulate results. If DiD estimates are consistent across control groups with different characteristics, confidence in the estimate increases substantially.

4. **Define the outcome variable before looking at results.** Pre-committing to the primary outcome (e.g., 30-day retention, average order value) prevents p-hacking and outcome switching.

5. **Account for anticipation effects** by shifting your treatment date earlier if users or units knew about the upcoming change. Check behavioral data in the 30–90 days before launch for pre-treatment shifts.

6. **Use the Callaway-Sant'Anna or Sun-Abraham estimator** for staggered rollout DiD to avoid negative weighting bias from two-way fixed effects (TWFE) with heterogeneous treatment timing.

7. **Document sample composition** across pre and post periods. Differential attrition (e.g., churned users dropping from the treated panel) creates compositional bias that can mimic or mask real treatment effects.

8. **Report effect sizes in business-relevant units**, not just p-values. A statistically significant 0.2% lift in conversion is often economically meaningless; a non-significant 5% lift may be practically important and worth a larger sample.

9. **Conduct a placebo test** by applying the DiD design to an outcome that should not be affected by the treatment. If you find a significant effect on the placebo outcome, the design is likely picking up confounders.

10. **Communicate the counterfactual assumption explicitly** to business stakeholders. Say: "We are assuming that, without the loyalty program, repeat purchase rates in treated regions would have changed at the same rate as control regions."

---

### DON'T

1. **Don't use a single pre-period data point.** One pre-period observation cannot test parallel trends and provides no evidence that the assumption holds. Demand at minimum 3–5 pre-period observations.

2. **Don't choose the control group after seeing the data.** Selecting the control group that makes your treated group look best is specification searching and produces biased, non-replicable results.

3. **Don't ignore spillovers.** In product contexts with viral or network effects (referral programs, collaboration tools), treating one group and using nearby groups as control will contaminate the control, biasing estimates toward zero.

4. **Don't conflate statistical significance with business significance.** With large user populations (millions of users), even trivially small and unimportant effects will be statistically significant. Always compute and report effect size and confidence intervals.

5. **Don't apply TWFE DiD with heterogeneous treatment timing without checking for negative weights.** The standard two-way fixed effects estimator can produce negatively weighted averages when early-adopter groups are used as controls for late-adopter groups — a known and serious issue in panel DiD.

6. **Don't use DiD when treatment assignment is endogenous to the outcome trajectory.** If regions with declining sales were specifically chosen to receive the intervention (a common business mistake), parallel trends is almost certainly violated.

7. **Don't forget to check for compositional changes in your panel.** If the user population in the treated region changes (migration, targeting shifts, onboarding changes) between pre and post periods, you are not comparing the same units.

8. **Don't over-extend the post-period** to the point where other concurrent policies, competitor actions, or macroeconomic events contaminate the comparison. Document and assess concurrent changes in every DiD report.

9. **Don't suppress the event-study plot** in favor of reporting only the summary DiD coefficient. The plot contains diagnostic information stakeholders need to assess credibility.

10. **Don't use DiD when you have very few treated clusters.** With 3 treated offices and 3 control offices, inference based on clustered standard errors is unreliable. Use permutation/Fisher tests explicitly designed for small-cluster settings.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: AI-Powered Code Review Tool Rollout

**Trigger:** A mid-size software consultancy (8,000 engineers across 12 global offices) rolls out an AI code review assistant to its four European offices in Q1. Eight Asia-Pacific offices remain on the standard code review process. The product team wants to know whether the tool reduces bug escape rate (bugs found in production per 1,000 lines of code shipped).

**Analysis:**
- Pre-period: 6 quarters of bug escape rate data available for all 12 offices. Event study confirms parallel pre-trends (pre-period coefficients: β_{-5} = 0.02, β_{-4} = −0.01, β_{-3} = 0.03; all p > 0.40; joint F-test p = 0.61).
- DiD regression with office and quarter fixed effects, clustered SEs at office level.
- Treated group (EU): bug escape rate fell from 4.2 to 2.8 per 1,000 lines (ΔY_T = −1.4).
- Control group (APAC): bug escape rate fell from 4.1 to 3.6 per 1,000 lines (ΔY_C = −0.5; attributable to industry-wide shift toward TDD practices).
- DiD estimate: −1.4 − (−0.5) = −0.9 bugs per 1,000 lines. 95% CI: [−1.4, −0.4]. p = 0.003.

**Decision:** DiD estimate is statistically and economically significant. With 200 million lines shipped annually, this implies ~180,000 fewer production bugs per year. ROI calculation proceeds on this basis. Full rollout to APAC offices approved for Q3.

**Result:** Post-rollout tracking at 12 months confirms sustained reduction. APAC offices achieve −0.85 bugs per 1,000 lines after rollout, consistent with the DiD estimate, providing out-of-sample validation.

**Anti-Example:** The product team originally wanted to compare bug rates before and after rollout using only the EU offices — a simple pre-post comparison. During the DiD analysis, they discovered that a major industry-wide shift toward test-driven development had reduced bug rates globally by ~0.5 per 1,000 lines. The simple pre-post estimate (−1.4) would have over-attributed causal impact by 56%, leading to inflated ROI projections and potentially overpaying for the vendor license. DiD's second difference corrected for this.

---

### Scenario 2: Minimum Wage Policy and Gig Platform Worker Supply

**Trigger:** A gig economy platform (ride-sharing + delivery) operates in 30 US cities. Seattle raises its minimum wage for platform workers in March. The economics team wants to estimate the causal effect on active driver supply (drivers completing at least 1 trip per week).

**Analysis:**
- Pre-period: 8 months of weekly driver supply data across all 30 cities. Seattle is the sole treated city; 29 others serve as controls.
- Problem: Only 1 treated cluster (Seattle). Standard clustered SEs are unreliable. Team uses permutation inference: randomly reassign treatment to each of the 29 other cities 1,000 times, compute DiD estimate each time, form empirical null distribution.
- Seattle's DiD estimate: −12% in active weekly drivers. Permutation p-value: 0.04 (42 of 1,000 placebo cities showed effects of this magnitude or larger).
- Parallel trends: 8-month event study shows Seattle and controls tracking tightly pre-March (all pre-period estimates within ±2% of zero).
- Potential spillover: Portland drivers crossing into Seattle investigated; cross-market data shows minimal cross-border supply movement.

**Decision:** Evidence of statistically significant driver supply reduction at permutation p = 0.04. Magnitude (−12%) implies ~340 fewer active weekly drivers in Seattle — operationally significant for wait times. Platform escalates to regulatory engagement and considers dynamic surge pricing adjustments to offset reduced supply.

**Result:** Wait times in Seattle increase by 8% in the following quarter, consistent with a supply reduction of this magnitude given historical elasticity estimates. The causal estimate enables accurate operational planning rather than pure reaction.

**Anti-Example:** An earlier internal report used Seattle's own pre-post trend as the causal estimate, finding a −15% driver supply decline. However, this was the period when gig driver supply was declining nationally by approximately 4% due to a macroeconomic labor market tightening. The single-difference estimate over-stated the policy effect by 4 percentage points. Additionally, the report used individual-driver-level clustered standard errors (n = 12,000+), producing dramatically underestimated standard errors and spurious precision. DiD with permutation inference corrected both errors.

---

### Scenario 3: Onboarding Redesign and 90-Day Retention in SaaS Product

**Trigger:** A B2B SaaS company (project management software, 15,000 enterprise accounts) redesigns its onboarding flow for new accounts. Due to engineering capacity, the new onboarding is deployed only to accounts in its European data center (DC-EU) in January. Accounts in the North American data center (DC-NA) continue on the legacy onboarding. The growth team wants to estimate the causal effect on 90-day account retention.

**Analysis:**
- Pre-period: 6 monthly account cohorts before January for both DCs. Parallel trends test: European and North American 90-day retention cohorts track within ±1.5 percentage points across the 6 pre-periods; joint pre-period F-test p = 0.55.
- DiD estimate: DC-EU retention improved from 71% to 78% (ΔY_T = +7pp). DC-NA retention improved from 70% to 72% (ΔY_C = +2pp; attributable to a global customer success initiative launched in the same period).
- DiD = +7pp − +2pp = +5pp. Clustered SEs at account level. 95% CI: [+2.8pp, +7.2pp]. p = 0.001.
- Placebo test: the same DiD design applied to 30-day retention (should be less affected by late-stage onboarding changes) yields +0.8pp, p = 0.41 — consistent with the mechanism being mid-to-late onboarding.

**Decision:** +5pp improvement in 90-day retention is highly significant. At an average contract value of $24,000/year and a churn-retention revenue model, each percentage point of retention improvement is worth approximately $3.6M in annual recurring revenue. Full rollout to DC-NA accelerated to Q2.

**Result:** DC-NA 90-day retention rises by 4.8pp after rollout — within the confidence interval of the original DiD estimate, providing strong replication evidence.

**Anti-Example:** A product manager initially segmented the analysis by account size, computing separate DiD estimates for SMB, Mid-Market, and Enterprise tiers — without adjusting for multiple comparisons. The Enterprise segment showed +8pp (p = 0.03) while SMB showed +3pp (p = 0.22) and Mid-Market showed +5pp (p = 0.07). The PM reported the Enterprise finding as the headline result. With a Bonferroni correction for 3 comparisons, the Enterprise threshold becomes p < 0.017 — no segment would survive. The correct approach is to report the pooled DiD estimate as the primary result and pre-specified subgroup analyses as exploratory only.

---

## Practitioner Playbook

### Phase 0: Problem Framing (before any data work)

1. **Articulate the causal question in one sentence.** "Does intervention X cause outcome Y to change, and by how much?" If you cannot state this clearly, you are not ready to run DiD.

2. **Identify the unit of observation.** Is treatment assigned at the user level, account level, office level, or regional level? Treatment assignment unit = clustering unit for standard errors.

3. **Identify the natural experiment.** What makes treatment assignment as-if random? Document this explicitly. DiD requires that treatment and control groups are comparable in trajectory — not just in level.

4. **Pre-register the primary outcome, comparison groups, and analysis window** before accessing post-treatment data. Use an internal analysis plan document signed off by a senior stakeholder.

---

### Phase 1: Data Construction

5. **Assemble a balanced or near-balanced panel.** Verify that each unit appears in both pre and post periods. Document any attrition and test whether attrition rates differ between treated and control groups.

6. **Construct the treatment indicator (Treated_i)** as a time-invariant unit-level indicator (1 if the unit ever receives treatment, 0 otherwise).

7. **Construct the post-period indicator (Post_t)** as a time-varying indicator (1 after the treatment date, 0 before).

8. **Construct the interaction term (Treated_i × Post_t)** — this is the variable whose coefficient is your DiD estimate (β₃).

9. **Collect covariate data** for potential inclusion in the regression (unit size, pre-period baseline outcome, industry, geography). Covariates do not fix a broken parallel trends assumption but can improve precision.

---

### Phase 2: Parallel Trends Validation

10. **Run the event-study regression:**
    ```
    Y_it = α_i + γ_t + Σ_{k≠-1} β_k · (Treated_i × 1[t = k]) + ε_it
    ```
    Omit the period immediately before treatment (k = −1) as the reference category.

11. **Plot the event-study coefficients** with 95% confidence intervals. Pre-period coefficients (k < 0) must be near zero for parallel trends to hold.

12. **Conduct the joint F-test** on all pre-period β_k coefficients. If p < 0.10, flag a parallel trends concern and document it prominently. Consider alternative control groups.

13. **Test for anticipation effects** by examining behavioral data in the 60–90 days before treatment. If pre-period trends shift close to the announcement date, use the announcement date (not the implementation date) as t = 0.

---

### Phase 3: Estimation

14. **Estimate the baseline DiD** using OLS with unit and time fixed effects:
    ```
    Y_it = α_i + γ_t + β · (Treated_i × Post_t) + X_it'δ + ε_it
    ```

15. **Cluster standard errors at the unit of treatment assignment.** In most IT/product settings, this means clustering at the office, region, or account-segment level — not the individual user level.

16. **If fewer than 20 clusters,** use wild cluster bootstrap or permutation inference. Document which inference method was used and why.

17. **If treatment is staggered across time,** use the Callaway-Sant'Anna (2021) or Sun-Abraham (2021) estimator instead of TWFE. Check for negative weights using the Bacon decomposition if using TWFE.

---

### Phase 4: Robustness and Validation

18. **Run placebo outcome tests:** apply the DiD design to outcomes that should not respond to the treatment. A significant placebo estimate signals a confounded design.

19. **Run placebo group tests:** apply the treatment to groups that did not receive it and verify the estimate is near zero.

20. **Vary the control group:** repeat the analysis with alternative control group definitions. Consistent estimates across control group specifications increase confidence.

21. **Check for contamination/spillovers:** examine whether control units show behavioral changes that could be attributed to the treated units' intervention (e.g., customer cross-shopping, shared-infrastructure effects in cloud deployments).

---

### Phase 5: Reporting

22. **Lead with the event-study plot** as the primary credibility exhibit. Follow with the regression table as a secondary exhibit.

23. **Report effect size in business-relevant units** (revenue impact, retention percentage points, cost reduction in dollars) alongside the statistical estimate.

24. **State the counterfactual assumption explicitly** in the executive summary: "This estimate assumes [control group] represents what would have happened to [treated group] absent the intervention."

25. **Document limitations:** parallel trends reliance, potential spillovers, inference method for small samples, any concurrent events in the post-period.

26. **Recommend a follow-up validation study:** if the full rollout proceeds, collect post-rollout data from the newly treated group and compare against the original DiD estimate for replication.

---

## Content Critique & Depth Gaps

### What the Source Content Gets Right

The source content correctly identifies the core mechanism (double differencing removes group fixed effects and time trends), names the parallel trends assumption as the central identifying restriction, and provides sensible illustrative examples. The restaurant/minimum wage examples are pedagogically standard.

---

### Critical Gaps for IIM/HBS MBA Depth

**1. Heterogeneous Treatment Effects (HTE) are completely absent.**
The source treats DiD as if it produces a single homogeneous treatment effect. In practice — especially in product analytics — treatment effects vary substantially across user segments, geographies, and time. The Callaway-Sant'Anna estimator and group-time average treatment effects (ATT(g,t)) are essential for disaggregated causal analysis. Without HTE analysis, a product manager cannot answer "for which users does this feature work?" — arguably the most important downstream question.

**2. Staggered Adoption / Rollout is not addressed.**
Real product deployments are almost never simultaneous. Feature flags, phased regional launches, and cohort-based onboarding mean treatment is staggered. The source's silence on this is a significant gap because TWFE with staggered treatment and heterogeneous effects is now known (Goodman-Bacon 2021) to produce biased estimates. Any MBA-level practitioner using DiD in a product context must understand the Bacon decomposition and when to use alternative estimators.

**3. Inference for small clusters is not discussed.**
The source mentions no discussion of how to handle the extremely common real-world situation where there are very few treated clusters (e.g., 3 offices, 5 cities). Standard errors based on clustered OLS are unreliable with fewer than 20 clusters. Wild cluster bootstrap and permutation tests are the standard remedy — completely absent from the source.

**4. SUTVA and network/spillover effects are not addressed.**
In IT, SaaS, and AI product contexts, SUTVA is almost always under threat. Collaboration tools (Slack, Teams, GitHub Copilot) have explicit network effects between users. Treating some users in a team while leaving others as controls produces interference that contaminates the DiD estimate. The source contains no guidance on this.

**5. No discussion of the Bacon decomposition or negative weighting.**
The 2021 methodological revolution in DiD (Goodman-Bacon, Callaway-Sant'Anna, Sun-Abraham) is entirely absent. For consulting practitioners advising companies on A/B test design, product analytics, or policy evaluation, ignorance of negative weighting in TWFE is a liability.

**6. No power analysis framework.**
The source does not mention how to size a DiD study — critical for deciding whether to run the study at all, and for determining how many pre-period observations and control units are needed. This is a basic MBA-level analytical gap.

**7. Anticipation effects receive no treatment.**
In enterprise software and regulatory contexts, units often change behavior in anticipation of treatment. The source does not discuss how to detect, test, or correct for anticipation effects.

**8. No discussion of continuous treatment DiD.**
The binary treatment framing is appropriate for introductory coverage, but many policy questions involve continuous treatment intensity (e.g., hours of AI tool usage, amount of wage increase). Dose-response DiD and its identification challenges are absent.

**9. No integration with Regression Discontinuity or Instrumental Variables.**
At IIM/HBS level, students need to understand when DiD is the right tool versus an RD (when a threshold determines treatment) or IV (when there is an instrument for treatment). The source presents DiD in isolation.

**10. Practical data pipeline discussion is absent.**
How do you construct a balanced panel? How do you handle missing data? What do you do when your event date is ambiguous (e.g., a policy rolled out gradually over a quarter)? These practical considerations are critical for consulting engagements but entirely missing.

---

## Quick-Recall Card

- **Core idea:** Compare the change in outcomes over time for a treated group vs. a control group; the "difference in differences" removes permanent group gaps and common time trends.
- **The identifying assumption:** Parallel trends — treated and control groups would have followed the same trajectory without the intervention. This is an assumption, not a testable fact, but it can be supported with pre-period evidence.
- **The DiD estimate (ATT) = (Y_T,post − Y_T,pre) − (Y_C,post − Y_C,pre)**
- **The regression coefficient of interest:** β₃ on the interaction term (Treated × Post) in a unit and time fixed-effects regression.
- **Primary credibility check:** Event-study plot showing near-zero pre-period coefficients. No pre-period plot = no credibility.
- **Cluster SEs at the level of treatment assignment,** not at the individual level. With < 20 clusters, use wild cluster bootstrap or permutation inference.
- **For staggered rollouts:** TWFE is biased. Use Callaway-Sant'Anna or Sun-Abraham estimators.
- **Robustness trinity:** (1) Placebo outcome test, (2) Placebo group test, (3) Alternative control group test.
- **Top threats:** Parallel trends violation, spillovers/SUTVA violation, differential attrition, anticipation effects, negative weighting in staggered TWFE.
- **Business communication rule:** Always state the counterfactual assumption explicitly; always report effect size in business units (revenue, retention points, cost dollars) alongside p-values.
- **Power:** DiD gains power from both N (units) and T (time periods). If you have few units, extend the panel; if you have few time periods, increase unit sample size.
- **In IT/AI/Product contexts:** Be alert to network effects (SUTVA violations), phased rollouts (staggered DiD), and anticipation from internal launch communications.
- **The single most dangerous failure mode:** Choosing a control group after seeing the data, or selecting the post-period window that maximizes statistical significance.

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Can I credibly construct a counterfactual — a comparison group that shows what would have happened to my treated users/offices/regions without the intervention — and is the parallel trends assumption defensible given the pre-period data I have?"

---

## Self-Audit Report

<!-- Self-Audit:
SECTION COMPLETENESS:
1. Jargon Buster — COMPLETE. 12 terms provided (minimum 8). All terms defined with practical IT/AI/Product/Consulting relevance. Table format with three columns as specified.
2. Frameworks & Mental Models — COMPLETE. Four frameworks provided, each with ASCII diagrams: (1) 2x2 DiD identity table, (2) Parallel trends visual with counterfactual, (3) Event-study coefficient plot, (4) Threat taxonomy map.
3. Formulas, Thresholds & Rules of Thumb — COMPLETE. Six formulas/rules provided: core DiD estimator, regression form, parallel trends pre-test rule, MDE formula, variance inflation from clustering, minimum cluster rule of thumb. Each has contextual explanation.
4. Do / Don't — COMPLETE. 10 Do items and 10 Don't items provided (minimum 8 each). All grounded in IT/AI/Product/Consulting scenarios.
5. Metric-Driven Scenarios with Anti-Examples — COMPLETE. Three scenarios: (1) AI code review tool in global consulting firm, (2) Minimum wage and gig platform driver supply, (3) SaaS onboarding redesign. Each follows Trigger → Analysis → Decision → Result → Anti-Example structure.
6. Practitioner Playbook — COMPLETE. 26 numbered steps across 5 phases: Problem Framing, Data Construction, Parallel Trends Validation, Estimation, Reporting.
7. Content Critique & Depth Gaps — COMPLETE. 10 substantive gaps identified with IIM/HBS MBA depth framing: HTEs, staggered adoption, small-cluster inference, SUTVA, Bacon decomposition, power analysis, anticipation effects, continuous treatment, comparison with RD/IV, data pipeline.
8. Quick-Recall Card — COMPLETE. Bullet format. Final line starts with exact phrase "As a PM/Consultant/AI Lead" as required.
9. Self-Audit Report — PRESENT (this section).

INDUSTRY LENS CHECK: All scenarios, examples, and applications reference IT, AI/ML product, SaaS, consulting, or gig economy digital platforms. No purely traditional industry framing used without IT/product context.

CONNECTS TO: Related audit files in this course folder include causal inference fundamentals, regression discontinuity design, instrumental variables, synthetic control methods, and A/B testing frameworks.

ESTIMATED FILE SIZE: ~16-17 KB. Exceeds 13 KB minimum requirement.

ROLE-LENS QUESTION: Begins with exact phrase "As a PM/Consultant/AI Lead" — confirmed.

KNOWN LIMITATIONS: ASCII diagrams are simplified representations; actual event-study plots should be generated in R (using fixest or did packages) or Python (using linearmodels or did package). Formulas use simplified notation for readability; production implementations should reference Callaway & Sant'Anna (2021) and Sun & Abraham (2021) for staggered DiD.

AUDIT STATUS: PASS — all 9 sections present, all minimum requirements met, industry lens consistent throughout.
-->

---

**Connects to:**
- `01-correlation-vs-causation.md` — foundational distinction that motivates all quasi-experimental methods including DiD
- `02-randomized-controlled-trials.md` — DiD is the quasi-experimental analog to RCTs; parallel trends is the DiD substitute for random assignment
- `03-regression-discontinuity.md` — alternative quasi-experimental design when a threshold determines treatment; compare when to use RD vs DiD
- `04-instrumental-variables.md` — alternative identification strategy when parallel trends is implausible but a valid instrument exists
- `06-synthetic-control.md` — extension of DiD logic for settings with a single treated unit (e.g., one country, one city) using a weighted combination of controls
- `07-interrupted-time-series.md` — single-group alternative to DiD when no comparable control group is available; understand when this is and is not sufficient
- `08-ab-testing-product-analytics.md` — randomized DiD; when you have experimental control over treatment assignment, DiD logic applies within an A/B framework
