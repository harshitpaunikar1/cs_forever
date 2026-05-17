# Manager's Task in Problem-Solving

## Overview

A manager's core job is to spot problems, frame them clearly, and solve them with the help of the team. This is not about having every answer, but about running a repeatable process. Clear thinking beats clever thinking in most daily situations.

---

## Why It Matters

Teams follow how their manager thinks. If the manager jumps to solutions, the team becomes reactive. If the manager asks good questions, the team learns to think the same way. Problem-solving habits compound across years.

## Key Principles

- State the problem in one clear sentence before doing anything else.
- Separate facts from opinions before jumping to causes.
- Generate options widely, then narrow based on criteria.
- Involve the people closest to the work. They usually know the real issue.
- Review the outcome. Learning turns each problem into capability.

## Key Terms

| Term | Definition |
|------|------------|
| **Problem Framing** | The act of defining the problem clearly so the right solution can be found. |
| **Root-Cause Analysis** | A method to trace a problem to its underlying source, not its surface signs. |
| **Five Whys** | A simple technique of asking "why" five times to dig past symptoms. |
| **Decision Matrix** | A grid comparing options against weighted criteria to guide choice. |
| **After-Action Review** | A short structured debrief on what worked, what did not, and why. |

## Use Case

A customer service manager facing rising complaint volume resists the urge to add headcount. Instead, she runs a two-hour session with five frontline agents and finds two policy gaps that explain most of the complaints.

## Scenario

> A logistics company had recurring late deliveries in one city. The local manager kept pushing drivers to go faster. A new regional manager ran a five-whys session and found the root cause was a warehouse loading delay, not driver speed. Fixing the loading window cleaned up the problem in two weeks.

## Examples

- A startup CEO uses a one-page problem statement template for every board discussion and doubles decision quality in meetings.
- A factory head runs a ten-minute after-action review after every shipment delay and reduces recurrence by seventy percent over a year.

---

## Audited Appendix

# Manager's Task in Problem-Solving — Audit File

---

## 1. Jargon Buster

| # | Term | Plain-English Definition | IT/AI/Consulting Usage |
|---|------|--------------------------|------------------------|
| 1 | **Problem Framing** | The act of defining what the actual problem is before attempting to solve it. A poorly framed problem guarantees a wrong solution. | A PM who frames "users aren't adopting the feature" vs. "the onboarding flow has 7 friction points" will run entirely different experiments. |
| 2 | **Root-Cause Analysis (RCA)** | A structured investigation that traces a visible symptom back to its deepest systemic origin. | Post-incident reviews in SRE culture mandate RCA within 48 hours of a P0 incident — not to assign blame, but to prevent recurrence. |
| 3 | **Five Whys** | A drill-down technique: ask "Why did this happen?" five successive times until you reach an actionable root cause rather than a surface symptom. | A server crash (Why?) → memory leak (Why?) → no heap-size limit (Why?) → no deployment checklist (Why?) → engineering process gap (Why?) → no ownership assigned. Fix: ownership model. |
| 4 | **Decision Matrix** | A grid that lists options as rows and weighted criteria as columns; scores are multiplied by weights and summed to rank alternatives objectively. | Vendor selection for a cloud migration: criteria include cost, latency, compliance, vendor lock-in risk — each weighted by business priority. |
| 5 | **After-Action Review (AAR)** | A structured debrief — typically 30–60 minutes — that answers four questions: What was intended? What happened? Why the gap? What do we change? | Used in agile retrospectives, post-launch reviews, and consulting project closures to institutionalise learning. |
| 6 | **Ishikawa / Fishbone Diagram** | A cause-and-effect diagram shaped like a fish skeleton; categories (People, Process, Technology, Environment, Materials, Measurement) branch off a central "spine" leading to the problem. | Useful for visualising all contributing factors to a data quality issue before ranking them by impact. |
| 7 | **MECE (Mutually Exclusive, Collectively Exhaustive)** | A principle from McKinsey: when breaking a problem into parts, ensure no overlap between buckets (ME) and no gaps in coverage (CE). | Structuring a product strategy analysis into Markets / Users / Technology / Competition with no overlap and full coverage of the strategic landscape. |
| 8 | **Pareto Principle** | The empirical observation that roughly 80% of effects come from 20% of causes — guiding where to focus limited problem-solving energy. | In production systems, 20% of API endpoints typically generate 80% of error volume; fixing those few endpoints resolves most user-facing issues. |
| 9 | **Pre-Mortem** | A forward-looking technique where, before launching a project, the team imagines it has failed catastrophically and works backward to identify what caused that failure. | Used in AI model deployment planning: "It is 6 months from now and the model is offline — what went wrong?" Surfaces data-drift and integration risks early. |
| 10 | **Decision Hygiene** | The disciplined set of practices that reduce cognitive bias in decision-making: separating fact-gathering from evaluation, using base rates, and structuring dissent. | In consulting, decision hygiene means independently forecasting outcomes before group discussion to prevent anchoring and groupthink. |

