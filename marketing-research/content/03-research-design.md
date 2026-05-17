# Research Design

## Overview

Research design is the plan for how you will collect and use information. It answers: what data you need, from whom, how you’ll collect it, and how you’ll analyze it.

---

## Why It Matters

A strong design gives trustworthy results. A weak design leads to wrong conclusions and bad decisions.


## Key Principles

- Match design to the problem
- Decide data type: qualitative or quantitative
- Plan before collecting data (don’t “collect first, think later”)
- Reduce bias and errors


## Key Terms

| Term | Definition |
|------|------------|
| **Exploratory research** | Used when you don’t know the problem well |
| **Descriptive research** | Describes what is happening (who/what/where) |
| **Causal research** | Tests cause-and-effect (does X change Y?) |
| **Methodology** | Overall approach and techniques used |


## Use Case

A brand wants to know whether changing packaging will increase sales. It plans a test in select stores and compares results.


## Scenario

> A company wants to increase subscriptions. It first explores reasons (exploratory), then measures how common each reason is (descriptive), then tests a new pricing plan (causal).


## Examples

- Exploratory: focus groups to explore why people don’t trust a brand.
- Causal: A/B testing two ad versions to see which drives more clicks.

---

## Audited Appendix

# Research Design

**Course:** Marketing Research
**File Code:** MR-03
**Industry Lens:** IT / AI / Product / Consulting
**Connects to:** [01-introduction-to-marketing-research.md](./01-introduction-to-marketing-research.md) | [02-problem-definition.md](./02-problem-definition.md) | [04-data-collection-methods.md](./04-data-collection-methods.md) | [05-sampling.md](./05-sampling.md) | [06-questionnaire-design.md](./06-questionnaire-design.md)

---

## Overview

Research design is the master blueprint that governs how a study is structured, executed, and interpreted. It specifies what data is required, from whom, through which collection mechanism, and by what analytical approach the data will be converted into insight. In IT, AI, and product contexts, research design is not a one-time academic exercise — it is the governance layer that prevents teams from spending six weeks building the wrong feature, shipping an AI model trained on biased samples, or making a pricing change that alienates a high-value segment.

A weak design produces results that feel conclusive but are actually artifacts of methodological error. A strong design produces results you can defend in a boardroom, a court of law, or a peer-reviewed journal.

---

## 1. Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|------|--------------------------|---------------------------|
| **Exploratory Research** | Open-ended inquiry conducted when the problem is poorly understood; uses qualitative methods like interviews, focus groups, or ethnography to generate hypotheses rather than test them | In AI product development, exploratory research is the discovery sprint before roadmap lock — it prevents teams from building solutions to the wrong problem |
| **Descriptive Research** | Structured study that measures the frequency, distribution, or magnitude of a phenomenon; answers "how many," "how often," or "how much" | Quantifies the size of a problem before resource commitment; a SaaS PM uses descriptive research to confirm that 67 % of churning users cite onboarding friction, not pricing |
| **Causal Research** | Experimental or quasi-experimental design that establishes cause-and-effect relationships by manipulating one variable while controlling others | The gold standard for product decisions — A/B tests, multivariate tests, and randomized controlled trials (RCTs) are all causal designs; without causality you are pattern-matching, not deciding |
| **Research Methodology** | The overarching philosophical and procedural approach that governs how knowledge is gathered and validated (e.g., positivist quantitative vs. interpretivist qualitative) | Methodology determines what counts as evidence; a consulting firm needs to align on methodology before fielding a study or client deliverables will be contested |
| **Hypothesis** | A testable, falsifiable statement about the relationship between two or more variables | Forces precision before data collection; "engagement will increase" is not a hypothesis — "daily active usage will increase by 15 % within 30 days of the onboarding redesign" is |
| **Dependent Variable (DV)** | The outcome you are measuring; the "effect" in cause-and-effect | In a pricing experiment, DV = conversion rate; in an AI trust study, DV = user override rate of model recommendations |
| **Independent Variable (IV)** | The factor you manipulate or observe as the potential cause | In an A/B test of two onboarding flows, IV = onboarding version (A or B); everything else should be held constant |
| **Confounding Variable** | An unmeasured third variable that influences both IV and DV, producing a spurious relationship | Seasonal traffic spikes can confound a conversion A/B test run across Black Friday vs. January — the design must account for time as a confounder |
| **Internal Validity** | The degree to which the study design supports a causal conclusion within the study itself | High internal validity means the experiment was clean; low internal validity means the result could be due to design flaws, not the variable you changed |
| **External Validity** | The degree to which findings generalize beyond the study sample to the real-world population | A user study with 12 power users has low external validity for a mass-market app; always ask: "Who are we actually generalizing to?" |
| **Cross-Sectional Design** | A snapshot study that collects data from many subjects at one point in time | Useful for benchmarking; a product analytics team uses cross-sectional data to compare user cohorts on a given day, but cannot infer change over time |
| **Longitudinal Design** | Tracks the same subjects over time to observe change | Essential for churn modeling, LTV estimation, and AI model drift analysis; expensive but irreplaceable when temporal dynamics matter |

