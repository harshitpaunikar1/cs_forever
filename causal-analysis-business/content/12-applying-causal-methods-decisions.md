# Applying Causal Methods to Business Decisions

## Overview
Applying causal methods to business decisions means selecting the right analytical approach for the specific question, data, and constraints a company faces, then translating the results into actionable strategy. No single method works for every situation, so practitioners must understand the strengths, limitations, and assumptions of each tool in the causal toolkit. The goal is to move organizations from making decisions based on gut instinct or simple correlations to making decisions grounded in rigorous causal evidence. This final topic ties together everything in the course.

---

## Why It Matters
The value of causal methods is realized only when they inform real decisions. A perfectly designed study that sits in a report and never changes strategy adds nothing to the business. Leaders need to know when to run an experiment, when to use quasi-experimental methods, and when the data simply cannot support a causal claim. Building organizational capability in causal reasoning creates a lasting competitive advantage.

## Key Principles
- Start by clearly defining the causal question before choosing a method; the question determines the design, not the other way around
- Consider feasibility constraints including budget, timeline, data availability, and ethical concerns when selecting a method
- Communicate findings in business language with clear action implications, not just statistical jargon
- Build a culture of causal thinking by training teams to ask what causes what rather than what correlates with what

## Key Terms
| Term | Definition |
|------|------------|
| **Causal Question** | A precisely stated inquiry about whether and how one factor produces a change in another |
| **Identification Strategy** | The logical argument and methodological approach used to isolate a causal effect from observational or experimental data |
| **Internal Validity** | The degree to which a study accurately estimates the causal effect for the population and context being studied |
| **External Validity** | The degree to which causal findings from one study can be generalized to other populations, settings, or time periods |

## Use Case
A chief strategy officer must decide how to evaluate whether the company's recent expansion into a new market caused the observed revenue increase, choosing between difference-in-differences, a synthetic control method, and a simple before-and-after comparison based on the available data.

## Scenario
> A fast-growing fintech company launches a referral bonus program and sees a 20 percent increase in new account openings. The CEO wants to know if the program caused the growth. The analytics team evaluates options: a pure experiment is impossible because the program is already live nationwide. They use a combination of difference-in-differences, comparing early-launch regions to later ones, and propensity score matching to account for regional differences. The team presents findings showing the program caused roughly 12 of the 20 percentage points of growth, with the remainder attributable to seasonal trends. The CEO uses this to justify expanding the bonus amount.

## Examples
- A retail chain uses A/B testing for website changes, difference-in-differences for store-level policy changes, and regression discontinuity for evaluating the effect of its loyalty program tier thresholds
- A consulting firm builds a decision tree for clients that maps each type of causal question to the most appropriate method given the client's data availability and operational constraints

---

## Audited Appendix

# Applying Causal Methods to Business Decisions

This topic ties together the full causal toolkit. Practitioners must select the right analytical approach for the specific question, data, and constraints a company faces, then translate results into actionable strategy. No single method works for every situation.

**Industry Lens:** IT / AI / Product / Consulting throughout.