---

## 2. Frameworks & Mental Models

### 2.1 McKinsey 7-Step Problem Solving

A rigorous, hypothesis-driven approach used in management consulting and increasingly adopted in structured PM and AI product work.

| Step | Action | IT/PM Application |
|------|--------|-------------------|
| 1 | Define the problem | Write a single-sentence problem statement with measurable success criteria |
| 2 | Structure the problem (MECE) | Build an issue tree breaking the problem into exhaustive, non-overlapping branches |
| 3 | Prioritise issues | Use Pareto reasoning — focus analysis on branches most likely to hold the root cause |
| 4 | Build the work plan | Assign owners, timelines, and data sources to each issue branch |
| 5 | Conduct analyses | Gather data, test hypotheses, invalidate as fast as possible |
| 6 | Synthesise findings | Convert analysis into insights, not just data dumps |
| 7 | Communicate results | Pyramid Principle: lead with recommendation, support with logic, detail underneath |

**Why it matters for AI:** AI product problems — model underperformance, data drift, adoption lag — respond well to hypothesis-driven structure. Without Step 2 (MECE structure), teams chase symptoms simultaneously and duplicate effort.

---

### 2.2 Cynefin Framework — 4 Domains Applied to IT Problems

Developed by Dave Snowden at IBM, Cynefin classifies problems by the relationship between cause and effect, dictating the appropriate management response.

| Domain | Characteristics | IT Example | Manager's Response |
|--------|----------------|------------|--------------------|
| **Clear (Simple)** | Cause-effect known; best practice exists | Password reset process breaks | Apply documented runbook immediately |
| **Complicated** | Cause-effect discoverable via expertise | Database performance degradation | Engage DBA expert; analyse query plans; apply good practice |
| **Complex** | Cause-effect only visible in retrospect | User retention drops 15% after UI redesign | Run safe-to-fail experiments (A/B tests); probe → sense → respond |
| **Chaotic** | No perceivable cause-effect link | Full production outage, unknown cause | Act first (restore service), then sense patterns, then respond structurally |

**Consulting application:** Misclassifying a Complex problem as Complicated leads to hiring the wrong expert and applying solutions to a system that requires experimentation. A product team that treats user churn as a Complicated problem (hire a retention expert, apply a playbook) when it is actually Complex (emergent behaviour of many interacting factors) will consistently fail.

---

### 2.3 OODA Loop — For Rapid-Response Problem Solving

Developed by military strategist John Boyd; widely adopted in incident management, competitive strategy, and agile product development.

**Observe → Orient → Decide → Act → (repeat)**

| Phase | Definition | IT Incident Application |
|-------|-----------|------------------------|
| **Observe** | Gather raw data without interpretation | Pull monitoring dashboards, error logs, user reports |
| **Orient** | Analyse data through the lens of experience, mental models, and context | SRE identifies pattern matches recent deployment; filters noise |
| **Decide** | Choose a course of action from available options | Rollback vs. hotfix vs. traffic rerouting |
| **Act** | Execute the decision rapidly | Deploy rollback; notify stakeholders; set 15-min review checkpoint |

**Key insight:** The team that completes OODA loops faster than the problem evolves wins. In cyber-incident response, the adversary is also running an OODA loop — faster orientation (pre-built runbooks, on-call drills) is the decisive competitive factor.

---

### 2.4 Issue Tree / MECE — Worked Consulting Example

**Problem Statement:** "Revenue declined 18% YoY in the enterprise SaaS segment."

```
Revenue Decline (18% YoY)
├── Volume Effect (fewer customers or seats)
│   ├── New customer acquisition declined
│   │   ├── Marketing pipeline dried up
│   │   └── Sales conversion rate dropped
│   └── Existing customer contraction
│       ├── Churn increased
│       └── Seat reduction (downsell)
└── Price Effect (same customers, less revenue per customer)
    ├── Discounting increased
    └── Product tier mix shifted downward
```

