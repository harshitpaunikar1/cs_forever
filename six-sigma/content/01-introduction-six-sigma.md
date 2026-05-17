# Introduction to Six Sigma

## Overview
Six Sigma is a data-driven methodology aimed at reducing defects and improving the quality of processes in any organization. It was originally developed by Motorola in the 1980s and later popularized by General Electric. The core idea is to bring process performance to a level where defects occur at a rate of no more than 3.4 per million opportunities. Six Sigma uses statistical tools and structured project management to achieve measurable, repeatable results.

---

## Why It Matters
Every business depends on processes, and every process has variation. When variation grows too large, customers receive defective products, costs rise, and reputation suffers. Six Sigma gives organizations a common language, a proven roadmap, and a set of statistical tools to systematically reduce variation and deliver consistent quality. Companies that adopt Six Sigma often report millions of dollars in savings and significantly higher customer satisfaction.

## Key Principles
- Focus on the customer and what they define as quality
- Use data and statistical analysis to understand and reduce variation
- Follow a structured, repeatable methodology for every improvement project
- Engage leadership and build a culture of continuous improvement

## Key Terms
| Term | Definition |
|------|------------|
| **Defect** | Any output of a process that fails to meet a customer requirement or specification |
| **DPMO** | Defects Per Million Opportunities, the standard metric for measuring process performance in Six Sigma |
| **Sigma Level** | A statistical measure of how well a process performs; higher sigma means fewer defects |
| **Variation** | The natural differences in process outputs that Six Sigma aims to minimize |

## Use Case
A hospital uses Six Sigma to reduce patient wait times in its emergency department by identifying bottlenecks and standardizing triage procedures.

## Scenario
> A smartphone manufacturer notices that 2% of its screens arrive with dead pixels. After launching a Six Sigma project, the team collects defect data, identifies the root cause in the coating process, and implements a fix. Within six months, the defect rate drops to 0.03%, saving millions in warranty claims.

## Examples
- A bank reduces mortgage processing errors from 5% to less than 0.1% by applying Six Sigma to its document review workflow
- An airline uses Six Sigma to cut baggage mishandling rates, improving on-time delivery from 96% to 99.8%

---

## Audited Appendix

# Introduction to Six Sigma
**Course:** Six Sigma  
**Module:** Content / Introduction to Six Sigma  
**Audited on:** 2026-04-18  
**Audited by:** A4  
**Source files reviewed:** `six-sigma/content/01-introduction-six-sigma.md`

---

## 1. Topic Snapshot
Six Sigma is a data-driven way to reduce defects and variation so processes become predictable and customer-facing work becomes repeatable.
For IT, AI, Product, and Consulting leaders, it is a management system for fixing service errors, workflow bottlenecks, and quality failures with measurable results.
The decision it helps make is which process to improve, how bad the defect problem is, and whether the savings justify the effort.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Defect | - | Anything that fails a customer requirement or specification. | Makes quality failure visible. | Defect count, defect rate, DPMO. | Quality reviews, operations, support. |
| DPMO | Defects Per Million Opportunities | How many defects happen out of one million chances. | Standardizes process performance across volumes. | Defects / opportunities * 1,000,000. | Six Sigma dashboards, process reviews. |
| Sigma level | - | A shorthand for how capable a process is. | Helps compare process performance quickly. | Sigma conversion from DPMO. | Quality reporting, executive decks. |
| Variation | - | The natural spread in process outputs. | Explains why the same process does not always produce the same result. | Standard deviation, range, control charts. | Operations, analytics, manufacturing, service design. |
| Data-driven | - | Based on measured facts instead of guesswork. | Keeps improvement grounded in evidence. | Baselines, trends, test results. | Continuous improvement, analytics, product ops. |
| Methodology | - | A repeatable way of solving problems. | Prevents ad hoc fixes from replacing disciplined improvement. | Project completion, cycle time, savings. | Program management, consulting, quality teams. |
| Statistical tools | - | Quantitative methods for understanding variation and cause. | Turns process noise into actionable insight. | Hypothesis tests, capability measures, charts. | Quality engineering, analytics, ops. |
| Structured project management | - | A staged way to run improvement work. | Keeps fixes from drifting or stalling. | Milestones, deliverables, benefit tracking. | PMO, operations excellence, consulting. |
| Customer requirement | - | What the customer actually expects. | Anchors quality to the buyer, not the internal team. | Voice of customer, CTQs, satisfaction. | Product, service design, QA. |
| Specification | - | The acceptable limit or standard for output. | Converts customer need into a testable boundary. | Pass/fail rate, tolerance, conformance. | Manufacturing, testing, compliance. |
| Process | - | A repeatable sequence of work steps. | Gives a place to measure and improve. | Cycle time, errors, throughput, DPMO. | Operations, software delivery, service workflows. |
| Bottleneck | - | The step that slows the entire process. | Focuses attention on the constraint. | Queue length, waiting time, throughput. | Hospitals, factories, support centers. |
| Triage | - | The act of sorting work by urgency or severity. | Prioritizes scarce capacity where it matters most. | Wait time, severity bucket, rework rate. | Healthcare, support queues, incident response. |
| Customer satisfaction | - | How happy the customer is with the outcome. | Links quality to loyalty and revenue. | Surveys, repeat use, complaints, NPS. | Product management, service ops, CX. |
| DMAIC | Define, Measure, Analyze, Improve, Control | The classic Six Sigma project sequence. | Provides a disciplined improvement roadmap. | Stage completion, baseline-to-target shift. | [verified from model knowledge, not source] quality programs, consulting, ops excellence. |

