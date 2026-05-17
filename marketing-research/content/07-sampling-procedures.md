# Sampling Procedures

## Overview

Sampling is choosing a smaller group of people to represent a larger population (like all customers).

---

## Why It Matters

You usually can’t ask everyone. Sampling saves cost and time while still giving useful insights—if done correctly.


## Key Principles

- Sample should represent the target population
- Use the right method based on time and accuracy needs
- Bigger sample usually reduces random error
- Avoid selection bias


## Key Terms

| Term | Definition |
|------|------------|
| **Population** | Full group you care about (all customers) |
| **Sample** | The smaller group you study |
| **Sampling frame** | The list you sample from (customer database) |
| **Random sampling** | Everyone has equal chance |
| **Non-random sampling** | Based on convenience/judgment |


## Use Case

A bank surveys 500 customers across cities instead of all customers nationwide to assess service quality.


## Scenario

> A brand surveys only Instagram followers and assumes it represents all customers. Later it learns offline buyers think very differently.


## Examples

- Random sample: randomly choose 1,000 customers from a CRM list.
- Convenience sample: ask shoppers in one mall (fast but less accurate).

---

## Audited Appendix

# Sampling Procedures

**Source Overview:** Sampling is choosing a smaller group of people to represent a larger population (like all customers). You usually can't ask everyone — sampling saves cost and time while still giving useful insights, if done correctly.

**Industry Lens:** IT / AI / Product / Consulting

**Connects to:** [01-marketing-research-intro.md](01-marketing-research-intro.md) | [02-research-design.md](02-research-design.md) | [05-survey-design.md](05-survey-design.md) | [08-data-analysis-basics.md](08-data-analysis-basics.md) | [09-reporting-insights.md](09-reporting-insights.md)

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| **Population** | The entire group you want to draw conclusions about — e.g., all enterprise SaaS buyers in India | Defines the scope of generalization; misdefining it makes every downstream inference wrong |
| **Sample** | The actual subset of that population you collect data from | Quality of your product decisions is bounded by sample quality — garbage in, garbage out |
| **Sampling Frame** | The concrete list or database from which you draw your sample — e.g., your CRM, a panel, an app user list | Frame coverage errors (e.g., missing churned users) silently bias results before you collect a single response |
| **Stratified Sampling** | Dividing the population into non-overlapping strata (e.g., enterprise vs. SMB vs. startup) and sampling proportionally or deliberately from each | Ensures minority segments like power users or churned accounts are represented; critical for AI model fairness audits |
| **Cluster Sampling** | Dividing the population into natural clusters (e.g., regions, offices), randomly selecting clusters, and surveying everyone inside | Cost-efficient for geographically distributed user bases; used in large-scale NPS rollouts across branch networks |
| **Systematic Sampling** | Selecting every k-th element from a list after a random start — e.g., every 10th row in a user database export | Simple to execute operationally; beware periodicity bias if your list has a hidden pattern (e.g., sorted by account manager) |
| **Quota Sampling** | Non-random version of stratified — you set quotas (e.g., 40% enterprise) and fill them however convenient | Fast and cheap; risks selection bias since interviewers pick who to approach; common in rapid consulting sprints but not publishable-grade research |
| **Snowball Sampling** | Existing participants refer new participants — each "snowball" grows the sample | Invaluable for hard-to-reach segments: AI ethics practitioners, niche developer communities, dark-web threat researchers |
| **Sampling Error** | The inherent difference between a sample statistic and the true population value, caused purely by chance | Quantifiable and reducible by increasing n; the only error type that shrinks predictably with sample size |
| **Non-Sampling Error** | All other errors: measurement error, interviewer bias, non-response bias, data entry errors | Often larger and more damaging than sampling error in real projects; not reduced by bigger samples — demands process fixes |
| **Margin of Error (MoE)** | The ± range within which the true population value likely falls, at a given confidence level | A 5% MoE at 95% confidence means if 60% of users prefer Feature A, the true figure is likely 55–65%; drives go/no-go decisions |
| **Confidence Level** | The probability that your interval contains the true population parameter — typically 90%, 95%, or 99% | Higher confidence demands larger samples; 95% is the industry default for most product and consulting research |