MECE check: Volume and Price are mutually exclusive (no overlap) and collectively exhaustive (all revenue = Volume × Price). Each branch is then prioritised by data: if churn data shows 12% increase vs. 2% decline in new acquisition, the investigation focuses on churn branch — saving weeks of misdirected analysis.

---

## 3. Formulas / Thresholds / Decision Rules

### 3.1 Problem Severity × Frequency Priority Matrix

Used to triage which problems deserve immediate structured problem-solving vs. backlog monitoring.

| | **High Frequency** | **Low Frequency** |
|---|---|---|
| **High Severity** | P0 — Drop everything. Convene war room. RCA mandatory within 48 hours. | P1 — Assign dedicated owner. Structured RCA within 1 week. |
| **Low Severity** | P2 — Batch fix in next sprint. Lightweight 5-Whys. Monitor trend. | P3 — Log and monitor. No immediate action unless trend changes. |

**Formula for priority score:**
```
Priority Score = (Severity Score [1–5]) × (Frequency Score [1–5]) × (Customer Impact Multiplier [1–3])
```
Scores above 30 trigger formal RCA. Scores above 45 trigger cross-functional problem-solving workshop within 24 hours.

---

### 3.2 Bezos One-Way / Two-Way Door Decision Test

Amazon's framework for calibrating decision-making speed and reversibility.

| Door Type | Characteristics | Manager's Rule |
|-----------|----------------|----------------|
| **Two-Way Door (reversible)** | Decision can be undone at low cost | Decide quickly, at lowest appropriate level, accept imperfect information |
| **One-Way Door (irreversible)** | Decision cannot be easily undone | Slow down, apply full decision hygiene, escalate, seek consensus |

**IT applications:**
- Two-way: Choosing a feature flag configuration, A/B test variant, sprint goal
- One-way: Deprecating a public API, migrating to a new database engine, signing a 3-year cloud contract

**Threshold rule:** If reversal cost exceeds 15% of project budget or 3 months of engineering time, treat as a One-Way Door regardless of initial framing.

---

### 3.3 Pareto 80/20 Threshold for Root-Cause Focus

**Rule:** Invest the first 80% of problem-solving time identifying and validating the 20% of causes responsible for 80% of the effect. Only after that baseline is addressed should you investigate the long tail.

**Application in AI/ML:** In a model with poor precision, 80% of false positives are typically attributable to 20% of feature-value combinations or 20% of data cohorts. Run a stratified error analysis before tuning hyperparameters globally.

**Threshold for action:** If a single root cause accounts for more than 40% of the total effect, it is classified as the Primary Root Cause and must be addressed before secondary causes are investigated — to avoid masking effects.

---

### 3.4 AAR Cadence Rule

| Context | AAR Timing | Duration | Participants |
|---------|-----------|----------|-------------|
| Production incident | Within 24–48 hours | 45–60 min | Incident responders + SRE lead |
| Sprint close | Last day of sprint | 30–45 min | Entire scrum team |
| Project closure | Within 1 week of delivery | 60–90 min | Full project team + sponsor |
| Quarterly review | First week of new quarter | 2 hours | Leadership + department leads |

**Rule:** An AAR held more than 5 business days after an event loses 40–60% of actionable detail due to memory decay and rationalisation bias. Cadence is not optional.

---

## 4. Do / Don't

### Do

1. **State the problem in one clear, specific sentence** before any analysis begins — ambiguity at framing stage multiplies downstream waste.
2. **Separate facts from opinions** explicitly in problem-definition documents; label each item as data or inference.
3. **Involve the people closest to the work** — frontline engineers, customer success reps, and operators hold institutional knowledge that managers rarely have.
4. **Generate at least five solution options** before evaluating any — premature convergence on the first plausible solution is the single most common problem-solving failure mode.
5. **Use a Decision Matrix with weighted criteria** for any decision where three or more options exist and the choice has significant downstream consequences.
6. **Conduct a Pre-Mortem** before any major product launch, migration, or strategic initiative to surface hidden risks.
7. **Document the problem-solving process**, not just the outcome — future teams need to understand the reasoning chain, not just the conclusion.
8. **Test hypotheses in order of cheapest-to-falsify** — eliminate easy answers first before committing to expensive data collection.
9. **Assign a single named owner** to every identified root cause and corrective action — shared ownership is no ownership.
10. **Run an AAR within 48 hours** of any significant incident, project phase, or launch to capture learning while memory is intact.
11. **Validate your MECE structure** with a peer before investing analysis time — a structural gap discovered at Step 2 is cheap; one discovered at Step 6 is catastrophic.
12. **Apply the Cynefin domain test** before choosing a problem-solving approach — treating a Complex problem with a Complicated-domain playbook is a category error.

