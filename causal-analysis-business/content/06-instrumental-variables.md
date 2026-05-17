# Instrumental Variables

## Overview
Instrumental variables is a technique used when the relationship between a treatment and an outcome is confounded by unobserved factors that cannot be controlled for directly. It works by finding a third variable, the instrument, that affects the treatment but has no direct effect on the outcome except through the treatment. The instrument acts as a source of as-if random variation in the treatment, allowing analysts to isolate a causal effect. This method is especially valuable when experiments are impossible and standard regression falls short.

---

## Why It Matters
In many business settings, the factors that drive a decision also independently affect the outcome, making it impossible to separate cause from correlation using standard methods. Instrumental variables provide a way to cut through this endogeneity problem. When a valid instrument is available, it offers one of the few credible paths to causal claims from purely observational data.

## Key Principles
- The instrument must be strongly correlated with the treatment variable so it meaningfully shifts the treatment
- The exclusion restriction requires that the instrument affects the outcome only through its effect on the treatment, not through any other channel
- A weak instrument that barely moves the treatment produces unreliable and imprecise estimates
- Finding a valid instrument is often the hardest part; the assumptions cannot be fully tested with data and require substantive justification

## Key Terms
| Term | Definition |
|------|------------|
| **Instrument** | A variable that influences the treatment but affects the outcome only indirectly through the treatment |
| **Endogeneity** | A situation where the treatment variable is correlated with unobserved factors that also affect the outcome, biasing standard estimates |
| **Exclusion Restriction** | The assumption that the instrument has no direct effect on the outcome other than through its influence on the treatment |
| **Two-Stage Least Squares** | A common estimation procedure that first predicts the treatment using the instrument, then uses those predictions to estimate the causal effect on the outcome |

## Use Case
A company wants to estimate how advertising spending affects sales but knows that spending decisions are influenced by expected demand, which also drives sales. It uses weather variation as an instrument because bad weather reduces outdoor ad visibility (affecting ad exposure) but does not directly change purchasing behavior through any other channel.

## Scenario
> An education technology firm wants to know whether using its platform causes students to earn higher grades. Students who choose to use the platform are likely more motivated, creating selection bias. The firm notices that a server outage randomly prevented some students from accessing the platform for two weeks. This outage serves as an instrument because it affected platform usage without being related to student ability or motivation. Using the outage as an instrument, the firm estimates the causal effect of platform usage on grades.

## Examples
- Economists use distance to college as an instrument for years of education when estimating the causal effect of schooling on earnings, since distance affects attendance but not earnings directly
- A retailer uses supply-chain disruptions that randomly limited product availability as an instrument to estimate how product assortment breadth causally affects store revenue

---

## Audited Appendix

# Instrumental Variables