**Connects to:**
- `01-correlation-vs-causation.md` — foundational distinction that motivates the entire causal toolkit
- `02-counterfactual-reasoning.md` — the logic underlying every causal estimate
- `05-randomized-controlled-trials.md` — gold-standard method; baseline for comparing observational methods
- `06-difference-in-differences.md` — workhorse method for natural experiments
- `07-regression-discontinuity-design.md` — sharp-threshold identification strategy
- `08-instrumental-variables.md` — addressing endogeneity without an experiment
- `09-propensity-score-matching.md` — balancing covariates in observational data
- `10-synthetic-control.md` — constructing counterfactual donor pools for single treated units
- `11-causal-graphs-dags.md` — graphical tool for encoding and testing causal assumptions

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| Causal Question | A question framed as "Does X cause Y?" rather than "Is X associated with Y?" | Without a precise causal question, analysts risk measuring the wrong thing and making misleading recommendations |
| Identification Strategy | The statistical approach — RCT, DiD, IV, RDD, etc. — used to isolate cause from confounding factors | Choosing the wrong strategy means estimates are biased, and business decisions built on them may destroy value |
| Internal Validity | The degree to which a study's findings correctly capture the causal effect within the study setting | A technically elegant model with poor internal validity gives executives a false sense of certainty |
| External Validity | The degree to which findings generalize to other populations, geographies, or time periods | A finding that is internally valid for Mumbai may not hold for Bengaluru; scaling assumptions need scrutiny |
| Estimand | The precise quantity you are trying to estimate (e.g., Average Treatment Effect, ATT, LATE) | Confusion between estimands is the single most common source of disagreement between data science teams and business stakeholders |
| Counterfactual | What would have happened to the treated unit had it never received the treatment | Every causal claim implicitly compares an observed world to a counterfactual; making this explicit forces clearer thinking |
| Parallel Trends Assumption | The assumption in DiD that treated and control groups would have followed the same trajectory absent treatment | Violating this — e.g., treated group was already on a different growth path — invalidates DiD conclusions |
| Positivity | Every unit in the study population must have a nonzero probability of receiving either treatment or control | Without positivity, comparisons involve extrapolation, not matching; estimates become unreliable |
| SUTVA (Stable Unit Treatment Value Assumption) | The treatment of one unit does not affect the outcomes of other units | Referral programs violate SUTVA: your bonus influences whether your friend signs up, creating spillovers |
| Propensity Score | Predicted probability of receiving treatment given observed covariates | Collapsing all confounders into a single scalar makes matching feasible, but unmeasured confounders remain a threat |
| Sensitivity Analysis | Testing how much an unmeasured confounder would have to differ to overturn the causal conclusion | Required in any consulting deliverable; tells the client how fragile the finding is |
| Effect Heterogeneity | The causal effect of X on Y varies across subgroups (regions, personas, product tiers) | Average effects can be misleading; product managers must segment to find where interventions actually work |

---

## Frameworks & Mental Models

### Framework 1 — The Causal Method Selection Tree

Use this mental model before any analysis. Work top-down to identify the highest-validity feasible method given your constraints.

```
                    CAN YOU RANDOMIZE?
                   /                  \
                 YES                   NO
                  |                    |
            RUN AN RCT          IS THERE A NATURAL EXPERIMENT?
         (gold standard)        /                            \
                              YES                             NO
                               |                              |
               IS THERE A SHARP         IS THERE A        USE OBSERVATIONAL
               THRESHOLD?          PLAUSIBLY EXOGENOUS    METHODS (PSM,
               /        \           INSTRUMENT?           DiD w/ parallel
             YES          NO        /          \          trends, Synth)
              |            |      YES            NO            |
            RDD           DiD    IV         WEAKER:       DOCUMENT
                                        REGRESSION-ONLY   ASSUMPTIONS
                                        + SENSITIVITY     CAREFULLY
                                          ANALYSIS
```

### Framework 2 — The Causal Credibility Ladder

Each rung represents increasing credibility of the causal claim. Consulting deliverables must state which rung the analysis occupies.

```
  RUNG 5  |  RCT (randomized; gold standard)
           |
  RUNG 4  |  Quasi-experiment with strong identification
           |  (RDD, strong IV, sharp natural experiment)
           |
  RUNG 3  |  DiD with credible parallel trends
           |  or synthetic control
           |
  RUNG 2  |  Regression with rich controls
           |  + sensitivity analysis
           |
  RUNG 1  |  Observational correlation only
           |  (descriptive; cannot support causal claims)
  ─────────────────────────────────────────────────────
          Low credibility ──────────────────► High credibility
```

### Framework 3 — The Causal Business Translation Matrix

Bridges the gap between statistical outputs and boardroom language.

```
  ┌─────────────────────┬──────────────────────┬────────────────────────────┐
  │  Statistical Output │  What It Means       │  Executive Translation      │
  ├─────────────────────┼──────────────────────┼────────────────────────────┤
  │  ATT = +12 pp       │  Treated units gained│  "The program drove 12 of  │
  │                     │  12 pp on average    │   our 20 pp growth"        │
  ├─────────────────────┼──────────────────────┼────────────────────────────┤
  │  CI: [8 pp, 16 pp]  │  95% confidence band │  "Realistically, program   │
  │                     │                      │   drove 8–16 pp; plan for  │
  │                     │                      │   the conservative end"    │
  ├─────────────────────┼──────────────────────┼────────────────────────────┤
  │  p-value < 0.01     │  Very unlikely by    │  "We are highly confident  │
  │                     │  chance alone        │   this is a real effect,   │
  │                     │                      │   not noise"               │
  ├─────────────────────┼──────────────────────┼────────────────────────────┤
  │  Effect heterogene- │  Effect differs      │  "Scale in Tier-1 cities   │
  │  ity across regions │  by subgroup         │   first; ROI is 3x higher" │
  └─────────────────────┴──────────────────────┴────────────────────────────┘
```