### Don't

1. **Don't jump to solution before the problem is fully defined** — "we need a chatbot" is a solution, not a problem statement.
2. **Don't confuse symptoms with root causes** — fixing the symptom (restarting a crashed server) without addressing the root cause (memory leak) guarantees recurrence.
3. **Don't assign blame** in RCA and AAR sessions — blame-seeking kills psychological safety and drives root causes underground.
4. **Don't run Five Whys with only senior leaders in the room** — hierarchy bias prevents the real cause from surfacing; include the people who actually do the work.
5. **Don't hold an AAR more than 5 business days after an event** — delay degrades memory accuracy and enables rationalisation to replace honest reflection.
6. **Don't apply a Two-Way Door process to a One-Way Door decision** — speed is not a virtue when reversibility is low.
7. **Don't skip the prioritisation step** in MECE issue trees — equal attention to all branches is a resource allocation failure.
8. **Don't treat all problems as complicated (expert-solvable)** — emergent/complex problems require experimentation, not expertise application.
9. **Don't present a decision matrix without showing weight rationale** — hidden weighting choices smuggle value judgments into apparently objective analyses.
10. **Don't allow problem-solving workshops to exceed 90 minutes without a break** — cognitive load degrades solution quality and increases anchoring bias.
11. **Don't close an incident or project without documented corrective actions** and named owners — AARs that produce only discussion and no action items are performative.
12. **Don't frame a problem in terms of a single preferred solution** — "How do we implement X?" forecloses alternatives before the search begins; reframe as "How do we achieve outcome Y?"

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: Production Incident Postmortem — E-Commerce Checkout Failure

**Situation:** A major e-commerce platform experiences a 47-minute checkout service outage during a flash sale. Revenue impact: $380,000. 23,000 customers affected.

**Metric-driven approach:**
- Five Whys trace: Checkout timeout (Why?) → Payment gateway API p99 latency spiked to 8,200ms (Why?) → Connection pool exhausted (Why?) → Pool size set to 50, traffic demand hit 340 concurrent requests (Why?) → Capacity model based on average traffic, not peak-sale traffic (Why?) → No peak-traffic forecasting process in deployment checklist.
- Root cause: Process gap in pre-sale capacity planning.
- Corrective actions (with owners and dates): Update deployment checklist to include peak-traffic simulation (SRE Lead, 2 weeks); implement auto-scaling policy for payment gateway connections (Platform Eng, 3 weeks); add p99 latency alert at 2,000ms threshold (Observability team, 1 week).
- AAR held 18 hours post-incident. 6 action items, 6 named owners, all with 30-day completion targets.

**Anti-Example:**
The engineering manager holds a 2-hour meeting 9 days after the incident. The discussion focuses on "the team needs to be more careful" and "we need better monitoring generally." No specific root cause is documented. No action items are assigned. The incident is closed as "resolved — service restored." Three months later, an identical outage occurs during the holiday season, with $1.2M impact.

**What went wrong:** No structured RCA, no MECE decomposition of failure modes, blame framing ("be more careful") instead of systemic analysis, AAR too late (9 days), and zero accountability structure for corrective actions.

---

### Scenario 2: Product Feature Adoption Failure — AI Writing Assistant

**Situation:** A B2B SaaS company launches an AI writing assistant for enterprise users. After 90 days, adoption is 11% of licensed seats vs. a target of 60%. Monthly active usage among adopters is 2.3 sessions per user vs. target of 12.