Instrumental variables (IV) is a technique for estimating causal relationships when the treatment-outcome relationship is confounded by unobserved factors. It introduces a third variable — the instrument — that affects the treatment but has no direct path to the outcome except through the treatment. IV is especially valuable when randomized experiments are impossible, unethical, or impractical, and when standard regression is insufficient due to endogeneity.

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|------|--------------------------|----------------------------|
| Instrument | A variable that influences the treatment (e.g., ad spend) but has no direct effect on the outcome (e.g., sales) except through the treatment | Without a valid instrument, IV estimation is impossible; finding one is the whole game |
| Endogeneity | A problem where the treatment variable is correlated with the error term — often because unmeasured factors drive both treatment and outcome | Ignoring endogeneity gives biased coefficients that mislead strategic decisions |
| Exclusion Restriction | The assumption that the instrument affects the outcome only via its effect on the treatment, and through no other channel | Violation of this assumption invalidates the entire IV approach; it is untestable in most real-world scenarios |
| Two-Stage Least Squares (2SLS) | The most common IV estimator: Stage 1 regresses treatment on instrument; Stage 2 uses the predicted treatment from Stage 1 to estimate its effect on the outcome | The workhorse method — used in policy research, platform analytics, and economic consulting |
| Weak Instrument | An instrument that is only loosely correlated with the treatment variable | Produces inflated standard errors and unreliable estimates; can be worse than OLS with endogeneity |
| Local Average Treatment Effect (LATE) | The causal effect estimated by IV applies only to "compliers" — units whose treatment status is actually moved by the instrument | Critical nuance: IV does not give you the Average Treatment Effect (ATE) for the full population |
| Complier | A unit that takes the treatment when nudged by the instrument and does not take it when not nudged | Understanding who compliers are determines how generalizable the IV estimate is |
| First Stage F-Statistic | A diagnostic test for instrument strength; an F-statistic above 10 (or 104.7 in modern practice) is considered acceptable | A low F-stat signals a weak instrument — estimates become unreliable and bias from endogeneity can be amplified |
| Over-Identification Test (Sargan-Hansen) | When multiple instruments are available, tests whether the instruments satisfy the exclusion restriction | Useful but not conclusive; identifies internal inconsistency among instruments, not absolute validity |
| Selection Bias | Systematic difference between who chooses a treatment and who does not, driven by unobserved characteristics | The core problem IV is designed to solve — e.g., highly motivated students using an EdTech platform |
| Reduced Form | The direct regression of the outcome on the instrument, bypassing the treatment variable | A credibility check: if the instrument has no reduced-form effect, it cannot have an IV effect |
| Monotonicity Assumption | The instrument must move all units' treatment probability in the same direction (no "defiers") | Required for LATE interpretation; rarely stated explicitly but underlies most IV applications |

---

## Frameworks & Mental Models

### Framework 1: The IV Validity Triangle

```
           [Instrument Z]
          /               \
Relevant /                 \ BLOCKED
(Correl) /                   \ (Exclusion Restriction)
        /                     \
[Treatment D] -----------> [Outcome Y]
             Causal Effect
             (what we want)

Rules:
  Z --> D  : Must be STRONG (First Stage)
  Z --> Y  : Must be ZERO except through D (Exclusion Restriction)
  Z ⊥ U   : Z must be independent of unobserved confounders U
```

**Reading:** If any arrow in the triangle is violated — instrument is weak, there is a direct path from Z to Y, or Z correlates with omitted variables — the IV estimate is invalid.

---

### Framework 2: Two-Stage Least Squares (2SLS) Pipeline

```
RAW DATA
    |
    v
[Stage 1: First Stage]
Regress Treatment D on Instrument Z
  D_hat = alpha + beta * Z + controls
    |
    | (Extract predicted values D_hat)
    v
[Stage 2: Second Stage]
Regress Outcome Y on D_hat
  Y = gamma + delta * D_hat + controls
    |
    v
[Causal Estimate: delta]
This is the LATE — Local Average Treatment Effect
(Effect among compliers only)
```

**Key insight:** 2SLS isolates the variation in treatment that is "clean" (driven only by the instrument), and uses only that variation to identify the causal effect. All endogenous variation is discarded.

---

### Framework 3: The Compliance Taxonomy

```
Instrument Z = 0           Instrument Z = 1
(Not nudged)               (Nudged)

D = 0  D = 1            D = 0   D = 1
  |      |                 |       |
Never   Defier           Defier   Always
Taker   (takes only      (takes   Taker
(never  when NOT         only     (always
treats) nudged)          when NOT takes)
                         nudged)
                                  |
                              Complier
                         (takes ONLY when
                          nudged by Z)

IV estimates the causal effect for COMPLIERS only.
```

**IT/AI application:** In a product A/B test using a server outage as an instrument, compliers are students who used the platform when available and stopped when it went down. Always-takers (e.g., students who found workarounds) and never-takers (students who would not use it regardless) are excluded from the LATE estimate.

---

### Framework 4: Endogeneity Diagnostic Map

