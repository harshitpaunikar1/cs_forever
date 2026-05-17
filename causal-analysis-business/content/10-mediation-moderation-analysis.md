# Mediation and Moderation Analysis

## Overview
Mediation analysis investigates the mechanism through which a cause produces an effect by identifying intermediate variables that carry the causal influence. Moderation analysis examines whether the strength or direction of a causal effect changes depending on the level of another variable. Together, these methods move beyond asking whether something works to understanding how and for whom it works. They are essential for designing targeted business strategies.

---

## Why It Matters
Knowing that a marketing campaign increases sales is useful, but knowing that it works by increasing brand awareness, which in turn drives purchase intent, is far more actionable. Similarly, discovering that a pricing change boosts revenue among new customers but hurts retention among loyal customers lets a company fine-tune its approach. Mediation and moderation turn blunt causal findings into precise, actionable insights.

## Key Principles
- A mediator is a variable that lies on the causal path between the treatment and the outcome and explains part or all of the effect
- A moderator is a variable that changes the size or direction of the causal effect without being caused by the treatment itself
- Full mediation means the entire effect of the treatment flows through the mediator, while partial mediation means some effect is direct
- Moderation is tested by including an interaction term between the treatment and the moderator in the model

## Key Terms
| Term | Definition |
|------|------------|
| **Mediator** | A variable that transmits the causal effect from the treatment to the outcome, explaining the mechanism of action |
| **Moderator** | A variable that influences the strength or direction of the relationship between the treatment and the outcome |
| **Direct Effect** | The portion of the treatment's influence on the outcome that does not pass through the mediator |
| **Interaction Effect** | The combined effect of two variables that differs from the sum of their individual effects, indicating moderation |

## Use Case
A software company wants to understand whether its customer success outreach reduces churn by increasing product usage (mediation) and whether the effect is stronger for enterprise clients than for small business clients (moderation).

## Scenario
> A fitness app company discovers that sending push notification reminders increases weekly workout frequency. Mediation analysis reveals that the reminders work primarily by increasing app opens, which then lead to workouts. Moderation analysis shows that the effect is three times larger for users who have been on the platform for less than 30 days compared to long-term users. The company decides to concentrate its notification strategy on new users and focus on different retention tactics for veterans.

## Examples
- A retailer finds that employee training improves customer satisfaction scores, and mediation analysis shows the effect operates through improved product knowledge rather than friendlier service
- A pharmaceutical company finds that a drug reduces symptoms, and moderation analysis reveals that the effect is stronger in patients under 40 than in older patients

---

## Audited Appendix

# Mediation and Moderation Analysis

Mediation analysis investigates the mechanism through which a cause produces an effect by identifying intermediate variables (mediators) that carry causal influence. Moderation analysis examines whether the strength or direction of a causal effect changes depending on the level of another variable (moderator). Together they move beyond "does it work" to "how and for whom."

Key Principles:
- A mediator lies on the causal path between treatment and outcome
- A moderator changes the size or direction of the causal effect (not caused by the treatment itself)
- Full mediation: entire effect flows through mediator; partial mediation: some direct effect remains
- Moderation is tested by including an interaction term between treatment and moderator

Key Terms: Mediator, Moderator, Direct Effect, Interaction Effect

Use Case: Software company wants to understand whether customer success outreach reduces churn by increasing product usage (mediation) and whether the effect is stronger for enterprise clients than for small business clients (moderation).

Scenario: Fitness app discovers that push notification reminders increase weekly workout frequency. Mediation analysis reveals reminders work primarily by increasing app opens, which lead to workouts. Moderation analysis shows the effect is 3x larger for users on the platform less than 30 days vs long-term users. Company concentrates notification strategy on new users.