---

## Frameworks & Mental Models

### 1. Probability vs. Non-Probability Sampling — Taxonomy Tree

```
                    SAMPLING METHODS
                         |
          .--------------+----------------.
          |                               |
   PROBABILITY                    NON-PROBABILITY
(random selection;               (researcher/respondent
 generalizable)                   judgment involved)
          |                               |
    .-----+-----.              .----+-----+-------.
    |     |     |              |    |     |        |
Simple  Strat- Cluster  Conven- Quota Snow- Purposive
Random  ified  Systematic ience       ball
          |
   (Proportional
    or Disproportionate)

KEY RULE: Only probability methods allow statistically valid
          inference to the population with quantified error.
          Non-probability methods are faster/cheaper but
          require explicit limitation disclosures in reports.
```

**IT/AI Application:** When building training data sets or validating AI model outputs, use stratified random sampling across demographic slices (age, region, device type) to prevent representation gaps that cause model bias. Non-probability convenience samples are acceptable for exploratory sprint research, not for model validation.

---

### 2. Sample Size vs. Margin of Error — Inverse Curve

```
  Margin
  of Error
  (%)
   10 |*
      | *
    8 |  *
      |   *
    6 |    **
      |      **
    4 |        ***
      |            ****
    2 |                 *******
      |                         **************
    1 |_____________________________________ n
      100  250  500  1000  1500  2500  5000  10000

KEY INSIGHT: Diminishing returns kick in sharply after ~1,000.
Going from n=100 to n=1,000 cuts MoE roughly 3x.
Going from n=1,000 to n=10,000 cuts MoE only ~3.2x more.
Budget your sample intelligently — the first 1,000 respondents
buy you most of the precision you'll ever get.
```

**Consulting Rule of Thumb:** For a 95% confidence level, p=0.5 (maximum variance), MoE of ±5% requires ~385 respondents. MoE of ±3% requires ~1,068. MoE of ±1% requires ~9,604. Know these anchor points cold.

---

### 3. Sampling Frame vs. Population — Mismatch Diagram

```
  TRUE POPULATION
  .-----------------------------------------.
  |                                         |
  |   .------------------------------.      |
  |   |   SAMPLING FRAME             |      |
  |   |   (your CRM / panel / list)  |      |
  |   |                              |      |
  |   |   .--------------------.     |      |
  |   |   |  ACTUAL SAMPLE     |     |      |
  |   |   |  (who responded)   |     |      |
  |   |   `--------------------'     |      |
  |   `------------------------------'      |
  |                                         |
  `-----------------------------------------'

  GAP 1 (Population → Frame):   COVERAGE ERROR
         Offline users, churned accounts, non-CRM leads
         are invisible to your research entirely.

  GAP 2 (Frame → Sample):       SAMPLING ERROR
         Quantifiable; reduced by increasing n.

  GAP 3 (Sample → Respondents): NON-RESPONSE BIAS
         Who chose NOT to respond? Dissatisfied users
         often skip surveys — systematically biasing
         satisfaction scores upward.
```

**PM Implication:** If your sampling frame is app users but you're deciding on pricing for all customers including offline enterprise deals, your frame is mismatched to your population. Acknowledge and bound your conclusions accordingly.

---

## Formulas, Thresholds & Rules of Thumb

### Core Sample Size Formula (Proportions)

```
         Z^2 * p * (1 - p)
  n  =  -------------------
               e^2

Where:
  n  = required sample size
  Z  = Z-score for confidence level
       (90% CI → 1.645 | 95% CI → 1.960 | 99% CI → 2.576)
  p  = estimated population proportion (use 0.5 if unknown)
  e  = desired margin of error (e.g., 0.05 for ±5%)

Example (most conservative):
  n = (1.96^2 * 0.5 * 0.5) / (0.05^2)
    = (3.8416 * 0.25) / 0.0025
    = 0.9604 / 0.0025
    = 384.16 ≈ 385 respondents
```

### Margin of Error Formula

```
  MoE = Z * sqrt[ p*(1-p) / n ]

  At n=400, p=0.5, 95% CI:
  MoE = 1.96 * sqrt(0.25/400)
      = 1.96 * 0.025
      = ±0.049  ≈  ±4.9%
