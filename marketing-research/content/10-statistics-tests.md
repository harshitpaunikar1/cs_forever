# Basic Statistics and Tests (Descriptive, z/t, Chi-square)

## Overview

Basic statistics summarize data using numbers like averages and percentages. Simple tests (z, t, chi-square) help you check if differences or relationships are real, not just random.

---

## Why It Matters

Managers need clear summaries and proof. These tools help you confidently say things like “this ad works better” or “age group affects buying.”


## Key Principles

- Start with descriptive summaries before tests
- Choose the right test for the question
- Statistical results must still make business sense
- Don’t treat numbers as truth without context


## Key Terms

| Term | Definition |
|------|------------|
| **Mean** | Average |
| **Median** | Middle value |
| **Standard deviation** | How spread out values are |
| **z-test / t-test** | Compare averages between groups (t is common) |
| **Chi-square test** | Checks relationship between categories |
| **Significance** | Whether results are likely real, not random |


## Use Case

A brand compares satisfaction scores between two cities using a t-test to see if the difference is meaningful.


## Scenario

> A company thinks “women buy more than men.” Chi-square test shows buying is linked more to income group than gender.


## Examples

- Descriptive: “60% preferred Pack A; average rating was 4.2/5.”
- Chi-square: “Payment method (UPI/Card/Cash) is related to age group.”

---

## Audited Appendix

# Basic Statistics and Tests (Descriptive, z/t, Chi-square)
**Course:** Marketing Research  
**Module:** Content  
**Audited on:** 2026-04-19  
**Audited by:** A1  
**Source files reviewed:** `marketing-research/content/10-statistics-tests.md`

---

## 1. Topic Snapshot
Basic statistics turn raw survey or product data into summaries, and inferential tests check whether an observed gap is likely real or just noise. [verified from model knowledge, not source]
For IT/AI/Product/Consulting leaders, this is the go/no-go layer for experiments, segment comparisons, and dashboard decisions. [verified from model knowledge, not source]
Decision it helps make: whether to ship, pause, or re-test a change when averages, percentages, or category counts move. [verified from model knowledge, not source]

## 2. Jargon & Terminology

The expanded terminology below uses standard statistics language to operationalize the source terms. [verified from model knowledge, not source]

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Descriptive statistics | Descriptive statistics | Summaries such as averages and percentages | Turns many observations into a readable snapshot | Mean, median, percentage, spread | BI dashboards, research readouts |
| Mean | Arithmetic mean | Average value | Gives one center-point for numeric data | `sum(x_i) / n` | KPI reviews, survey summaries |
| Median | Median | Middle value after sorting | Handles skewed data better than the mean | 50th percentile | Spend, salary, response-time analysis |
| Standard deviation | Standard deviation | Typical distance from the mean | Shows whether the average is stable or noisy | `sqrt(sum((x_i - xbar)^2) / (n - 1))` | Quality, operations, CX reviews |
| Percentage | Percentage | Part out of 100 | Makes proportions easy to compare across segments | `count / total * 100` | Conversion dashboards, survey shares |
| z-test | z statistic test | Tests whether a sample result is far enough from a benchmark when the sample is large or variance is known [verified from model knowledge, not source] | Supports fast inference on means or proportions | z score and p-value | Experiment readouts, quality checks |
| t-test | Student's t-test | Tests whether one average or two averages differ when population variance is unknown [verified from model knowledge, not source] | Safer than a z-test for small samples | t statistic and p-value | Product experiments, A/B tests |
| Chi-square test | Chi-squared test | Tests whether categorical variables are associated [verified from model knowledge, not source] | Answers relationship questions about counts, not averages | Chi-square statistic and p-value | Segment analysis, survey crosstabs |
| Significance | Statistical significance | Whether an observed difference is likely too large to blame on chance alone | Prevents overreacting to random noise | p-value versus alpha, usually 0.05 [verified from model knowledge, not source] | Experiment reviews, academic papers |

## 3. Frameworks & Matrices

### Question Type to Test Ladder
**Purpose:** Convert the business question into the right statistical tool before anyone starts calculating.

**Text Diagram:**
```text
Business question
    |
    v
What is being compared?
    |
    +--> Averages / numeric values --> z-test or t-test
    |
    +--> Percentages / category counts --> chi-square test
    |
    v
Is the result significant enough to act on?
```