```
PROBLEM DETECTED?
       |
  Yes (OLS biased)
       |
  Is an experiment feasible?
  /           \
Yes            No
 |              |
RCT         Find Instrument
(Gold        /      \
 Standard) Valid?   Not Valid?
           /              \
         2SLS           Difference-in-
                        Differences / RDD /
                        Proxy Variables
```

---

## Formulas, Thresholds & Rules of Thumb

### Core 2SLS Formula

**First Stage:**

```
D_i = alpha_0 + alpha_1 * Z_i + alpha_2 * X_i + v_i
```

Where D_i = treatment, Z_i = instrument, X_i = controls, v_i = error.

**Second Stage:**

```
Y_i = beta_0 + beta_1 * D_hat_i + beta_2 * X_i + epsilon_i
```

Where D_hat_i = predicted treatment from Stage 1. The coefficient beta_1 is the 2SLS/IV estimate of the causal effect.

**Wald Estimator (simplest IV with binary instrument):**

```
IV Estimate = (E[Y | Z=1] - E[Y | Z=0]) / (E[D | Z=1] - E[D | Z=0])

           = Reduced Form Effect / First Stage Effect
```

**Context:** The Wald estimator is intuitive — it scales the intent-to-treat (ITT) effect by the compliance rate. If 60% of students switched behavior due to the outage and grades rose by 3 points on average, the causal effect on the compliers is 3 / 0.6 = 5 points.

---

### Thresholds & Rules of Thumb

| Rule | Value | Context |
|------|-------|---------|
| First Stage F-Statistic (instrument strength) | F > 10 (traditional); F > 104.7 (Stock-Yogo, 5% bias threshold) | Below 10 is a red flag; below 4 is indefensible |
| Minimum sample size for reliable IV | n > 500 (practical guideline) | Small samples amplify weak instrument bias dramatically |
| Reduced Form must be significant | p < 0.05 on Z --> Y | If instrument has no reduced-form effect, it cannot have an IV effect — the analysis collapses |
| LATE vs. ATE gap | Always acknowledge LATE ≠ ATE | In consulting, clients often want ATE; you must flag that IV gives only complier-specific estimates |
| Number of instruments vs. endogenous variables | Instruments >= Endogenous regressors | Exactly identified (one instrument, one endogenous variable) is ideal; over-identified allows testing |
| Exclusion restriction | Not statistically testable; must rely on theory | The most common cause of invalid IV in practice — always argue from domain knowledge |

---

## Do / Don't

### DO

1. **Validate instrument relevance statistically** — Always report the first-stage F-statistic and confirm it exceeds the 10 or 104.7 threshold before proceeding with 2SLS.
2. **Argue exclusion restriction from first principles** — Construct a domain-specific theoretical argument for why the instrument cannot affect the outcome directly. Document it explicitly.
3. **Report LATE with a clear definition of compliers** — Specify which sub-population the estimate applies to. In product analytics, this means defining which user segment was actually moved by the instrument.
4. **Check the reduced form first** — Run Y ~ Z before running 2SLS. If the reduced form is not significant, no amount of instrumental variable machinery will produce a meaningful estimate.
5. **Run robustness checks with alternative instruments** — If multiple plausible instruments exist, estimate the model with each and compare. Convergence of estimates increases credibility.
6. **Use 2SLS standard errors, not OLS** — Standard errors from the second-stage regression must be corrected for the two-stage process; most statistical packages do this automatically when using IV commands.
7. **Explain the instrument to non-technical stakeholders using the Wald intuition** — Frame it as: "We're only looking at the part of the treatment that was randomly assigned by the instrument."
8. **Document the instrument's mechanism explicitly** — In an AI/ML product context, if you use geographic variation as an instrument, explain why geography affects treatment but not outcome through any other channel.
9. **Conduct placebo tests** — Test whether the instrument predicts outcomes in a period or subgroup where it logically should have no effect. Significant results indicate instrument contamination.
10. **Acknowledge limitations in the final recommendation** — IV estimates are often noisier than OLS. Report confidence intervals and contextualize uncertainty for decision-makers.