### Framework 4 — The Assumption Audit Checklist (before publishing findings)

```
  ┌──────────────────────────────────────────────────────────────┐
  │                  ASSUMPTION AUDIT                            │
  ├──────────────────────────────────────────────────────────────┤
  │  Method-specific assumptions:                                │
  │  [ ] Parallel trends (DiD)                                   │
  │  [ ] Continuity at threshold (RDD)                           │
  │  [ ] Instrument relevance + exclusion (IV)                   │
  │  [ ] Common support / overlap (PSM)                          │
  │  [ ] Donor pool validity (Synthetic Control)                 │
  │                                                              │
  │  Cross-method assumptions:                                   │
  │  [ ] SUTVA holds (no spillovers)                             │
  │  [ ] Positivity holds                                        │
  │  [ ] No anticipation effects                                 │
  │  [ ] Estimand matches the business question                  │
  │  [ ] Sensitivity analysis completed                          │
  └──────────────────────────────────────────────────────────────┘
```

---

## Formulas, Thresholds & Rules of Thumb

### 1. DiD Estimator

```
DiD = (Y_treated_post - Y_treated_pre) - (Y_control_post - Y_control_pre)
```

**Context:** Removes time-invariant confounders and common time trends. Valid only if parallel trends holds pre-treatment. In IT/consulting, run at least 4–6 pre-treatment periods of trend data to visually inspect and statistically test the assumption.

### 2. Propensity Score Matching — Caliper Rule of Thumb

```
Max caliper width = 0.2 × SD(logit(propensity score))
```

**Context:** Industry standard (Austin, 2011). Smaller caliper = better balance, but more unmatched units. In high-dimensional product analytics, report % of treated units lost to caliper; if > 20%, reconsider the estimand (restrict to common support explicitly).

### 3. Minimum Detectable Effect (MDE) for Experiments

```
MDE = (Z_alpha/2 + Z_beta) × sqrt(2 × p(1-p) / n)
```

Where p = baseline conversion rate, n = sample size per arm.

**Context:** Before any A/B test in product management, compute the MDE. If the MDE is larger than the smallest effect the business would act on, the experiment is underpowered and will be inconclusive by design. Rule of thumb: for conversion rate experiments in SaaS, plan for 80% power, 5% significance, and 2-week minimum runtime to account for weekly seasonality.

### 4. Synthetic Control — Fit Quality Rule of Thumb

```
Pre-treatment RMSPE = sqrt( mean( (Y_treated - Y_synthetic)^2 ) ) across pre-periods
```

**Context:** If RMSPE is large relative to the scale of Y, the synthetic control is a poor fit and results are unreliable. Rule of thumb: RMSPE / mean(Y_treated_pre) < 5% is acceptable. In IT market entry studies, this threshold determines whether the donor pool needs restructuring.

### 5. Rosenbaum Sensitivity Parameter (Gamma)

```
If Gamma = 2: a hidden confounder that doubles odds of treatment would overturn the finding
```

**Context:** Report Gamma in every PSM-based consulting study. Gamma > 1.5 is generally considered robust for business decisions; Gamma < 1.25 should trigger explicit caveats and requests for additional data before a go/no-go decision.

### 6. First-Stage F-Statistic (IV Relevance)

```
F > 10 (Stock-Yogo rule) for a valid instrument
```

**Context:** Weak instruments (F < 10) produce severely biased IV estimates, often worse than OLS. In fintech and AI platform analytics, natural instruments are rare; treat any instrument with F between 10 and 15 as borderline and report Nagar bias as a robustness check.

### 7. Effect Size Classification (Cohen's d)

```
Small: d = 0.2 | Medium: d = 0.5 | Large: d = 0.8
```

