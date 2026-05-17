# Questionnaire Design

## Overview

Questionnaire design means writing survey questions in a way that people can understand and answer honestly.

---

## Why It Matters

Bad questions create bad data. A well-designed questionnaire reduces confusion, bias, and wrong answers.


## Key Principles

- Use simple wording
- Ask one idea per question (avoid double questions)
- Avoid leading questions
- Keep flow logical (easy → sensitive)


## Key Terms

| Term | Definition |
|------|------------|
| **Leading question** | Pushes a certain answer (“Don’t you agree…?”) |
| **Double-barreled question** | Two questions in one (“price and quality”) |
| **Pretest/Pilot** | Testing the survey on a small group first |
| **Response options** | The answer choices given |


## Use Case

An e-commerce site surveys customers after delivery to measure satisfaction and find the biggest problems.


## Scenario

> A survey asks: “How great was our excellent service?” People feel forced to be positive. After rewriting neutrally, responses become more accurate.


## Examples

- Bad: “Are you satisfied with price and quality?” Good: separate into two questions.
- Bad: “Our support is fast, right?” Good: “How would you rate our support speed?”

---

## Audited Appendix

# Questionnaire Design

**Overview:** Questionnaire design means writing survey questions in a way that people can understand and answer honestly. It is both an art and a science — word choice, question order, response scales, and skip logic all interact to either surface truth or manufacture distortion.

**Why It Matters:** Bad questions create bad data. In IT/AI/Product/Consulting contexts, flawed questionnaires lead to misallocated roadmap investment, inaccurate NPS benchmarks, and faulty model training labels. A well-designed questionnaire reduces confusion, bias, and wrong answers — making downstream analytics trustworthy.

**Key Principles:**
- Use simple, unambiguous wording
- Ask one idea per question (avoid double-barreled questions)
- Avoid leading or loaded questions
- Keep flow logical: easy to sensitive, general to specific
- Pilot before full deployment

**Key Terms:** Leading question, Double-barreled question, Pretest/Pilot, Response options, Acquiescence bias, Social desirability bias, Skip logic, Cognitive burden

**Use Case:** An e-commerce SaaS platform surveys enterprise customers post-onboarding to measure feature adoption satisfaction and surface the biggest friction points in their workflow.

**Scenario:** A product team asks: "How great was our excellent AI-powered onboarding?" Respondents feel socially pressured to agree. After rewriting neutrally — "How would you rate your onboarding experience?" with a balanced 5-point scale — variance increases and true pain points emerge.

**Examples:**
- Bad: "Are you satisfied with price and quality?" Good: separate into two questions.
- Bad: "Our AI assistant is fast, right?" Good: "How would you rate the response speed of our AI assistant?"

**Connects to:** [05-sampling-methods.md](05-sampling-methods.md) | [07-scales-and-measurement.md](07-scales-and-measurement.md) | [08-data-collection-methods.md](08-data-collection-methods.md) | [09-validity-and-reliability.md](09-validity-and-reliability.md)

---

## Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| **Acquiescence Bias** | The tendency of respondents to agree with statements regardless of their actual views — also called "yes-saying." | Inflates positive ratings of product features; AI training labels built on survey data inherit this bias, causing models to overestimate user satisfaction. Use balanced agree/disagree scales and reverse-coded items to detect it. |
| **Social Desirability Bias** | Respondents answer in a way they believe is socially acceptable or expected rather than truthfully. | In consulting surveys about digital adoption, employees overstate technology usage. Anonymity guarantees and behavioral anchors (e.g., "most people do X — do you?") reduce this. |
| **Order Effects** | The sequence in which questions appear influences how respondents answer subsequent questions. | In a product feedback survey, placing NPS first before feature questions anchors sentiment; placing it after detailed critique typically lowers scores. Randomizing question blocks in digital surveys controls this. |
| **Funnel Technique** | Structuring questions from broad/general to narrow/specific, mirroring how respondents mentally approach a topic. | Opens respondents comfortably, reduces early dropout, and ensures broader context is captured before eliciting specific AI/product feedback that requires cognitive effort. |
| **Skip Logic** | Conditional branching rules that route respondents to different questions based on previous answers. | Prevents irrelevant questions (e.g., asking about "cloud migration experience" to respondents who answered "we use on-premise only"), reduces cognitive burden, and improves data quality in multi-segment IT surveys. |
| **Open-Ended vs Closed-Ended** | Open-ended questions allow free-text responses; closed-ended questions offer pre-defined response options. | Open-ended surfaces unexpected insights (e.g., a new AI use-case no one anticipated) but is hard to quantify. Closed-ended enables benchmarking and statistical analysis. Best practice: use both — closed for metrics, open for depth. |
| **Response Rate** | The percentage of people who complete the survey out of all who were invited. | Low response rates (below 30% for B2B) create non-response bias — the people who do respond may not represent the full population. A 5% response rate on an AI feature survey could mean only power users replied. |
| **Cognitive Burden** | The mental effort required to understand and answer a question. | Long surveys, complex wording, and unfamiliar terminology in IT/AI questionnaires cause respondent fatigue, leading to straightlining (same answer repeatedly) and early dropout. Target under 12 minutes for enterprise respondents. |
| **Leading Question** | A question that implicitly or explicitly suggests a particular answer. | "How much has our AI platform accelerated your team's productivity?" presupposes acceleration occurred. This inflates perceived performance metrics and makes competitive benchmarking unreliable. |
| **Double-Barreled Question** | A question that asks about two separate issues simultaneously, forcing a single response. | "Are you satisfied with our pricing and customer support?" If pricing is poor but support is excellent, no answer option is accurate. Always decompose into separate questions. |
| **Pilot / Pretest** | Running the questionnaire on a small sample (5–30 people) before full deployment to identify problems. | Catches confusing wording, skip logic errors, and underestimated completion time before the survey goes to thousands of enterprise clients or is embedded in a product flow. |
| **Response Options / Scale Design** | The set of choices offered to respondents (e.g., Likert scale, semantic differential, ranking). | A 4-point scale forces a lean; a 5-point allows neutrality; a 7-point adds granularity. For AI satisfaction surveys, the scale design must match the statistical method planned for analysis. |

---

## Frameworks & Mental Models

### 1. Question Quality Checklist (CLEAR Framework)

Before any question goes live, run it through CLEAR:

```
+--------------------------------------------------------------+
|              QUESTION QUALITY: CLEAR CHECKLIST               |
+--------------------------------------------------------------+
|                                                              |
|  C — Clear?         Is the wording unambiguous?             |
|       YES ---> continue    NO ---> rewrite                  |
|                                                              |
|  L — Leading?       Does it suggest an answer?              |
|       NO  ---> continue    YES ---> neutralize              |
|                                                              |
|  E — Exclusive?     Are response options mutually           |
|                     exclusive and exhaustive?               |
|       YES ---> continue    NO ---> redesign options         |
|                                                              |
|  A — Answerable?    Can respondents actually know/          |
|                     recall what you're asking?              |
|       YES ---> continue    NO ---> add context or cut       |
|                                                              |
|  R — Relevant?      Is this question tied to a             |
|                     research objective?                     |
|       YES ---> keep        NO ---> remove                   |
|                                                              |
+--------------------------------------------------------------+
| Apply to EVERY question before pilot deployment.            |
+--------------------------------------------------------------+
```

---

### 2. Funnel Structure for Questionnaire Opening

The funnel technique moves from broad awareness to specific product/AI experience:

```
      BROAD GENERAL CONTEXT
     /                      \
    / "Overall, how would    \
   /   you rate your         \
  /    experience with        \
 /     AI tools at work?"      \
/________________________________\
         CATEGORY LEVEL
        /              \
       / "In the past    \
      /   3 months, how   \
     /   often did you     \
    /   use [Product X]?"   \
   /__________________________\
            FEATURE LEVEL
           /            \
          / "How helpful  \
         /  was Feature Y  \
        /   in completing   \
       /    Task Z?"         \
      /______________________\
               SENSITIVE / SPECIFIC
              /                    \
             / "Would you recommend  \
            /  this AI product to a   \
           /   colleague? (NPS)"       \
          /____________________________\
```

**Why Funnel Works in IT/Product Surveys:** It primes respondents with context before asking specific questions, reduces misinterpretation, and captures macro sentiment before micro details. Placing NPS at the end — after users have actively recalled specific experiences — yields more grounded scores than placing it first.