Examples:
- Retailer finds employee training improves customer satisfaction — mediation analysis shows effect operates through improved product knowledge rather than friendlier service
- Pharmaceutical company finds drug reduces symptoms — moderation analysis reveals effect is stronger in patients under 40

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| Mediator | A variable that sits on the causal path between cause and effect — it is caused by the treatment and in turn causes the outcome | Tells product and consulting teams which mechanism to invest in; if the mediator is not activated, the intervention will fail even if it is deployed correctly |
| Moderator | A variable that changes the strength or direction of the causal effect without itself being caused by the treatment | Enables segmentation strategy — tells you for whom an intervention is most powerful, allowing resource concentration and personalization |
| Direct Effect (DE) | The portion of the total effect that goes directly from treatment to outcome, bypassing the mediator | Reveals whether the treatment has value beyond the hypothesized mechanism; critical for kill/continue decisions when the mediator is hard to influence |
| Indirect Effect (IE) | The portion of the total effect that flows through the mediator (Treatment → Mediator → Outcome) | Quantifies the mechanism's contribution; if IE ≈ Total Effect, full mediation is occurring and the mediator is the lever to pull |
| Total Effect (TE) | The sum of Direct Effect and Indirect Effect; the overall causal impact of the treatment on the outcome | Baseline benchmark; compare TE vs IE to understand how much of the story you have explained |
| Interaction Term | A new variable created by multiplying the treatment indicator by the moderator variable; its coefficient captures moderation | The statistical test of whether the causal effect differs across segments; a significant interaction coefficient means heterogeneous treatment effects exist |
| Conditional Average Treatment Effect (CATE) | The average causal effect of the treatment for a specific sub-group defined by moderator levels | Operationally actionable — allows targeting, tiered pricing, and differentiated playbooks by customer segment |
| Full Mediation | The scenario where the Direct Effect drops to zero (or near zero) once the mediator is included in the model | Signals that removing the treatment but preserving the mediator (e.g., habit or capability) could sustain the outcome; major implication for product sunset decisions |
| Partial Mediation | The situation where both Direct Effect and Indirect Effect remain non-zero | More common in practice; means the product works through multiple pathways and no single lever fully explains outcomes |
| Baron-Kenny Steps | The classic four-step procedure for establishing mediation (establish total effect, show treatment predicts mediator, show mediator predicts outcome controlling for treatment, check direct effect reduction) | Still widely used in consulting engagements and board presentations despite having been superseded statistically; knowing it avoids methodological embarrassment |
| Sobel Test | A significance test for the indirect effect calculated as the product of two regression coefficients divided by a standard error formula | Low power for small samples; bootstrapped confidence intervals are preferred in modern practice, but the Sobel test appears in legacy analyses and academic papers you will need to critique |
| Bootstrap CI for Indirect Effect | Resampling-based confidence interval for the indirect (mediated) effect that does not assume normality | The gold standard for inference in mediation; if the 95% CI for the indirect effect excludes zero, mediation is statistically supported |

---

## Frameworks & Mental Models

### Framework 1 — The Mediation Path Diagram

The core structure of any mediation model. The "a" path connects treatment to mediator; the "b" path connects mediator to outcome; the "c'" path (c-prime) is the direct effect from treatment to outcome after accounting for the mediator. The "c" path (without prime) is the total effect.

```
                    a path              b path
  Treatment ──────────────► Mediator ──────────────► Outcome
      │                                                  ▲
      │                    c' path (direct)              │
      └──────────────────────────────────────────────────┘

  Indirect Effect (IE) = a × b
  Total Effect (TE)    = c = c' + (a × b)
  Proportion Mediated  = IE / TE

  Full Mediation:    c' ≈ 0,  IE ≈ TE
  Partial Mediation: c' > 0,  IE > 0
  No Mediation:      c' ≈ TE, IE ≈ 0
```

Product Example: Customer Success Outreach (Treatment) → Product Usage (Mediator) → Churn Reduction (Outcome). If a=0.45 and b=0.60, then IE=0.27. If TE=0.35, then c'=0.08 (partial mediation, 77% mediated through usage).

### Framework 2 — The Moderation (Interaction) Diagram

Moderation is visualized as a variable that changes the slope of the treatment-outcome relationship. The moderator does not sit between cause and effect; it sits beside the relationship and alters its magnitude.

```
                  Moderator (Z)
                       │
                       │ modifies
                       ▼
  Treatment (X) ──────────────► Outcome (Y)

  Regression Model:
  Y = β0 + β1·X + β2·Z + β3·(X × Z) + ε

  β3 = interaction coefficient = moderation effect

  If β3 > 0 and significant:
    High Z ──► Stronger treatment effect
    Low  Z ──► Weaker treatment effect

  Interaction Plot:
  Outcome
    │          ╱  High Moderator
    │        ╱
    │      ╱
    │   ──────  Low Moderator
    │─────────────────────────────
         Control    Treatment
```

Consulting Example: AI Automation Tool (Treatment), Team Technical Maturity (Moderator), Productivity Gain (Outcome). β3 significant and positive means the automation delivers 2x productivity lift for high-maturity teams versus marginal gains for low-maturity teams. Rollout recommendation changes dramatically.

### Framework 3 — The PROCESS Model Decision Tree (Hayes)

Used to decide which of the 92+ PROCESS macro models to apply based on the analytical question.

```
  START: What is your causal question?
          │
          ├──► "HOW does X affect Y?"
          │         └──► Mediation Framework
          │               │
          │               ├── Single mediator? → Model 4 (simple mediation)
          │               ├── Serial mediators? → Model 6 (chain mediation)
          │               └── Multiple parallel mediators? → Model 4 extended
          │
          └──► "FOR WHOM does X affect Y?"
                    └──► Moderation Framework
                          │
                          ├── Simple moderation? → Model 1
                          ├── Moderated mediation? → Model 14 / 7 / 58
                          └── Mediated moderation? → Model 8
```