**Context:** Statistical significance is insufficient for business decisions. A statistically significant but small effect (d < 0.2) may not justify the cost of scaling a program. Always pair p-values with effect sizes in executive presentations.

---

## Do / Don't

### Do

1. **Define the causal question precisely before opening a data file.** Write it in one sentence: "Does [intervention X] cause [outcome Y] for [population Z] within [time window T]?" Ambiguity at this stage compounds into analytical chaos.
2. **Match the method to the identification opportunity, not to your comfort zone.** If a sharp threshold exists, use RDD even if you are more familiar with regression. Choosing a suboptimal method because it is easier to explain is a professional risk.
3. **Check and report all key assumptions explicitly.** Parallel trends, SUTVA, positivity, instrument exclusion — each deserves its own subsection in a consulting deck, not a footnote.
4. **Run pre-treatment trend tests before committing to DiD.** Plot treated and control group outcomes for at least six periods before treatment. Use an event-study specification to visualize leads and lags.
5. **Report effect heterogeneity, not just the average treatment effect.** Product decisions are almost always targeted at subgroups. A 5% average effect that is 18% in the high-intent segment and 0% elsewhere is a very different business signal.
6. **Conduct sensitivity analyses and report them to stakeholders.** Rosenbaum bounds for PSM, placebo tests for DiD, RMSPE ratios for synthetic control — these are not academic extras; they are fiduciary requirements in consulting.
7. **Translate statistical findings into business language before the executive presentation.** Coefficients and p-values belong in an appendix. Slide one should say "the referral program caused 12 of our 20 pp growth."
8. **Document the estimand clearly.** Are you estimating ATE, ATT, or LATE? The answer changes what the result means and whether it supports the proposed decision.
9. **Iterate between causal question and method.** If the best available method for your question requires data you cannot get, reframe the question or acknowledge the limitation explicitly rather than forcing a weak analysis.
10. **Build causal review into the analytics team's workflow.** Quarterly causal reviews — "what causal questions did we answer this quarter?" — shift culture from correlation-reporting to decision-relevant analysis.

### Don't

1. **Don't confuse statistical significance with business significance.** A p-value of 0.001 on a 0.1% lift in conversion does not justify a $2M campaign budget. Always pair significance with effect magnitude.
2. **Don't apply DiD without testing parallel trends.** Assuming parallel trends because it is convenient produces estimates with unknown bias. The visual pre-trend test takes 30 minutes; skip it only if you are willing to own the consequent error.
3. **Don't use propensity score matching without checking common support.** If 30% of treated units have no comparable control, your ATT estimate is extrapolating into regions with no empirical support.
4. **Don't report an IV estimate without the first-stage F-statistic.** A weak instrument produces results that look precise but are badly biased. In AI product analytics, weak instruments are endemic; always report F.
5. **Don't cherry-pick the method that gives the result leadership wants.** This is p-hacking with extra steps. The identification strategy must be chosen before analysis, documented, and defended.
6. **Don't ignore SUTVA when evaluating network products.** Referral programs, viral features, and marketplace dynamics all create spillovers. Ignoring them understates the true treatment effect.
7. **Don't generalize a lab-style RCT result to a full market rollout without an external validity discussion.** Opt-in A/B test participants in a fintech app are not representative of the general population of potential customers.
8. **Don't treat the absence of a statistically significant result as proof of no effect.** An underpowered study cannot confirm the null. Distinguish "we found no effect" from "we could not detect an effect."
9. **Don't skip the sensitivity analysis because the client is in a hurry.** If your finding reverses under mild confounding, the strategy built on it may fail publicly. A five-slide Rosenbaum analysis is better than a headline retraction six months later.
10. **Don't present a causal claim without stating explicitly which assumption could break it.** Every causal result has a weakest link. Naming it builds credibility; hiding it destroys it when the assumption is eventually questioned.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1 — SaaS Platform: Attribution of a Feature Launch

**Trigger:** A B2B SaaS company launches a collaborative editing feature. Within 60 days, average session duration increases by 35% and 30-day retention improves by 8 pp. The VP of Product wants to know whether the feature caused these improvements before deciding whether to allocate a $4M engineering budget to expand it.