---

### 3. Questionnaire Flow Map (End-to-End)

```
+------------------+
|  Research Obj.   |  Define: What decisions will this data drive?
+--------+---------+
         |
         v
+------------------+
|  Draft Questions  |  Apply CLEAR checklist; map each question to
|  (per objective)  |  an objective; assign open/closed type
+--------+---------+
         |
         v
+------------------+
|  Design Response  |  Choose scale type; ensure exhaustive options;
|  Options & Scales |  add "Prefer not to answer" where appropriate
+--------+---------+
         |
         v
+------------------+
|  Set Skip Logic  |  Route by segment: Enterprise vs SMB vs Consumer;
|  & Branching     |  route by role: PM vs Developer vs Executive
+--------+---------+
         |
         v
+------------------+
|  Order & Group   |  Funnel structure; group by theme; warm-up first,
|  Questions       |  sensitive last; demographics at end
+--------+---------+
         |
         v
+------------------+
|  Pilot Test      |  n = 5–30; measure time, dropout points,
|  (Internal/Ext.) |  confusion; iterate
+--------+---------+
         |
         v
+------------------+
|  Deploy & Monitor |  Track partial completes; monitor early response
|                   |  rates; check for straightlining
+--------+---------+
         |
         v
+------------------+
|  Clean & Analyze |  Remove speeders (<1/3 expected time); remove
|                   |  straightliners; weight if needed
+------------------+
```

---

### 4. Question Type Decision Tree

```
What do you need to measure?
         |
         +----> ATTITUDE / OPINION -----> Likert Scale (5 or 7 pt)
         |                                or Semantic Differential
         |
         +----> BEHAVIOR / FREQUENCY ---> Ordinal Scale
         |                                (Never / Rarely / Sometimes / Often / Always)
         |
         +----> RANKING / PRIORITY -----> Rank-Order Question
         |                                (drag-and-drop in digital)
         |
         +----> OPEN EXPLORATION -------> Open-Ended / Text Box
         |                                (for qualitative insight)
         |
         +----> YES/NO SCREENER --------> Dichotomous Question
         |                                + Skip Logic
         |
         +----> NET PROMOTER SCORE -----> 0-10 Scale (validated)
                                          Placed AFTER feature questions
```

---

## Formulas, Thresholds & Rules of Thumb

### Response Rate Benchmarks (IT/B2B/SaaS Context)

| Survey Channel | Expected Response Rate | Acceptable Minimum |
|---|---|---|
| In-product survey (post-action trigger) | 20–45% | 15% |
| Email survey (existing customers) | 15–30% | 10% |
| Email survey (cold/prospect) | 2–10% | 5% |
| Embedded Slack/Teams survey | 10–25% | 8% |
| NPS survey (quarterly, warm base) | 25–40% | 20% |
| User research panel | 50–70% | 40% |

**Rule of Thumb:** If response rate falls below the acceptable minimum, non-response bias is a serious concern. Conduct a non-response follow-up with a short 3-question version to compare with full respondents.

---

### Pilot Sample Size Guidelines

| Survey Length | Pilot Sample Size | Purpose |
|---|---|---|
| Under 10 questions | 5–8 participants | Catch wording issues |
| 10–25 questions | 10–15 participants | Catch flow, skip logic, time |
| 25–50 questions | 20–30 participants | Full simulation |
| Over 50 questions | 30+ participants | Detect fatigue and dropout points |

**Formula — Expected Completion Time:**
```
Estimated Time (minutes) = Number of Questions × 0.5 (closed-ended)
                          + Number of Open-Ended Questions × 2.0

Example: 15 closed + 3 open = (15 × 0.5) + (3 × 2.0) = 7.5 + 6.0 = 13.5 minutes
Target: Under 12 minutes for enterprise B2B; under 8 minutes for consumer
```

---

### Question Count Limits (by Survey Type)

| Survey Type | Recommended Maximum | Hard Cap |
|---|---|---|
| In-app micro-survey | 3–5 questions | 7 |
| Post-purchase / post-service | 8–12 questions | 15 |
| Quarterly NPS / relationship survey | 12–20 questions | 25 |
| Annual employee engagement | 30–50 questions | 60 |
| Academic / UX deep dive | 50–80 questions (moderated) | 100 |