### Framework 4 — The Heterogeneous Treatment Effects (HTE) Segmentation Matrix

After identifying moderation, map subgroups against effect size to prioritize deployment.

```
  Effect Size vs Segment Size Matrix

  Large Effect │  PRIORITY SEGMENT  │  SCALE WITH CARE  │
               │  (concentrate here)│  (capacity needed) │
               ├────────────────────┼────────────────────┤
  Small Effect │  MONITOR / TEST    │  DEPRIORITIZE      │
               │  (may improve)     │  (poor ROI)        │
               └────────────────────┴────────────────────┘
                   Small Segment         Large Segment
                     Size                   Size
```

---

## Formulas, Thresholds & Rules of Thumb

### Core Mediation Formulas

**Total Effect decomposition:**
```
TE = DE + IE
c  = c' + (a × b)
```
Context: Always verify this decomposition holds numerically in your output. Discrepancies indicate model misspecification or multicollinearity.

**Proportion of effect mediated:**
```
PM = IE / TE = (a × b) / c
```
Context: PM > 0.80 suggests near-full mediation. PM between 0.20 and 0.80 is partial mediation. Negative PM (inconsistent mediation) occurs when the direct and indirect effects have opposite signs — common in competitive dynamics and immune system interventions.

**Sobel Test statistic (legacy, still cited):**
```
z = (a × b) / sqrt(b²·SE_a² + a²·SE_b²)
```
Context: Treat p < 0.05 on this test as a floor, not a ceiling. Always supplement with bootstrapped CIs because Sobel assumes normality of the product (a×b), which rarely holds.

**Bootstrap Confidence Interval for IE:**
```
Resample dataset with replacement 5,000–10,000 times
Compute IE = a × b in each resample
95% CI = [2.5th percentile, 97.5th percentile of IE distribution]
Mediation supported if 0 is excluded from the CI
```
Context: Use 10,000 iterations for publication-grade analysis. Use 5,000 for internal consulting decks. Always report both the point estimate and the CI.

### Core Moderation Formulas

**Interaction regression model:**
```
Y = β0 + β1·X + β2·Z + β3·(X·Z) + ε
```
Context: β3 is the moderation coefficient. A significant β3 (p < 0.05) means the effect of X on Y differs by level of Z. Center continuous moderators (Z_centered = Z − mean(Z)) before computing the interaction to reduce multicollinearity and make β1 interpretable.

**Simple slopes at conditional values of Z:**
```
Slope of X at Z_high (mean + 1SD): β1 + β3·(mean + 1SD)
Slope of X at Z_mean:              β1 + β3·(mean)
Slope of X at Z_low  (mean − 1SD): β1 + β3·(mean − 1SD)
```
Context: Report effect of X on Y at these three levels. This is what gets shown in a client moderation plot.

### Rules of Thumb for IT/AI/Product/Consulting Practice

| Rule | Threshold | Rationale |
|---|---|---|
| Sample size for mediation | n ≥ 200 for bootstrap to stabilize | Smaller samples yield unstable indirect effect estimates |
| Sample size for moderation | n ≥ 400 for detecting moderate interactions (f² = 0.01) | Interaction effects are typically small in field settings; need power |
| Proportion mediated for strategy action | PM ≥ 0.40 before redesigning product around the mediator | Weaker mediation may not justify structural product change |
| Effect size for CATE-based segmentation | Difference in treatment effect across segments ≥ 0.20 SD | Smaller differences rarely justify differentiated GTM strategies |
| Multicollinearity check | VIF < 5 for mediator and treatment in outcome model | VIF > 5 signals the mediator is collinear with treatment, distorting DE estimate |
| Minimum interaction sample per cell | n ≥ 30 per treatment × moderator cell | Cell sizes below 30 yield unreliable CATE estimates |

---

## Do / Don't

### Do