**Analysis:** The feature was rolled out in two waves: enterprise customers in month 1, SMB customers in month 2. This phased rollout creates a natural DiD opportunity. The analytics team uses enterprise as the treatment group and SMB as the control group, with five months of pre-rollout data to verify parallel trends. An event-study specification shows no pre-trends. DiD estimate: feature caused +6.2 pp of the 8 pp retention improvement (95% CI: 4.1–8.3 pp). The remaining ~1.8 pp is attributable to a concurrent improvement in onboarding emails confirmed by a separate RCT. Session duration DiD estimate: +22 pp of the 35 pp increase; remainder explained by a seasonal product-use spike around fiscal year-end.

**Decision:** VP of Product approves a phased $2M expansion of the collaborative editing feature, targeted first at enterprise segments where the retention effect is +9.1 pp (vs. +4.3 pp for SMB). Budget is staged: $1M immediately, $1M contingent on 90-day re-measurement confirming ATT > 4 pp for new enterprise cohorts.

**Result:** At 90-day re-measurement, ATT = 5.7 pp for new enterprise cohorts. Full $2M budget unlocked. Feature becomes anchor of the enterprise tier product roadmap.

**Anti-Example:** The product manager initially presented the 8 pp raw improvement as "proof" the feature worked and requested the full $4M. Had the VP approved without causal analysis, $4M would have been invested in a feature that explained only 6.2 pp of the effect — and the remaining $2M would have been misallocated to a feature rather than to the onboarding email improvements that were actually delivering the balance of the lift.

---

### Scenario 2 — Fintech: Referral Bonus Program Evaluation

**Trigger:** A fintech company launches a referral bonus program nationwide. Within three months, new account openings increase by 20% compared to the same period last year. The CEO wants to confirm the program caused the growth before doubling the bonus amount.

**Analysis:** Because the program is already live nationwide, a traditional RCT is impossible. However, regional launch timing varied: eight states launched in week 1 (early-treated), fourteen states launched in week 6 (late-treated, serving as control for the early window). This creates a staggered DiD design. Parallel trends are checked for the pre-program period and hold across all 22 states. Propensity score matching is applied to account for regional differences in urban density, average income, and baseline fintech adoption. Two-stage analysis: (1) DiD estimates the causal effect of early vs. late launch; (2) PSM reweights the comparison to adjust for region-level confounders. Combined finding: program caused approximately 12 pp of the 20 pp growth. The remaining 8 pp decomposes as 5 pp seasonal trend (tax-refund-driven account openings historically spike in this quarter) and 3 pp attributable to a concurrent TV advertising campaign identified via media mix modeling.

**Decision:** CEO approves a 50% increase in bonus amount for a pilot in four test states, with a 60-day window to measure the marginal causal effect of the higher bonus using the remaining states as control. Decision to go nationwide with the higher bonus is gated on the pilot DiD estimate exceeding 3 pp incremental lift at 95% confidence.

**Result:** Pilot DiD estimate = 4.1 pp incremental lift from bonus increase. CEO approves nationwide expansion. The decision framework — causal estimate first, then staged scale — prevents the company from overspending on a bonus level that delivers diminishing returns.

**Anti-Example:** Had the CEO simply compared the 20% year-over-year growth to a 12% growth rate from two years prior and attributed the entire 8 pp difference to the program, the bonus increase would have been calibrated to capture a 20 pp causal effect. In reality, the program only explains 12 pp. Investing to drive 20 pp through bonus spending alone would require a bonus amount that is not cost-recoverable given average customer lifetime value.

---

### Scenario 3 — AI Consulting: Model Deployment ROI Attribution

**Trigger:** A management consulting firm deploys an AI-driven demand forecasting model for a retail client. The client observes a 14% reduction in inventory holding costs over the subsequent two quarters. The client's CFO wants causal evidence before committing to a three-year contract renewal at a higher price point.

**Analysis:** The firm identifies that the model was rolled out across 40 of 120 store clusters in the first quarter (treated), with the remaining 80 clusters scheduled for rollout in quarter 2 (control). This phased deployment enables a DiD analysis. However, treated and control clusters differ on a key variable: treated clusters were selected by store managers who volunteered, introducing selection bias. The team applies PSM using cluster-level covariates (store size, historical inventory turnover, product category mix, regional demand volatility) to create a matched control group. Post-matching balance is confirmed (standardized mean differences < 0.1 on all covariates). DiD on the matched sample: AI model caused a 9.2% reduction in holding costs (95% CI: 7.1–11.3%). The remaining 4.8% decomposed as: 3.1% from a supplier-negotiated lead time reduction implemented simultaneously, and 1.7% from seasonally lower demand reducing average inventory levels.