### DON'T

1. **Don't use a weak instrument** — A first-stage F-statistic below 10 produces estimates that can be more biased than plain OLS with endogeneity. Weak instrument bias runs toward OLS.
2. **Don't assume the exclusion restriction holds without argument** — "It seems unrelated" is not a valid justification. Think carefully about all possible channels through which the instrument could directly affect the outcome.
3. **Don't generalize LATE to the full population** — IV estimates apply to compliers only. Recommending platform-wide changes based on complier effects can be strategically misleading.
4. **Don't skip the first stage entirely** — Some practitioners jump to second-stage results without reporting first-stage statistics. This hides instrument quality from reviewers and clients.
5. **Don't confuse intent-to-treat (ITT) with LATE** — ITT is the average effect of being assigned the instrument. LATE adjusts for the compliance rate. These are different numbers with different interpretations.
6. **Don't use instruments that are themselves endogenous** — If the proposed instrument is correlated with unobserved confounders, it inherits the very problem it was supposed to solve.
7. **Don't treat IV as a substitute for understanding the system** — IV is a rescue technique, not a first resort. Invest in understanding the data-generating process before defaulting to instruments.
8. **Don't ignore the monotonicity assumption** — If a meaningful share of units are defiers (they take treatment when not nudged and do not take it when nudged), LATE interpretation is invalid.
9. **Don't use natural experiments without checking temporal validity** — An instrument from five years ago (e.g., a historical policy change) may not be relevant to the current treatment mechanism.
10. **Don't report IV estimates without comparing to OLS** — The direction and magnitude of the difference between OLS and IV estimates is itself informative about the nature of the endogeneity bias.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: SaaS Platform — Does Onboarding Call Length Cause Retention?

**Trigger:** A B2B SaaS company's Customer Success team suspects that longer onboarding calls increase 90-day retention. However, account executives spend more time with clients they perceive as high-value, creating selection bias. The data team cannot run an experiment because call lengths are driven by customer complexity.

**Analysis:**
- Proposed instrument: Call scheduling software that randomly assigned available 30-minute vs. 60-minute time slots based on rep calendar availability on the day of signup.
- First Stage: Calendar slot length strongly predicts actual call length (F-statistic = 47.3). Relevant.
- Exclusion Restriction: Calendar availability of reps is unrelated to client quality, revenue potential, or likelihood to churn (argued from HR scheduling data showing randomness).
- Reduced Form: 60-minute slots are associated with 8.2% higher 90-day retention (p = 0.003).
- 2SLS Estimate: A 10-minute increase in call length causes a 4.1 percentage point increase in retention (among compliers — clients whose call length was actually changed by the slot assignment).

**Decision:** Standardize onboarding calls to 60 minutes as default; restructure rep scheduling to eliminate 30-minute slots in the first 90 days of a client relationship.

**Result:** 90-day retention improved by 6.3% across the next cohort. Unit economics improved because retained clients had 3.2x the LTV of churned clients.

**Anti-Example:** The growth analytics team runs an OLS regression of retention on call length and finds a coefficient suggesting 10 extra minutes increases retention by 12 percentage points. Leadership uses this to mandate 2-hour onboarding calls. The OLS estimate was inflated by the selection bias (high-value clients got longer calls AND retained better for reasons unrelated to call length). The 2-hour mandate overwhelms reps and reduces overall onboarding quality, worsening retention.

---

### Scenario 2: EdTech Product — Does Platform Usage Cause Grade Improvement?

**Trigger:** An EdTech firm wants to prove to institutional clients (universities, school districts) that its platform causes better academic outcomes. A simple comparison of heavy users vs. light users is contaminated by motivation bias — students who use the platform more are also more intrinsically motivated to study.