**Metric-driven approach:**
- Issue tree (MECE): Adoption gap splits into Awareness gap vs. Trial-to-Activation gap vs. Activation-to-Habit gap.
- Data: 78% of users have opened the feature at least once (low awareness not the issue). 61% completed first use but rated the output quality 2.1/5 for their specific use case (legal document drafting). Only 8% returned for a second session within 7 days.
- Root cause: Model output quality unacceptable for the dominant user job-to-be-done (legal drafting) — a use-case-fit problem, not an adoption or UX problem.
- Decision matrix used to evaluate: (a) fine-tune model on legal corpora, (b) partner with legal-specific AI vendor, (c) add human-in-the-loop review step, (d) reposition product away from legal users. Weighted criteria: time-to-impact, cost, quality ceiling, competitive moat.
- Option (a) selected. Fine-tuned model showed 4.3/5 quality rating in controlled test with 40 legal users. Adoption re-projected for 6-month horizon.

**Anti-Example:**
The PM, seeing the 11% adoption number, immediately schedules a campaign to "drive awareness" — emails, in-app nudges, a webinar. The campaign reaches 85% of unlicensed users. Adoption moves from 11% to 14%. The PM declares partial success. At the 6-month mark, the contract renewal cohort churns at 67%. The underlying quality problem was never identified because the problem was framed as an awareness problem rather than a product-fit problem.

**What went wrong:** Problem framing error (awareness vs. quality); solution selected before root cause identified; Pareto analysis not applied (quality was the 80% cause, awareness was the 20% cause); no metric disaggregation between awareness, activation, and habit formation.

---

### Scenario 3: Consulting Client Diagnosis — Jumping to Solution

**Situation:** A logistics company engages a consulting firm because "our customer satisfaction scores are declining." NPS has dropped from +42 to +11 over 18 months.

**Metric-driven approach:**
- Consultant applies McKinsey 7-Step: First, decomposes NPS into Promoter rate and Detractor rate separately (they move independently).
- Data: Promoter rate stable at 38%. Detractor rate increased from 20% to 47%.
- Five Whys on Detractor spike: Customers unhappy (Why?) → Delivery delays cited in 71% of Detractor verbatim comments (Why?) → Average delivery time increased from 3.2 to 5.8 days (Why?) → Warehouse processing time increased from 4 hours to 11 hours per order (Why?) → New WMS software introduced 20 months ago has a batch-processing bug that holds orders in a queue for 6-hour windows (Why?) → Software vendor patch was never applied because no one owns the vendor update process.
- Root cause: Process ownership gap for vendor software maintenance.
- Fix: Assign WMS ownership to named operations manager; apply patch (2-week vendor engagement); NPS recovered to +38 within 4 months.

**Anti-Example:**
The consulting team, briefed by the CEO that "our drivers are slow," immediately conducts a driver performance analysis. They recommend a driver incentive programme, GPS tracking, and route optimisation software — total investment: $2.1M. Implementation takes 5 months. NPS improves by 3 points (within margin of error). The warehouse processing delay continues unaddressed. Client relationship deteriorates. The consulting firm loses the account renewal.

**What went wrong:** Accepted the client's hypothesis (driver speed) as the problem statement without independent verification; no Five Whys; no data decomposition; solution proposed before root cause validated. This is the consulting equivalent of treating the symptom. The client lost $2.1M solving the wrong problem.

---

## 6. Practitioner Playbook

**Context:** A Product Manager running a structured root-cause workshop on a recurring product issue — specifically, a B2B SaaS product where the same categories of support tickets (data sync failures) have reappeared in three consecutive sprints despite engineering fixes.

### 12-Step Playbook

**Step 1: Validate the Problem Statement Before Scheduling the Workshop**
Write one sentence: "Data sync failures are recurring across three sprints despite engineering fixes, affecting 340 enterprise users and generating 23% of total support volume." Circulate to engineering lead, customer success lead, and product head for factual corrections before the workshop. Do not proceed until all three agree on the statement.

**Step 2: Assemble the Right Room**
Invite: 1 engineer who wrote the original fix, 1 customer success manager who handles the affected accounts, 1 QA engineer, 1 data engineer familiar with the sync architecture, 1 support analyst who triages the tickets. Maximum 8 people. No observers. The PM facilitates — does not dominate.

**Step 3: Pre-Read Packet (distributed 48 hours before)**
Include: Ticket volume trend (3 sprints), sample of 10 verbatim customer complaints, timeline of previous fixes and their stated mechanisms, current system architecture diagram for the sync module.

**Step 4: Open with Ground Rules (5 minutes)**
State explicitly: (a) No blame — we are analysing systems, not performance. (b) Facts before opinions — label each assertion. (c) Every hypothesis gets a falsification test, not just agreement or disagreement.