1. Center continuous mediators and moderators before computing interaction terms — reduces multicollinearity and makes main effects interpretable at the mean of other variables.
2. Use bootstrapped confidence intervals (5,000+ iterations) for indirect effects rather than relying on Sobel test p-values alone — bootstrapping does not assume normality of the product distribution.
3. Establish temporal precedence before labeling a variable a mediator — the mediator must logically and temporally occur between treatment and outcome, not simultaneously.
4. Test the full causal chain: confirm Treatment → Mediator (a path), Mediator → Outcome controlling for Treatment (b path), and observe Direct Effect (c' path) before claiming mediation.
5. Plot simple slopes at high, medium, and low moderator values — visual representation of moderation is essential for client and executive communication.
6. Report both the proportion mediated (PM) and the absolute indirect effect (IE) with its confidence interval — stakeholders need magnitude, not just existence, of mediation.
7. Control for potential confounders of the Mediator → Outcome relationship, not just the Treatment → Outcome relationship — omitting confounders of the M→Y path is the most common source of biased mediation estimates.
8. Pre-register your hypothesized mediator and moderator before data collection in experimental contexts — prevents HARKing (Hypothesizing After Results are Known) and inflates credibility with technical stakeholders.
9. Conduct sensitivity analysis for unmeasured confounding (Imai et al. sensitivity framework or E-values) to assess how robust the indirect effect is to hidden variables.
10. When running moderated mediation, specify whether the moderation is on the a-path (treatment-to-mediator) or b-path (mediator-to-outcome) — these have completely different substantive interpretations and intervention implications.

### Don't

1. Do not label a variable a mediator simply because it correlates with both the treatment and the outcome — correlation does not imply it lies on the causal path; use DAG reasoning to justify causal ordering before running any regression.
2. Do not use cross-sectional data to claim definitive mediation — without temporal ordering or experimental manipulation, mediation estimates are descriptive path analyses, not causal claims.
3. Do not forget to check the mediator for treatment-induced confounding — if the treatment changes a potential confounder of M→Y, standard regression-based mediation is biased and you need the four-way decomposition.
4. Do not interpret a non-significant interaction term as proof of no moderation — the analysis may simply be underpowered; calculate required sample size for the expected interaction effect size before concluding homogeneity.
5. Do not include the mediator as a control variable in a study of the Total Effect of treatment — conditioning on the mediator blocks the indirect path and produces a biased estimate of total causal impact.
6. Do not run mediation analysis in a single regression with mediator and treatment simultaneously entered without first establishing the a-path — this is a common shortcut that skips critical diagnostic steps.
7. Do not present moderation results without specifying the coding of the moderator — a 0/1 binary moderator, a centered continuous moderator, and an uncentered continuous moderator yield different β1 interpretations; always clarify.
8. Do not conflate statistical moderation (interaction in regression) with practical moderation (a difference large enough to change business decisions) — a p < 0.05 interaction with effect size Δ = 0.05 standard deviations is real but irrelevant to resource allocation strategy.
9. Do not apply mediation findings from one context (e.g., consumer SaaS) to another (e.g., enterprise B2B) without re-estimating — the mechanism through which an intervention works frequently differs by market context.
10. Do not skip the M→Y confounder plot in your DAG — failure to identify and control for variables that affect both mediator and outcome is the primary driver of inflated mediation estimates in published consulting case studies.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1 — AI Feature Adoption and Revenue Expansion (SaaS)

**Trigger:** A B2B AI platform introduces a natural language query feature. Gross revenue retention improves by 8 percentage points in the quarter post-launch. The product leadership team wants to scale the feature and understand the mechanism before committing $4M in engineering headcount.

**Analysis:** Team runs a mediation analysis. Treatment = NL Query Feature (assigned via phased rollout serving as quasi-experiment). Mediator = Weekly Active Queries per Account. Outcome = Net Revenue Retention at 12 months. A path (β=0.52, p<0.001): feature access significantly increases query activity. B path (β=0.38, p<0.001): query activity significantly predicts NRR controlling for feature access. IE = 0.52 × 0.38 = 0.198. TE = 0.21. PM = 0.198/0.21 = 94% — near-full mediation. Direct Effect c'=0.012, not significant (p=0.41).

**Decision:** 94% of the NRR impact flows through query adoption. The feature itself is not the lever — activating query behavior is. Product team reallocates $1.5M of the engineering budget to in-app onboarding and query suggestion prompts designed to drive the mediator. Customer success team adds query activity to their account health score and proactive outreach playbook.

**Result:** 12 months post-decision, accounts receiving the query-activation onboarding show NRR of 118% vs 104% for accounts that received the feature without behavioral activation. Query adoption becomes a leading indicator in the company's board-level metrics dashboard.

**Anti-Example:** Without mediation analysis, a competitor concludes "the AI feature drives retention" and focuses all engineering resources on expanding feature functionality (adding more query types, multimodal inputs). Despite a richer feature set, their NRR does not improve because adoption rates remain at 23%. They spent $4M solving a problem that was actually a change management and onboarding problem, not a feature depth problem.

---

### Scenario 2 — Management Consulting Engagement on Leadership Training ROI

**Trigger:** A global management consulting firm rolls out a leadership development program (LDP) for senior managers. Engagement scores improve by 12 points firm-wide. A partner questions whether the investment is justified: "We don't know if it's the training itself, the cohort bonding, or just Hawthorne effects. And I don't know if it works equally for new partners versus tenured ones."

**Analysis — Mediation:** Treatment = LDP participation (randomized assignment to cohorts). Mediator = Psychological Safety Score (measured 3 months post-training). Outcome = Engagement Score (measured 6 months post-training). IE = 0.44 × 0.61 = 0.268. TE = 0.35. PM = 77%. Direct effect c' = 0.082 (p=0.08, marginally significant). Partial mediation: training works primarily through building psychological safety, with some residual direct effect (possibly Hawthorne-type).

**Analysis — Moderation:** Moderator = Tenure Group (< 3 years vs ≥ 3 years at firm). Interaction term β3 = 0.29, p=0.003. Simple slopes: newer managers show treatment effect of +18 engagement points; tenured managers show +5 points. CATE ratio = 3.6x larger effect for newer cohorts.

**Decision:** Firm restructures LDP delivery: new managers (< 3 years) participate in the full 5-day residential cohort. Tenured managers shift to a 1-day psychological safety refresher. Cost per CATE-equivalent point of engagement improvement drops by 54%. Psychological safety interventions are deployed as the primary mechanism (mediator-focused) rather than generic leadership content.

**Result:** Firm saves 40% of LDP budget while sustaining engagement gains. Attrition among sub-3-year cohorts drops 6 percentage points in the following year, reducing replacement recruiting costs by approximately $2.1M across the firm.

**Anti-Example:** Without moderation analysis, the firm applies the full residential LDP uniformly. Tenured partners resent being pulled from client engagements for marginal benefit. Resistance spreads, reducing participation quality and eventually contaminating the program's effectiveness for new managers through peer signaling. Uniform rollout assumptions destroyed differentiated value.

---

### Scenario 3 — Growth Team: Notification Strategy for Fitness App (Source Scenario)

**Trigger:** A fitness app's growth team observes that push notification campaigns increase weekly workout frequency by 1.8 sessions on average. Monthly active user costs are rising and they need to decide where to invest: more notification personalization (mechanism) or broader user targeting (reach)?

**Analysis — Mediation:** Treatment = Push Notification Campaign activation. Mediator = App Opens per Week. Outcome = Weekly Workout Sessions. A path = 0.61 (notifications significantly increase app opens). B path = 0.58 (app opens significantly predict workouts controlling for notifications). IE = 0.61 × 0.58 = 0.354. TE = 0.38. PM = 93%. Direct effect c' = 0.026 (not significant). Near-full mediation: notifications work almost entirely through prompting app opens, which then convert to workouts. Notifications that do not result in an app open deliver essentially zero workout benefit.

**Analysis — Moderation:** Moderator = Platform Tenure (< 30 days vs ≥ 30 days). Interaction β3 = 0.47, p < 0.001. Simple slopes: new users show +3.2 workout sessions per week from notifications; long-term users show +1.1 sessions. Effect is 2.9x larger for new users.

**Decision:** Growth team implements a tiered notification strategy. New users (< 30 days) receive high-frequency, personalized notifications with deep links that maximize app open probability (targeting the mediator at its highest-yield moment). Long-term users receive lower-frequency, content-quality notifications. Notification budget redistributed 70/30 toward new user cohorts.

**Result:** App opens per campaign increase 34% for the targeted new user cohort. Weekly workout frequency for new users increases to +3.8 sessions, exceeding the pre-intervention average. 30-day retention (the most commercially critical metric) increases by 11 percentage points. Long-term user notification fatigue (unsubscribe rates) drops 18%.

**Anti-Example:** Without mediation analysis, the growth team invests $300K in AI-personalized notification copy and send-time optimization targeting all users equally. Copy personalization yields marginal gains in open rates (+4%) but does not change the fundamental mechanism. Long-term users' workout frequency is barely affected. CAC-to-LTV ratio worsens because budget was spread across low-yield segments. The team confuses message optimization for mechanism activation.

---

## Practitioner Playbook

### Phase 1 — Problem Formulation and DAG Construction

1. Define the causal question with precision: write it as "Does X cause Y?" (total effect), "How does X cause Y through M?" (mediation), or "For whom does X cause Y differently based on Z?" (moderation). A single study can address all three but they require explicit separate hypotheses.

2. Draw a Directed Acyclic Graph (DAG) before running any regression. List all plausible confounders of the X→Y relationship, all plausible confounders of the M→Y relationship, and all candidate moderators. The DAG is your causal map and determines which variables to control for.

3. Identify the mediator based on substantive theory, not exploratory data mining. Ask: "What is the mechanism through which the intervention is supposed to work according to domain knowledge?" Mining for mediators post-hoc inflates false discovery rates.

4. Confirm temporal ordering: treatment must precede the mediator, and the mediator must precede the outcome. In cross-sectional data this is impossible to verify statistically — use longitudinal design or panel data with lagged measurements whenever possible.

### Phase 2 — Data Requirements and Power Planning

5. Conduct a power analysis for the indirect effect (not just the direct effect). Use tools such as the Monte Carlo Power Analysis for Indirect Effects (MCPIE) or the powerMediation R package. Rule of thumb: n ≥ 200 for stable bootstrap estimates in simple mediation.

6. For moderation, calculate required sample size using G*Power for interaction effects. For small interactions (f² = 0.01) in field data, n ≥ 800 is often needed. Do not proceed with moderation analysis below n = 400 without explicit power caveats in your report.

7. Check for and document missing data patterns. Multiple imputation is appropriate if data is Missing At Random (MAR). Complete-case analysis is acceptable only if missingness is demonstrably random and below 10%.

### Phase 3 — Mediation Estimation

8. Run Baron-Kenny Step 1: Regress Y on X alone. Establish that the total effect (c path) exists and is significant. If c is not significant, mediation analysis can still be conducted (suppression effects exist), but note this prominently.

9. Run Baron-Kenny Step 2: Regress M on X alone. Establish the a path. If a is not significant, the mediator is not being activated by the treatment — stop and revise the mechanism hypothesis.

10. Run Baron-Kenny Step 3: Regress Y on both X and M simultaneously. Extract b (M's coefficient) and c' (X's coefficient in this model, the Direct Effect). If b is significant and c' is smaller than c, partial mediation is supported.

11. Estimate the Indirect Effect as IE = a × b. Run bootstrapping with 5,000–10,000 iterations to obtain the 95% confidence interval. Report: IE point estimate, 95% Bootstrap CI, Proportion Mediated (PM = IE/TE).

12. Conduct sensitivity analysis: use the R package "sensemakr" or Imai et al.'s sensitivity framework to determine how large an unmeasured confounder of M→Y would need to be to nullify the indirect effect. Report the sensitivity threshold to stakeholders as a credibility benchmark.

### Phase 4 — Moderation Estimation

13. Center continuous moderators (Z_c = Z − mean(Z)) before computing the interaction term X × Z_c. For binary moderators (e.g., enterprise vs SMB), use 0/1 dummy coding with the reference category explicitly defined.

14. Enter treatment (X), moderator (Z_c), and interaction (X × Z_c) into the outcome regression simultaneously. The coefficient on X × Z_c is the moderation effect (β3). Do not use hierarchical entry in separate steps for causal estimation — enter all terms together.

15. If β3 is significant, compute and plot simple slopes of X on Y at Z = mean−1SD, Z = mean, Z = mean+1SD (for continuous Z) or at Z=0 and Z=1 (for binary Z). Use the Johnson-Neyman technique to identify the precise range of Z at which the effect of X is significant.

16. Calculate and report the CATE for each key segment. Express CATEs in business units (e.g., revenue dollars, churn percentage points, engagement points) not just regression coefficients — this is what drives executive decisions.

### Phase 5 — Integration and Communication

17. Build an integrated narrative: "The intervention works (Total Effect = X). It works primarily through [Mediator] (IE = Y, PM = Z%). The effect is strongest for [Segment] (CATE = A vs B for [Moderator] high vs low)."

18. Translate statistical findings into intervention targets. The mediator identifies the proximate lever to engineer (onboarding flows, behavioral nudges, capability building). The moderator identifies the priority segment for resource concentration.

19. Design the follow-on experiment to test the mediation mechanism directly: randomize at the mediator level (if feasible) to eliminate residual confounding of the M→Y path. This is the gold standard for mechanism verification.

20. Document all analytical decisions, model specifications, and sensitivity results in a reproducible analysis script (R, Python, Stata). For consulting deliverables, archive the script alongside the deck so findings can be audited or updated when new data arrives.

---

## Content Critique & Depth Gaps

### What the Source Content Handles Well
The source content correctly frames the conceptual distinction between mediation and moderation, introduces the key vocabulary (mediator, moderator, direct effect, indirect effect), and provides concrete business examples that connect the statistics to decision-making. The fitness app scenario is particularly well-constructed because it addresses both mechanisms in a single integrated example.

### Critical Depth Gaps for IIM/HBS MBA Rigor

**1. Causal Identification Problem**
The source content treats mediation as a statistical procedure but does not address the fundamental identification problem: regression-based mediation estimates the total effect of the mediator on the outcome, not the causal effect, because the mediator is not randomly assigned. Without an instrument for the mediator or a design that randomizes both treatment and mediator, the indirect effect estimate is descriptive, not causal. IIM/HBS students need to understand why "controlling for a mediator" in regression does not solve this problem and why experimental mediation (randomizing the mechanism) or principal stratification approaches are needed for genuine causal claims.

**2. Post-Treatment Confounding and the Four-Way Decomposition**
The source content does not mention that including a post-treatment variable (the mediator) as a control in an outcome model can introduce collider bias if that variable is also a common effect of the treatment and an unmeasured confounder. The VanderWeele four-way decomposition separating controlled direct effects, pure indirect effects, reference interaction, and mediated interaction effects is missing and is essential for rigorous policy analysis.

**3. Moderated Mediation and Mediated Moderation**
The source content addresses mediation and moderation separately but does not cover their combination (moderated mediation: the mediation mechanism varies across moderator levels, and mediated moderation: the moderation effect is explained by a mediator). These are the most practically relevant configurations in product analytics and organizational consulting.

**4. Machine Learning Approaches to Heterogeneous Treatment Effects**
For high-dimensional moderator spaces (e.g., many user attributes simultaneously), classical interaction regression is insufficient. Causal Forest (Wager and Athey, 2018), BART (Bayesian Additive Regression Trees), and meta-learners (T-learner, S-learner, X-learner) are the state-of-practice methods for CATE estimation in tech companies. The source content does not mention any of these.

**5. Longitudinal and Panel Data Mediation**
Most business mediators (product usage, capability, satisfaction) are dynamic — they change over time. Cross-lagged panel models and structural equation modeling with latent growth curves are needed for time-varying mediation. The source content treats all analysis as single-time-point, which is a significant limitation for enterprise consulting where longitudinal data is the norm.

**6. Sensitivity Analysis Standards**
The source content does not specify sensitivity analysis methods for assessing robustness of mediation findings to unmeasured confounding. E-values (VanderWeele and Ding, 2017), the Imai sensitivity framework, and partial R² benchmarking are expected at HBS case study standards and are completely absent.

**7. Commercial Stakes and Sample Size Economics**
There is no discussion of the business economics of sample size investment — specifically, how to determine whether the incremental information from achieving sufficient power for moderation analysis (often requiring 2-4x more observations than the main effect analysis) is worth the data collection cost or experimentation delay. This cost-benefit framing is central to consulting engagements.

**8. Multiple Comparisons in Moderation**
When testing many moderators simultaneously (common in A/B testing platforms with rich user attribute data), the family-wise error rate inflates dramatically. The source content provides no guidance on Bonferroni correction, FDR control, or pre-registration as countermeasures — an omission that leads to false discovery in practice.

---

## Quick-Recall Card

**Mediation at a Glance**
- Mediator sits on the causal path: Treatment → Mediator → Outcome
- Total Effect = Direct Effect + Indirect Effect (TE = c' + a×b)
- Proportion Mediated = IE / TE; full mediation when PM ≈ 1.0
- Use bootstrapped CI (5,000+ iterations) for the indirect effect — not Sobel test alone
- Near-full mediation: engineering the mediator IS the product strategy; do not optimize the treatment in isolation

**Moderation at a Glance**
- Moderator changes the strength or direction of Treatment → Outcome; it is not caused by the treatment
- Test with interaction term: Y = β0 + β1·X + β2·Z + β3·(X·Z) + ε
- β3 significant and meaningful = heterogeneous treatment effects exist across segments
- Compute CATE at high/mean/low moderator; plot simple slopes; use Johnson-Neyman for continuous moderator
- Practical test: is the CATE difference large enough to change the deployment, pricing, or targeting strategy?

**Analytical Sequence**
- Draw DAG first → establish temporal ordering → power analysis → estimate total effect → test mediation → test moderation → estimate CATEs → sensitivity analysis → translate to intervention design

**Common Failure Modes**
- Labeling a variable a mediator based on correlation alone (not causal ordering)
- Conditioning on the mediator when estimating the total effect (blocks the indirect path)
- Interpreting a non-significant moderation test as proof of homogeneous effects (power problem)
- Reporting proportion mediated without absolute effect size and CI (obscures practical significance)
- Applying universal rollout when CATE analysis reveals 3x+ heterogeneity across segments

**Decision Rules**
- PM ≥ 0.80: redesign the intervention to target the mediator directly
- PM 0.40–0.79: maintain both direct and mediator-focused components
- PM < 0.40: mechanism is unclear; investigate alternative mediators before scaling
- CATE ratio ≥ 2x across moderator levels: differentiate strategy by segment
- β3 significant but CATE Δ < 0.20 SD: statistical moderation but not practically actionable

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Does this intervention work through a specific mechanism I can engineer at scale, and is that mechanism more powerful for one segment than another — because those two answers determine whether I optimize the product, the target, or both?"

---

## Self-Audit Report

<!-- Self-Audit:
WORKER: A6
FILE: 10-mediation-moderation-analysis.md
DATE: 2026-04-18
TARGET PATH: /Users/harshitpanikar/Documents/s_d_1/audit_management_course/causal-analysis-business/10-mediation-moderation-analysis.md

SECTION COMPLETION AUDIT:
1. Jargon Buster — COMPLETE. 12 terms provided (minimum was 8). All terms include Term, Plain-English Definition, and Why It Matters in Practice columns. Industry lens: IT/AI/Product/Consulting throughout.
2. Frameworks & Mental Models — COMPLETE. 4 frameworks provided, each with ASCII diagram. Frameworks cover: Mediation Path Diagram, Moderation Interaction Diagram, PROCESS Model Decision Tree, HTE Segmentation Matrix.
3. Formulas, Thresholds & Rules of Thumb — COMPLETE. Core mediation formulas, core moderation formulas, and rules-of-thumb table with thresholds and rationale. Context provided for each formula.
4. Do / Don't — COMPLETE. 10 Dos and 10 Don'ts provided (minimum was 8 each). All items are substantive and IIM/HBS MBA level.
5. Metric-Driven Scenarios with Anti-Examples — COMPLETE. 3 scenarios provided. Each follows Trigger → Analysis → Decision → Result → Anti-Example structure. Scenarios cover SaaS, Management Consulting, and Fitness App (source scenario).
6. Practitioner Playbook — COMPLETE. 20 numbered steps across 5 phases: Problem Formulation, Data Requirements, Mediation Estimation, Moderation Estimation, Integration and Communication.
7. Content Critique & Depth Gaps — COMPLETE. 8 substantive gaps identified with IIM/HBS rigor framing: causal identification, four-way decomposition, moderated mediation, ML approaches, longitudinal mediation, sensitivity analysis, sample size economics, multiple comparisons.
8. Quick-Recall Card — COMPLETE. Structured in thematic bullet groups. Final line begins exactly "As a PM/Consultant/AI Lead" as required. Role-lens question addresses mechanism engineering and segmentation simultaneously.
9. Self-Audit Report — COMPLETE (this section). HTML comment format as required.

CONNECTS TO: Links to related audit files noted below.

QUALITY CHECKS:
- File size: Substantially exceeds 13 KB minimum (estimated 18-20 KB)
- Industry lens: IT/AI/Product/Consulting maintained throughout all sections
- Role-lens question: Begins with exact phrase "As a PM/Consultant/AI Lead" — VERIFIED
- No sections omitted — VERIFIED
- Source content fully incorporated — VERIFIED
- Anti-examples present in all 3 scenarios — VERIFIED
- ASCII diagrams present in all frameworks — VERIFIED
- Bootstrapped CI and sensitivity analysis emphasized appropriately — VERIFIED

KNOWN LIMITATIONS:
- Moderated mediation formulas (Hayes PROCESS Models 7, 14, 58) not fully specified in Formulas section due to complexity; referenced in Framework 3 Decision Tree and Depth Gaps section
- Causal Forest and ML-based CATE estimation are flagged in Depth Gaps but not fully elaborated (appropriate for an audit gap section)
- Longitudinal mediation models (cross-lagged panel, SEM with latent growth) referenced in Depth Gaps but not demonstrated with formula (scope appropriate for gap identification)

STATUS: COMPLETE — all 9 mandatory sections written at IIM/HBS MBA depth.
-->

---

**Connects to:**
- `01-causation-vs-correlation.md` — foundational distinction between association and causal effect that underlies all mediation and moderation reasoning
- `02-directed-acyclic-graphs.md` — DAG methodology required for identifying valid adjustment sets in mediation analysis and avoiding collider bias
- `03-potential-outcomes-framework.md` — the Rubin causal model formalization of direct and indirect effects (controlled direct effects, natural direct/indirect effects)
- `04-randomized-controlled-trials.md` — experimental designs that enable clean identification of total effects; foundation for mediation experiments
- `05-instrumental-variables.md` — IV methods for identifying causal effects when mediators cannot be randomized; principal stratification approach to mediation
- `07-difference-in-differences.md` — DiD design for estimating heterogeneous treatment effects across groups (a moderation framework in panel data)
- `08-regression-discontinuity.md` — RD designs can be combined with heterogeneous effects analysis to identify CATEs near the threshold
- `09-interrupted-time-series.md` — longitudinal extension where mediators and moderators evolve over time, requiring time-varying effect models
- `11-causal-inference-observational-data.md` — observational settings where mediation analysis requires stronger identification assumptions and sensitivity analysis
- `12-heterogeneous-treatment-effects.md` — advanced CATE estimation using Causal Forests, meta-learners, and BART that extend the moderation framework to high-dimensional settings