**Analysis:**
- Proposed instrument: A server outage that randomly prevented a cohort of 1,200 students from accessing the platform for two weeks mid-semester, due to a data center failure unrelated to any student characteristic.
- First Stage: Server outage status reduced platform usage hours by an average of 14.2 hours over the two-week period (F-statistic = 89.5). Strongly relevant.
- Exclusion Restriction: Server outage affected access, not motivation, study habits, or instructor quality. No contemporaneous academic events (exams, holidays) occurred during the outage window.
- Reduced Form: Students affected by the outage scored 3.1 points lower on semester-end assessments (p = 0.008).
- 2SLS Estimate: Each additional 10 hours of platform usage causally increases semester scores by 2.2 points (LATE — applies to students whose usage was genuinely changed by the outage, i.e., regular users).

**Decision:** Use IV estimate (not OLS) in marketing materials and institutional contracts. Segment users to identify "complier-type" students (regular users, not always-on power users or never-users) as the primary value proposition target.

**Result:** Three university procurement contracts were signed using the IV-backed causal claim. One competitor's claim was challenged because it was based on OLS, which inflated the effect size by 2.4x.

**Anti-Example:** The product team runs a simple before-after comparison for students who started using the platform vs. those who did not. Grades improved by 11 points in the user group. The team presents this as causal. A skeptical university statistician points out that students who voluntarily adopted the platform were already higher performers and more engaged. The contract falls through. The IV estimate of 2.2 points per 10 hours would have been defensible.

---

### Scenario 3: AI Consulting — Does AI Tool Adoption Improve Analyst Productivity?

**Trigger:** A global consulting firm deploys an AI writing assistant to its analyst pool. Leadership wants to know if adoption causes faster report delivery. However, analysts who voluntarily adopt AI tools are typically more tech-savvy and already faster workers. OLS shows AI adoption reduces report time by 40% — but this is almost certainly inflated by selection.

**Analysis:**
- Proposed instrument: Mandatory AI tool training was rolled out by office location in alphabetical order due to trainer availability logistics. Offices A-M received training in Quarter 1; N-Z in Quarter 2.
- First Stage: Q1 training assignment increased AI adoption rate by 38 percentage points (F-statistic = 62.1). Relevant.
- Exclusion Restriction: Office location (by first letter) has no direct relationship with analyst productivity or report complexity. Confirmed by checking pre-period productivity metrics — no systematic differences across office groups.
- Reduced Form: Q1-trained offices showed a 19% reduction in average report delivery time vs. Q2 offices during the same quarter.
- 2SLS Estimate: AI tool adoption causally reduces report delivery time by 28% (LATE — applies to analysts who adopted because they received early training, not voluntary early adopters).

**Decision:** Accelerate global rollout of AI tool training. Invest in change management for the 62% non-adopter segment (the never-takers revealed by the analysis). Target onboarding resources to the complier profile — mid-tenure analysts without prior AI exposure.

**Result:** Full rollout with structured onboarding reduced firm-wide report delivery time by 23% (consistent with LATE estimate when adjusted for non-compliers). Partner utilization improved, enabling 11% more client engagements per quarter.

**Anti-Example:** The People Analytics team presents the OLS estimate (40% reduction) to the managing partners and proposes linking analyst bonuses to AI tool usage rates. When the tool is mandated without proper onboarding, resistant senior analysts produce lower-quality reports. The overstated 40% efficiency claim sets unrealistic expectations, and the bonus structure creates perverse incentives to log AI usage without meaningful adoption. Morale drops. The IV estimate would have set realistic expectations and flagged the non-complier problem early.

---

## Practitioner Playbook

**Step-by-step guide for applying IV in IT, AI, and consulting contexts.**

1. **Identify the endogeneity problem clearly.** Before searching for an instrument, articulate precisely why OLS will be biased. Name the unobserved confounder (e.g., motivation, ability, client quality). Document this in writing before proceeding to instrument selection.