Axes / Quadrants / Components explained:
Component 1: data type, which tells you whether the decision lives in numbers or categories.
Component 2: comparison goal, which tells you whether the task is a mean test, percentage test, or association test.
Component 3: decision threshold, which tells you whether the result is good enough to ship.
IT/AI/Product/Consulting worked example: A SaaS team compares average onboarding time between two flows; the ladder sends them to a t-test, not a chi-square test, because the outcome is numeric time. [verified from model knowledge, not source]
When to pull this out in a meeting: When the team asks, "What test should we use?" before anyone has defined the variable type.

### Test Selection Matrix
**Purpose:** Pick the simplest valid test for the data and the management question. [verified from model knowledge, not source]

**Text Diagram:**
```text
                           Question type
+---------------------------+---------------------------+---------------------------+
|                           | Compare to benchmark      | Compare groups / segments |
+---------------------------+---------------------------+---------------------------+
| Numeric data              | z-test (large n)          | t-test                    |
| Categorical data          | percentage comparison     | chi-square test           |
+---------------------------+---------------------------+---------------------------+
```

Axes / Quadrants / Components explained:
Component 1: numeric data, such as time, score, revenue, or rating.
Component 2: categorical data, such as region, gender, plan type, or payment method.
Component 3: benchmark comparison, which asks whether one group is above or below a target.
Component 4: group comparison, which asks whether two or more groups differ from each other.
IT/AI/Product/Consulting worked example: A product manager compares 30-day activation rates by customer segment; because the outcome is categorical conversion, chi-square is the right starting point. [verified from model knowledge, not source]
When to pull this out in a meeting: When someone wants to compare two dashboards but has not checked whether the dashboard metrics share the same scale.

### Significance vs Business Impact Matrix
**Purpose:** Stop the team from confusing statistical significance with a meaningful business move. [verified from model knowledge, not source]

**Text Diagram:**
```text
                         Business impact
                    Low                     High
Statistically   +----------------+   +----------------+
significant     | Monitor        |   | Ship / scale   |
                +----------------+   +----------------+
Not            | Ignore or      |   | Re-test, add   |
significant     | document noise  |   | sample, or fix |
                +----------------+   +----------------+
```

Axes / Quadrants / Components explained:
Component 1: statistical signal, usually represented by p-value or test statistic.
Component 2: business impact, which captures revenue, retention, risk, or service quality.
Component 3: sample adequacy, because a weak test can hide a real effect.
IT/AI/Product/Consulting worked example: A model improves click-through by 0.2 percentage points with p < 0.05, but the lift is too small to justify engineering time, so the team documents it and moves on. [verified from model knowledge, not source]
When to pull this out in a meeting: When a stakeholder says, "It's significant, so we should do it," without asking whether the delta is worth the cost.

## 4. Formulas

The formulas below expand the source into standard operational rules for business use. [verified from model knowledge, not source]

### Formula 1: Percentage
Formula: `percentage = (part / whole) * 100`
Variables:
Part = number of respondents or events in the category of interest.
Whole = total number of respondents or events.
Why this formula exists: It answers, "What share of the base is this?" which is the first question behind many marketing and product dashboards.
How to interpret the output:
Value < 10% -> small share -> usually monitor or segment further
Value 10% to 30% -> meaningful share -> compare across groups
Value > 30% -> dominant share -> prioritize in planning
Worked example with numbers: 84 of 240 beta users activated the feature, so percentage = 84/240 * 100 = 35%. That is large enough to investigate by segment, not just as a single blended number. [verified from model knowledge, not source]

### Formula 2: Mean
Formula: `mean = sum(x_i) / n`
Variables:
`x_i` = each observed value.
`n` = number of observations.
Why this formula exists: It gives a single center point for a numeric metric like wait time, satisfaction score, or spend.
How to interpret the output:
Value < target by more than 10% -> favorable if lower is better -> scale or preserve
Value within target +/- 10% -> roughly on plan -> monitor
Value > target by more than 10% -> unfavorable if lower is better -> investigate root cause
Worked example with numbers: The onboarding time for 50 users sums to 320 minutes, so the mean is 6.4 minutes. If the target is 5.5 minutes, the product team should fix the flow rather than declare victory. [verified from model knowledge, not source]

