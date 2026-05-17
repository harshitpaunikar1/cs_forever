# Data Preparation

## Overview

Data preparation means cleaning and organizing collected data so it’s ready for analysis.

---

## Why It Matters

Raw data often contains mistakes, missing answers, or inconsistent entries. Clean data helps you make correct decisions.


## Key Principles

- Check for missing/invalid values
- Remove duplicates and obvious errors
- Code answers (especially open-ended ones)
- Keep data consistent (formats, units, categories)


## Key Terms

| Term | Definition |
|------|------------|
| **Editing** | Fixing obvious mistakes in responses |
| **Coding** | Turning answers into numbers/categories |
| **Cleaning** | Removing errors and inconsistencies |
| **Tabulation** | Arranging data into tables |


## Use Case

A company collects 2,000 survey responses and cleans the dataset before generating charts and summaries.


## Scenario

> Survey data includes “Delhi,” “New Delhi,” and “delhi.” Preparation combines them into one category so results aren’t misleading.


## Examples

- Convert “Male/Female/M/f” into a single consistent format.
- Remove responses where age is “300” (clearly invalid).

---

## Audited Appendix

# Data Preparation

**Overview:** Data preparation means cleaning and organizing collected data so it's ready for analysis.

**Why It Matters:** Raw data often contains mistakes, missing answers, or inconsistent entries. Clean data helps you make correct decisions.

**Key Principles:**
- Check for missing/invalid values
- Remove duplicates and obvious errors
- Code answers (especially open-ended ones)
- Keep data consistent (formats, units, categories)

**Key Terms:** Editing, Coding, Cleaning, Tabulation

**Use Case:** A company collects 2,000 survey responses and cleans the dataset before generating charts and summaries.

**Scenario:** Survey data includes "Delhi," "New Delhi," and "delhi." Preparation combines them into one category so results aren't misleading.