2. **Generate a list of candidate instruments using domain knowledge.** Brainstorm variables that plausibly affect the treatment but have no direct path to the outcome. In IT/product contexts, look for: random system events (outages, rollouts, queue assignments), geographic or temporal variation in policy rollout, lottery-based access, hardware failures, or administrative assignment rules.

3. **Apply the three IV validity tests as a filter:**
   - Relevance: Does the instrument correlate with the treatment? (Testable)
   - Exclusion: Does the instrument affect the outcome only through treatment? (Untestable — argue theoretically)
   - Independence: Is the instrument uncorrelated with unobserved confounders? (Partially testable via balance checks)

4. **Run the first-stage regression.** Regress treatment D on instrument Z and all controls. Extract the F-statistic. If F < 10, do not proceed with 2SLS — return to step 2 and find a stronger instrument or abandon IV.

5. **Check the reduced form.** Regress outcome Y directly on instrument Z. If the reduced form effect is not statistically significant, the IV estimate will not be meaningful. The IV estimate is literally the ratio of reduced form to first stage — a zero numerator gives a zero result regardless of denominatorm.

6. **Run 2SLS using dedicated IV commands.** Use ivreg in R, ivregress in Stata, or IV2SLS in Python's linearmodels library. Do NOT manually run two OLS regressions and use the second-stage coefficient — standard errors will be wrong.

7. **Report and interpret the LATE with a precise definition of compliers.** Who are the compliers in your specific context? Describe them in plain English. State explicitly that the estimate does not necessarily apply to always-takers or never-takers.

8. **Compare IV and OLS estimates.** Conduct the Hausman/Wu test for endogeneity. Report both estimates side by side. The direction of the difference between IV and OLS tells you the direction of the omitted variable bias.

9. **Run placebo and falsification tests.** Test whether the instrument predicts outcomes in placebo periods (before the instrument was activated) or in subgroups where the treatment mechanism is absent. Significant placebo effects signal instrument contamination.

10. **If multiple instruments are available, run over-identification tests.** Use the Sargan-Hansen J-test. Rejection suggests at least one instrument violates the exclusion restriction. Investigate which instrument is the likely culprit.

11. **Communicate the estimate and its limitations clearly to stakeholders.** Use the Wald intuition: "We are measuring the causal effect only among users whose behavior was actually changed by [the instrument]. Our estimate may not represent users who would never have changed regardless." Provide confidence intervals.

12. **Document all instrument validity arguments in the analysis brief.** Since exclusion restriction is untestable, the credibility of the IV estimate rests on the quality of the theoretical argument. Write it down. Have a domain expert review it independently.

13. **Revisit the instrument's relevance over time.** Natural experiment instruments (policy changes, outages) may lose validity as conditions change. An instrument valid in 2023 may be irrelevant by 2026 if the treatment mechanism has evolved.

---

## Content Critique & Depth Gaps

**What the source material covers well:**
- The intuition behind instrumental variables is clearly stated.
- The core validity conditions (relevance, exclusion restriction) are identified.
- Practical examples (weather as instrument for ad visibility; server outage for EdTech) are well-chosen and relatable to product analytics contexts.

**What is missing for IIM/HBS MBA-level depth:**

1. **No discussion of LATE vs. ATE vs. ATT.** The source treats IV as if it gives a population-level causal effect. In reality, IV gives LATE (Local Average Treatment Effect), which applies only to compliers. This distinction is critical for policy recommendations and product strategy. HBS case discussions routinely interrogate this.

2. **Weak instruments problem is mentioned but not operationalized.** The source says "weak instruments produce unreliable estimates" without explaining the mechanics: weak instrument bias runs toward OLS bias, and finite-sample distributions become extremely skewed. The Stock-Yogo critical values for F-statistics are not mentioned.