---

## 2. Frameworks & Mental Models

### 2.1 The Research Design Selection Matrix

Choose the design type based on two dimensions: (1) how well the problem is defined, and (2) whether you need to establish causality.

```
                         CAUSALITY NEEDED?
                          No            Yes
                    +------------+-------------+
  PROBLEM      Low  | Exploratory | Exploratory |
  DEFINITION        | (Phase 1)   | + Causal    |
  (Clarity)         |            | (Phase 1→3) |
                    +------------+-------------+
                High | Descriptive |   Causal   |
                     | (Survey /   |  (A/B Test /|
                     |  Analytics) |   RCT)     |
                    +------------+-------------+
```

**Rule:** Always ask "Do I know what I don't know?" before choosing a design. If the answer is no, start exploratory.

---

### 2.2 The Research Funnel (Diverge → Converge)

```
 WIDE (Exploratory)
 ___________________
 |                 |
 |  Interviews     |   <- Generate hypotheses; surface unknown unknowns
 |  Focus Groups   |
 |  Netnography    |
 |_________________|
         |
         V
 ________|________
 |               |
 |  Descriptive  |   <- Quantify hypotheses; estimate prevalence
 |  Survey / Log |
 |  Analytics    |
 |_______________|
         |
         V
    _____|_____
    |         |
    |  Causal |   <- Test cause-and-effect; validate intervention
    |  A/B    |
    |  RCT    |
    |_________|
         |
         V
     NARROW (Decision)
     Single defensible insight
     that drives a product/strategy choice
```

---

### 2.3 The PICOS Framework (for Research Design Scoping)

Used in rigorous evidence-based research; adapted here for product/AI contexts.

```
+-------+-----------------------------------------------+---------------------------+
| P     | Population / Participants                     | Who is in scope?          |
|       | (e.g., enterprise SaaS users on paid tier)    |                           |
+-------+-----------------------------------------------+---------------------------+
| I     | Intervention / Independent Variable           | What are you changing or  |
|       | (e.g., new AI recommendation engine)          | comparing?                |
+-------+-----------------------------------------------+---------------------------+
| C     | Comparison / Control                          | What is the baseline?     |
|       | (e.g., rule-based recommendation system)      |                           |
+-------+-----------------------------------------------+---------------------------+
| O     | Outcome / Dependent Variable                  | How will you measure      |
|       | (e.g., click-through rate, task completion)   | success?                  |
+-------+-----------------------------------------------+---------------------------+
| S     | Study Design / Setting                        | What methodology and      |
|       | (e.g., 4-week A/B test, 95 % CI required)     | context?                  |
+-------+-----------------------------------------------+---------------------------+
```

**PICOS forces precision before a single line of code is written.** Without it, a data science team will run an experiment and then argue retroactively about what "success" meant.

---

### 2.4 The Validity Quadrant