### Formula 3: z-test statistic
Formula: `z = (p1 - p2) / sqrt(p(1-p)(1/n1 + 1/n2))`
Variables:
`p1` = proportion in group 1.
`p2` = proportion in group 2.
`p` = pooled proportion across both groups.
`n1`, `n2` = sample sizes.
Why this formula exists: It answers whether a difference in proportions is likely to be more than random noise when sample sizes are large. [verified from model knowledge, not source]
How to interpret the output:
Value < 1.96 in absolute terms -> not significant at 5% two-tailed -> do not scale yet
Value 1.96 to 2.58 in absolute terms -> borderline -> look at effect size and cost
Value > 2.58 in absolute terms -> strong evidence -> consider rollout if business value is real
Worked example with numbers: Variant A converts 992 of 8000 visitors (12.4%), and Variant B converts 864 of 8000 visitors (10.8%). The z score is about 3.16, so the lift is statistically convincing and worth a controlled rollout. [verified from model knowledge, not source]

### Formula 4: t-test statistic
Formula: `t = (xbar1 - xbar2) / sqrt(s1^2/n1 + s2^2/n2)`
Variables:
`xbar1`, `xbar2` = sample means.
`s1`, `s2` = sample standard deviations.
`n1`, `n2` = sample sizes.
Why this formula exists: It answers whether two averages differ enough to matter when the population variance is unknown.
How to interpret the output:
Value < 1.96 in absolute terms -> likely no clear difference -> keep current design or gather more data
Value 1.96 to 2.58 in absolute terms -> possible difference -> check business impact and confidence interval
Value > 2.58 in absolute terms -> strong evidence -> ship the better average if the effect is operationally meaningful
Worked example with numbers: Flow A has mean onboarding time 6.8 minutes, sd 2.4, n=60. Flow B has mean 5.9 minutes, sd 2.1, n=60. The t value is about 2.18, so the faster flow is a reasonable candidate for rollout. [verified from model knowledge, not source]

### Formula 5: Chi-square statistic
Formula: `chi^2 = sum((O - E)^2 / E)`
Variables:
`O` = observed count in each cell.
`E` = expected count if the categories were unrelated.
Why this formula exists: It answers whether counts across categories are independent or linked.
How to interpret the output:
Value small relative to degrees of freedom -> weak evidence of association -> keep one policy
Value near the critical value -> borderline -> inspect segment-level cells
Value large relative to degrees of freedom -> strong association -> tailor strategy by segment
Worked example with numbers: Enterprise users have 90 adopters and 60 non-adopters; SMB users have 50 adopters and 100 non-adopters. The chi-square statistic is about 21.43, which is strong evidence that adoption is related to segment. [verified from model knowledge, not source]

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Compare two mean response times with a chi-square test. | Use a t-test or z-test when the outcome is numeric. |
| Call a 1 percentage-point lift a win without checking sample size. | Report the denominator, the test statistic, and the p-value. |
| Treat a skewed spend distribution as if the mean tells the whole story. | Check the median and standard deviation before deciding. |
| Say "p < 0.05" means the product is important. | Pair significance with business impact and implementation cost. |
| Use a test before defining the business question. | Define the decision first, then choose the test that matches the data. |

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Onboarding flow A/B test
Situation: A product team compares two AI onboarding flows for 60 users each. Flow A takes 6.8 minutes on average to reach the first successful output, while Flow B takes 5.9 minutes. The team wants to know whether the faster flow should become the default. [verified from model knowledge, not source]
Applicable framework/metric: t-test on mean time-to-value.
Analysis: With sd 2.4 for Flow A and 2.1 for Flow B, the t statistic is about 2.18. The improvement is about 13.2 percent, so the result is both statistically and operationally interesting. [verified from model knowledge, not source]
Decision rule: If p < 0.05 and the reduction in time is more than 10 percent, do the rollout. If p is between 0.05 and 0.10, run a larger test. If p > 0.10, keep the current flow.
Action: Freeze the better flow for a controlled launch, add instrumentation for drop-off reasons, and brief engineering on the two slowest steps.