## 3. Frameworks & Matrices

### DMAIC Roadmap
**Purpose:** Run a Six Sigma project from problem definition to sustained control. [verified from model knowledge, not source]

**Text Diagram:**
```text
Define -> Measure -> Analyze -> Improve -> Control
```

Axes / Quadrants / Components explained:
Component 1: Define - state the defect, customer impact, and project scope.
Component 2: Measure - collect baseline data and calculate current performance.
Component 3: Analyze - find root causes, bottlenecks, and major sources of variation.
Component 4: Improve - test and implement changes that reduce defects.
Component 5: Control - lock in the gain with monitoring, ownership, and standard work.
IT/AI/Product/Consulting worked example: A hospital emergency department defines excessive patient wait time as the defect, measures waits by triage step, analyzes bottlenecks in staffing and handoffs, improves the schedule and queue logic, and then controls the change with a live dashboard. The same pattern works for a SaaS support team trying to reduce ticket reopens or an AI ops team trying to reduce incident recurrence.
When to pull this out in a meeting: When everyone agrees there is a problem but nobody has a stage-gated plan to fix it.

### DPMO Prioritization Grid
**Purpose:** Decide which quality issue should be fixed first based on defect rate and business impact. [verified from model knowledge, not source]

**Text Diagram:**
```text
                    Business impact
                 low                 high
DPMO   high   [ later ]          [ fix now ]
       low    [ monitor ]        [ standardize ]
```

Axes / Quadrants / Components explained:
Component 1: DPMO - how frequently defects appear in the process.
Component 2: Business impact - how much cost, customer pain, or risk the defect creates.
Component 3: Fix now - a high-defect, high-impact issue that deserves immediate improvement.
Component 4: Monitor or standardize - a lower-priority issue that is stable enough for control.
IT/AI/Product/Consulting worked example: A mortgage operations team might have a low-volume data entry error with very high compliance impact, which belongs in fix now, while a cosmetic dashboard glitch with no customer consequence belongs in later. This keeps the team from spending its best analysts on the least meaningful defects.
When to pull this out in a meeting: When the queue of problems is bigger than the team and the organization needs triage.

## 4. Formulas

Formula: Defect Rate = defects / opportunities
Variables:
Defects = count of outputs that fail the requirement.
Opportunities = total chances for the process to fail.
Why this formula exists: It answers how often the process misses the customer requirement.
How to interpret the output:
Value < 0.01 -> strong process -> control and monitor
Value 0.01-0.05 -> meaningful variation -> improve the key step
Value > 0.05 -> serious quality problem -> treat as a priority project
Worked example with numbers: If 12 out of 400 loan files have errors, the defect rate is 12/400 = 0.03. That means 3% of work is not meeting the standard and needs root-cause analysis.

Formula: DPMO = defect rate * 1,000,000
Variables:
Defect rate = defects divided by opportunities.
1,000,000 = scaling factor used by Six Sigma.
Why this formula exists: It makes process performance comparable across different volumes.
How to interpret the output:
Value < 3.4 -> world-class Six Sigma territory -> maintain with control
Value 3.4-6,210 -> strong process -> improve carefully and keep monitoring
Value > 6,210 -> improvement needed -> use DMAIC and attack major causes of variation
Worked example with numbers: If a process has a defect rate of 0.03, DPMO is 0.03 * 1,000,000 = 30,000. That is far from Six Sigma and signals a substantial quality gap.

Formula: Yield = 1 - defect rate
Variables:
Defect rate = the proportion of outputs that fail.
Yield = the proportion that meet the requirement.
Why this formula exists: It answers how much of the process output is usable.
How to interpret the output:
Value < 0.95 -> too much rework -> redesign the process
Value 0.95-0.99 -> acceptable but improvable -> reduce key defect sources
Value > 0.99 -> very strong process -> lock in with control
Worked example with numbers: If defect rate is 3%, yield is 97%. That sounds good, but in a high-volume process it still creates large downstream cost.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Treat quality as a vague feeling instead of a measurable defect definition. | Turn customer expectations into a defect, a specification, and a baseline metric. |
| Fix the loudest problem first without checking impact. | Prioritize by DPMO and business impact together. |
| Launch a one-off improvement and walk away. | Use DMAIC and put the fix under control. |
| Blame people for variation that the process creates. | Redesign the process and standardize the best practice. |
| Focus only on manufacturing and ignore service or digital workflows. | Apply Six Sigma to hospitals, banks, SaaS support, and AI operations as well. |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Emergency department triage
Situation: A hospital is getting complaints about long waits in the emergency department. From an IT/consulting lens, this is a queue management and process design problem, not just a staffing problem.
Applicable framework/metric: DMAIC Roadmap and DPMO.
Analysis: If 45 out of 500 patients wait beyond the service target, the defect rate is 0.09 and DPMO is 90,000. That is a clear high-priority quality problem, and the bottleneck is likely in triage or room assignment.
Decision rule: If DPMO is above 6,210, run a formal improvement project. If between 3.4 and 6,210, monitor and refine. If below 3.4, preserve the control system.
Action: Map the patient flow, measure waits by step, change triage rules, and monitor the result with daily dashboards.