```
                    HIGH INTERNAL VALIDITY
                           |
         Lab / Controlled  |  RCT / Field Experiment
         Experiment        |  (Gold Standard)
                           |
  LOW                      |                       HIGH
  EXTERNAL  ---------------+---------------  EXTERNAL
  VALIDITY                 |                  VALIDITY
                           |
         Case Study /      |  Large-scale
         Expert Interview  |  Survey / Log Analysis
         (Rich but narrow) |  (Broad but correlational)
                           |
                    LOW INTERNAL VALIDITY
```

**Implication for AI teams:** Model evaluation on held-out test sets has high internal validity. Deployment in production has high external validity. Both are necessary; neither alone is sufficient.

---

### 2.5 The Confound Control Hierarchy

```
STRONGEST CONTROL
      |
      |   1. Randomized Assignment (RCT / A/B test)
      |      -- eliminates selection bias by design
      |
      |   2. Matched Pairs / Stratified Sampling
      |      -- controls for known confounders
      |
      |   3. Statistical Controls (Regression, ANCOVA)
      |      -- removes measured confounders post-hoc
      |
      |   4. Natural Experiments / Difference-in-Differences
      |      -- exploits exogenous variation when RCT is impossible
      |
      |   5. Cross-sectional Correlation
      |      -- observe only; confounders uncontrolled
      |
WEAKEST CONTROL
```

---

## 3. Formulas, Thresholds & Rules of Thumb

### 3.1 Minimum Detectable Effect (MDE)

Before running any experiment, calculate the smallest effect size worth detecting — this drives sample size.

```
MDE = Effect size that would change a business decision

Rule of Thumb:
  If detecting a 5 % lift matters → you need ~15,000 observations per variant (at 80 % power, 95 % CI)
  If detecting a 20 % lift is sufficient → you need ~1,000 observations per variant

Implication: Smaller effects require exponentially larger samples.
Do not run an experiment unless you can realistically gather the required N.
```

### 3.2 Sample Size Formula (Proportions)

```
n = (Z_alpha/2 + Z_beta)^2 * [p1(1-p1) + p2(1-p2)] / (p1 - p2)^2

Where:
  Z_alpha/2 = 1.96 for 95 % confidence
  Z_beta    = 0.84 for 80 % power
  p1        = baseline conversion rate
  p2        = expected conversion rate under intervention

Context: A SaaS onboarding experiment with baseline CTR = 10 %, 
expected lift to 13 %, requires:
  n = (1.96 + 0.84)^2 * [0.10*0.90 + 0.13*0.87] / (0.03)^2
  n ≈ 3,500 per variant → 7,000 total
```

### 3.3 Confidence Interval Interpretation

```
95 % CI means: If you repeated this study 100 times, 95 of the resulting 
intervals would contain the true population parameter.

It does NOT mean: "There is a 95 % chance the true value is in this interval."
(Common misinterpretation that leads to overconfident decisions)

Threshold Rule:
  CI does not cross zero (or 1.0 for ratios) → statistically significant
  CI is narrow → precise estimate
  CI is wide → high uncertainty; collect more data before deciding
```

### 3.4 Statistical Power Thresholds

```
Power = Probability of detecting a true effect when it exists

Standard Industry Thresholds:
  80 % power = minimum acceptable (consumer tech A/B tests)
  90 % power = recommended for high-stakes decisions (pricing, AI model rollout)
  95 % power = used in clinical / regulatory contexts

Warning: Running an experiment with insufficient power creates:
  1. False negatives (you miss real effects)
  2. Noisy estimates (when you do detect, the magnitude is unreliable)
```

### 3.5 Rule of Thumb: Exploratory Sample Sizes

```
Method               Min N      Saturation Rule
Depth Interviews      8–12      Stop when last 3 interviews yield no new themes
Focus Groups          2–3 groups  (6–8 participants each)
Card Sorting          15–20     Covers ~90 % of tree structures
Usability Testing     5         Detects ~85 % of major usability issues (Nielsen)
Diary Studies         8–15      Depending on duration and cognitive load
```

### 3.6 Cohen's d for Effect Size Interpretation