### Scenario 2: Email subject-line experiment
Situation: A marketing team sends Variant A to 8000 opens and gets 992 clicks, then sends Variant B to 8000 opens and gets 864 clicks. The CMO wants to know whether the higher click rate is real or just noise. [verified from model knowledge, not source]
Applicable framework/metric: z-test on conversion rate.
Analysis: Variant A converts at 12.4 percent and Variant B at 10.8 percent. The z score is about 3.16, so the lift is significant enough to consider scaling if the margin holds. [verified from model knowledge, not source]
Decision rule: If the z score is above 1.96 and the incremental gain clears the campaign cost threshold, scale it. If it is between 1.65 and 1.96, re-test. If it is below 1.65, do not change the campaign.
Action: Roll the winning subject line into the next campaign wave, then segment results by audience and device.

### Scenario 3: Feature adoption by customer segment
Situation: A consulting team reviews whether enterprise, mid-market, and SMB accounts adopt a new reporting feature at different rates. The client wants a segmentation rule for rollout and training. [verified from model knowledge, not source]
Applicable framework/metric: chi-square test for association.
Analysis: In a 2x2 version of the data, enterprise users show 90 adopters and 60 non-adopters while SMB users show 50 adopters and 100 non-adopters. The chi-square statistic is about 21.43, which indicates adoption depends on segment. [verified from model knowledge, not source]
Decision rule: If chi-square is above the critical value, tailor the rollout by segment. If it is close to the threshold, collect more data. If it is well below the threshold, use one standard rollout plan.
Action: Build a segment-specific adoption dashboard, train customer success on the weaker segment, and separate rollout messaging by account size.

## 7. Implementation Playbook
1. Write the decision memo first, with the exact business action the statistic will support.
2. Classify every variable as numeric or categorical, and note the sample size and unit of analysis.
3. Select the smallest valid test, and write the null hypothesis before looking at the data.
4. Check assumptions: independence, expected cell counts, approximate normality, and clean data definitions. [verified from model knowledge, not source]
5. Compute the summary, test statistic, and p-value in a spreadsheet or notebook, then record the effect size. [verified from model knowledge, not source]
6. Translate the result into a product, marketing, or consulting action rule tied to cost and risk. [verified from model knowledge, not source]
7. Log exclusions, outliers, and caveats in the research memo so the result can be defended later.

## 8. Content Quality Audit
Covered well: The source gives a clean, beginner-friendly statement of what descriptive summaries, z/t tests, chi-square tests, and significance are for. It is short enough to teach the right instinct without burying the reader in notation.
Underplayed or missing: It does not explain assumptions, sample size, confidence intervals, effect size, power, one-tailed versus two-tailed tests, or what to do when data are skewed. It also does not tell the learner when a percentage comparison needs a z-test versus when a mean comparison needs a t-test. [verified from model knowledge, not source]
Supplement with: Anderson, Sweeney, Williams, Camm, Cochran, Fry, and Ohlmann, *Statistics for Business and Economics*; Moore, McCabe, and Craig, *Introduction to the Practice of Statistics*; McAfee and Brynjolfsson (2012), HBR, "Big Data: The Management Revolution"; Pearson (1900) on the chi-square criterion; Student/Gosset (1908) on the t-test; Fisher (1925) on significance testing. [verified from model knowledge, not source]
IIM/HBS cases: Pair this topic with case-method material on experiment-driven marketing, pricing, or onboarding decisions from the HBS case catalogue and the IIMA Case Centre so the learner sees how test output changes a real management call. [verified from model knowledge, not source]
Red flags in the source: The phrase "simple tests" can make hypothesis testing look easier than it is, and the source does not warn against treating significance as proof of business value. [verified from model knowledge, not source]

## 9. Quick-Recall Card
```text
Topic: Basic Statistics and Tests
Core idea: Summaries tell you what happened; z-tests, t-tests, and chi-square tests tell you whether the pattern is probably real.
Key metric/formula: mean = sum(x_i) / n; z, t, and chi-square use p-values against an alpha threshold.
Framework trigger: Use it when the question is "how big is the difference, and is it likely real?"
Watch out for: Statistical significance without business significance.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Should we ship, re-test, or ignore this difference?
```
<!-- Self-Audit Report Pass 1 scores: [1:3, 2:4, 3:4, 4:3, 5:4, 6:4, 7:4, 8:3, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [IT/AI/Product/Consulting lens throughout; source-term inventory and operational definitions; test-selection and significance decision matrices; explicit z/t/chi-square formulas with worked numbers; decision-level do/don't rules; metric-driven scenarios; source-quality critique with supplemental reading] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:39 Audited by: A1 -->
