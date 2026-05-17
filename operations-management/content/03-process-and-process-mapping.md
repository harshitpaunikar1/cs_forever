# Process & Process Mapping

## Overview

A process is the step-by-step path work follows. Process mapping is drawing those steps so you can see where time is wasted or where mistakes happen.

---

## Why It Matters

Most problems hide inside processes. Mapping makes the work visible, so you can improve it instead of guessing.

## Key Principles

- Write steps in the real order they happen
- Include decision points (yes/no)
- Identify handoffs (where work changes people/teams)
- Find delays, rework loops, and unclear steps

## Key Terms

| Term | Definition |
|------|------------|
| **Process Map / Flowchart** | Visual of steps and decisions |
| **Handoff** | When work moves from one person/team to another |
| **Rework** | Doing the same work again due to errors |
| **Value-added step** | A step the customer would pay for |

## Use Case

A service center maps complaint handling to reduce back-and-forth and speed up resolutions.

## Scenario

> A company maps “order to shipment” and discovers orders sit unprocessed for 12 hours each day because approvals only happen in the morning.

## Examples

- Mapping a hospital patient journey to reduce waiting between tests.
- Mapping a manufacturing process to reduce repeated inspections.

---

## Audited Appendix

# Process & Process Mapping
**Course:** Operations Management  
**Module:** Content / Process and Process Mapping  
**Audited on:** 2026-04-18  
**Audited by:** A7  
**Source files reviewed:** `operations-management/content/03-process-and-process-mapping.md`

---

## 1. Topic Snapshot
Process mapping is the discipline of drawing the actual step-by-step path work follows, not the way people say it works.
For an IT/AI/Product/Consulting leader, it is the fastest way to see where handoffs, delays, and rework are hurting service, delivery, or product operations.
The decision it supports is where to simplify, automate, or standardize a workflow so the customer sees faster and cleaner service.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Process / Step-by-step path | - | The sequence work follows from start to finish. | Makes work repeatable and visible. | Cycle time, completion rate, error rate. | SOPs, process reviews, operations. |
| Process Map / Flowchart | - | A visual drawing of steps and decisions. | Lets teams see the work instead of guessing. | Number of steps, decision points, delays. | Lean, BPM, operations workshops. |
| Handoff | - | The point where work moves to another person or team. | Exposes where work can stall or get lost. | Handoff count, wait time, defect escape rate. | Service ops, project work, cross-functional teams. |
| Rework | - | Doing the same work again because something went wrong. | Shows process waste and quality failure. | Rework rate, scrap, repeat tickets. | Support, manufacturing, QA. |
| Value-added step | - | A step the customer would actually pay for. | Separates real value from busywork. | Value-added time / total time. | Lean, process design, customer journey reviews. |
| Decision point / Yes-No branch | - | A step where the process splits based on a choice. | Keeps exceptions explicit. | Decision accuracy, exception rate. | Flowcharts, approvals, controls. |
| Delay / Back-and-forth / Unclear step | - | Waiting or confusion inside the workflow. | Finds time waste and bottlenecks. | Waiting time, queue time, cycle time. | Service centers, operations, PMO. |
| Complaint handling / Order to shipment / Patient journey / Repeated inspections / Service center | - | The example processes from the source. | Shows process mapping in service and product settings. | Resolution time, shipment delay, patient wait, defect rate. | Healthcare, logistics, support, manufacturing. |

## 3. Frameworks & Matrices

### Framework 1: Process Visibility Map
**Purpose:** Turn a hidden workflow into a visible sequence that people can agree on.

**Text Diagram:**
```text
Start -> Step 1 -> Step 2 -> Step 3 -> End
```

Axes / Quadrants / Components explained:
Component 1: start and end points.
Component 2: actual steps in order.
Component 3: decision points that change the path.
Component 4: visible delays and ownership at each step.

IT/AI/Product/Consulting worked example: A support team maps incident intake, triage, escalation, and closure so the product manager can see where customers wait. The visibility map turns "slow support" into a specific process question.

When to pull this out in a meeting: When different teams describe the same work differently.

### Framework 2: Handoff and Rework Matrix
**Purpose:** Find where work is lost between teams or repeated because of errors.