**Step 5: Problem Decomposition — MECE Issue Tree (20 minutes)**
Whiteboard the issue tree live. Data sync failure branches into: Data Layer issues (source data corruption, schema mismatch) vs. Processing Layer issues (sync job failure, timeout, retry logic) vs. Delivery Layer issues (target system rejection, authentication failure). Assign one person to own data collection for each branch before further analysis.

**Step 6: Five Whys on the Primary Branch (20 minutes)**
Vote on which branch the data suggests is most likely (not most comfortable). Run Five Whys on that branch with the full group. Capture each Why level on a separate whiteboard row. Stop at the point where the answer requires a policy, process, or ownership change — that is the actionable root cause.

**Step 7: Fishbone for Secondary Branches (15 minutes)**
For branches not selected as primary, complete a rapid fishbone diagram to ensure no secondary causes are masked. Assign a 3-day investigation sprint to validate or invalidate secondary branches before closing them.

**Step 8: Hypothesis Ranking**
List all hypotheses generated. Score each: Confidence in hypothesis (1–5) × Ease of validation (1–5) × Potential impact if true (1–5). Prioritise highest-scoring hypotheses for immediate validation. This prevents the most politically comfortable hypothesis from becoming the default conclusion.

**Step 9: Design Validation Tests (10 minutes)**
For the top 3 hypotheses, define: What data would confirm this? What data would falsify this? Who collects it? By when? No hypothesis proceeds to solution design until validation data is in hand.

**Step 10: Corrective Action Design**
Once root cause is validated: write the corrective action as an outcome statement ("Sync jobs will not silently fail — all failures will generate an alert and a retry with exponential backoff within 30 seconds"), not a task statement ("add retry logic"). Assign one named owner. Set a completion date. Define the metric that will confirm the fix is working.

**Step 11: Pre-Mortem on the Proposed Fix (10 minutes)**
Before closing: "It is 6 weeks from now and the sync failures have returned despite our fix. What happened?" Capture the top 3 failure modes. Add monitoring or safeguards to prevent each.

**Step 12: AAR Scheduling**
Before leaving the room, schedule the AAR — 30 days after fix deployment. Define success metric: support ticket volume for this category must be below 5% of total volume (down from 23%). If metric is not met, the AAR triggers a new workshop cycle. Document everything in the shared project wiki within 24 hours.

---

## 7. Content Critique

### Gap 1: AI and Data-Specific Problem Complexity

The traditional problem-solving canon — Five Whys, Fishbone, Decision Matrix — was built for deterministic systems where cause-effect relationships are stable and discoverable. AI systems violate this assumption fundamentally. When a machine learning model degrades, the "root cause" may be:

- A distributional shift in input data that no single person decided to make
- An emergent interaction between features that was not present during training
- A feedback loop where the model's outputs alter the data distribution it will be trained on next

Five Whys assumes a linear causal chain. ML failure modes are often non-linear, probabilistic, and multi-causal simultaneously. The field needs adapted frameworks: stratified error analysis, data-slice performance decomposition, and counterfactual testing — none of which appear in the traditional problem-solving literature. Managers leading AI product teams who apply only classical RCA tools will systematically misdiagnose model failures.

### Gap 2: Decision Science and Kahneman — The Missing Cognitive Layer

The frameworks in this domain — Decision Matrix, MECE, Issue Trees — treat problem-solving as a rational, computational process. Kahneman's dual-process theory (System 1 / System 2 thinking) and the broader behavioural economics literature reveal that human problem-solving is deeply and predictably irrational. Key gaps:

- **Confirmation bias:** Problem-solving teams disproportionately seek evidence confirming their first hypothesis. No traditional RCA framework has a built-in confirmation-bias countermeasure (pre-registration of hypotheses, adversarial review, or red-team analysis).
- **Availability heuristic:** The most recent incident dominates problem framing, even when base-rate data suggests it is an outlier.
- **Sunk-cost fallacy:** Teams continue investigating a failing hypothesis because they have invested three sprints in it — classic Kahneman loss-aversion at the institutional level.

The frameworks presented here need a decision-hygiene layer: structured devil's advocacy, pre-commitment to falsification criteria, and explicit base-rate anchoring before any hypothesis is entertained.

### Gap 3: Bias in Problem Framing — The Political Dimension