3. **No treatment of multiple endogenous regressors.** Most real-world consulting problems involve more than one endogenous variable. The source covers only the single-instrument, single-treatment case.

4. **Over-identification and instrument testing are absent.** The Sargan-Hansen J-test, Wu-Hausman test for endogeneity, and Anderson-Rubin confidence intervals for weak-instrument-robust inference are all missing.

5. **No discussion of heterogeneous treatment effects.** IV identifies LATE under monotonicity. If treatment effects are heterogeneous across subgroups (likely in product and AI contexts), the LATE may not be representative of any actionable segment.

6. **Compliance taxonomy is not addressed.** The four types of units — always-takers, never-takers, compliers, defiers — are absent from the source. This taxonomy is essential for interpreting what the IV estimate actually means in practice.

7. **No guidance on instrument discovery.** For practitioners, the hardest part of IV is finding a valid instrument. The source acknowledges this is difficult but provides no systematic framework for instrument discovery in business settings (natural experiments, randomized access, supply-side shocks, geographic variation, etc.).

8. **No comparison to alternative approaches.** Regression Discontinuity Design, Difference-in-Differences, and synthetic control methods are all alternatives to IV in quasi-experimental settings. Understanding when IV is preferable to these alternatives requires a comparative framework that is absent.

9. **Standard error correction in 2SLS is not mentioned.** Running two OLS regressions manually produces incorrect standard errors. Practitioners who do not know to use dedicated IV commands will make inference errors.

10. **No discussion of IV in machine learning contexts.** DeepIV, neural network-based IV estimators, and double machine learning (DML) for IV with high-dimensional controls are increasingly relevant in AI product teams but entirely absent.

---

## Quick-Recall Card

- **Core problem IV solves:** Endogeneity — the treatment variable is correlated with unobserved factors that also drive the outcome, making OLS estimates biased.
- **Three validity conditions for any instrument:** (1) Relevance — Z must correlate with D; (2) Exclusion restriction — Z affects Y only through D; (3) Independence — Z is uncorrelated with unobserved confounders.
- **The Wald estimate:** IV effect = (Y|Z=1 - Y|Z=0) / (D|Z=1 - D|Z=0). Reduced form divided by first stage.
- **2SLS in plain English:** Stage 1 extracts the "clean" (instrument-driven) variation in treatment. Stage 2 uses only that clean variation to estimate the treatment's effect on the outcome.
- **LATE is not ATE:** IV identifies the causal effect only among compliers — units whose treatment was actually changed by the instrument. Always-takers and never-takers are excluded.
- **First Stage F-statistic diagnostic:** F > 10 minimum; F > 104.7 for strong instrument. Below 10, do not trust the IV estimate.
- **Exclusion restriction is untestable:** It must be argued from domain knowledge. This is the most fragile assumption and the most common source of invalid IV estimates in practice.
- **Reduced form check:** Always run Y ~ Z first. If the instrument has no direct reduced-form effect on the outcome, 2SLS will not save you.
- **Complier profile matters:** Identify who the compliers are in your specific context. They define the population to whom the LATE applies and inform the strategic relevance of the finding.
- **OLS vs. IV comparison is informative:** The direction of OLS - IV tells you the direction of omitted variable bias. If OLS > IV, the unmeasured confounder was positively correlated with both treatment and outcome.
- **Classic instruments in business:** Lottery-based access (randomized rollout), geographic/alphabetical assignment, system outages, weather variation, distance to service, supply chain disruptions.
- **Do not manually run 2SLS:** Use dedicated IV commands (ivreg, ivregress, IV2SLS) to get correct standard errors. Manual two-stage OLS produces wrong inference.
- **Placebo tests build credibility:** Test whether the instrument predicts outcomes in contexts where it theoretically should not. Failure of placebo (significant result where none expected) flags instrument contamination.

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Is the variation in our treatment that I am attributing to a causal effect actually driven by a source I can argue is random and unrelated to any other driver of the outcome — and if not, what instrument can I find to isolate that clean variation?"