**Decision:** Consulting firm presents the 9.2% causal figure (not the raw 14%) in the contract negotiation. The ROI model built on 9.2% is conservative but defensible. The firm proposes contract pricing tied to a minimum guaranteed holding cost reduction of 7%, with upside sharing if effect exceeds 11%. The client, reassured by the rigor, signs the three-year contract.

**Anti-Example:** A junior team on a competing bid presented the raw 14% reduction as the model's causal impact. The competing client signed a contract priced on a 14% expected improvement. At the 12-month audit, actual causal improvement was 8.7%. The client disputed the ROI claim, the consulting relationship deteriorated, and the contract was not renewed — a direct commercial consequence of conflating observed improvement with causal attribution.

---

## Practitioner Playbook

**Context:** You are a product manager, strategy consultant, or AI lead who has been asked to evaluate whether an intervention caused a business outcome. This playbook applies whether you are preparing a DiD analysis, reviewing a vendor's causal claim, or building the analytics culture in your organization.

1. **Write the causal question in one sentence.** Format: "Does [X] cause [Y] for [population Z] in [context C]?" Pin this sentence to the top of your analysis document. Every subsequent decision is evaluated against this sentence.

2. **Identify the estimand.** Are you interested in the Average Treatment Effect (ATE: effect averaged across all units), the Average Treatment Effect on the Treated (ATT: effect on units that actually received treatment), or the Local Average Treatment Effect (LATE: effect on compliers in an IV setting)? The business question usually determines the estimand; document it explicitly.

3. **Audit data availability before choosing a method.** Answer four questions: (a) Do I have pre- and post-treatment outcome data for treated and control units? (b) Is there a sharp threshold around which treatment assignment varies discontinuously? (c) Is there a plausible instrument — a variable that affects treatment but has no direct effect on the outcome? (d) Can I construct a credible donor pool for a synthetic control? The answers narrow the feasible method set.

4. **Select the highest-credibility feasible method.** Use the Causal Method Selection Tree (Framework 1). If multiple methods are feasible, run all of them as robustness checks. Agreement across methods strengthens the finding; disagreement is itself informative and must be explained.

5. **Document and test all key assumptions before running the primary analysis.** For DiD: plot pre-treatment trends for treated and control groups; run a formal parallel trends test using lagged treatment indicators. For RDD: test for density manipulation at the threshold (McCrary test); check for covariate jumps at the threshold. For IV: run the first stage and report the F-statistic; articulate the exclusion restriction in plain language and invite challenge. For PSM: check common support; report balance statistics before and after matching.

6. **Run the primary analysis with full specification.** Report point estimates, confidence intervals, and p-values. Do not report only the p-value.

7. **Conduct placebo and robustness tests.** For DiD: run a placebo treatment in a pre-treatment period and confirm no spurious effect. For RDD: vary the bandwidth; results should be stable. For IV: use alternative instruments if available. For PSM: vary the caliper; vary the matching algorithm (nearest neighbor vs. kernel). Document which robustness checks pass and which raise concerns.

8. **Quantify sensitivity to unmeasured confounding.** For PSM-based designs, compute Rosenbaum's Gamma. For all designs, articulate the magnitude and direction of bias that a plausible unmeasured confounder would introduce. Present this as "our finding holds unless there exists an unmeasured variable that [specific magnitude and direction]."

9. **Decompose the observed change.** If the raw observed change is 20 pp and the causal estimate is 12 pp, account for the remaining 8 pp. Decomposition builds credibility and avoids overclaiming. Identify alternative explanations — seasonality, concurrent initiatives, macro trends — and quantify their contribution where possible.

10. **Translate to business language.** Build a one-page "Causal Finding Summary" with: (a) the causal question, (b) the method used and its key assumption, (c) the causal estimate with confidence interval, (d) the decomposition of the full observed change, (e) the decision implication, (f) the conditions under which the finding would reverse.