```
d = (Mean_treatment - Mean_control) / Pooled_SD

  d < 0.2  = Negligible effect (not worth acting on unless cost is near zero)
  d = 0.2  = Small effect (meaningful in large-scale digital product contexts)
  d = 0.5  = Medium effect (clear, replicable improvement)
  d = 0.8+ = Large effect (often signals a fundamental product change or 
              a serious pre-existing problem being solved)
```

---

## 4. Do / Don't

### DO

1. **Define your research question before touching any data.** Write the question as a single falsifiable sentence. If you cannot do this, you are not ready to design a study.
2. **Pre-register your hypothesis, design, and analysis plan** before data collection begins. This prevents p-hacking and HARKing (Hypothesizing After Results are Known) — a major integrity risk in AI/product research.
3. **Match design to the stage of knowledge.** Use exploratory designs when the landscape is uncertain; use causal designs only when you have well-defined hypotheses derived from prior research.
4. **Calculate required sample size before starting.** An underpowered study produces noise, not knowledge. Running an experiment you know is underpowered is worse than not running it.
5. **Identify and measure confounding variables in advance.** List every known factor that could co-vary with your IV and DV, then build controls into the design.
6. **Run a pilot study** before full-scale deployment. Even a 5 % pilot surfaces instrument failures, respondent misinterpretation, and data pipeline issues that would otherwise corrupt the entire study.
7. **Use mixed methods when appropriate.** Quantitative data tells you what is happening; qualitative data tells you why. For product decisions with significant investment implications, combine both.
8. **Document every design decision and its rationale.** Future stakeholders (legal, compliance, new team members) will need to reconstruct the study logic; undocumented studies cannot be defended or replicated.
9. **Plan the analysis before collecting data.** The statistical tests you will use must be consistent with the study design — you cannot decide to run a regression after seeing the data because "it fits better."
10. **Consider the unit of randomization.** In network-effect products (social apps, B2B collaboration tools), individual-level randomization creates contamination. Use cluster randomization instead.

### DON'T

1. **Don't start with the data you have and work backward to a question.** This is HARKing — it inflates false discovery rates and produces conclusions that do not replicate.
2. **Don't confuse correlation with causation in dashboards.** Product analytics tools (Mixpanel, Amplitude) show correlations; they do not establish causality. An A/B test is required for causal claims.
3. **Don't use convenience samples and generalize broadly.** Testing a new AI feature only with internal employees or power users will produce results that do not hold for the general user base.
4. **Don't run multiple A/B tests simultaneously without accounting for interaction effects.** Two concurrent tests can interfere with each other, especially when they touch the same user journey.
5. **Don't stop an experiment early because the numbers "look good."** Peeking at results and stopping at the first significant p-value inflates Type I error dramatically — this is called optional stopping and it is a major form of research misconduct in product analytics.
6. **Don't ignore practical significance in favor of statistical significance.** With millions of users, trivially small effects become statistically significant. Ask: is this effect large enough to change a decision?
7. **Don't let qualitative research replace quantitative validation.** Five interviews can generate rich hypotheses; they cannot validate that 40 % of your user base holds that view.
8. **Don't design surveys before defining the analysis plan.** Every question on a survey should map to a specific analytical output. Surveys designed without an analysis plan produce data graveyards.
9. **Don't assume a failed experiment means the intervention doesn't work.** It may mean the experiment was underpowered, ran too short, used the wrong outcome metric, or was confounded. Diagnose before abandoning the hypothesis.
10. **Don't skip ethical review for human-subjects research.** In AI contexts, this includes data sourcing, model training on user behavior, and experiments that alter user experience — all require ethical scrutiny, not just IRB compliance.

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: AI Feature Adoption Study at a B2B SaaS Company

**Trigger:** Product analytics shows that only 18 % of enterprise accounts have activated the AI-assisted contract review feature 90 days post-launch, despite a 70 % awareness rate among account administrators.