**Text Diagram:**
```text
Few handoffs / few errors     Many handoffs / few errors
Few handoffs / many errors    Many handoffs / many errors
```

Axes / Quadrants / Components explained:
Component 1: handoff count.
Component 2: rework count.
Component 3: ownership clarity.
Component 4: queue or waiting time after the handoff.

IT/AI/Product/Consulting worked example: An AI product release needs legal, security, and product review. The matrix reveals whether the delay is from too many handoffs or from rework caused by unclear approval rules.

When to pull this out in a meeting: When everyone says the delay is "somewhere else."

### Framework 3: Value-Added vs Waste Filter
**Purpose:** Separate customer value from non-value-added motion.

**Text Diagram:**
```text
Value-added work -> necessary but non-value-added -> pure waste
```

Axes / Quadrants / Components explained:
Component 1: value-added steps.
Component 2: necessary controls or compliance steps.
Component 3: wasteful rework, waiting, or back-and-forth.
Component 4: simplification or automation opportunity.

IT/AI/Product/Consulting worked example: A bank account-opening process includes identity checks, document review, and manual approval. The filter shows which steps are customer value, which are compliance, and which are pure delay.

When to pull this out in a meeting: When the team wants to automate a broken process without removing waste first.

### Framework 4: Delay-to-Delivery Map
**Purpose:** Show how waiting and backlogs affect service speed.

**Text Diagram:**
```text
Arrival -> Queue -> Work -> Queue -> Delivery
```

Axes / Quadrants / Components explained:
Component 1: arrival rate of work.
Component 2: queue size and waiting time.
Component 3: processing speed at each step.
Component 4: final delivery time to the customer.

IT/AI/Product/Consulting worked example: A hospital outpatient journey or a coffee shop lunch line can look efficient until you map the queues. The delay-to-delivery view shows whether the bottleneck is staffing, batching, or approvals.

When to pull this out in a meeting: When customers complain about time, not the final output itself.

## 4. Formulas
No explicit numeric formulas appear in the source. The formulas below are decision heuristics synthesized from the source themes and marked [verified from model knowledge, not source].

### Formula 1: Cycle Time
Formula: `Cycle Time = process time + waiting time + handoff delay`
Variables:
process time = time spent doing the work
waiting time = time spent in queue
handoff delay = time lost between owners
Why this formula exists: It answers how long the customer actually waits.
How to interpret the output:
Long cycle time -> remove queues or handoffs
Cycle time dominated by waiting -> fix scheduling or approvals
Cycle time dominated by process time -> improve the work itself
Worked example with numbers: A complaint takes 12 minutes of work and 48 minutes of waiting. Decision: the fix is queue management, not faster typing.

### Formula 2: Rework Rate
Formula: `Rework Rate = reworked cases / total cases`
Variables:
reworked cases = items or cases sent back for correction
total cases = total completed work
Why this formula exists: It answers how much of the process is being done twice.
How to interpret the output:
Low rework -> process is stable
Rising rework -> quality or clarity problem
High rework -> redesign the upstream step
Worked example with numbers: 30 of 600 orders are corrected again, so rework rate is 5%. Decision: inspect the order entry step and the approval criteria.

### Formula 3: Value-Added Ratio
Formula: `Value-Added Ratio = value-added time / total process time`
Variables:
value-added time = time the customer would pay for
total process time = all time in the workflow
Why this formula exists: It answers how much of the process is truly useful to the customer.
How to interpret the output:
Low ratio -> too much waste -> simplify
Moderate ratio -> improve flow and remove checks
High ratio -> efficient process -> protect the design
Worked example with numbers: A 60-minute process has 15 minutes of value-added time. Decision: cut waiting and rework before adding more capacity.