11. **Specify the decision gate.** Every causal finding should map to a specific decision: go/no-go, scale/don't scale, invest/divest. Define the threshold: "We will proceed with full rollout if the causal estimate exceeds [X] at [Y]% confidence." Precommitting to decision thresholds prevents post-hoc rationalization.

12. **Design the follow-on measurement.** If a scale decision is made, design the measurement plan for the scaled intervention before launch. Specify: the outcome metric, the comparison group, the time window, the minimum detectable effect, and the team responsible for analysis. Causal learning compounds only if measurement is continuous.

13. **Present findings with an explicit statement of limitations.** The strongest consultants are the ones who name the assumptions that could break the finding. A one-paragraph "caveats and limitations" section in the deck signals rigor and preempts the client from discovering the gaps on their own.

14. **Build the causal question into ongoing strategy reviews.** Institutionalize: every major strategic initiative proposed at the quarterly business review must include a causal evaluation plan. Over 12 months, this shifts the organization from a correlation-reporting culture to a causal-learning culture.

---

## Content Critique & Depth Gaps

This section identifies what the source material covers adequately, where it is thin, and what additional content is required to reach IIM/HBS MBA depth.

### What the Source Covers Well

- Correct framing: start with the causal question before choosing the method
- Practical recognition that experiments are not always feasible
- Multi-method triangulation (DiD + PSM in the fintech scenario)
- Decomposition of observed change into causal vs. non-causal components
- Translation imperative: communicate in business language

### Critical Gaps for MBA Depth

**1. Dynamic Treatment Effects and Staggered DiD**
The source mentions DiD but does not address the growing literature on staggered rollouts. In modern product analytics, nearly every launch is phased. The Callaway-Sant'Anna (2021) and Sun-Abraham (2021) estimators correct for contamination bias in two-way fixed effects DiD with staggered timing. Any practitioner using standard TWFE DiD on a phased rollout may be getting a weighted average of treatment effects that includes negative weights — a known bias source omitted from the source.

**2. Mediation Analysis**
The source does not address mediation — understanding *how* X causes Y through intermediate mechanisms. For product decisions (e.g., does the referral program cause retention through social proof or through financial incentive?), mediation analysis is critical. The Natural Direct Effect and Natural Indirect Effect decomposition from Pearl's framework is absent.

**3. External Validity and Generalization Frameworks**
The source mentions external validity as a key term but does not provide a framework for assessing it. The Shadish-Cook-Campbell framework for threats to external validity, or Deaton-Cartwright's critique of RCTs, should be included for MBA depth.

**4. Costs of Causal Inference Errors**
The source does not address the asymmetric costs of Type I (false positive: scaling a program that does not work) vs. Type II (false negative: not scaling a program that does work) causal errors. In high-stakes IT or consulting decisions, the cost calculus determines the appropriate significance threshold and power level — a point with direct decision relevance.

**5. Interference and Network Effects**
SUTVA is listed as a jargon term but its violation in network-platform contexts is not analyzed. Cluster-randomized experiments, graph-based experiment designs, and the Horvitz-Thompson estimator for interference should be introduced for AI/product teams operating on network platforms (LinkedIn, Slack, GitHub Copilot).

**6. Pre-Analysis Plans (PAPs)**
The source does not mention pre-analysis plans — the practice of registering the analysis methodology, primary outcome, and sample size before data collection. PAPs are increasingly required by serious analytics organizations to prevent p-hacking and HARKing (Hypothesizing After Results are Known). This is a major credibility tool absent from the source.

**7. Bayesian vs. Frequentist Causal Inference**
For AI product teams at companies like Google, Meta, or Indian tech unicorns running thousands of experiments simultaneously, Bayesian approaches to experimental analysis (e.g., Thompson sampling, Bayesian A/B testing) offer continuous monitoring without inflating Type I error. The source is exclusively frequentist.

**8. Cost-Benefit Analysis Integration**
The source stops at "causal estimate." MBA-level analysis requires integrating the causal estimate into a net present value or ROI model. A 12 pp causal lift on new account openings is strategically meaningless until it is converted into: (a) revenue per account, (b) cost of the bonus per account, (c) marginal customer lifetime value, (d) comparison to alternative uses of the same marketing budget. This integration is absent.

---

## Quick-Recall Card

**Core Idea**
- Every major business decision rests on an implicit causal claim; the only question is whether that claim is rigorous or accidental
- Method selection is a function of: causal question, data availability, feasibility constraints, and desired credibility level

