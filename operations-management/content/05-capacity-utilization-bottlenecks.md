# Capacity, Utilization, and Bottlenecks

## Overview

Capacity is how much you can produce. A bottleneck is the slowest step that limits the whole system.

---

## Why It Matters

If you improve a non-bottleneck step, overall output may not change. Focusing on the bottleneck gives the biggest impact.

## Key Principles

- System output is limited by the bottleneck
- Protect the bottleneck from downtime and poor scheduling
- Don’t overload the system—high utilization can create long waits

## Key Terms

| Term | Definition |
|------|------------|
| **Capacity** | Maximum output per time |
| **Utilization** | Used capacity / available capacity |
| **Bottleneck** | Step with the lowest capacity (limits throughput) |
| **Cycle time** | Time between completed units at a step |

## Use Case

In batch production, the slowest machine determines total daily output.

## Scenario

> A shirt factory has cutting, sewing, and packing. Sewing is slowest, so piles build up before sewing. Improving packing won’t help much until sewing improves.

## Examples

- Adding one worker to the bottleneck station increases total output.
- Fixing frequent breakdowns at the bottleneck reduces delays across the line.

---

## Audited Appendix

# Capacity, Utilization, and Bottlenecks
**Course:** Operations Management  
**Module:** Content / Capacity, Utilization, and Bottlenecks  
**Audited on:** 2026-04-18  
**Audited by:** A7  
**Source files reviewed:** `operations-management/content/05-capacity-utilization-bottlenecks.md`

---

## 1. Topic Snapshot
Capacity is the ceiling on how much work a system can do, and the bottleneck is the slowest step that sets the real ceiling.
For an IT/AI/Product/Consulting leader, this is the difference between adding resources that actually raise throughput and adding resources that only increase idle cost.
The decision it supports is which step to protect, which step to expand, and which step to leave alone because it is not the constraint.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Capacity / Available capacity / Used capacity | - | How much the system can do, and how much of it is actually being used. | Sets the upper limit on output. | Units per hour, day, or shift; utilization. | Ops planning, staffing, production. |
| Utilization | - | Used capacity divided by available capacity. | Shows whether resources are slack or stretched. | `used / available`. | Capacity reviews, workforce planning. |
| Bottleneck | - | The slowest step that limits throughput. | Explains why improving one step may not raise system output. | Step capacity, queue length, cycle time. | Lean, line balancing, service ops. |
| Throughput / Total daily output | - | How much finished work the system actually produces. | Connects capacity to real output. | Units finished per time period. | Manufacturing, service centers, logistics. |
| Cycle time | - | Time between completed units at a step. | Links step speed to customer waiting. | Time per unit, wait time, takt gap. | Production, queue management. |
| Downtime / Breakdowns / Poor scheduling | - | Lost time from failures or bad plans. | Protects the bottleneck from avoidable loss. | Lost minutes, uptime, schedule adherence. | Maintenance, dispatch, operations control. |
| Batch production / Line / Workers / Machine | - | The specific operating context used in the source. | Shows how one slow step can constrain the whole line. | Output per line, worker utilization, machine uptime. | Factory floors, assembly lines. |
| Cutting / Sewing / Packing / Shirt factory | - | The example line in the source. | Makes the bottleneck idea concrete. | Station capacity, queue before step, line output. | Apparel, light manufacturing. |
| Piles build up / Long waits / Delays / Frequent breakdowns / Bottleneck station | - | The visible symptoms of a constrained system. | Signals that the system is out of balance. | Queue size, waiting time, missed orders. | Service ops, warehouses, production control. |

## 3. Frameworks & Matrices

### Framework 1: Constraint Ladder
**Purpose:** Move from raw capacity to the actual system constraint.

**Text Diagram:**
```text
Available capacity -> Used capacity -> Bottleneck -> Throughput
```

Axes / Quadrants / Components explained:
Component 1: available capacity - what the system could do.
Component 2: used capacity - what it is doing.
Component 3: bottleneck - what caps the whole line.
Component 4: throughput - what the customer actually gets.

IT/AI/Product/Consulting worked example: An AI support workflow has enough analysts overall, but the review step is slow. The ladder shows that the system is constrained by review capacity, not total headcount.

When to pull this out in a meeting: When a team wants to add people everywhere instead of fixing the actual constraint.

### Framework 2: Bottleneck Protection Map
**Purpose:** Protect the slowest step from avoidable loss.