### Formula 4: Throughput
Formula: `Throughput = completed units / time period`
Variables:
completed units = finished cases, orders, or patients
time period = hour, day, or week
Why this formula exists: It answers how much work the system finishes.
How to interpret the output:
Low throughput -> constraint or bottleneck
Throughput below demand -> backlog will grow
Throughput above demand -> capacity is adequate if quality holds
Worked example with numbers: A service desk closes 80 tickets a day while 100 arrive. Decision: backlog will grow unless a bottleneck is removed or capacity is added.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Draw the process the way policy says it works | Map the process the way work actually happens |
| Ignore handoffs because they seem minor | Count handoffs and watch where work gets lost |
| Assume waiting is a customer-side problem | Treat queues and backlogs as process defects |
| Automate a broken workflow | Remove waste and ambiguity before automation |
| Celebrate speed if rework is rising | Track cycle time and quality together |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Service Center Complaint Handling
Situation: A service center gets repeated complaints about slow resolution. Agents are busy, but customers keep calling back because the case moves between teams.
Applicable framework/metric: Handoff and Rework Matrix and Rework Rate.
Analysis: Out of 400 complaints, 52 need a second pass. Rework rate is 13%. The biggest delay is the handoff from frontline support to technical review.
Decision rule: If rework is above 10%, redesign the handoff or clarify the rules. If waiting time falls but rework rises, the new process is too loose.
Action: Add a single owner, define escalation criteria, and remove duplicate approval steps.

### Scenario 2: Order to Shipment Delay
Situation: An e-commerce team maps order to shipment and finds that orders sit unprocessed for 12 hours every day because approvals happen only in the morning.
Applicable framework/metric: Delay-to-Delivery Map and Cycle Time.
Analysis: Process time is 30 minutes, but waiting time is 12 hours. Throughput is adequate when the queue is empty, but backlog builds overnight.
Decision rule: If waiting dominates cycle time, change staffing or approval cadence. If work stays in queue more than one business cycle, the process is designed wrong.
Action: Add rolling approvals, pre-approve low-risk orders, and track same-day shipment rate.

### Scenario 3: Hospital Testing Path
Situation: A hospital wants to shorten the path from patient check-in to test results. The process includes test registration, lab routing, and result verification.
Applicable framework/metric: Process Visibility Map and Value-Added Ratio.
Analysis: Only 18 minutes of a 70-minute flow is value-added. The rest is waiting, transport, or duplicate entry. The main issue is not clinician speed but process design.
Decision rule: If value-added ratio is below 30%, simplify steps before adding more staff. If quality drops after simplification, restore only the critical control points.
Action: Combine check-in steps, digitize test routing, and remove duplicate data entry.

## 7. Implementation Playbook
1. Map the current process from start to finish with the people who actually do the work.
2. Mark every decision point, handoff, delay, and rework loop on the map.
3. Measure cycle time, rework rate, throughput, and value-added ratio for the main path.
4. Identify the one bottleneck or handoff that creates the biggest delay.
5. Test one simplification, staffing change, or approval rule change before redesigning everything.
6. Standardize the improved process in a short SOP or checklist and review it weekly.

## 8. Content Quality Audit
Covered well: The source gives a clean introduction to process visibility and correctly focuses attention on delays, rework, handoffs, and value-added steps.
Underplayed or missing: Process variation, queueing theory, bottleneck analysis, capacity planning, and the difference between process design and process control.
Supplement with: Hammer and Champy, *Reengineering the Corporation* [verified from model knowledge, not source]; Womack and Jones, *Lean Thinking* [verified from model knowledge, not source]; Dumas et al., *Fundamentals of Business Process Management* [verified from model knowledge, not source]; and case-style teaching material on Toyota process redesign, service blueprinting, and hospital flow improvement [verified from model knowledge, not source].
Red flags in the source: The chapter is intentionally simplified, so it can make mapping look easier than it is in real organizations where variation, compliance, and stakeholder conflict complicate the workflow.

## 9. Quick-Recall Card
```text
Topic: Process & Process Mapping
Core idea: Make work visible so you can remove delay, rework, and handoff friction.
Key metric/formula: Cycle time, rework rate, value-added ratio, throughput.
Framework trigger: Use it when a process is slow, messy, or full of back-and-forth.
Watch out for: Automating a broken process or ignoring queues.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which step is causing the biggest delay or waste?
```

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:4, 3:5, 4:4, 5:5, 6:5, 7:5, 8:4, 9:5, 10:5]
Pass 1 average: 4.6
Sections rewritten: [2, 4, 8]
Enrichments applied: [source-term clustering; IT/AI/Product/Consulting lens throughout; 3 metric-driven scenarios; model-knowledge formulas explicitly labeled; operations/process-improvement reading list and case framing]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 15:23 IST
Audited by: A7
-->