**Analysis:** Awareness is not the bottleneck (70 % is high). The gap between awareness and activation suggests friction in the adoption journey. The team runs exploratory research (8 in-depth interviews with non-activating administrators) and identifies three themes: (a) IT security review delays, (b) uncertainty about AI accuracy thresholds, and (c) lack of workflow integration with existing contract management tools. A descriptive survey (n = 340, stratified by company size and industry) confirms that 61 % cite IT security review as the primary barrier, 28 % cite accuracy concerns, and 11 % cite integration gaps.

**Decision:** The team re-designs the activation flow to include a pre-built IT security checklist and an accuracy benchmarking report. A causal A/B test (n = 2,200 per variant, 6-week duration) is launched against non-activated accounts. Primary DV = activation within 30 days. Secondary DV = time-to-first-document-review.

**Result:** Treatment group shows 34 % activation vs. 19 % in control (p < 0.001, d = 0.38, practical significance confirmed by 15 pp lift). The security checklist alone accounts for 72 % of the effect, confirmed by an interaction analysis.

**Anti-Example:** A competing internal team skips the exploratory phase and directly A/B tests a new email drip campaign offering a 30-day free extension. Activation moves from 18 % to 20 % (p = 0.04, but 95 % CI: 0.5 pp to 3.5 pp). The team declares success, the intervention is rolled out, and the underlying friction (IT security review) is never addressed. Six-month activation remains below 25 %.

---

### Scenario 2: Pricing Experiment for an AI Consulting Retainer

**Trigger:** A consulting firm's AI transformation practice has a win rate of 31 % on proposals, below the 45 % target. Client feedback is mixed and unsystematic. The hypothesis is that pricing architecture (fixed fee vs. outcome-based fee) influences win rate.

**Analysis:** Exploratory phase: 10 interviews with lost-deal contacts reveal that procurement teams in financial services consistently flag fixed-fee structures as difficult to justify internally, while outcome-based models align with their ROI-approval processes. Descriptive phase: CRM analysis of 180 closed deals (won and lost) over 24 months confirms that outcome-based proposals have a 47 % win rate vs. 28 % for fixed-fee — but this is correlational; the firm may have used outcome-based pricing selectively for stronger deals.

**Decision:** A quasi-experimental design is used (full RCT is not feasible given deal-level complexity). A difference-in-differences analysis compares win rates before and after a deliberate policy change: all proposals to financial services clients with deal size > $500K are shifted to outcome-based pricing. A matched control group (comparable deal size, industry = professional services) retains fixed-fee pricing. Pre-period: 12 months. Post-period: 9 months.

**Result:** DiD estimate: +16 pp win rate improvement attributable to pricing architecture (95 % CI: +9 pp to +23 pp). Average deal size increases by 12 % due to alignment with client ROI approval gates.

**Anti-Example:** The firm's business development lead reviews the CRM data and concludes "outcome-based pricing wins more deals" from the raw correlation (47 % vs. 28 %). She mandates outcome-based pricing for all deals. Large consulting engagements with government clients — where outcome-based pricing is contractually prohibited — begin to stall. The firm's overall win rate drops to 26 % before the error is diagnosed.

---

### Scenario 3: Research Design for AI Model Bias Audit

**Trigger:** An internal audit flags that the company's AI-powered resume screening model has an approval rate of 68 % for male applicants vs. 51 % for female applicants on equivalent qualification profiles. Legal requests a defensible research design to determine whether the disparity is caused by the model or by pre-existing application patterns.

**Analysis:** This requires a causal design. A synthetic audit study is commissioned: 500 matched resume pairs are constructed (identical qualifications, experience, and education; names randomized across gender-typical and gender-neutral categories). Resumes are submitted to the screening model and the pre-AI human screening process. DV = screening pass rate. IV = applicant gender signal (name). Confounders controlled: job function, seniority level, applicant volume period.

The study finds: (a) the AI model produces a 14 pp disparity (statistically significant, d = 0.31), (b) the human screening process produces a 9 pp disparity, and (c) the AI model amplifies pre-existing human bias rather than introducing entirely new bias. Root-cause analysis traces the amplification to training data from 2014–2018, a period with high human-reviewer gender disparity.