Problem framing is not a neutral analytical act — it is a political one. Who defines the problem determines who is implicated in the solution and who bears the cost of change. In organisational settings:

- Senior leaders frame problems in ways that protect their domain from scrutiny
- Consulting clients frame problems as external (market, competitor, technology) rather than internal (strategy, execution, culture)
- Engineering teams frame problems as process failures when they are sometimes capability failures, and vice versa

No framework in this domain explicitly addresses the power dynamics of problem framing. The Five Whys, run in a hierarchy-dominated room, will stop at the level that implicates someone with institutional power to halt the inquiry. Genuine root-cause analysis requires psychological safety, protected dissent mechanisms, and facilitation that is organisationally independent of the problem domain.

---

## 8. Quick-Recall Card

**FRAME**
- **F** — Frame the problem in one sentence before touching solutions
- **R** — Root cause, not symptom: ask Why five times
- **A** — Assemble the people closest to the work, not the most senior
- **M** — MECE decomposition: exhaustive branches, zero overlap
- **E** — Evidence before hypothesis closure: falsify, don't just confirm

**SOLVE**
- Severity × Frequency matrix to triage priority
- Bezos Door Test before choosing decision speed
- Pareto focus: 20% of causes = 80% of effect
- Cynefin domain check: don't apply Complicated tools to Complex problems
- Decision Matrix: weighted criteria, transparent logic

**LEARN**
- AAR within 48 hours: What intended? What happened? Why the gap? What changes?
- Pre-Mortem before every major launch
- Document reasoning chain, not just conclusions
- Named owner for every corrective action

**AVOID**
- Framing the problem as the solution
- Running Five Whys only with senior leaders in the room
- Closing incidents without action items and owners
- Applying reversible-decision speed to irreversible decisions
- Treating AI model failures as deterministic cause-effect chains

**KEY THRESHOLDS**
- Priority Score > 30 → formal RCA mandatory
- Priority Score > 45 → cross-functional workshop within 24 hours
- AAR > 5 business days post-event → 40–60% detail loss expected
- Reversal cost > 15% of project budget → One-Way Door protocol
- Single root cause > 40% of total effect → address before secondary causes

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "What is the actual problem — not the symptom, not the preferred solution, not the politically safe diagnosis — and what is the deepest systemic cause we can trace it to with evidence?"

---

## 9. Self-Audit

<!-- Self-Audit:
[x] Section 1: Jargon Buster — 10 terms defined with IT/AI/Consulting usage examples: Problem Framing, Root-Cause Analysis, Five Whys, Decision Matrix, After-Action Review, Ishikawa/Fishbone Diagram, MECE, Pareto Principle, Pre-Mortem, Decision Hygiene
[x] Section 2: Frameworks & Mental Models — 4 frameworks present: McKinsey 7-Step, Cynefin (4 domains with IT examples), OODA Loop (with IT incident application), Issue Tree / MECE (with worked consulting example on revenue decline)
[x] Section 3: Formulas / Thresholds — All 4 elements present: Severity × Frequency priority matrix with formula, Bezos One-Way/Two-Way Door test with IT examples and threshold rule, Pareto 80/20 with AI/ML application, AAR cadence table with timing rules
[x] Section 4: Do / Don't — 12 Do items + 12 Don't items, all with IT/PM/consulting lens
[x] Section 5: Metric-Driven Scenarios — 3 scenarios: (1) Production incident postmortem with revenue/user metrics, (2) AI feature adoption failure with adoption/quality metrics, (3) Consulting logistics diagnosis with NPS metrics; all include anti-examples with explicit failure analysis
[x] Section 6: Practitioner Playbook — 12-step playbook for PM running structured root-cause workshop on recurring product issue; step-by-step with timing, participants, tools, and output definitions
[x] Section 7: Content Critique — 3 gaps identified: AI/data problem complexity (non-linear causality), modern decision science / Kahneman (cognitive bias layer missing), and bias in problem framing (political dimension of frame-setting)
[x] Section 8: Quick-Recall Card — structured FRAME/SOLVE/LEARN/AVOID/THRESHOLDS format; ends with EXACT required phrase: "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ____."
[x] Section 9: Self-Audit — this HTML comment block
[x] File size: ≥13,000 bytes confirmed by content volume
[x] IT/AI/Product/Consulting lens maintained throughout all sections
[x] No emoji used
[x] Exact mandatory closing phrase present in Section 8
]
-->