**Examples:**
- Convert "Male/Female/M/f" into a single consistent format.
- Remove responses where age is "300" (clearly invalid).

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| Imputation | The process of filling in missing data values with estimated substitutes — mean, median, mode, or model-predicted values — rather than deleting the row. | In IT product analytics or consulting datasets, dropping rows with missing data can introduce selection bias. Imputation preserves sample size and statistical power, but the method chosen (mean vs. regression-based) changes your results — document it carefully. |
| Outlier Treatment | Identifying and deciding how to handle data points that fall far outside the typical distribution — either by removing, capping (Winsorizing), or transforming them. | A SaaS company tracking monthly revenue per customer might see one enterprise client generating 100x the median. Including it skews averages; excluding it without justification is cherry-picking. The decision must be documented and defensible. |
| Dummy Coding | Converting categorical variables (e.g., "Segment: SMB / Mid-Market / Enterprise") into binary 0/1 numeric variables so statistical models can process them. | Essential when running regression analyses on segmentation data in consulting engagements. Incorrect dummy coding (including all categories without a reference group) creates multicollinearity and produces garbage model outputs. |
| Data Dictionary | A reference document that defines every variable in a dataset — its name, data type, allowed values, units, and coding rules. | Without a data dictionary, a junior analyst may interpret "NPS Score" as 1–10 when it was collected on a 0–10 scale. In AI/ML pipelines, a data dictionary is foundational to reproducibility and model governance. |
| Missing Completely at Random (MCAR) | Missingness is entirely unrelated to any variable in the dataset — the data just happened to not be collected for random reasons (e.g., a survey page failed to load). | MCAR is the best-case scenario. If proven, simple listwise deletion does not bias results. In practice, verifying MCAR requires Little's MCAR test — most product teams skip this and pay the price in biased analysis. |
| Missing at Random (MAR) | Missingness is related to other observed variables in the dataset but NOT to the missing variable itself (e.g., older respondents tend to skip income questions, but income itself is not driving the skip). | MAR is addressable via multiple imputation or model-based approaches. Most real-world consulting and product datasets fall here. Recognizing MAR allows you to impute correctly rather than delete rows. |
| Missing Not at Random (MNAR) | Missingness IS related to the value of the missing variable itself (e.g., high earners skip the income question because they don't want to disclose high incomes). | MNAR is the most dangerous pattern — you cannot fix it purely through imputation. It requires collecting auxiliary data, redesigning the instrument, or explicitly acknowledging the limitation. AI systems trained on MNAR data systematically underperform on the hardest or most sensitive cases. |
| Data Validation | The process of checking that each data point conforms to defined rules — correct range, format, type, and logical consistency — before it enters the analysis pipeline. | In product analytics (e.g., Mixpanel, Amplitude, BigQuery pipelines), missing validation at ingestion causes compounding errors downstream. A single unvalidated field can corrupt months of trend data before anyone notices. |
| Editing | The field- or office-level review of raw data to catch recording errors, illegible responses, or out-of-range values before formal cleaning begins. | In consulting primary research, field editing (done on-site by enumerators) catches errors that office editing cannot retroactively fix — e.g., a respondent who answered Q5 before Q3 was asked. |
| Coding | Assigning numeric or categorical labels to qualitative/open-ended responses so they can be quantified and analyzed systematically. | In UX research and product discovery interviews, coding themes (e.g., "Performance Issue," "Pricing Concern," "Onboarding Friction") is the bridge between qualitative insight and quantitative prioritization. Inconsistent coding destroys comparability. |
| Tabulation | Organizing cleaned, coded data into summary frequency tables or cross-tabulations that show distributions and relationships between variables. | Cross-tabulation (segment × NPS, region × churn rate) is the first analytical output most consulting decks rely on. Errors in tabulation at this stage cascade into every chart and recommendation that follows. |
| Winsorization | Capping extreme outlier values at a defined percentile threshold (e.g., 1st and 99th percentile) rather than removing them entirely. | Preferred over deletion in financial modeling and AI training data where extreme values carry real information. A startup with one VC-funded enterprise client should Winsorize revenue data, not delete the row. |

---

## Frameworks & Mental Models

### 1. Data Preparation Pipeline

The end-to-end flow from raw collection to analysis-ready dataset.

```
RAW DATA COLLECTED
        |
        v
+-------------------+
|   FIELD EDITING   |  <-- Enumerator/Survey Platform checks
|  (on-site/real-   |      range, completeness, logic
|   time review)    |
+-------------------+
        |
        v
+-------------------+
|  OFFICE EDITING   |  <-- Research team reviews for
|  (desk review)    |      consistency, legibility, outliers
+-------------------+
        |
        v
+-------------------+
|  DATA VALIDATION  |  <-- Rules engine: type check, range
|  (automated QA)   |      check, referential integrity
+-------------------+
        |
        v
+-------------------+
|   MISSING DATA    |  <-- Classify as MCAR / MAR / MNAR
|   DIAGNOSIS       |      Run Little's test; visualize pattern
+-------------------+
        |
        v
+-------------------+
|  OUTLIER ANALYSIS |  <-- Z-score / IQR detection
|  & TREATMENT      |      Delete / Winsorize / Transform
+-------------------+
        |
        v
+-------------------+
|  CODING & RECODING|  <-- Open-ended → categories
|                   |      Categorical → dummy codes
+-------------------+
        |
        v
+-------------------+
| STANDARDIZATION   |  <-- Units, formats, naming conventions
| & NORMALIZATION   |      aligned to data dictionary
+-------------------+
        |
        v
+-------------------+
|   DOCUMENTATION   |  <-- Data dictionary updated
|   & AUDIT TRAIL   |      Every decision logged with rationale
+-------------------+
        |
        v
  ANALYSIS-READY
    DATASET
```

**IT/AI Lens:** In ML pipelines, steps 3–7 are often automated via tools like Great Expectations, dbt tests, or Pandas Profiling — but the decisions behind the rules still require human judgment. A pipeline without human-designed validation rules is just a fast way to produce confidently wrong outputs.

---

### 2. Missing Data Taxonomy (MCAR / MAR / MNAR)

```
MISSING DATA
     |
     +------------------------------------------+
     |                    |                     |
     v                    v                     v
   MCAR                 MAR                  MNAR
(Missing           (Missing at           (Missing Not
Completely at       Random)              at Random)
  Random)
     |                    |                     |
Missingness        Missingness           Missingness IS
unrelated to       related to OTHER      related to the
any variable       observed vars,        MISSING value
in dataset         NOT to missing        itself
                   value itself
     |                    |                     |
Can use:           Can use:              Must use:
- Listwise         - Multiple            - Auxiliary
  deletion           imputation            data collection
- Mean             - Model-based         - Sensitivity
  imputation         methods               analysis
- ML impute        - MAR-aware           - Transparent
                     algorithms            limitation
                                           disclosure
     |                    |                     |
IMPACT: LOW        IMPACT: MEDIUM        IMPACT: HIGH
(if <5%)           (manageable)          (potential
                                          systematic
                                          bias)
```

**Consulting Application:** Before presenting survey findings to a C-suite, always characterize the missing data pattern. "We had 12% non-response on the budget question" lands very differently when you can say "this was MNAR — high-budget firms were less likely to disclose — so our budget distribution skews low."

---

### 3. Coding Workflow for Open-Ended Responses

```
OPEN-ENDED RESPONSES COLLECTED
(e.g., "What is your biggest pain point?")
              |
              v
    +------------------+
    |  INITIAL READ    |  <-- Two coders independently read
    |  (First Pass)    |      all responses; note themes
    +------------------+
              |
              v
    +------------------+
    | CODEBOOK DRAFT   |  <-- Define 8–15 mutually exclusive
    |                  |      and exhaustive categories
    +------------------+
              |
              v
    +------------------+
    | PILOT CODING     |  <-- Apply codebook to ~20% sample
    | (Calibration)    |      independently (both coders)
    +------------------+
              |
              v
    +------------------+
    | INTER-RATER      |  <-- Calculate Cohen's Kappa
    | RELIABILITY CHECK|      Target: κ ≥ 0.70
    +------------------+
              |
         κ ≥ 0.70?
        /           \
      YES             NO
       |               |
       v               v
  Proceed to     Reconcile
  Full Coding    Disagreements,
                 Revise Codebook,
                 Re-pilot
              |
              v
    +------------------+
    | FULL CODING      |  <-- Apply final codebook to
    |                  |      all responses
    +------------------+
              |
              v
    +------------------+
    | SECOND-CODER     |  <-- ~20% random spot-check
    | SPOT CHECK       |      Final κ calculated and logged
    +------------------+
              |
              v
    CODED DATASET READY
    FOR QUANTITATIVE
    ANALYSIS
```

**AI/Product Lens:** In AI annotation pipelines (e.g., training data for NLP models), this workflow maps directly onto label schema design → annotator calibration → inter-annotator agreement (IAA) checks → label quality auditing. Skipping calibration is the single most common cause of poor model performance that teams blame on architecture rather than data.

---

## Formulas, Thresholds & Rules of Thumb

### Missing Data Thresholds

| Missing % | Recommended Action |
|---|---|
| < 5% | Generally safe to use listwise deletion (if MCAR confirmed) or simple mean/mode imputation. Low bias risk. |
| 5% – 15% | Multiple imputation strongly recommended. Document method. Flag in report limitations. |
| 15% – 40% | Proceed with extreme caution. Use model-based imputation. Consider whether variable should be dropped or question redesigned for future waves. |
| > 40% | Consider dropping the variable. Alternatively, collect auxiliary data and reframe as a qualitative finding rather than a quantitative metric. |

**Formula — Missing Data Rate:**
```
Missing Data Rate (%) = (Number of Missing Values / Total Possible Values) x 100
```

---

### Outlier Detection: Z-Score Method

```
Z = (X - μ) / σ

Where:
  X  = individual data point
  μ  = mean of the variable
  σ  = standard deviation of the variable
```

**Threshold Rules:**
- |Z| > 2.0 — Flag for review in small samples (n < 100)
- |Z| > 2.5 — Flag for review in medium samples (100 < n < 500)
- |Z| > 3.0 — Standard threshold for outlier classification (large samples)
- |Z| > 3.5 — Extreme outlier; strong case for Winsorization or investigation

**IQR Method (Distribution-Agnostic Alternative):**
```
Lower Fence = Q1 - 1.5 * IQR
Upper Fence = Q3 + 1.5 * IQR

Where IQR = Q3 - Q1

Values outside fences = outliers
Values beyond Q1 - 3*IQR or Q3 + 3*IQR = extreme outliers
```

**Rule of Thumb:** Use Z-score for approximately normal distributions; use IQR for skewed distributions (e.g., revenue, time-to-close, feature adoption rates in SaaS).

---

### Cronbach's Alpha (Post-Cleaning Reliability Check)

Used to verify that a scale or index (e.g., customer satisfaction composite, NPS proxy scale) remains internally consistent after items are recoded or cleaned.

```
α = (k / (k - 1)) * (1 - (Σσᵢ²) / σ²_total)

Where:
  k         = number of items in the scale
  Σσᵢ²     = sum of item variances
  σ²_total  = variance of the total scale score
```

**Interpretation Thresholds:**
| α Value | Interpretation |
|---|---|
| ≥ 0.90 | Excellent reliability (may indicate redundant items) |
| 0.80 – 0.89 | Good — acceptable for most research and consulting use |
| 0.70 – 0.79 | Acceptable — minimum for exploratory research |
| 0.60 – 0.69 | Questionable — justify retention or redesign scale |
| < 0.60 | Poor — do not use composite score; report items separately |

**IT/AI Application:** When building a "User Engagement Score" composite from multiple product metrics, run Cronbach's alpha before shipping the score to dashboards. An α of 0.55 tells you the metrics are measuring different things — the composite is meaningless.

---

### Inter-Rater Reliability: Cohen's Kappa

```
κ = (Po - Pe) / (1 - Pe)

Where:
  Po = observed proportion of agreement
  Pe = expected proportion of agreement by chance
```

**Thresholds:**
| κ Value | Interpretation |
|---|---|
| > 0.80 | Near-perfect agreement |
| 0.61 – 0.80 | Substantial agreement |
| 0.41 – 0.60 | Moderate agreement |
| 0.21 – 0.40 | Fair agreement |
| ≤ 0.20 | Slight or no agreement — codebook must be revised |

**Minimum Acceptable Standard:** κ ≥ 0.70 before proceeding to full coding.

---

### Response Rate & Effective Sample Size

```
Response Rate (%) = (Completed Responses / Total Contacts Attempted) x 100

Effective N After Cleaning = Raw N - Deleted Cases (blanks + invalids + duplicates)
```

**Rule of Thumb:** If effective N after cleaning drops below 80% of your minimum required sample size for statistical significance, pause analysis, investigate the source of attrition, and consider re-fielding.

---

## Do / Don't

### Do

1. **Build and maintain a data dictionary before data collection begins.** Define every variable, its allowable range, unit, and coding rule. This prevents ambiguity during cleaning and enables reproducibility across team members and project waves.

2. **Run descriptive statistics immediately after data ingestion.** Frequency tables, mean/median/mode, and range checks on every variable catch systematic errors (e.g., all responses for one question = 99) before they corrupt downstream analysis.

3. **Diagnose the missing data mechanism** (MCAR, MAR, MNAR) using Little's MCAR test and visual pattern analysis (heatmaps of missing data by row and column) before choosing an imputation strategy.

4. **Use multiple imputation (MI) for MAR data.** MI generates several plausible complete datasets, runs analysis on each, and pools results using Rubin's Rules — producing uncertainty estimates that reflect the missingness, not false precision.

5. **Document every cleaning decision with a rationale.** Create an audit log: variable name, issue identified, action taken, reason, date, and analyst name. This is non-negotiable in consulting deliverables and AI model governance.

6. **Apply outlier treatment consistently across segments.** If you Winsorize revenue at the 99th percentile for SMBs, apply the same rule for enterprise clients — unless you have a documented analytical reason to differentiate.

7. **Verify inter-rater reliability (κ ≥ 0.70) before full coding of qualitative data.** Investing 2 hours in calibration prevents weeks of rework and defensibility crises during client presentations.

8. **Re-check Cronbach's alpha after recoding or dropping items from a composite scale.** Cleaning one item can change the reliability of the entire construct. Always recalculate before finalizing any index score.

9. **Preserve raw data in a separate, read-only file.** All cleaning is done on a copy. The original raw data is sacrosanct — you may need to revisit cleaning decisions, respond to auditors, or re-run analysis with different rules.

10. **Test cleaned data against known benchmarks.** If industry churn rates average 8% and your cleaned dataset shows 2%, something went wrong in cleaning — not in the market.

---

### Don't

1. **Don't delete missing data without diagnosing the mechanism.** Listwise deletion under MAR or MNAR conditions introduces systematic bias. The rows being deleted are not random — they are systematically different from retained rows in ways that matter for your conclusions.

2. **Don't impute the mean for skewed distributions.** Mean imputation on right-skewed variables (revenue, response time, deal size) artificially compresses variance and distorts correlations. Use median imputation or model-based imputation instead.

3. **Don't treat all outliers as errors.** An enterprise client with $10M ARR is an outlier in a SMB dataset but represents a real and important data point. Distinguish between measurement errors and legitimate extreme values — they require different responses.

4. **Don't recode variables without updating the data dictionary.** Recoding "Gender: M/F/Other" to "1/2/3" without documenting it means the next analyst (or your future self in six months) will not know what the numbers mean.

5. **Don't over-impute.** If more than 40% of a variable's values are missing, imputing them creates a mostly fabricated variable. Report the limitation instead of masking it with imputed data that gives false confidence.

6. **Don't ignore logical inconsistencies.** A respondent who reports being "18 years old" with "25 years of work experience" is internally inconsistent. Flag, investigate, and if unresolvable, remove — don't silently retain.

7. **Don't apply cleaning rules differently to data that supports vs. contradicts your hypothesis.** This is p-hacking territory. Pre-register your cleaning rules or document them before seeing results, and apply them uniformly.

8. **Don't skip the spot-check on automated cleaning pipelines.** Automated rules (e.g., "remove rows where age > 100") can have unintended consequences — e.g., removing legitimate age = 101 respondents in a geriatric health study. Always manually verify a sample of automated deletions.

9. **Don't forget to re-validate after merging datasets.** When joining two data sources (e.g., CRM data + survey responses), new duplicates, mismatched keys, and format conflicts are introduced. Run full validation again post-merge.

10. **Don't confuse data cleaning with data manipulation.** Cleaning corrects errors and enforces consistency. It does not mean adjusting values to produce a desired result. The boundary between legitimate recoding and data fabrication must be maintained explicitly and documented.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: SaaS Product Analytics — Cleaning Usage Data for Churn Prediction Model

**Trigger:** A B2B SaaS company (Series B, 800 enterprise customers) is building a churn prediction model. The raw dataset has 23% missing values on "Last Login Date" and contains duplicate customer IDs from a CRM migration six months ago.

**Analysis:**
- Missing "Last Login Date" values are diagnosed as MNAR: customers who churned silently stopped logging in before the contract expired, so their last login was never recorded in the new system.
- Duplicates arise from the CRM migration — the same customer appears under both the old and new account IDs.
- Z-score analysis on "Monthly Active Users (MAU)" reveals 14 accounts with |Z| > 3.5 — all are early beta accounts with inflated engagement from internal testing.

**Decision:**
- MNAR missingness: imputation is inappropriate. Instead, "missing last login" is recoded as a binary indicator variable ("Login Recorded: Yes/No") and treated as a predictive feature in the churn model — the absence of data IS the signal.
- Duplicates: merge records using a master customer ID mapping table from the engineering team; retain the most recent activity record for merged duplicates.
- Beta accounts: Winsorize MAU at 99th percentile (excluding beta accounts from Winsorization — instead, tag and exclude them from model training, include a separate model validation run with them included to test sensitivity).

**Result:** Effective N drops from 800 to 763 after duplicate resolution and beta exclusion. The "Login Recorded" binary feature becomes the second-strongest predictor in the churn model (after "Days Since Last Support Ticket"). Model AUC improves from 0.71 to 0.84.

**Anti-Example:** A previous analyst had mean-imputed "Last Login Date" for missing values (substituting the dataset mean of 45 days ago). This masked the churn signal entirely — the model predicted 0% churn probability for customers who hadn't logged in for 180 days because their imputed login date was 45 days ago. The model was deployed, flagged zero at-risk accounts, and the company lost 11% of its customer base before anyone noticed.

---

### Scenario 2: Management Consulting — Cleaning Primary Research Data for Market Entry Report

**Trigger:** A Tier-1 consulting firm conducts 400 interviews across four cities for a client evaluating market entry into India's mid-market ERP segment. The coding team uses 6 different coders for open-ended questions about "key purchase barriers." Pre-analysis, the lead analyst notices extreme variation in how coders categorized "vendor trust" vs. "data security concerns."

**Analysis:**
- Inter-rater reliability check (Cohen's Kappa) on a 20% sample reveals κ = 0.41 (moderate agreement) — far below the required κ ≥ 0.70.
- Review reveals two coders interpreted "vendor trust" as a relationship/brand concern and coded it separately from "data security," while four coders collapsed both into "trust/security" as a single category.
- Additionally, 8% of interviews have missing data on "current ERP vendor" — diagnosed as MAR (larger firms were more likely to decline disclosure, correlated with firm size which is observed).

**Decision:**
- Halt coding, revise codebook: "Vendor Trust (Relationship/Brand)" and "Data Security / Compliance Concerns" are split into two distinct codes with anchoring examples.
- Re-calibration session with all 6 coders on a fresh 15% sample; achieve κ = 0.78 before resuming full coding.
- For missing "current ERP vendor": use multiple imputation conditioned on firm size, industry, and revenue band. Flag imputed cases in output tables with a footnote.

**Result:** After recoding, "Data Security / Compliance Concerns" emerges as the #1 purchase barrier at 67% mention rate — previously obscured because it was merged with "Vendor Trust" (which was only 31%). The client's go-to-market strategy pivots to lead with compliance certifications rather than relationship-based sales. This is a material strategic shift driven entirely by cleaning quality.

**Anti-Example:** In an earlier engagement (different project, same firm), the team accepted the original κ = 0.41 coding, presented "Trust/Security" as a combined 58% barrier, and recommended a relationship-first GTM. The client launched, found sales cycles dominated by compliance due-diligence (not relationship meetings), and returned for a strategy revision six months later — a $300K re-engagement that could have been avoided with a coding calibration session.

---

### Scenario 3: AI/ML — Cleaning Training Data for a Customer Support Intent Classification Model

**Trigger:** An AI product team at a FinTech company is building an NLP model to classify inbound customer support tickets into 12 intent categories. The training dataset of 15,000 labeled tickets (labeled by 4 support agents over 18 months) shows 19% of tickets labeled "Other" — the catch-all category — and Cronbach's alpha on the inter-agent labeling consistency composite is 0.58.

**Analysis:**
- The "Other" category is over-used (should be < 5% in a well-designed taxonomy) — agents are using it as a dustbin for tickets they find ambiguous or time-consuming to classify.
- Cronbach's alpha of 0.58 confirms agents are not consistently interpreting category boundaries.
- Random sample of 200 "Other" tickets reveals: 41% belong to existing categories (agents just didn't want to decide), 33% belong to two emerging categories not in the original taxonomy ("API Integration Issues" and "Regulatory Document Requests"), and 26% are genuinely uncategorizable.

**Decision:**
- Add two new intent categories: "API Integration Issues" and "Regulatory Document Requests."
- Re-label all 15,000 tickets using updated taxonomy with a calibrated two-agent system (κ target ≥ 0.80 for model training data — higher standard than research because model performance depends on it).
- Genuine "Other" (26% of original "Other" bucket, ~750 tickets) retained as "Other" with a confidence flag; model trained to route these to human review rather than auto-classify.
- Post-recoding Cronbach's alpha on labeling consistency: 0.81.

**Result:** Model accuracy improves from 68% to 83% on the test set. "Other" category drops from 19% to 4.8% of training data. Human review queue is reduced by 60% because the model can now confidently classify what was previously labeled as ambiguous. The two new intent categories reveal product gaps that are escalated to the product team as high-priority roadmap items.

**Anti-Example:** The initial model was trained on the uncleaned 15,000-ticket dataset as-is. The model learned to predict "Other" at a 19% base rate, and more insidiously, learned to route regulatory document requests (which are time-sensitive) into the generic "Account Management" bucket — resulting in a 48-hour average response time for regulatory queries. Two enterprise clients filed complaints and one escalated to a regulatory body. The root cause was dirty training data, not model architecture.

---

## Practitioner Playbook

**Context:** You are a PM, strategy consultant, or AI lead responsible for delivering a data-driven recommendation. You have just received a raw dataset from a field team or data engineering pipeline.

1. **Before touching the data, retrieve or create the data dictionary.** Confirm every variable's name, type, allowable range, coding scheme, and unit of measurement. If no dictionary exists, create one now — before cleaning decisions are made — so you are not post-hoc rationalizing choices.

2. **Run a dataset profile report.** Use tools appropriate to your stack (Pandas Profiling, ydata-profiling, Power BI's data profiling, or manual frequency tables in Excel). Review: row count, column count, data types per column, % missing per column, value distributions (min/max/mean/median), and cardinality of categorical variables.

3. **Check for duplicates at the unit of analysis level.** Define your unit of analysis (respondent, customer, ticket, transaction) and identify duplicate records at that level. Determine the source of duplication (system error, double entry, data merge artifact) and document your deduplication rule.

4. **Assess missing data patterns.** For each variable with > 1% missing: (a) run Little's MCAR test across the full dataset, (b) create a missing data heatmap to visualize whether missingness is clustered by row, column, or subgroup, (c) classify each variable's missing mechanism as MCAR, MAR, or MNAR.

5. **Select and apply the appropriate missing data strategy per variable.** MCAR + < 5%: listwise deletion acceptable. MAR: multiple imputation using predictors of missingness. MNAR: create a binary missingness indicator variable; consider sensitivity analysis with and without imputation; disclose as a limitation.

6. **Identify and classify outliers.** Run Z-score (for normal distributions) or IQR fence analysis (for skewed distributions) on all continuous variables. For each flagged outlier: determine whether it is a measurement error (fix or delete), a data entry error (correct if source is available, otherwise delete), or a legitimate extreme value (retain with Winsorization or as-is with documentation).

7. **Standardize formats and categories.** Harmonize all categorical values to a single canonical form (e.g., "delhi" / "Delhi" / "New Delhi" → "New Delhi"). Standardize date formats, currency units, and measurement units across all records. Apply recoding rules from the data dictionary.

8. **Code qualitative/open-ended data using the calibrated codebook.** If this is the first coding pass: draft codebook, pilot on 20% sample, calculate inter-rater reliability (Cohen's Kappa), achieve κ ≥ 0.70, then proceed to full coding with spot-checks. If updating an existing codebook: document all changes before re-coding.

9. **Validate dummy coding for categorical variables destined for regression or ML models.** Confirm reference category is explicitly defined and excluded. Confirm there are no collinearity issues between dummy variables. Confirm the data dictionary documents which category is the reference group.

10. **Recalculate reliability for composite scores and indices post-cleaning.** For any composite variable (engagement score, satisfaction index, risk rating), re-run Cronbach's alpha on the cleaned dataset. If α drops below 0.70, revisit item selection before finalizing the composite.

11. **Conduct a logic and consistency audit.** Check cross-variable logical consistency: (a) age vs. years of experience, (b) role/seniority vs. reported decision-making authority, (c) stated NPS score vs. selected "reason for score" direction, (d) timestamp sequences (e.g., account created before first login). Flag and resolve all inconsistencies with documented decisions.

12. **Update the data dictionary and create a cleaning audit log.** The audit log records: issue identified, action taken, number of records affected, analyst name, and date. This document becomes part of the research methodology appendix in consulting deliverables and the model card in AI deployments.

13. **Recalculate effective sample size and check against minimum required N.** Confirm the post-cleaning effective N still satisfies the power requirements of your analysis (e.g., required for the desired significance level and effect size). If not: escalate before proceeding. Do not analyze under-powered data without explicit client/stakeholder acknowledgment.

14. **Run a final sanity check against external benchmarks.** Compare key distributions (churn rate, NPS, response rate by segment, top pain points) against industry benchmarks, previous wave data, or regional norms. Significant deviations are red flags — either your data is unique and requires explanation, or cleaning introduced an error.

15. **Lock the cleaned dataset and archive the raw dataset separately.** The cleaned dataset used for final analysis is version-controlled, read-only, and date-stamped. The raw dataset is preserved in a separate archive. Any future changes to the cleaned dataset require a new version with a new audit log entry — never overwrite the analysis dataset.

---

## Content Critique & Depth Gaps

**What the source content covers adequately:**
The source material provides an accessible, introductory-level overview of data preparation concepts suitable for undergraduate marketing courses or practitioner onboarding. The use case (survey cleaning) and scenario (city name harmonization) are appropriately concrete for foundational understanding.

**Critical gaps for IIM/HBS MBA-level depth:**

1. **No treatment of missing data mechanisms.** The source lumps all missing data into "check for missing values" without distinguishing MCAR, MAR, and MNAR. This distinction is foundational to choosing the correct remedy — and choosing wrong introduces systematic bias that invalidates conclusions. No MBA-level marketing research course should present data preparation without this taxonomy.

2. **No discussion of imputation methods or their trade-offs.** Mean imputation, multiple imputation, k-NN imputation, and model-based imputation have fundamentally different implications for variance, bias, and downstream statistical inference. The source implies "fill in or remove" without addressing the consequences.

3. **Absent: outlier taxonomy and treatment philosophy.** The source gives one example of an obvious invalid response (age = 300) but does not address legitimate outliers, the distinction between errors and extreme values, or methods like Winsorization. In business analytics, this gap leads to either over-deletion (losing information) or under-deletion (distorting analysis).

4. **No inter-rater reliability framework for qualitative coding.** The source mentions coding open-ended responses but provides no framework for ensuring coding consistency (Cohen's Kappa, calibration sessions, codebook design). In consulting and UX research, inconsistent coding is one of the most common sources of flawed findings.

5. **No reliability assessment for composite variables.** Cronbach's alpha and its post-cleaning application are absent. Any research that constructs composite scores (customer satisfaction indices, risk scores, engagement scores) without reliability checks is methodologically incomplete.

6. **No audit trail or documentation standards.** The source treats data preparation as a technical task rather than a governance responsibility. In consulting, regulatory contexts, and AI model development, the cleaning audit log is as important as the cleaned data itself — and is often legally required.

7. **Absent: data preparation in automated/pipeline contexts.** The source frames data preparation as a manual, post-collection activity. For IT/AI/Product roles, data preparation happens in real-time ingestion pipelines, requires validation rule design, and must be robust to adversarial inputs. Tools like dbt, Great Expectations, and Apache Spark data quality frameworks are not mentioned.

8. **No discussion of the data preparation – analysis boundary.** Where does legitimate cleaning end and data manipulation begin? This ethical boundary is critical for consulting integrity and AI governance — but the source does not address it.

9. **Absent: cross-dataset join scenarios.** In practice, most business datasets are merged from multiple sources (CRM, survey, transactional, behavioral). Data preparation for merged datasets introduces new classes of problems (key mismatches, format conflicts, duplicate emergence post-join) that are absent from the source.

10. **No power analysis check post-cleaning.** Dropping rows through cleaning reduces effective sample size. The source does not prompt analysts to verify that post-cleaning N still satisfies the minimum sample size requirements for the planned analysis — a critical step before proceeding.

---

## Quick-Recall Card

**Data Preparation — What Every MBA/PM/AI Lead Must Remember**

- Data preparation is the highest-leverage point in any analysis pipeline: errors introduced here compound through every downstream step.
- Raw data always contains errors. Never analyze without cleaning. Never clean without documenting.
- The missing data mechanism (MCAR / MAR / MNAR) determines your remedy — diagnose before treating.
- MCAR: deletion is acceptable. MAR: use multiple imputation. MNAR: the absence itself is a signal — treat it as a variable, not a gap.
- Missing data > 5% requires imputation with documentation. Missing data > 40% on a single variable: consider dropping the variable.
- Outliers are not automatically errors. Distinguish measurement errors from legitimate extreme values before deleting anything.
- Z-score |Z| > 3.0 (large samples) or IQR fence analysis (skewed distributions) are your primary outlier detection tools.
- Winsorize rather than delete when the outlier contains real business information.
- Cohen's Kappa ≥ 0.70 is the minimum inter-rater reliability threshold before full coding of qualitative data proceeds.
- Cronbach's alpha ≥ 0.70 is the minimum internal consistency threshold for any composite score or index.
- The data dictionary is not optional — it is the contract between data producers and data consumers.
- The cleaning audit log is not a nice-to-have — in consulting it is a methodology artifact; in AI it is a model governance requirement.
- Preserve raw data separately, read-only. All cleaning is done on copies. Never overwrite raw data.
- Post-cleaning, verify effective N still meets minimum sample size requirements for your planned statistical tests.
- Harmonize before you analyze: city names, date formats, currency units, gender codes — all must be standardized before a single chart is drawn.
- In ML/AI pipelines, data preparation is ongoing — streaming data requires validation rules at ingestion, not just at project kick-off.
- The boundary between cleaning and manipulation is ethical, not technical — document every decision and apply rules uniformly across all subgroups.

**As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Is every decision made during data preparation documented, defensible, and applied consistently — such that a skeptical peer, regulator, or client could reconstruct the path from raw data to cleaned dataset and trust that the results reflect reality rather than the choices made in cleaning?"**

---

## Self-Audit Report

<!-- Self-Audit:
SECTION COMPLETION CHECK:
[x] Section 1 - Jargon Buster: 12 terms included (minimum 8 required). All 8 mandatory terms present: imputation, outlier treatment, dummy coding, data dictionary, MCAR, MAR, MNAR, data validation. Additional terms: editing, coding, tabulation, Winsorization. Each term includes IT/AI/Product/Consulting lens in "Why It Matters" column.
[x] Section 2 - Frameworks & Mental Models: 3 frameworks with ASCII diagrams: (1) Data Preparation Pipeline (full end-to-end flow), (2) Missing Data Taxonomy MCAR/MAR/MNAR (branching decision tree), (3) Coding Workflow for open-ended responses. All three required frameworks included.
[x] Section 3 - Formulas, Thresholds & Rules of Thumb: Missing data thresholds (< 5%, 5-15%, 15-40%, > 40%), Z-score outlier formula and thresholds, IQR fence formula, Cronbach's alpha formula and interpretation table, Cohen's Kappa formula and thresholds, response rate and effective N formulas. All include practical rules of thumb.
[x] Section 4 - Do / Don't: 10 Do items and 10 Don't items (minimum 8 each required). All items are specific, actionable, and written with IT/AI/Product/Consulting context.
[x] Section 5 - Metric-Driven Scenarios with Anti-Examples: 3 scenarios included. Each follows exact structure: Trigger → Analysis → Decision → Result → Anti-Example. Industries covered: SaaS/AI (churn prediction), Management Consulting (market entry), AI/ML (NLP intent classification).
[x] Section 6 - Practitioner Playbook: 15 numbered steps covering the full data preparation workflow from data dictionary retrieval through final dataset locking. Step-by-step, operational, role-appropriate for PM/Consultant/AI Lead.
[x] Section 7 - Content Critique & Depth Gaps: 10 distinct gaps identified with specific methodology names, IIM/HBS MBA standards referenced explicitly.
[x] Section 8 - Quick-Recall Card: Bullet-format summary. Final line begins exactly "As a PM/Consultant/AI Lead" as required.
[x] Section 9 - Self-Audit Report: This comment block.

INDUSTRY LENS CONSISTENCY: IT/AI/Product/Consulting lens applied throughout all sections. Specific tool references (dbt, Great Expectations, Pandas Profiling, Mixpanel, Amplitude, Spark) grounded in current industry practice.

ESTIMATED FILE SIZE: Approximately 18-20 KB — exceeds 13 KB minimum requirement.

CONNECTS TO: Links section intentionally positioned after Self-Audit per standard file structure.

QUALITY FLAGS:
- All formulas include symbolic notation and plain-English variable definitions.
- All thresholds include interpretation guidance, not just numbers.
- Anti-examples in Section 5 include specific, plausible business consequences (not generic warnings).
- Playbook steps are sequenced for dependency — cannot be reordered arbitrarily.
- No section omitted. No generic filler content — every bullet and row carries specific, MBA-applicable information.
-->

---

**Connects to:**
- [01-introduction-to-marketing-research.md](./01-introduction-to-marketing-research.md) — foundational context for why data quality determines research validity
- [05-questionnaire-design.md](./05-questionnaire-design.md) — instrument design decisions that create or prevent data preparation problems
- [07-sampling.md](./07-sampling.md) — sample size and composition decisions that interact with post-cleaning effective N
- [08-data-collection.md](./08-data-collection.md) — field and digital collection methods that determine the types of errors introduced
- [10-data-analysis.md](./10-data-analysis.md) — analysis methods that data preparation must be calibrated to support
- [11-reporting-and-presentation.md](./11-reporting-and-presentation.md) — how cleaning decisions and limitations must be disclosed in final deliverables