**Decision:** The model is retrained on a de-biased dataset with calibrated post-processing thresholds. A longitudinal monitoring design is established: monthly synthetic audit submissions (n = 50 per run) to track disparity drift. Threshold: if disparity exceeds 5 pp in two consecutive months, automatic escalation to the AI Ethics Review Board.

**Result:** After retraining, disparity drops to 3.2 pp (not statistically significant at 95 % CI). The longitudinal monitoring design catches a drift event 7 months later (caused by a new feature engineering change) before it reaches 5 pp in production traffic.

**Anti-Example:** The legal team reviews aggregate hiring outcome data and finds that the overall hire rate across genders is 4.8 % vs. 4.6 % — not statistically significant. They conclude the model is unbiased and close the audit. The aggregate analysis obscures the disparity at the screening stage (top of funnel), which is masked by compensating human review decisions downstream. The bias continues undetected until a regulatory inquiry 18 months later.

---

## 6. Practitioner Playbook

A step-by-step research design process for IT/AI/Product/Consulting contexts.

**Phase 0: Alignment (Days 1–3)**

1. Convene the decision-maker and the research lead. Write the business decision that this research will inform — one sentence. Example: "We will decide whether to invest $2M in rebuilding the onboarding flow."
2. Write the research question derived from that decision — one falsifiable sentence.
3. Identify the decision deadline and work backward to establish the research timeline. Research that arrives after a decision has been made is waste.
4. Confirm who will consume the research output and what format they require (slide deck, statistical report, dashboard, verbal brief).

**Phase 1: Design Selection (Days 3–5)**

5. Assess the current state of knowledge using the Research Design Selection Matrix (Framework 2.1). Is the problem well-defined? Is causality required? Select design type accordingly.
6. If exploratory: define the number of interviews, topic guide structure, and recruitment criteria. Specify the point of saturation (the criterion for stopping data collection).
7. If descriptive: define the survey instrument draft, sampling frame, and required n. Map every survey question to a specific analytical output.
8. If causal: complete a PICOS document (Framework 2.3). Calculate MDE, required sample size, and experiment duration before proceeding.

**Phase 2: Confound and Validity Planning (Days 5–7)**

9. List every known confounding variable. For each, specify the control mechanism (randomization, matching, statistical control, or natural experiment design).
10. Evaluate internal validity threats using the Campbell-Stanley checklist: history effects, maturation, testing effects, instrumentation changes, regression to the mean, selection bias, attrition.
11. Evaluate external validity: to whom and to what context do you intend to generalize? Confirm the sample matches that population on key dimensions.

**Phase 3: Instrument Design (Days 7–14)**

12. For surveys: use validated scales where available (e.g., NPS, SUS, CSAT, TAM). Pilot with 10–15 respondents from the target population. Revise based on comprehension and completion rate.
13. For interviews: develop a topic guide, not a script. Include probing questions. Brief all interviewers on protocol consistency.
14. For experiments: define the technical implementation spec. Specify the randomization unit (user, session, account, geography). Define the holdout period and any novelty-effect correction.
15. Define the primary outcome metric and all secondary metrics in advance. Lock these in writing before the study begins.

**Phase 4: Pilot and Quality Assurance (Days 14–17)**

16. Run a 5 % pilot of the full study. Check: data pipeline integrity, instrument comprehension, dropout rates, and whether the primary metric is being captured correctly.
17. Conduct a data quality audit: check for missing values, duplicate responses, speeders (survey completions under 1/3 of median time), and bot responses.
18. If pilot reveals instrument problems, revise and re-pilot before full launch.

**Phase 5: Data Collection (Duration per design)**

19. Monitor data collection in real time. Set up automated alerts for anomalies (sudden spikes in dropout, unexpected demographic shifts in respondents, data pipeline failures).
20. Do not peek at outcome results during an experiment. Appoint a designated analyst who reviews data quality only (not outcomes) during the collection period.
21. Document every deviation from the pre-registered design as it occurs, with a timestamp and rationale.

**Phase 6: Analysis and Interpretation (Post-collection)**