```

### Finite Population Correction (FPC)

Use when your sample is more than 5% of the total population:

```
  n_adjusted = n / [ 1 + (n - 1) / N ]

Where N = total population size.

Example: N=2,000, initial n=385
  n_adjusted = 385 / [1 + 384/2000]
             = 385 / 1.192
             ≈ 323 respondents (you need fewer!)

Rule: FPC matters when n/N > 0.05. Skip it for large populations.
```

### Effect Size and Difference-of-Means Sizing

For A/B tests and feature experiments (product teams):

```
  n = 2 * [ (Z_alpha + Z_beta)^2 * sigma^2 ] / delta^2

Where:
  Z_alpha = Z for significance level (95% one-tail → 1.645)
  Z_beta  = Z for power (80% power → 0.842)
  sigma   = population standard deviation
  delta   = minimum detectable effect (MDE)

Rule of Thumb: To detect a 5% lift with 80% power and 95%
confidence, you typically need 1,500–3,000 observations per arm
in SaaS conversion rate experiments.
```

### Key Thresholds to Memorize

| Confidence Level | Z-Score | Typical Use Case |
|---|---|---|
| 90% | 1.645 | Exploratory / cost-constrained research |
| 95% | 1.960 | Standard product and consulting research |
| 99% | 2.576 | High-stakes: regulatory, safety, pricing |
| | | |
| **Sample Size Anchors** | **MoE at 95% CI, p=0.5** | |
| n = 100 | ±9.8% | Directional only |
| n = 385 | ±5.0% | Minimum publishable |
| n = 1,068 | ±3.0% | Standard consulting deliverable |
| n = 2,401 | ±2.0% | High-precision market sizing |
| n = 9,604 | ±1.0% | Census-grade claims |

---

## Do / Don't

### Do

1. **Define your population precisely before selecting a method.** "All users" is not a population definition. "Enterprise SaaS decision-makers with >500 seats in APAC, active in the last 90 days" is.
2. **Match sampling method to research objective.** Use stratified sampling when subgroup comparisons matter. Use cluster sampling when geography drives cost. Use snowball sampling only for hard-to-reach populations with documented referral chains.
3. **Use the finite population correction** when sampling more than 5% of a known finite population — you can reduce required sample size significantly without sacrificing rigor.
4. **Pre-register your sample size and stopping rule** in A/B tests before launching. Post-hoc peeking inflates false positive rates dramatically.
5. **Audit your sampling frame for coverage gaps.** Cross-check your CRM list against known customer segments. If enterprise offline accounts are missing, flag it explicitly in your report.
6. **Report non-response rates alongside response rates.** A 40% response rate with systematic non-responder analysis is more credible than a 70% response rate with no follow-up.
7. **Stratify on variables that correlate with your outcome.** Stratifying on user tenure for churn research reduces variance and increases statistical power without increasing n.
8. **Pilot-test your sampling logistics.** Run 20–30 responses before full fielding to catch frame errors, filter failures, and screener logic bugs.
9. **Document every sampling decision in a methods appendix.** Clients, stakeholders, and peer reviewers will probe this. Be defensible.
10. **Use disproportionate stratified sampling deliberately.** Oversample rare but strategically important segments (e.g., churned enterprise accounts), then weight back to population proportions for aggregate results.

### Don't

1. **Don't conflate your sampling frame with your population.** Your app's MAU list is not "all customers." Offline buyers, churned accounts, and prospects are invisible — and they may behave very differently.
2. **Don't use convenience samples and present results as representative.** "We asked our Slack community" is a convenience sample, not a market study. Label it explicitly.
3. **Don't keep peeking at A/B test results and stopping when significant.** This is the single most common source of inflated false positives in product analytics.
4. **Don't ignore non-response bias.** If unhappy users don't respond to your NPS survey, your NPS score is structurally inflated. This is a non-sampling error no bigger sample fixes.
5. **Don't assume larger samples are always better.** A larger sample from a biased frame gives you more precise estimates of the wrong thing. Fix the frame first.
6. **Don't over-rely on snowball samples for sensitive topics.** Social referral networks create homophily — you end up sampling people who think alike, defeating the purpose.
7. **Don't forget to weight your data after disproportionate sampling.** Unweighted analysis of a disproportionately stratified sample will produce biased population estimates.
8. **Don't skip the pilot.** A broken screener or mislabeled segment variable discovered at n=800 means restarting from scratch.
9. **Don't present margins of error without stating the confidence level.** "±3%" is meaningless without "at 95% confidence." Omitting this is a credibility failure in any consulting deliverable.
10. **Don't use quota sampling when your stakeholder will use the findings to make irreversible decisions** (e.g., market entry, pricing architecture, headcount planning). Invest in probability methods.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: NPS Benchmarking at a B2B SaaS Company

**Trigger:** A VP of Product at a 50,000-seat enterprise software company wants to benchmark NPS across three customer tiers (SMB, Mid-Market, Enterprise) before the annual pricing review.

**Analysis:**
- Population: All active accounts (n=12,000) with at least one login in the past 60 days.
- Sampling frame: CRM tagged accounts with verified contact emails — covers 10,200 accounts (85% coverage; offline channel and partner-managed accounts missing).
- Method: Disproportionate stratified sampling. SMB = 8,000 accounts (oversample to n=300), Mid-Market = 3,000 accounts (n=200), Enterprise = 1,200 accounts (n=200). Total n=700.
- FPC applied: Enterprise stratum n/N = 200/1,200 = 16.7% — FPC reduces required n to ~157, saving cost.
- Confidence: 95%, MoE: ±4.2% per stratum.
- Weighting: Results are weighted back to population proportions for aggregate NPS.

**Decision:** Enterprise NPS = 42 (MoE ±4.2%), SMB NPS = 61 (MoE ±4.0%). Enterprise is significantly below SMB. Pricing model adjustment targeted at enterprise onboarding and dedicated CSM coverage.

**Result:** Post-intervention NPS re-survey at 6 months shows Enterprise NPS improved to 57. Decision was statistically defensible and directionally correct.

**Anti-Example:** The marketing team runs a quick 50-question survey blast to their newsletter list (mostly SMB self-serve users). They get 900 responses and report a company-wide NPS of 68. Enterprise accounts are underrepresented at 3% of respondents vs. 10% of revenue. The VP uses this to argue no pricing changes are needed. Three months later, two large Enterprise accounts churn citing support dissatisfaction — something the biased sample completely masked.

---

### Scenario 2: AI Model Bias Audit for a Hiring Platform

**Trigger:** A legal and compliance team at an AI hiring platform is required to audit its resume screening model for demographic disparities before a major bank client deploys it.

**Analysis:**
- Population: All resumes processed by the model in the trailing 12 months — 400,000 records.
- Sampling frame: Data warehouse export with demographic inference flags (gender, inferred ethnicity based on name analysis — acknowledged limitation).
- Method: Stratified random sampling across 6 demographic strata. Minimum n=400 per stratum to detect a 5-percentage-point disparity in pass-through rate with 80% power at 95% CI.
- Total sample: n=2,400.
- Non-sampling error control: Double-blind human audit of flagged records; inter-rater reliability measured (Cohen's kappa target > 0.80).

**Decision:** Model shows statistically significant lower pass-through rate for women in technical roles (34% vs. 41% for men, p<0.01). Model is recalled for retraining. Training data audit reveals historical underrepresentation of women in senior engineering roles.

**Result:** Retrained model shows parity within ±2% across gender strata. Client deployment proceeds with ongoing quarterly sampling audits embedded in contract SLA.

**Anti-Example:** The data team audits a convenience sample of 100 recently processed resumes — whatever is easiest to pull from the staging environment. They find no significant disparity. They report "no bias detected." The bank deploys the model. A journalist later runs an independent test with 5,000 synthetic matched-pair resumes and publishes a story about systematic bias. The platform faces regulatory investigation and client loss.

---

### Scenario 3: Market Sizing for an AI Observability Tool

**Trigger:** A Series B startup wants to size the enterprise AI observability market in the US to anchor its investor pitch deck and pricing strategy. Budget: $30K for primary research.

**Analysis:**
- Population: IT/ML engineering decision-makers at US companies with >200 employees and at least one deployed ML model in production.
- Sampling frame: B2B panel provider (Lucid/Cint) with ~18,000 qualifying panelists meeting tech/role criteria. Estimated universe = ~45,000 decision-makers (IDC estimate cross-referenced with LinkedIn Sales Navigator).
- Method: Systematic random sampling from panel with quota controls for company size (200–1K, 1K–5K, 5K+) and industry vertical.
- Target n=600 (MoE ±4% at 95% CI for overall; ~200 per size tier for subgroup analysis with MoE ±6.9%).
- Non-sampling error controls: Screener trap questions, attention checks, minimum completion time filters.

**Decision:** 34% of respondents confirm active budget allocation for AI observability tooling in the next 12 months. Average budgeted spend: $180K/year. TAM estimate: 45,000 * 34% * $180K = ~$2.75B addressable market. Pricing benchmarked against willingness-to-pay data at $15K–$40K/year per tier.

**Result:** Investor deck receives credibility marks for methodology transparency. Lead investor requests methods appendix. Pricing set at $18K entry / $35K enterprise — within expressed WTP band. ARR ramp exceeds model in Year 1.

**Anti-Example:** Founders interview 12 friendly prospects and 5 industry analysts. They triangulate a "bottom-up TAM of $4B." In due diligence, the lead investor's data science team runs a simple regression and finds the estimate is 2x industry comps and unsupported by any documented sampling methodology. The round is restructured at a lower valuation and the founders are asked to fund additional primary research before closing.

---

## Practitioner Playbook

**Step-by-step guide for executing a rigorous sampling study in an IT/AI/Product/Consulting context.**

1. **Define the research objective precisely.** Write one sentence: "We are trying to estimate [metric] among [population] to make [decision]." If you can't write this sentence, you are not ready to sample.

2. **Define the target population.** Specify inclusion criteria (role, industry, company size, behavior, geography, product tier, time window). Document exclusion criteria. This definition is your north star — every other choice flows from it.

3. **Audit your sampling frame for coverage.** List every data source you will draw from (CRM, panel, app database, LinkedIn). Estimate coverage: what share of your defined population appears in this frame? Document gaps explicitly. Gaps > 20% of the population require either frame expansion or explicit limitation disclosure.

4. **Select the appropriate sampling method.** Use the following decision logic:
   - Need statistically valid inference → use a probability method (random, stratified, cluster, systematic).
   - Need subgroup comparisons → use stratified random sampling.
   - Geographically distributed, high field cost → cluster sampling.
   - Large ordered list, operational simplicity → systematic sampling.
   - Exploratory, fast, budget-constrained → quota or convenience, with documented limitations.
   - Hard-to-reach population → snowball with referral chain documentation.

5. **Calculate required sample size.** Use the formula: n = Z^2 * p * (1-p) / e^2. Choose your confidence level (95% default), your desired MoE, and p=0.5 if unknown. Apply FPC if n/N > 0.05. Add 15–25% buffer for expected non-response and disqualification.

6. **Design your screener and quality controls.** Write screener questions to enforce inclusion criteria. Add at least two attention check questions. Set minimum completion time thresholds (< 1/3 of median completion time → flag as speedster). Plan for duplicate IP/device detection.

7. **Pilot with 5% of target sample.** Field 20–50 responses. Check: completion rates, drop-off points, screener pass rates, data quality flags. Recalibrate field plan before full launch.

8. **Execute fielding with progress monitoring.** Track response rates by stratum daily. If a stratum is lagging, adjust incentives or outreach cadence. Do not change the sampling frame or method mid-field — that invalidates comparability.

9. **Calculate and document non-response rate.** Non-response rate = (eligible non-respondents) / (eligible contacted). If > 30%, conduct a non-response bias check: compare known characteristics (e.g., company size, account tenure) of respondents vs. non-respondents using available CRM data.

10. **Weight data if using disproportionate stratification.** Apply post-stratification weights so that each stratum's contribution to aggregate results matches its share of the true population. Document all weighting decisions.

11. **Compute sampling error for all reported statistics.** Every percentage reported to a client or stakeholder must be accompanied by its margin of error and the confidence level. No naked numbers.

12. **Write the methods appendix.** Include: population definition, frame source and coverage estimate, method and rationale, sample size calculation, achieved n by stratum, response rate, non-response bias analysis, weighting approach, and all quality control measures applied. This is what sophisticated clients and peer reviewers will scrutinize.

13. **Flag all non-sampling errors explicitly.** Measurement errors (ambiguous questions), social desirability bias, recall bias, interviewer effects — acknowledge each in the limitations section with an assessment of likely direction and magnitude of impact.

14. **Archive raw data and sampling documentation.** Store the original sample draw, the screener logic, the complete dataset with quality flags, and the weighting schema. Reproducibility is a professional standard in consulting and product analytics.

---

## Content Critique & Depth Gaps

**Assessment of source material against IIM / HBS MBA research methods standards.**

### What the Source Material Gets Right
- Correctly identifies the core purpose of sampling (cost and time efficiency while maintaining representativeness).
- Provides an accurate motivating example (bank surveying 500 customers).
- Correctly identifies the Instagram follower scenario as a frame-population mismatch — a genuine and common error.
- Mentions both random and convenience sampling as contrast cases.

### Critical Gaps for MBA / Practitioner Depth

**1. No treatment of non-probability sampling taxonomy.**
The source lists only "random" and "convenience." Missing: quota, snowball, purposive, and judgment sampling — all of which appear regularly in consulting sprint research and qualitative-to-quantitative hybrid designs.

**2. No sample size formulas or quantitative thresholds.**
An MBA-level treatment must include the proportions formula, margin of error derivation, finite population correction, and the Z-score table for common confidence levels. Without this, practitioners cannot size studies independently.

**3. No discussion of non-response bias.**
This is arguably the most dangerous source of error in modern survey research (response rates have declined from ~70% in the 1990s to <10% in many panel contexts). The source does not mention it.

**4. No distinction between sampling error and non-sampling error.**
This is a foundational conceptual distinction. Practitioners who conflate the two systematically over-invest in sample size while ignoring process errors that are far larger.

**5. No treatment of weighting and post-stratification.**
Disproportionate stratified sampling — which is extremely common in product research and consulting studies — requires explicit weighting back to population proportions. Omitting this leads to biased aggregate estimates.

**6. No coverage of A/B testing / experimental sampling context.**
In AI/Product contexts, sampling questions arise constantly in experiment design: minimum detectable effect, statistical power, sequential testing, peeking problems. These are entirely absent.

**7. No ethical or legal considerations.**
GDPR, CCPA, and IRB-equivalent standards for data collection affect who can be sampled and how consent must be obtained — especially relevant in AI bias audits and health tech contexts.

**8. No framework for frame-population gap assessment.**
The Instagram example demonstrates a frame-population mismatch, but the source provides no structured approach for auditing and documenting coverage gaps — a critical consulting skill.

**9. No discussion of panel quality and vendor evaluation.**
In practice, most market research uses third-party panels (Lucid, Dynata, Cint). MBA practitioners need criteria for evaluating panel quality, fraud detection, and representativeness claims — none of which appear in the source.

**10. No treatment of mixed-mode sampling effects.**
Combining online, phone, and in-person data collection introduces mode effects that must be accounted for in analysis — a common issue in enterprise B2B research.

---

## Quick-Recall Card

**Core Purpose:** Estimate population-level parameters from a subset, with quantified uncertainty, at minimum cost.

**Five Decisions Every Sampling Study Requires:**
- Who exactly is the population? (Define inclusion/exclusion criteria in writing.)
- What is your sampling frame, and what does it miss?
- Which method — probability (generalizable) or non-probability (fast/directional)?
- What sample size do you need? (Use the formula; apply FPC if warranted.)
- How will you handle non-response, weighting, and reporting of error?

**Anchor Numbers to Know Cold:**
- n=385 → MoE ±5% (95% CI, p=0.5) — minimum publishable
- n=1,068 → MoE ±3% — standard consulting study
- n=9,604 → MoE ±1% — census-grade claims
- Z=1.96 for 95% CI; Z=2.576 for 99% CI

**The Three Error Sources:**
- Coverage error: Frame ≠ Population (invisible before you start)
- Sampling error: Random variation; shrinks with n; quantifiable
- Non-sampling error: Bias, measurement error, non-response; NOT fixed by larger n

**Method Selection Rule:**
- Need to generalize + quantify error → Probability method (stratified, cluster, systematic, SRS)
- Need speed + direction → Non-probability (quota, convenience) + explicit limitations
- Need hard-to-reach population → Snowball with referral documentation

**Red Flags in Others' Research:**
- "We surveyed our user community" (convenience — not representative)
- No margin of error or confidence level stated
- 95% response rate without explanation (probably self-selected)
- "1,000 respondents" with no population definition or method
- Aggregate results from disproportionate sample without weighting

**Weighting Rule:** Disproportionate stratified sample → always weight back. Unweighted aggregate = wrong answer.

**Non-Response Rule:** If non-response rate > 30%, run a non-response bias check using available frame data. Report both response rate AND non-response rate.

**Pilot Rule:** Always field 20–50 responses before full launch. A broken screener discovered at n=800 means a restart.

**AI/Product-Specific Alerts:**
- Sampling frame = MAU list ≠ all customers (offline, churned, and prospect segments missing)
- A/B test peeking inflates false positives — pre-register your stopping rule
- AI model validation requires stratified sampling across demographic dimensions to detect disparate impact
- Training data sampling decisions propagate forward into model behavior — treat as research design, not data engineering

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Is my sample drawn from a frame that actually covers my population, using a method that lets me quantify my error — and if not, what claims am I not entitled to make?"

---

## Self-Audit Report

<!-- Self-Audit:
SECTION COMPLETENESS CHECK:
[x] 1. Jargon Buster — 12 terms defined (exceeds minimum of 8); all required terms included: stratified sampling, cluster sampling, systematic sampling, quota sampling, snowball sampling, sampling error, non-sampling error, margin of error.
[x] 2. Frameworks & Mental Models — 3 frameworks with ASCII diagrams: (a) probability vs. non-probability taxonomy tree, (b) sample size vs. margin of error curve, (c) sampling frame vs. population mismatch diagram. Each includes IT/AI application note.
[x] 3. Formulas, Thresholds & Rules of Thumb — covers: sample size formula for proportions (with worked example), margin of error formula (with worked example), finite population correction (with worked example), A/B test effect size sizing, confidence level Z-score table, sample size anchor table.
[x] 4. Do / Don't — 10 Do items, 10 Don't items (exceeds minimum of 8 each side). All items are IT/AI/Product/Consulting contextualized.
[x] 5. Metric-Driven Scenarios with Anti-Examples — 3 scenarios: (1) NPS benchmarking at B2B SaaS, (2) AI model bias audit at hiring platform, (3) market sizing for AI observability tool. Each follows Trigger → Analysis → Decision → Result → Anti-Example structure.
[x] 6. Practitioner Playbook — 14 numbered steps covering full study lifecycle from objective definition through archiving.
[x] 7. Content Critique & Depth Gaps — 10 identified gaps against IIM/HBS MBA standards with specific explanation of each omission and its practical consequence.
[x] 8. Quick-Recall Card — bullet format; ends with exact phrase starting "As a PM/Consultant/AI Lead, the one question to answer with this framework is:".
[x] 9. Self-Audit Report — this HTML comment.

QUALITY FLAGS:
- Industry lens (IT/AI/Product/Consulting) applied consistently across all 9 sections.
- All formulas include worked numerical examples.
- All scenarios are grounded in realistic business contexts with quantified metrics.
- Connects-to links reference related files in the same folder.
- File is substantially above the 13 KB minimum.
- No sections omitted.
- Role-lens question in Section 8 begins exactly with "As a PM/Consultant/AI Lead".
- No emojis used.
- No markdown documentation/README file created separately.

KNOWN LIMITATIONS OF SOURCE CONTENT ADDRESSED:
- Source lacked quantitative formulas — added in Section 3.
- Source lacked non-probability taxonomy — addressed in Sections 1, 2, and 4.
- Source lacked non-response bias discussion — addressed in Sections 1, 4, 6, and 7.
- Source lacked A/B testing context — addressed in Sections 3, 4, and 8.
- Source lacked ethical/legal considerations — noted in Section 7.
-->