**Text Diagram:**
```text
Downtime -> scheduling -> feeding work -> bottleneck output
```

Axes / Quadrants / Components explained:
Component 1: downtime protection - keep the bottleneck running.
Component 2: scheduling discipline - give it steady work.
Component 3: feeding work - avoid starvation and blockage.
Component 4: output stability - keep throughput predictable.

IT/AI/Product/Consulting worked example: A software release pipeline protects the final QA gate with better scheduling and fewer last-minute changes. The protection map shows that uptime at the bottleneck matters more than overtime elsewhere.

When to pull this out in a meeting: When the constraint is known but keeps getting interrupted.

### Framework 3: Utilization vs Wait Curve
**Purpose:** Show why very high utilization creates long waits.

**Text Diagram:**
```text
Low utilization -> little waiting
High utilization -> long queues
```

Axes / Quadrants / Components explained:
Component 1: utilization level.
Component 2: waiting time or queue length.
Component 3: service reliability.
Component 4: customer impact.

IT/AI/Product/Consulting worked example: A call center running at 95% utilization may look efficient on paper, but customers wait longer and service quality falls. The curve shows why more load is not always better.

When to pull this out in a meeting: When a team celebrates utilization without looking at waiting time.

### Framework 4: Improvement Order Map
**Purpose:** Decide what to fix first so capacity work actually changes output.

**Text Diagram:**
```text
Fix bottleneck -> then remove nearby waste -> then rebalance the rest
```

Axes / Quadrants / Components explained:
Component 1: bottleneck fix.
Component 2: waste removal around the bottleneck.
Component 3: line balancing or scheduling changes.
Component 4: non-bottleneck changes only after the constraint moves.

IT/AI/Product/Consulting worked example: A shirt factory improves sewing first, not packing, because sewing is the slowest step. The map prevents wasted effort on non-constraints.

When to pull this out in a meeting: When the team is improving the wrong station.

## 4. Formulas
No explicit numeric formulas appear in the source. The formulas below are decision heuristics synthesized from the source themes and marked [verified from model knowledge, not source].

### Formula 1: Utilization
Formula: `Utilization = used capacity / available capacity`
Variables:
used capacity = actual output or time used
available capacity = total possible output or time
Why this formula exists: It answers how intensely a resource is being used.
How to interpret the output:
Below 70% -> slack or underuse
70%-85% -> usually healthy
Above 85% -> queue risk rises
Worked example with numbers: A machine is available 10 hours and used 8.5 hours, so utilization is 85%. Decision: protect the bottleneck from further overload.

### Formula 2: Throughput
Formula: `Throughput = completed units / time period`
Variables:
completed units = finished items, cases, or orders
time period = hour, day, or shift
Why this formula exists: It answers how much finished work the line produces.
How to interpret the output:
Throughput below demand -> backlog grows
Throughput equal to demand -> stable if quality holds
Throughput above demand -> slack or buffer capacity
Worked example with numbers: A sewing line finishes 300 shirts a day, but demand is 360. Decision: the bottleneck must be relieved or the backlog will keep growing.

### Formula 3: Bottleneck Capacity
Formula: `Bottleneck Capacity = minimum(step capacities)`
Variables:
step capacities = output capability of each step
Why this formula exists: It answers which step actually sets the ceiling for the whole system.
How to interpret the output:
The lowest-capacity step is the constraint
Raising any other step alone will not raise total output
Raising the bottleneck raises system throughput
Worked example with numbers: Cutting = 500/day, sewing = 300/day, packing = 450/day. Decision: the line capacity is 300/day until sewing changes.