22. Run the pre-specified analysis plan. Do not change analytical approach based on preliminary results without explicit documentation and rationale.
23. Report effect sizes and confidence intervals, not just p-values. A p-value without an effect size is an incomplete result.
24. Conduct sensitivity analyses: what happens to the conclusion if you exclude outliers? If you use a different model specification? If you apply a Bonferroni correction for multiple comparisons?
25. Separate statistical significance from practical significance. Ask: is this effect large enough to change the business decision?

**Phase 7: Synthesis and Communication (Post-analysis)**

26. Write the insight as a one-sentence recommendation tied to the original business decision. Avoid burying it in caveats.
27. Include a limitations section that is honest about what the design cannot establish.
28. Archive all materials: pre-registration document, instruments, raw data (anonymized), analysis code, and final report. This is the audit trail for replication and defense.

---

## 7. Content Critique & Depth Gaps

The source content provides an accurate but surface-level introduction to research design. The following gaps must be addressed to reach IIM/HBS MBA-level rigor:

**Gap 1: No treatment of validity threats.**
The source content does not mention internal validity, external validity, or construct validity. At an advanced level, research design is fundamentally about managing validity trade-offs. The Campbell-Stanley threats to internal validity (history, maturation, instrumentation, selection, attrition, regression to the mean) are foundational and conspicuously absent.

**Gap 2: No discussion of the unit of analysis problem.**
In IT/AI/product contexts, the unit of analysis (user, session, account, market) is a critical design decision with direct statistical implications. Randomizing at the wrong unit creates pseudo-replication and inflates false-positive rates. This is a common and costly error in product experimentation programs.

**Gap 3: No treatment of network effects and interference.**
In social and collaborative products, the Stable Unit Treatment Value Assumption (SUTVA) is routinely violated — users in control groups are influenced by users in treatment groups. The source does not acknowledge this problem, which is critical for any company operating a network-effect product.

**Gap 4: Missing statistical power framework.**
The source does not mention statistical power, Type I error, or Type II error. This is a significant omission for anyone running experiments. A study without a power calculation is not a study — it is a data collection exercise with unknown interpretive value.

**Gap 5: No discussion of pre-registration and research integrity.**
In AI/product contexts, p-hacking (running multiple analyses until one is significant) and HARKing (Hypothesizing After Results are Known) are pervasive. Pre-registration — committing to a hypothesis and analysis plan before data collection — is the primary defense. The source does not mention it.

**Gap 6: No coverage of longitudinal vs. cross-sectional trade-offs.**
Understanding whether a phenomenon is stable or dynamic requires different designs. In AI contexts, model drift, user behavior change, and market evolution are longitudinal phenomena. Cross-sectional snapshots systematically miss these dynamics.

**Gap 7: No ethical framework.**
Research design in AI and product contexts raises ethical questions (consent, data use, vulnerable populations, experimental harm) that are absent from the source. At HBS/IIM level, ethics is a design constraint, not a post-hoc consideration.

**Gap 8: No discussion of secondary data and mixed-methods integration.**
The source implies primary data collection is the default. In practice, most research begins with secondary data (product analytics, CRM data, market reports) and primary data is used to fill gaps. The source does not address this sequencing.

**Gap 9: Absence of Bayesian alternatives.**
The source assumes frequentist statistics. In product experimentation at scale, Bayesian A/B testing (which allows updating beliefs as data arrives and does not require a fixed sample size) is increasingly standard. At MBA level, students should understand when to use each approach.

**Gap 10: No connection to decision theory.**
Research design choices are fundamentally economic decisions — you invest resources to reduce decision uncertainty. The value of information framework (Expected Value of Perfect Information, EVPI) provides a rational basis for deciding how much to invest in research vs. acting on existing knowledge. This is absent.

---

## 8. Quick-Recall Card