**Method Summary**
- RCT: feasible and randomization is ethical — gold standard; do it
- DiD: phased rollout or natural comparison group — check parallel trends first
- RDD: sharp eligibility threshold exists — run McCrary test, vary bandwidth
- IV: instrument available with strong first stage (F > 10) and defensible exclusion restriction
- PSM: rich covariate data, no method-specific opportunity — check common support, report Rosenbaum Gamma
- Synthetic Control: single treated unit (a country, a market) with many potential donors

**Red Flags**
- Raw before-and-after comparison presented as causal evidence
- DiD without parallel trends test
- PSM without common support check
- IV with F-statistic below 10
- Effect size not reported alongside p-value
- No sensitivity or placebo analysis
- Causal claim that ignores SUTVA in a network context

**Translation Rules**
- ATT estimate + CI goes to slide 1; statistical output goes to appendix
- Decompose: causal effect + alternative explanations = total observed change
- Define the decision gate before seeing results, not after

**Culture Levers**
- Require a causal evaluation plan for every major initiative at the strategy review
- Pre-analysis plans prevent p-hacking
- Causal credibility ladder helps stakeholders understand what "confident" actually means

**Connecting Threads**
- Correlation vs. causation: foundational framing
- Counterfactual: the logic behind every causal estimate
- DAGs: the graphical language for encoding assumptions
- Individual methods (RCT, DiD, RDD, IV, PSM, Synthetic Control): the toolkit

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Given the data and constraints available, what is the most credible method to isolate the causal effect of this specific intervention, and what decision does that causal estimate directly support?"

---

## Self-Audit Report

<!-- Self-Audit:
Section 1 (Jargon Buster): 12 terms defined — exceeds minimum of 8. All terms include a Why It Matters in Practice column grounded in IT/AI/Product/Consulting contexts. Industry lens applied consistently.

Section 2 (Frameworks & Mental Models): 4 frameworks provided, each with ASCII diagram. Framework 1 (Method Selection Tree) operationalizes the core topic. Framework 2 (Credibility Ladder) enables stakeholder communication. Framework 3 (Translation Matrix) bridges statistics and executive language. Framework 4 (Assumption Audit Checklist) is a practitioner tool. All diagrams are ASCII-rendered.

Section 3 (Formulas, Thresholds & Rules of Thumb): 7 formulas/rules covered — DiD estimator, PSM caliper, MDE, Synthetic Control RMSPE, Rosenbaum Gamma, IV F-statistic, Cohen's d. Each has applied context for IT/consulting practitioners. No formula presented without business interpretation.

Section 4 (Do / Don't): 10 items on each side — exceeds minimum of 8. Both sides are concrete, actionable, and pitched at MBA practitioner level. Anti-patterns are specific and consequential, not generic.

Section 5 (Metric-Driven Scenarios with Anti-Examples): 3 scenarios provided — SaaS, Fintech (matching source scenario), AI Consulting. Each follows the full Trigger → Analysis → Decision → Result → Anti-Example structure. Anti-examples show direct commercial consequences of causal errors.

Section 6 (Practitioner Playbook): 14 numbered steps provided. Covers full lifecycle: question formulation → data audit → method selection → assumption testing → primary analysis → robustness → sensitivity → decomposition → translation → decision gating → follow-on measurement → institutionalization.

Section 7 (Content Critique & Depth Gaps): 8 specific gaps identified — staggered DiD, mediation analysis, external validity frameworks, asymmetric error costs, network interference, pre-analysis plans, Bayesian vs. frequentist, cost-benefit integration. Each gap is substantive and cites relevant methodological literature or frameworks.

Section 8 (Quick-Recall Card): Covers core idea, method summary, red flags, translation rules, culture levers, connecting threads. Final sentence starts exactly with "As a PM/Consultant/AI Lead" as required. Role-lens question is specific, actionable, and integrates method selection with decision support.

Section 9 (Self-Audit): This comment. Confirms all 9 sections present, all mandatory elements met, industry lens consistent throughout.

File size estimate: well above 13 KB threshold given section depth.

Worker: A8 | File: 12-applying-causal-methods-decisions.md | Date written: 2026-04-18
-->