### Formula 4: Cycle Time
Formula: `Cycle Time = time between completed units at a step`
Variables:
completed units = finished units leaving the step
time between units = spacing between completions
Why this formula exists: It answers how quickly the process turns work into finished output.
How to interpret the output:
Shorter cycle time -> faster flow
Long cycle time -> queue or process problem
Cycle time at bottleneck -> line pacing indicator
Worked example with numbers: If one shirt leaves sewing every 2 minutes, cycle time is 2 minutes. Decision: compare that to demand to see whether sewing is the bottleneck.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Improve a non-bottleneck step and expect total output to rise | Find the slowest step first and fix that constraint |
| Treat high utilization as automatically good | Check whether queues and waits are rising too |
| Let the bottleneck sit idle because of poor scheduling | Protect the bottleneck with steady feeding and uptime |
| Add work everywhere at once | Rebalance the line around the constraint |
| Judge performance by one machine or team | Measure the whole system's throughput and waiting time |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Shirt Factory Sewing Bottleneck
Situation: A shirt factory has cutting, sewing, and packing. Sewing is the slowest step, so piles build up before sewing while packing stays busy but does not change total output.
Applicable framework/metric: Bottleneck Protection Map and Bottleneck Capacity.
Analysis: Cutting can produce 500 shirts/day, sewing 300, and packing 450. The line capacity is 300. Adding one worker to packing does not change the system output.
Decision rule: If the bottleneck is known, improve that step first. If another step has spare capacity, leave it alone until the constraint moves.
Action: Add maintenance to the sewing machine, smooth the sewing schedule, and reduce changeover time at the constrained station.

### Scenario 2: Support Team Queue
Situation: An AI support team has enough analysts overall, but ticket review takes too long. The result is long waits and rising customer complaints.
Applicable framework/metric: Utilization vs Wait Curve and Throughput.
Analysis: Review utilization is 93%, which creates queues. Throughput is 180 tickets/day while arrivals are 220. The queue will grow unless the review step is relieved.
Decision rule: If utilization is above 85% and demand exceeds throughput, reduce load on the bottleneck or add capacity there. If queues keep growing, the constraint is not being protected.
Action: Automate low-risk tickets, assign a fast lane for standard cases, and review the backlog every morning.

### Scenario 3: Hospital Lab Step
Situation: A hospital notices that patients wait too long between tests. Doctors are busy, but the delay is actually in the lab handoff and sample processing step.
Applicable framework/metric: Improvement Order Map and Cycle Time.
Analysis: One sample leaves the lab every 4 minutes, but arrivals are every 2 minutes during peak time. Cycle time at the bottleneck exceeds demand pacing, so queues build up.
Decision rule: If cycle time at one step is longer than demand pacing, fix that step before rebalancing the rest. If the queue sits in front of one station, that station is the constraint.
Action: Add shift coverage to the lab step, prioritize urgent samples, and protect the bottleneck from interruptions.

## 7. Implementation Playbook
1. Measure each step's capacity in the current line or workflow.
2. Identify the lowest-capacity step and confirm it with actual queue data.
3. Protect the bottleneck from downtime, poor scheduling, and starving.
4. Remove obvious waste around the bottleneck before expanding elsewhere.
5. Recheck throughput and utilization after each change.
6. Only rebalance the rest of the system after the constraint moves.

## 8. Content Quality Audit
Covered well: The source correctly teaches the most important OM idea: the system is limited by its bottleneck, not by the average of all steps.
Underplayed or missing: Variability, queueing behavior, capacity buffers, and the practical tradeoff between local utilization and system waiting time.
Supplement with: Goldratt and Cox, *The Goal* [verified from model knowledge, not source]; Hopp and Spearman, *Factory Physics* [verified from model knowledge, not source]; Womack and Jones, *Lean Thinking* [verified from model knowledge, not source]; Skinner (1969), "Manufacturing - Missing Link in Corporate Strategy" [verified from model knowledge, not source]; and case-style teaching material on Toyota line balancing and healthcare bottleneck management [verified from model knowledge, not source].
Red flags in the source: The bottleneck story is simplified to the point that it can sound deterministic, when real systems also depend on variability, batching, and priority rules.

## 9. Quick-Recall Card
```text
Topic: Capacity, Utilization, and Bottlenecks
Core idea: The slowest step sets the ceiling, so fix the constraint first.
Key metric/formula: Utilization, throughput, bottleneck capacity, cycle time.
Framework trigger: Use it when output is stuck, queues are growing, or a station is overloaded.
Watch out for: Raising the wrong step and mistaking local efficiency for system improvement.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which step is actually constraining total output?
```

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:4, 3:5, 4:4, 5:5, 6:5, 7:5, 8:4, 9:5, 10:5]
Pass 1 average: 4.6
Sections rewritten: [2, 4, 8]
Enrichments applied: [source-term clustering; IT/AI/Product/Consulting lens throughout; 3 metric-driven scenarios; model-knowledge formulas explicitly labeled; operations constraints and bottleneck reading list/case framing]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 15:25 IST
Audited by: A7
-->
