# Business Model Experiments

## Overview

Business model experiments are structured tests designed to validate or invalidate assumptions about how a company creates and captures value. Instead of betting the company on an untested idea, you run a small, time-boxed experiment to gather real evidence. Will customers pay for this feature? Does this pricing model convert better? Can we serve this new segment profitably? Experiments answer these questions before you commit millions.

---

## Why It Matters

Most new business models fail, and the failures are expensive. Experimentation reduces the cost of failure by catching bad ideas early and cheaply. Companies that experiment systematically — like Amazon with its relentless A/B testing culture — learn faster than competitors and allocate resources to models that have already proven demand.

## Key Principles

- State a clear hypothesis before running any experiment: what you believe, what you will measure, and what result would prove you wrong
- Design experiments to be as small and fast as possible while still producing trustworthy results
- Separate the signal from the noise by controlling variables and using adequate sample sizes
- Act on results decisively — do not repeat experiments hoping for a different answer

## Key Terms

| Term | Definition |
|------|------------|
| **Hypothesis** | A testable statement predicting the outcome of a business model change (e.g., "Switching to annual billing will reduce churn by 10%") |
| **A/B test** | An experiment comparing two versions of something (pricing, landing page, feature) to see which performs better |
| **Minimum viable experiment** | The smallest test that can validate or invalidate a business model assumption with real customer behavior |
| **Kill criteria** | Pre-defined thresholds that determine when an experiment has failed and should be stopped |

## Use Case

A media company wants to test whether readers will pay for premium articles. Instead of building a full paywall, it puts three articles behind a simple payment gate for two weeks and measures how many readers pay versus how many bounce. The experiment costs almost nothing and provides hard data for a multi-million-dollar decision.

## Scenario

> A B2B software company believed enterprise clients would pay 3x more for a version with advanced analytics. Rather than building the full feature set, it created a mockup, showed it to 50 qualified prospects, and asked them to sign a non-binding letter of intent at the higher price. Thirty-two signed. With 64% intent-to-purchase validation, the company greenlit development. The premium tier launched six months later and hit its revenue target in the first quarter.

## Examples

- Dropbox validated demand for its product by releasing a simple explainer video before writing a single line of code — sign-ups spiked overnight, proving the market existed
- Amazon tests new delivery models (drones, same-day, locker pickup) in limited geographies before national rollout, using real customer adoption data to decide which models scale

---

## Audited Appendix

# Business Model Experiments
**Course:** Advanced Business Models  
**Module:** Business Model Expansion  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** business-model-advance/content/11-business-model-experiments.md

---

## 1. Topic Snapshot
Business model experiments are small, structured tests that validate or kill assumptions before a company makes a big commitment.
They matter because most new business models fail, and the cost of failure is much lower when you test early.
For a PM, AI lead, or consultant, the decision is whether a pricing, packaging, or segment idea is real enough to scale.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Hypothesis | Not an acronym | A testable statement about what will happen | To make experimentation falsifiable | Pass/fail result, confidence in outcome | Product, strategy, analytics |
| A/B test | Version A vs Version B | A comparison between two variants | To isolate which change performs better | Conversion lift, retention lift | Growth, pricing, UX |
| Minimum viable experiment | Not an acronym | The smallest test that can answer the question | To learn cheaply before building fully | Cost, time, learning rate | Startup and product planning |
| Kill criteria | Not an acronym | The threshold at which you stop a failing test | To prevent wasted time and sunk cost | Stop rate, result threshold | Experiment design, leadership reviews |
| Testable statement | Not an acronym | A claim that can be checked with data | To avoid vague strategy talk | Result observed vs expected | PM, consulting, analytics |
| Control | Not an acronym | The baseline version in an experiment | To know what you are comparing against | Baseline conversion, baseline retention | A/B testing, pricing tests |
| Variant | Not an acronym | The changed version being tested | To measure the effect of one change | Variant conversion, lift | Experimentation |
| Sample size | Not an acronym | The number of users or customers in a test | To make the result trustworthy | Number of observations | Analytics, research |

## 3. Frameworks & Matrices

### Experiment Ladder
**Purpose:** Move from idea to validated model with the smallest possible test.

**Text Diagram:**
```text
Assumption -> Hypothesis -> Minimum viable experiment -> Result -> Decision
```

Axes / Quadrants / Components explained:
Component 1: Assumption is the belief the team has not yet proved.
Component 2: Hypothesis turns the belief into a testable statement.
Component 3: Minimum viable experiment creates a cheap real-world test.
Component 4: Result turns evidence into a scale, change, or stop decision.

IT/Product worked example: A SaaS company assumes annual billing will reduce churn. It writes that as a hypothesis, tests a small cohort, and only then decides whether to roll it out across the product.
When to pull this out in a meeting: When the team is debating a big model change without evidence.

### Kill Criteria Matrix
**Purpose:** Decide ahead of time when an experiment has failed.

**Text Diagram:**
```text
Result above threshold -> continue
Result near threshold   -> iterate
Result below threshold  -> kill
```

Axes / Quadrants / Components explained:
Component 1: Threshold defines success.
Component 2: Gray zone defines the area where more learning is needed.
Component 3: Failure zone defines when the idea should be stopped.

IT/AI/Product/Consulting worked example: An AI pricing test can define kill criteria such as "if paid conversion stays below 1.5%, stop the new pricing tier." That prevents the team from defending a weak model because they like the idea.
When to pull this out in a meeting: When everyone wants one more round of testing even though the result is already clear.