- Research design = the blueprint that governs what data is collected, from whom, how, and how it will be analyzed.
- Three design types: Exploratory (discover), Descriptive (measure), Causal (prove cause-and-effect).
- Always match design to the state of knowledge — do not run a causal study when you don't yet know what to test.
- The PICOS framework (Population, Intervention, Comparison, Outcome, Study design) forces precision before any study begins.
- Calculate MDE and required sample size before committing to an experiment — an underpowered study is worse than no study.
- Internal validity = clean design (you proved what you claimed). External validity = generalizable findings (it holds in the real world).
- The Confound Control Hierarchy: Randomization > Matching > Statistical Control > Natural Experiment > Correlation only.
- Pre-register your hypothesis and analysis plan before collecting data to prevent p-hacking and HARKing.
- Statistical significance is not practical significance — always report effect sizes and confidence intervals.
- In network-effect products, randomize at the cluster level (geography, account) not the individual level to avoid contamination.
- Mixed methods: qualitative discovers and explains, quantitative validates and quantifies — both are necessary for high-stakes decisions.
- The research timeline must be governed by the decision deadline — late research is waste, however rigorous.
- Five usability test participants reveal ~85 % of major issues (Nielsen); more are needed for quantitative claims.
- Longitudinal designs are essential when the phenomenon of interest changes over time (model drift, churn, LTV).
- Every deviation from a pre-specified design must be documented with a timestamp — this is your audit trail.

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Have I chosen a research design that can actually produce the level of evidence (exploratory insight, descriptive magnitude, or causal proof) required to make this specific business decision, and can I defend both the design and the conclusion to a skeptical senior stakeholder?"

---

## 9. Self-Audit Report

<!-- Self-Audit:
  File: 03-research-design.md
  Auditor Role: Worker A4
  Date Completed: 2026-04-18
  Industry Lens Applied: IT / AI / Product / Consulting — confirmed throughout all sections.

  Section Completion Check:
  [PASS] Section 1 — Jargon Buster: 12 terms provided (minimum 8 required). All terms include plain-English definition and practical relevance in IT/AI/Product/Consulting context.
  [PASS] Section 2 — Frameworks & Mental Models: 5 frameworks provided, each with ASCII diagram. Frameworks include Research Design Selection Matrix, Research Funnel, PICOS, Validity Quadrant, and Confound Control Hierarchy.
  [PASS] Section 3 — Formulas, Thresholds & Rules of Thumb: 6 entries including MDE, sample size formula, CI interpretation, statistical power thresholds, exploratory sample size rules of thumb, and Cohen's d effect size interpretation. All include contextual explanation.
  [PASS] Section 4 — Do / Don't: 10 items on each side (minimum 8 required). All items are specific, actionable, and relevant to IT/AI/Product/Consulting contexts.
  [PASS] Section 5 — Metric-Driven Scenarios with Anti-Examples: 3 complete scenarios provided. Each includes Trigger, Analysis, Decision, Result, and Anti-Example as required. Scenarios cover AI feature adoption, pricing experiment, and AI model bias audit.
  [PASS] Section 6 — Practitioner Playbook: 28 numbered steps across 7 phases. Each step is actionable and grounded in IT/AI/Product/Consulting practice.
  [PASS] Section 7 — Content Critique & Depth Gaps: 10 gaps identified covering validity threats, unit of analysis, network effects, statistical power, pre-registration, longitudinal design, ethics, secondary data, Bayesian alternatives, and decision theory. Explicitly addresses what is missing for IIM/HBS MBA depth.
  [PASS] Section 8 — Quick-Recall Card: 15 bullet points. Final sentence begins with exact required phrase: "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ____."
  [PASS] Section 9 — Self-Audit Report: This section. Formatted as HTML comment as required.

  Connects-to Links: 5 related audit files linked in the header.
  Estimated File Size: Well above 13 KB minimum.
  Tone and Depth: MBA-level rigor throughout. No generic filler. Every section contains specific, defensible, practitioner-grade content.
  Known Limitations: Bayesian A/B testing and EVPI are mentioned in Section 7 (gaps) but not developed in full in earlier sections — this is by design as the source content does not cover them and expanding fully would exceed the scope of an audit file for this specific topic.
  Overall Assessment: PASS — all mandatory sections present, all minimums met or exceeded, industry lens consistently applied, file is substantive and defensible at IIM/HBS MBA level.
-->