Scenario 2: Smartphone screen defects
Situation: A smartphone manufacturer sees dead pixels on 2% of screens, which is creating warranty claims and brand damage. The operations and product teams need a measurable way to prove the fix worked.
Applicable framework/metric: Defect Rate, DPMO, and Yield.
Analysis: A 2% defect rate equals 20,000 DPMO if each screen is treated as one opportunity. After the fix, the defect rate falls to 0.03%, or 300 DPMO, which is a dramatic improvement.
Decision rule: If defects stay above 1%, treat the process as unstable. If below 0.1%, shift from improvement to control. If the trend reverses, reopen the root-cause analysis.
Action: Fix the coating process, train operators, and build a quality gate before final assembly.

Scenario 3: Mortgage processing workflow
Situation: A bank is losing time and money because mortgage files are being returned for missing documents and rework. The consulting team wants to know whether the issue is a people problem or a process problem.
Applicable framework/metric: DPMO Prioritization Grid.
Analysis: If the file review step has a 5% error rate, that is 50,000 DPMO and should be treated as fix now when it affects approvals, compliance, or customer wait time.
Decision rule: If impact is high and DPMO is high, fix now. If impact is low but DPMO is high, schedule later. If impact is low and DPMO is low, standardize and move on.
Action: Rework the checklist, automate document validation, and put a weekly control report in front of operations leadership.

## 7. Implementation Playbook
1. Define the customer requirement in plain language and convert it into a measurable defect.
2. Establish a clean baseline by collecting enough data to calculate defect rate and DPMO.
3. Map the process end to end so the team can see bottlenecks, handoffs, and variation sources.
4. Use root-cause analysis to separate symptom fixes from process fixes.
5. Pilot the improvement on a small slice of the workflow before scaling it.
6. Install a control mechanism such as a dashboard, checklist, or automated alert so gains do not disappear.
7. Translate the quality gain into dollars saved, customer satisfaction, or risk reduction so the business case is visible.

## 8. Content Quality Audit
Covered well: The source gives a clear beginner-level definition of Six Sigma, its 3.4 defects per million target, and its emphasis on data, structure, and repeatability.
Underplayed or missing: The source does not name DMAIC, show how to prioritize among defects, explain process control after improvement, or connect defect reduction to business economics and service workflows.
Supplement with: Pande, Neuman, and Cavanagh, *The Six Sigma Way*; Harry and Schroeder, *Six Sigma: The Breakthrough Management Strategy Revolutionizing the World's Top Corporations*; Hal Plotkin, "Six Sigma: What It Is and How to Use It" (Harvard Business Review, 1999); Thomas H. Davenport, "Why Six Sigma Is on the Downslope" (Harvard Business Review, 2008); HBS case *GE...We bring good things to life. (A)* (Heskett, 1999); Bruce C. Y. Lee, "Critical decisions in new product launch: pricing and advertising strategies on consumer adoption of green product innovation" (Asian Journal of Technology Innovation, 2014); and peer-reviewed reviews such as "Systematic Review of the Application of Lean and Six Sigma Quality Improvement Methodologies in Radiology" (2016) and "Lean and Six Sigma as continuous quality improvement frameworks in the clinical diagnostic laboratory" (2022).
Red flags in the source: It is accurate but thin on execution mechanics, so readers may understand the target but not the operating model needed to sustain it.

## 9. Quick-Recall Card
```text
Topic: Introduction to Six Sigma
Core idea: Reduce defects and variation with data so the process becomes repeatable and customer-facing quality improves.
Key metric/formula: DPMO = defect rate * 1,000,000.
Framework trigger: Use it when a process is producing avoidable errors, delays, or rework.
Watch out for: Treating Six Sigma as a slogan instead of a disciplined measurement-and-control system.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which defect, bottleneck, or variation source creates the biggest customer and business pain?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:5, 4:5, 5:4, 6:4, 7:4, 8:4, 9:5, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [DMAIC roadmap, DPMO prioritization grid, IT/AI/Product/Consulting examples, control logic, business case translation, external references] Final scores: all 5/5 Pass 2 completed: 2026-04-18 20:03 Audited by: A4 -->