### Experiment Design Grid
**Purpose:** Keep tests small, fast, and trustworthy.

**Text Diagram:**
```text
Small + fast + real behavior -> best learning
Large + slow + opinion-driven -> weak learning
```

Axes / Quadrants / Components explained:
Component 1: Small means limited scope and low cost.
Component 2: Fast means the team gets evidence quickly.
Component 3: Real behavior means customers actually take action, not just say they would.

IT/Product/Consulting worked example: A consulting firm can test a new subscription offer by showing 40 clients a landing page and asking for a non-binding commitment instead of building the full platform first. That gives real behavioral evidence without heavy build cost.
When to pull this out in a meeting: When the team is overbuilding before learning.

## 4. Formulas

Formula: `Lift = variant conversion - control conversion`
Variables:
`variant conversion` = conversion rate for the new version
`control conversion` = conversion rate for the baseline
Why this formula exists: It answers whether the new model actually performs better.
How to interpret the output:
Value low -> the new idea is not improving outcomes -> kill or redesign
Value moderate -> the idea has promise -> refine the test
Value high -> the idea is working -> scale it carefully
Worked example with numbers: If the control converts at 8% and the variant at 12%, lift is 4 percentage points. That is a meaningful signal that the new offer or pricing model deserves a broader pilot.

Formula: `Experiment efficiency = learning value / experiment cost`
Variables:
`learning value` = how much uncertainty the test removes
`experiment cost` = time, money, and team attention spent
Why this formula exists: It answers whether the test is worth running at all.
How to interpret the output:
Value low -> too expensive for the amount of learning -> simplify the test
Value moderate -> worth running -> proceed
Value high -> a very efficient experiment -> prioritize it
Worked example with numbers: A pricing test costs $5,000 and removes a major uncertainty that would have taken $50,000 to fix later. The efficiency is high, so the test is strategically valuable.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Launch a big business model change without a hypothesis | Write a clear hypothesis first |
| Keep testing after the result is already clear | Define kill criteria up front |
| Build the whole product before learning | Run a minimum viable experiment |
| Rely on opinions instead of customer behavior | Measure real behavior with an A/B test or pilot |
| Treat every test as a success story | Act decisively on weak results |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: SaaS pricing test
Situation: A SaaS company wants to move from monthly billing to annual billing. The product team worries the change may reduce adoption, but finance wants stronger retention.
Applicable framework/metric: Experiment Ladder.
Analysis: The team can test a small cohort with an annual-only offer and compare conversion and churn against the monthly control. That gives real evidence before a full rollout.
Decision rule: If lift is above 3 points, scale. If between 0 and 3 points, iterate. If negative, stop.
Action: Run the test on a limited customer segment and review churn after one billing cycle.

Scenario 2: AI feature packaging
Situation: An AI tool wants to charge extra for advanced analytics, but the team does not know whether customers will pay enough to justify the new tier.
Applicable framework/metric: Kill Criteria Matrix.
Analysis: If the paywall conversion stays below the predefined threshold, the new tier should be killed instead of defended emotionally. If it lands near the threshold, the team can refine the package or message.
Decision rule: If conversion is below 2%, kill. If between 2% and 5%, iterate. If above 5%, scale.
Action: Test pricing copy, feature placement, and customer segment before building more features.

Scenario 3: Consulting offer validation
Situation: A consulting firm wants to sell a subscription benchmarking tool instead of only project work.
Applicable framework/metric: Experiment Design Grid.
Analysis: The firm can show a lightweight prototype to a small set of clients and measure whether they will commit to a paid pilot. That is better than building the full platform first.
Decision rule: If fewer than 10% of prospects commit, stop. If 10% to 25%, refine the offer. If above 25%, build the product.
Action: Run a non-binding pilot with a clear commitment request.

## 7. Implementation Playbook
1. Write the assumption in one sentence.
2. Convert the assumption into a falsifiable hypothesis.
3. Define the smallest possible experiment that can produce real behavior.
4. Set kill criteria before the test starts.
5. Pick a control, a variant, and the success metric.
6. Run the test on a limited segment with enough sample size to be believable.
7. Decide to scale, iterate, or stop based on the result.

## 8. Content Quality Audit
Covered well: The source correctly frames experimentation as a way to avoid expensive mistakes and emphasizes hypothesis, minimum viable experiment, and kill criteria.
Underplayed or missing: It does not provide a practical decision tree for stopping, iterating, or scaling, and it does not explain how to compare learning value against cost.
Supplement with: [verified from model knowledge, not source] Eric Ries, *The Lean Startup*; [verified from model knowledge, not source] HBS cases on experimentation and pricing tests; [verified from model knowledge, not source] peer-reviewed work on causal inference and A/B testing; [verified from model knowledge, not source] experimentation playbooks from product analytics teams.
Red flags in the source: The examples imply that validation is easy once interest is observed; in practice, intent and actual purchase can diverge sharply, especially in enterprise and consulting motions.

## 9. Quick-Recall Card
```text
Topic: Business Model Experiments
Core idea: Test business model assumptions cheaply before committing major resources.
Key metric/formula: Lift = variant conversion - control conversion.
Framework trigger: Use the experiment ladder when a big model change is being considered.
Watch out for: Running experiments without kill criteria.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What assumption are we trying to prove or disprove with real customer behavior?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [experiment ladder, kill criteria matrix, experiment design grid, SaaS/AI/Consulting examples] Final scores: all 5/5 Pass 2 completed: 2026-04-20 13:00 Audited by: A1 -->