---

## Self-Audit Report

<!-- Self-Audit:
SECTION COMPLETENESS CHECK:
1. Jargon Buster — COMPLETE. 12 terms included (exceeds minimum of 8). All terms are relevant to IV methodology with IT/AI/consulting applications. Each entry includes plain-English definition and practical significance.
2. Frameworks & Mental Models — COMPLETE. 4 frameworks with ASCII diagrams: IV Validity Triangle, 2SLS Pipeline, Compliance Taxonomy, Endogeneity Diagnostic Map. Each diagram is labeled and includes an interpretive note.
3. Formulas, Thresholds & Rules of Thumb — COMPLETE. Core 2SLS formula, Wald estimator, and a comprehensive thresholds table with context for each rule. Values are grounded in econometric literature (Stock-Yogo, traditional F > 10 threshold).
4. Do / Don't — COMPLETE. 10 items on each side (exceeds minimum of 8). All items are specific, actionable, and oriented toward IT/AI/product/consulting practitioners.
5. Metric-Driven Scenarios with Anti-Examples — COMPLETE. 3 scenarios: SaaS retention, EdTech grades, AI consulting productivity. Each follows the exact format: Trigger → Analysis → Decision → Result → Anti-Example. All scenarios are grounded in realistic business metrics.
6. Practitioner Playbook — COMPLETE. 13 numbered steps covering the full IV workflow from problem identification through communication and longitudinal validity maintenance.
7. Content Critique & Depth Gaps — COMPLETE. 10 specific gaps identified relative to IIM/HBS MBA-level depth. Includes technical gaps (LATE vs. ATE, weak instruments, over-identification) and emerging field gaps (DeepIV, double machine learning).
8. Quick-Recall Card — COMPLETE. 13 bullet points covering core concepts. Final line begins with exact phrase "As a PM/Consultant/AI Lead" as required.
9. Self-Audit Report — COMPLETE. This comment block.

INDUSTRY LENS CHECK: IT/AI/Product/Consulting lens applied consistently across all sections. Scenarios use SaaS, EdTech, and management consulting contexts. Playbook references Python/R/Stata tooling relevant to data science practitioners.

FILE SIZE ESTIMATE: Approximately 16-18 KB based on content volume. Exceeds minimum 13 KB requirement.

CONNECTS TO NOTE: See related audit files in this course folder for complementary causal inference methods.

ROLE-LENS QUESTION CHECK: Final bullet in Section 8 begins with exact phrase "As a PM/Consultant/AI Lead" — CONFIRMED.

KNOWN LIMITATIONS:
- Exclusion restriction remains untestable; all arguments are by construction theoretical.
- LATE estimates in all three scenarios are illustrative; actual values would require real data.
- Over-identification tests (Sargan-Hansen) are mentioned but not demonstrated with a worked example due to space constraints.

OVERALL ASSESSMENT: All 9 sections are present, complete, and meet depth requirements for IIM/HBS MBA-level audit standards. File is ready for use.
-->

---

**Connects to:**
- `01-correlation-vs-causation.md` — foundational distinction that motivates all causal inference methods including IV
- `02-confounders-and-omitted-variable-bias.md` — IV is the primary solution to omitted variable bias; these files are tightly coupled
- `03-regression-discontinuity-design.md` — RDD is an alternative quasi-experimental method; compare instrument vs. threshold-based identification
- `04-difference-in-differences.md` — DiD is another alternative; compare parallel trends assumption to IV exclusion restriction
- `05-natural-experiments.md` — IV almost always relies on a natural experiment; these files share foundational concepts
- `07-propensity-score-matching.md` — PSM addresses selection bias using observed variables; IV addresses it using unobserved variation
- `08-mediation-analysis.md` — IV can be used to identify mediator effects when mediators are endogenous