---

### Likert Scale Rules

- **Odd vs Even number of points:** Use odd (5, 7) to allow neutral; use even (4, 6) to force a lean — choose deliberately based on research goal.
- **7-point scales** yield higher reliability coefficients (Cronbach's alpha) but require more cognitive effort.
- **5-point scales** are the industry standard for NPS-adjacent satisfaction measurement.
- **Never mix scale directions** within a single questionnaire without clearly marking reversals.

---

### Cronbach's Alpha Benchmark (Scale Reliability)

```
Alpha >= 0.90  --> Excellent reliability (risk: over-redundant items)
Alpha 0.80–0.89 --> Good reliability (target for published research)
Alpha 0.70–0.79 --> Acceptable (minimum for product decisions)
Alpha < 0.70   --> Poor — redesign the scale
```

---

### Response Distribution Red Flags

| Pattern | Name | Threshold for Concern |
|---|---|---|
| All answers identical | Straightlining | > 5 consecutive same-scale responses |
| Completion time too fast | Speeding | < 1/3 of median expected time |
| All extreme responses | End-anchoring | > 90% using only endpoints |
| All middle responses | Central tendency bias | > 70% using only midpoint |

---

## Do / Don't

### DO

1. **Do map every question to a research objective** before drafting — if a question cannot be tied to a specific decision, cut it. In AI product surveys, this prevents collecting interesting-but-useless data.

2. **Do use plain language at a Grade 8 reading level** — even for technical audiences. Complexity creates ambiguity. "How often do you utilize the platform's asynchronous inference endpoint?" should become "How often do you use the AI feature that gives you results later, not instantly?"

3. **Do pilot test with 5–30 people** from your actual target population before full deployment. For a developer-focused survey, pilot with developers — not PMs.

4. **Do place sensitive or personal questions at the end** after rapport has been established. Demographic questions (role, company size, income bracket) should come last unless used as a screener.

5. **Do offer "Not applicable" or "I don't know"** as response options when the question may not apply to all segments. Forcing a response on irrelevant questions creates noise.

6. **Do use balanced Likert scales** — equal number of positive and negative options (e.g., Strongly Agree / Agree / Neither / Disagree / Strongly Disagree) to reduce acquiescence bias.

7. **Do randomize response option order** in digital surveys where possible (except for inherently ordered scales) to control for primacy and recency effects.

8. **Do set a clear maximum survey length** before design begins, and cut ruthlessly to stay within it. Use the estimated completion time formula to verify.

9. **Do include a brief explanation of how data will be used** in the survey introduction — this increases trust, honesty, and response rate, particularly in enterprise IT surveys where data sensitivity is a concern.

10. **Do track partial completions** and analyze dropout points — a spike in dropouts after a specific question is a signal to rewrite or reorder that question.

---

### DON'T

1. **Don't write double-barreled questions.** "Are you satisfied with our pricing and the quality of AI outputs?" cannot be answered honestly with a single response. Split every compound idea.

2. **Don't use leading or loaded language.** "How has our award-winning platform improved your workflow?" presupposes improvement. Strip all evaluative language from question stems.

3. **Don't use industry jargon without definition.** Asking SMB respondents about "LLM inference latency" or "API throughput" yields meaningless data if the terms are unfamiliar.

4. **Don't ask hypothetical future questions as if they measure real behavior.** "Would you pay $50/month for this feature?" consistently over-predicts actual willingness to pay by 40–60%. Use behavioral proxies or conjoint analysis instead.

5. **Don't rely solely on open-ended questions** for quantitative decision-making. Qualitative text requires coding and is not scalable for large samples without NLP tooling.

6. **Don't skip the pilot test** under time pressure. A flawed questionnaire deployed to 5,000 customers produces 5,000 rows of bad data — faster than a pilot would have taken.

7. **Don't bury the most important question** at the end of a long survey where fatigue is highest. Key metrics (NPS, CSAT, primary decision variable) should appear when engagement is still high — typically questions 3–7 in a 15-question survey.

8. **Don't make every question mandatory** — forcing responses increases satisficing (choosing any answer just to proceed) rather than honest engagement. Make critical items required; make others optional.

9. **Don't ignore non-response bias.** If only 8% of your enterprise customers responded, the 92% who did not may have entirely different satisfaction levels. Always analyze who did not respond.

10. **Don't use more than one open-ended question per 5 closed-ended questions** in digital surveys — cognitive fatigue from text entry is disproportionately high and causes dropout spikes.

---

## Metric-Driven Scenarios with Anti-Examples

### Scenario 1: NPS Survey Redesign for a SaaS AI Platform

**Trigger:** A B2B AI platform's quarterly NPS survey shows 72% of responses are either 9 or 10 (Promoters), but the product team is simultaneously seeing a 25% monthly churn rate among mid-market accounts. The numbers don't add up.

**Analysis:** The product manager audits the survey. The NPS question was preceded by five questions all framed positively: "How much has [Platform] accelerated your work?", "How much time has [Platform] saved you?", etc. Every question primes respondents toward a positive mindset before the NPS scale appears. Additionally, the survey was sent only to power users (5+ logins/month), excluding churned accounts and low-engagement users entirely. This creates selection bias stacked on top of question order effects.

**Decision:** Redesign the survey with three changes: (1) Neutralize the pre-NPS questions to remove positive framing; (2) Place NPS as question 3 of 10 instead of question 8 of 10; (3) Include all account holders with at least one login in the past 90 days, not just active power users.

**Result:** After redesign, NPS drops from +62 to +34. The distribution now reflects actual account health — 18% Detractors (previously invisible). The product team identifies two feature gaps driving detraction: poor CSV export functionality and missing SSO support. Both are added in the next sprint cycle. Churn rate drops 11% over the following quarter.

**Anti-Example:** The team keeps the original survey but adds a single open-ended question: "What could we do better?" They use the 28 responses they receive to guide roadmap decisions. But because only Promoters typically respond to open-ended questions (Detractors churn silently), the feedback skews toward nice-to-have features rather than table-stakes problems. The 25% churn rate continues unchanged.

---

### Scenario 2: Employee AI Adoption Survey in a Consulting Firm

**Trigger:** A global consulting firm's IT leadership wants to understand actual AI tool adoption rates across 2,000 consultants after rolling out a suite of generative AI tools. The survey results show 89% claiming "regular use" — but software telemetry shows only 31% of licenses have had meaningful activity in the past 30 days.

**Analysis:** The survey question read: "How regularly do you use our AI tools to support client work?" with options: Always / Often / Sometimes / Rarely / Never. Given that AI adoption was a firm-wide strategic initiative announced by the Managing Partner, consultants face strong social desirability pressure to report high usage. The question also lacks behavioral anchoring — "regularly" is undefined. Someone who opened the tool once could reasonably select "Sometimes."

**Decision:** Redesign the survey with behavioral anchoring and anonymity assurance. New question: "In a typical work week, approximately how many times do you open and actively use any AI tool for a client deliverable?" with options: 0 times / 1–2 times / 3–5 times / 6–10 times / More than 10 times. Add an explicit anonymity guarantee in the survey header and remove the manager from the distribution list to prevent identification anxiety.

**Result:** Redesigned survey shows 29% reporting 0 times per week — consistent with the 31% active license figure from telemetry. The gap closes from 58 percentage points to 2 percentage points. The firm now has actionable data: non-adopters cluster in financial services practice and cite "lack of client-approved use" and "insufficient training" as primary barriers. Targeted enablement programs address these specifically.

**Anti-Example:** IT leadership accepts the 89% adoption figure and reports success to the board. AI tool license costs are renewed and expanded. Twelve months later, a vendor audit reveals the same 30% active usage pattern. The firm has overpaid by approximately $2.1M in underused licenses.

---

### Scenario 3: Feature Prioritization Survey for an AI Product Roadmap

**Trigger:** A product team at an AI startup needs to prioritize five potential features for the next quarter. They run an "importance" survey asking: "How important is [Feature X] to you?" on a 5-point scale for each feature. All five features score between 4.1 and 4.4 out of 5. The survey provides no actionable differentiation.

**Analysis:** The "importance" scale suffers from ceiling effects — respondents rate everything as important because there is no cost to doing so. This is a classic problem with unbounded importance questions: users in IT/AI contexts will report every potential feature as highly important because they feel it should be built. Without forced trade-offs, the data is noise.

**Decision:** Replace the importance scale with a MaxDiff (Best-Worst Scaling) exercise. Present respondents with sets of 4 features at a time and ask: "Which of these would be most valuable to your work? Which would be least valuable?" Rotate through all feature combinations. This forces relative prioritization and eliminates the ceiling effect.

**Result:** MaxDiff analysis reveals Feature C (real-time collaboration on AI outputs) has a utility score 2.8x higher than the next-best feature (B: custom prompt templates). The team deprioritizes Features D and E — both of which had scored 4.2/5 on importance but rank last in MaxDiff. Feature C ships in Q2 and drives a 19% increase in team-plan upgrades.

**Anti-Example:** The team uses the importance ratings to prioritize the feature with the highest average score (4.4/5 — Feature A: Dark Mode). They invest one sprint on dark mode. Usage data shows dark mode adoption at 12%. Meanwhile, competitors ship real-time collaboration and begin capturing enterprise deals.

---

## Practitioner Playbook

A step-by-step process for designing a rigorous questionnaire in an IT/AI/Product/Consulting context.

1. **Define the research objectives before writing a single question.** List 3–5 specific decisions that survey data will inform. Example: "We need to decide whether to build SSO support in Q3 or deprioritize it." Each objective generates a question cluster.

2. **Identify respondent segments and their knowledge levels.** A survey sent to enterprise IT administrators requires different vocabulary than one sent to end-users or C-suite executives. Define personas and write to the lowest-common-denominator technical literacy within each segment.

3. **Draft a question outline mapped to objectives.** Create a two-column mapping: Research Objective | Candidate Questions. Ensure every question appears in at least one objective row. Discard any orphaned questions.

4. **Choose question types deliberately.** Use the decision tree (see Frameworks section) to assign the correct type to each question: Likert, dichotomous, open-ended, rank-order, MaxDiff, semantic differential, or behavioral frequency scale.

5. **Write first drafts of all questions and apply the CLEAR checklist.** Run every question through: Clear? Leading? Exclusive options? Answerable? Relevant? Rewrite any that fail any criterion.

6. **Design response options carefully.** Ensure scales are balanced, options are mutually exclusive and collectively exhaustive, "Not Applicable" is included where needed, and scale direction is consistent throughout (unless intentionally reversed for bias detection).

7. **Map skip logic and branching.** Identify which questions only apply to certain respondent sub-groups. Build the branching logic in a flowchart before implementing in the survey platform (Qualtrics, Typeform, SurveyMonkey, etc.). Test every logical path.

8. **Order questions using the funnel technique.** Open with broad, easy, low-stakes questions. Move to category-level questions. Introduce feature-specific or sensitive questions in the middle. Place key metrics (NPS, CSAT) after enough context has been established but before fatigue sets in. Place demographic questions last.

9. **Estimate completion time using the formula** (0.5 min per closed question + 2.0 min per open question). If estimate exceeds your target (e.g., 12 minutes for B2B), cut questions that serve the least critical objectives first.

10. **Write a professional survey introduction.** Include: purpose of the survey, estimated completion time, how data will be used, anonymity/confidentiality guarantee, and instructions for any complex question types (e.g., MaxDiff exercises). This increases trust and response quality.

11. **Conduct an internal cognitive pre-test.** Have 3–5 colleagues who are NOT on the project team attempt the survey. After completion, interview them: "Was anything confusing? What did you think question X was asking?" Document all issues.

12. **Conduct an external pilot with 10–30 target respondents.** Deploy to a small slice of the actual target population. Measure: completion time, dropout rate by question, variance in responses (low variance on most items suggests leading or boring questions), and any qualitative feedback.

13. **Analyze pilot data before full deployment.** Check for ceiling/floor effects, near-zero variance items, and unanticipated response patterns. Revise the questionnaire based on findings. Do not skip this step under time pressure.

14. **Deploy with a monitoring plan.** Set alerts for: response rate below acceptable threshold (see benchmarks table), dropout spikes at specific questions, and completion time anomalies (very fast = speeding; very slow = platform issues).

15. **Clean data before analysis.** Remove: speeders (completion time < 1/3 of median), straightliners (same response to all scale items), respondents who fail attention checks (if included), and duplicate IP submissions.

16. **Weight the data if necessary.** If your sample over-represents a particular segment (e.g., enterprise accounts in a survey targeting all tiers), apply post-stratification weights to align sample proportions with population proportions.

17. **Report findings tied explicitly to the original objectives.** Every finding should link back to a decision. "Feature C is the top priority" is not a finding — "Based on MaxDiff results, Feature C should be prioritized over Feature D in Q3 because it has 2.8x higher relative utility" is.

---

## Content Critique & Depth Gaps

The source material on questionnaire design is adequate for an introductory marketing course but falls significantly short of IIM/HBS MBA-level rigor. The following gaps represent what a senior product manager, management consultant, or AI product lead would need to know — and what is missing.

**1. No coverage of psychometric theory.** The source material does not address Cronbach's alpha, construct validity, convergent and discriminant validity, or factor analysis — all of which are required to design scales that are academically defensible or trustworthy for strategic decisions. A questionnaire measuring "AI trust" or "digital readiness" requires validated constructs, not ad-hoc question writing.

**2. Missing discussion of MaxDiff and conjoint analysis.** For product prioritization decisions — a core use case in IT/AI/Product — traditional Likert-based importance scales are provably inferior to MaxDiff (Best-Worst Scaling) and conjoint analysis. The source material only implies that "asking one idea at a time" is sufficient.

**3. No guidance on online survey platforms and their design constraints.** Qualtrics, Typeform, SurveyMonkey, and Google Forms each have different capabilities for skip logic, randomization, and data export. A practitioner needs to know how platform constraints affect design choices.

**4. No coverage of attention checks and data quality controls.** Including "Please select 'Disagree' for this question" or "Which of the following is a color? (Red / Democracy / Quickly)" allows identification and removal of inattentive respondents — a critical quality control mechanism not mentioned in source content.

**5. Missing treatment of longitudinal questionnaire design.** One-time surveys cannot track change over time. Panel surveys and repeated-measures designs require additional considerations: question consistency across waves, attrition management, and carry-over effects. Enterprise AI adoption tracking requires this capability.

**6. No discussion of mixed-methods integration.** Best-practice research in IT/AI/Consulting integrates survey data with behavioral telemetry, CRM data, interview transcripts, and support ticket themes. The source treats the questionnaire as a standalone instrument.

**7. Absent coverage of cultural and cross-national bias.** Global consulting firms and multinational SaaS companies deploy surveys across cultures where scale interpretation differs: East Asian respondents tend toward central tendency; Latin American respondents lean toward extreme positive responses. Neither the source material nor standard introductory texts address this at sufficient depth.

**8. No treatment of AI-assisted questionnaire design.** LLMs can now assist with question generation, bias detection, and cognitive burden estimation. Leading product teams at AI companies use automated pre-screening of draft questions against established bias taxonomies — an emerging practice entirely absent from foundational literature.

**9. Missing discussion of survey fatigue at the organizational level.** Enterprise customers who receive three surveys per quarter from a vendor develop response fatigue and habitually under-engage. Coordinating survey cadence across product, CX, and sales teams is a real operational challenge not addressed.

**10. No connection to causal inference.** Surveys generate correlational data. Practitioners at HBS/IIM level need to understand when to use experimental vignettes within surveys (survey experiments) to approximate causal claims — for example, testing whether a price framing changes willingness to recommend.

---

## Quick-Recall Card

- **Every question must trace to a decision** — if you can't name the decision, cut the question.
- **CLEAR checklist:** Clear, Leading (not), Exclusive options, Answerable, Relevant — run before pilot.
- **Funnel structure:** Broad general → category level → feature specific → sensitive/NPS.
- **Completion time formula:** (n closed × 0.5 min) + (n open × 2.0 min) — target under 12 min for B2B.
- **Response rate red lines:** Under 10% for email = non-response bias risk; investigate who is not responding.
- **Social desirability bias** inflates positive responses on AI adoption, feature satisfaction, and usage frequency — use anonymity guarantees and behavioral anchors.
- **Acquiescence bias** is detected with reverse-coded items — include at least 2 per multi-item scale.
- **Double-barreled = always split** — no exceptions, regardless of survey length pressure.
- **Skip logic** must be flow-charted before platform implementation — never built directly in the tool without a map.
- **Pilot with real target respondents** — internal pilots miss domain-specific confusion.
- **MaxDiff/conjoint** for prioritization; **Likert** for attitude; **behavioral anchors** for frequency — match method to measurement goal.
- **Straightliners and speeders must be removed** before analysis — data cleaning is not optional.
- **Cronbach's alpha below 0.70** means your scale is unreliable — redesign before using data for decisions.
- **Order effects are real** — place NPS after context questions, not as the first item.
- **Non-response bias** is as dangerous as measurement bias — always analyze who did not respond.
- **In AI/product contexts:** survey data alone is insufficient — triangulate with behavioral telemetry and user interviews.

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Are my survey questions designed to surface what respondents actually believe and do, or are they structured — through word choice, order, and framing — to confirm what we already want to hear?"

---

## Self-Audit Report

<!-- Self-Audit: 
SECTION COMPLETENESS CHECK:
[x] Section 1 - Jargon Buster: 12 terms included (minimum 8 required). All 8 mandatory terms present: acquiescence bias, social desirability bias, order effects, funnel technique, skip logic, open-ended vs closed-ended, response rate, cognitive burden. Additional terms: leading question, double-barreled, pilot/pretest, response options/scale design.
[x] Section 2 - Frameworks & Mental Models: 4 frameworks included with ASCII diagrams (minimum 3 required): CLEAR checklist, Funnel Structure diagram, Questionnaire Flow Map, Question Type Decision Tree. All 3 mandatory frameworks present: question quality checklist, funnel structure, questionnaire flow map.
[x] Section 3 - Formulas, Thresholds & Rules of Thumb: 6 sub-sections covering response rate benchmarks, pilot sample size, question count limits, Likert scale rules, Cronbach's alpha benchmarks, and response distribution red flags. Completion time formula included.
[x] Section 4 - Do/Don't: 10 DOs and 10 DON'Ts (minimum 8 each side required). All items are IT/AI/Product/Consulting-specific with substantive detail.
[x] Section 5 - Metric-Driven Scenarios: 3 scenarios included (minimum 3 required). Each scenario contains: Trigger, Analysis, Decision, Result, Anti-Example. Scenarios: NPS survey redesign, employee AI adoption survey, feature prioritization survey.
[x] Section 6 - Practitioner Playbook: 17 numbered steps covering full questionnaire design lifecycle from objective definition through data weighting and reporting.
[x] Section 7 - Content Critique & Depth Gaps: 10 numbered gaps identified covering: psychometric theory, MaxDiff/conjoint, platform constraints, attention checks, longitudinal design, mixed-methods, cross-cultural bias, AI-assisted design, survey fatigue, and causal inference.
[x] Section 8 - Quick-Recall Card: 16 bullet points. Ends with exact required phrase beginning "As a PM/Consultant/AI Lead".
[x] Section 9 - Self-Audit Report: Present as HTML comment.

INDUSTRY LENS: IT/AI/Product/Consulting maintained throughout all sections. Examples reference SaaS platforms, generative AI tools, enterprise B2B surveys, consulting firms, NPS/CSAT metrics, product roadmap decisions.

ROLE-LENS QUESTION CHECK: Section 8 ends with "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ..." - CONFIRMED PRESENT AND CORRECTLY FORMATTED.

CONNECTS TO LINKS: Present at top of document linking to related audit files: 05-sampling-methods.md, 07-scales-and-measurement.md, 08-data-collection-methods.md, 09-validity-and-reliability.md.

FILE SIZE ESTIMATE: Approximately 18,000+ characters / ~16 KB - well above the 13 KB minimum requirement.

QUALITY FLAGS:
- No section omitted
- All mandatory jargon terms included
- All mandatory frameworks included with ASCII diagrams
- Anti-examples present in all 3 scenarios
- Do/Don't minimum counts met
- Pilot section realistic and specific
- Formulas are actionable with examples
- Depth gaps section provides genuine IIM/HBS MBA-level critique
- No superficial or padding content detected

WORKER ID: A7
DATE: 2026-04-18
STATUS: COMPLETE - ready for orchestration review
-->
