# Assembly Line Design (Cycle Time, Line Balancing)

## Overview

An assembly line is work split into steps across stations. Line design decides what work goes where so the line runs smoothly without big delays.

---

## Why It Matters

A poorly balanced line creates idle time at some stations and overload at others, reducing output and increasing cost.

## Key Principles

- Balance tasks so each station has similar workload
- The slowest station sets the line speed
- Reduce unnecessary movement and handoffs

## Key Terms

| Term | Definition |
|------|------------|
| **Workstation** | A spot where a set of tasks is done |
| **Line balancing** | Distributing tasks evenly |
| **Cycle time** | Time allowed per unit at each station (sets pace) |
| **Idle time** | Time workers wait due to imbalance |

## Use Case

A company redesigns a line to meet demand without adding new machines.

## Scenario

> In “Don’t Bother Me I can’t cope,” the line feels chaotic. After balancing tasks, the same workers produce more with less stress.

## Examples

- Moving 10 seconds of work from an overloaded station to a lighter station increases output.
- Splitting one long task into two shorter tasks reduces bottleneck pressure.

---

## Audited Appendix

# Assembly Line Design (Cycle Time, Line Balancing)
**Course:** Operations Management  
**Module:** Content / Assembly Line Design  
**Audited on:** 2026-04-18  
**Audited by:** A6  
**Source files reviewed:** `operations-management/content/09-assembly-line-design.md`

---

## 1. Topic Snapshot
Assembly line design is the work of splitting a process into stations so the line runs smoothly without large delays or overloads.
For an IT/AI/Product/Consulting leader, it is the same design problem as structuring a software provisioning flow, a device build flow, or a service desk flow so work moves predictably.
The decision it helps make is how to place work across stations so cycle time is met, idle time is controlled, and the slowest station does not cap output.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Assembly line | - | A sequence of work steps split across stations. | Makes repetitive work faster and more controllable. | Output per hour, wait time, defect rate. | Factory design, operations reviews, lean projects. |
| Workstation | - | A place where a defined set of tasks is done. | Keeps work organized and assignable. | Station load, idle time, cycle compliance. | Plant floor, cell design, service operations. |
| Line balancing | - | Distributing tasks so stations carry similar workloads. | Prevents one station from dictating the whole line. | Balance delay, line efficiency, station time spread. | Production planning, industrial engineering, lean ops. |
| Cycle time | - | The time allowed for a unit at a station before the next unit should move. | Sets the pace of the line. | Seconds per unit, units per hour. | Scheduling, takt planning, line control. |
| Idle time | - | Time when a station or worker is waiting because work is unevenly assigned. | Shows wasted capacity. | Minutes waiting, idle percentage, labor utilization. | Balance studies, staffing reviews, cost audits. |
| Slowest station | - | The station that takes the longest and therefore limits line speed. | Identifies the bottleneck in a paced line. | Maximum station time, queue growth, missed output. | Bottleneck analysis, throughput reviews. |
| Unnecessary movement | - | Extra physical motion that does not change the product or service. | Reduces wasted effort and time. | Steps walked, motion time, handling count. | Lean audits, ergonomics reviews, plant layout work. |
| Handoffs | - | The transfer of work from one station or person to another. | Helps define where work changes owners. | Number of transfers, error rate at transfer, wait time. | Cross-functional process maps, service operations. |
| Demand | - | How many units or cases the line must meet in a period. | Sets the output target the line must satisfy. | Units per day, orders per shift, cases per hour. | Capacity planning, sales-operations review. |
| Takt time [verified from model knowledge, not source] | - | The pace required to meet customer demand. | Converts demand into a pacing target for the line. | Available time / demand. | Lean line design, capacity planning, shop-floor boards. |
| Precedence constraint [verified from model knowledge, not source] | - | A rule that some tasks must happen before others. | Keeps the line physically and logically feasible. | Feasible task sequence, violations per design. | Assembly planning, line balancing software. |

## 3. Frameworks & Matrices

### Cycle-Time Balance Map
**Purpose:** Check whether the work assigned to each workstation fits the pacing requirement.

**Text Diagram:**
```text
Demand -> required cycle time -> station load -> idle time / overload -> output
```

Axes / Quadrants / Components explained:
Component 1: required cycle time - the pace the line must hit.
Component 2: station load - the actual work time assigned to one workstation.
Component 3: overload - when station load exceeds cycle time and becomes the slowest station.
Component 4: idle time - unused time created when station load is below cycle time.

IT/AI/Product/Consulting worked example: An electronics operations team uses a dashboard to compare station time against cycle time every hour. If one station exceeds the pace because a firmware scan takes too long, the team reassigns that scan to a lighter station instead of hiring another operator.

When to pull this out in a meeting: When output misses target even though the line has enough people on paper.

### Precedence-Constrained Task Assignment
**Purpose:** Place tasks into stations without breaking the order in which the work must happen.

**Text Diagram:**
```text
Task A -> Task B -> Task C
   \                 /
    -> Task D -> Task E
```

Axes / Quadrants / Components explained:
Component 1: precedence - what must happen before the next task can begin.
Component 2: feasible assignment - which tasks can sit together in the same workstation.
Component 3: station count - how many stations are needed after respecting the order.
Component 4: handoffs - where work can safely move without creating rework.

IT/AI/Product/Consulting worked example: A device provisioning line must image the laptop before security enrollment, and security enrollment before handoff to the user. The assignment choice is not just "equalize time"; it is "equalize time while keeping the sequence valid."

When to pull this out in a meeting: When someone proposes moving work to a different station without checking task order.

### Line Efficiency and Idle-Time Tradeoff
**Purpose:** Compare alternative line designs using one simple managerial scorecard.

**Text Diagram:**
```text
More station time fit  ->  higher efficiency
More unused time       ->  more idle time
```

Axes / Quadrants / Components explained:
Component 1: total work content - all task times added together.
Component 2: available station time - stations multiplied by cycle time.
Component 3: line efficiency - share of available station time that is productive.
Component 4: balance delay - the time wasted because the line is not perfectly even.

IT/AI/Product/Consulting worked example: A consulting back-office team processing hardware swaps has two layout options. Option A has slightly fewer stations but higher idle time; Option B has more stations but lower overload risk. The scorecard shows which design gives better throughput without creating hidden waits.

When to pull this out in a meeting: When you need to choose between two line layouts, not just tweak one existing line.

## 4. Formulas
No explicit numeric formulas appear in the source. The formulas below are standard line-balancing decision tools added from model knowledge and marked [verified from model knowledge, not source].

### Formula 1: Takt Time [verified from model knowledge, not source]
Formula: `Takt time = available production time / customer demand`
Variables:
available production time = usable time in the shift or day
customer demand = required units in the same period
Why this formula exists: It answers how fast the line must move to meet demand.
How to interpret the output:
Value much lower than station time -> the line cannot meet demand without redesign
Value close to station time -> the design is feasible but tight
Value comfortably above station time -> the line has slack and can absorb variation
Worked example with numbers: A tablet line has 28,800 seconds of available time in a shift and must ship 480 units. Takt time = 60 seconds per unit. Decision: if any workstation takes more than 60 seconds, rebalance before launch.

### Formula 2: Minimum Stations [verified from model knowledge, not source]
Formula: `Minimum stations = ceil(total task time / cycle time)`
Variables:
total task time = the sum of all task durations for one unit
cycle time = the pacing target per station
Why this formula exists: It answers the smallest practical station count that can fit the work.
How to interpret the output:
Value jumps up sharply -> a tiny change in cycle time may force another station
Value stable -> the current design can likely be improved by rebalance, not by new capacity
Value very high -> the process may need task redesign or automation
Worked example with numbers: Total task time is 428 seconds and cycle time is 60 seconds. Minimum stations = ceil(428 / 60) = 8. Decision: if leadership wants 7 stations, the work content must be reduced or split.

### Formula 3: Line Efficiency [verified from model knowledge, not source]
Formula: `Line efficiency = total task time / (number of stations * cycle time)`
Variables:
total task time = all productive task time combined
number of stations = actual stations used in the design
cycle time = pacing target per station
Why this formula exists: It answers how much of the line's available station time is actually productive.
How to interpret the output:
Value below 80% -> the line is carrying too much idle time or too many stations
Value 80% to 90% -> usually workable and worth piloting
Value above 90% -> strong design, but verify quality and ergonomics are not being squeezed
Worked example with numbers: 428 seconds of work across 8 stations with a 60-second cycle time gives 428 / 480 = 89.2%. Decision: hold the layout if quality is stable; otherwise move a task from the slowest station to a lighter one.

### Formula 4: Balance Delay [verified from model knowledge, not source]
Formula: `Balance delay = 1 - line efficiency`
Variables:
line efficiency = the productive share of station time
balance delay = the share of time lost to imbalance
Why this formula exists: It answers how much capacity is being wasted by uneven task allocation.
How to interpret the output:
Value under 10% -> line is tightly balanced
Value 10% to 20% -> acceptable but worth a redesign review
Value above 20% -> imbalance is large enough to justify rework of the station plan
Worked example with numbers: If line efficiency is 89.2%, balance delay is 10.8%. Decision: use this to compare two designs and choose the one with less wasted station time.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Put work into stations just to make the chart look even. | Respect precedence and then balance the remaining load. |
| Ignore the slowest station because the average looks fine. | Design around the station that actually caps output. |
| Add headcount before checking idle time and handoffs. | Reassign tasks, remove unnecessary movement, then add capacity only if needed. |
| Treat cycle time as a slogan rather than a target. | Use cycle time as the operational pacing rule for each workstation. |
| Assume one overloaded station is harmless if everyone else is idle. | Treat overload as a throughput risk and rebalance quickly. |
| Optimize for speed while quality checks are falling through the handoffs. | Build quality checks into the station plan so speed does not create rework. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Consumer Electronics Final Assembly
Situation: A factory assembling smart speakers must ship 480 units per shift, and the line has 28,800 seconds of usable time. The team currently has eight workstations, but one station is always late because label printing and packing were bundled together.
Applicable framework/metric: Cycle-Time Balance Map and Line Efficiency.
Analysis: Takt time is 60 seconds. Total task time is 428 seconds. Minimum stations = ceil(428 / 60) = 8. Line efficiency with 8 stations = 89.2%. The slowest station is the one doing print-plus-pack, so the imbalance is local, not system-wide.
Decision rule: If any station exceeds cycle time, split or move work immediately. If efficiency is between 80% and 90%, rebalance before adding equipment. If efficiency exceeds 90% and quality is stable, freeze the design.
Action: Separate printing from packing, move barcode verification to a lighter station, and monitor output for one week before scaling the line.

### Scenario 2: AI Hardware Provisioning Line
Situation: An IT operations team provisions AI workstations for new hires. Each unit needs imaging, security enrollment, asset tagging, model-access setup, and handoff. Leadership wants a faster process without sacrificing compliance.
Applicable framework/metric: Precedence-Constrained Task Assignment and Balance Delay.
Analysis: The total work content is 252 seconds per unit and the target cycle time is 60 seconds. Minimum stations = ceil(252 / 60) = 5. Line efficiency with 5 stations is 84%, which is workable. One station runs at 63 seconds because the security enrollment step was placed too late in the flow.
Decision rule: If a station breaks cycle time, rebalance before speeding up the front end. If balance delay is above 15%, redesign the task mix. If delay is below 10%, standardize and automate.
Action: Move asset tagging earlier, pre-stage model-access approvals, and create a visual queue board so the team can see which handoff is slowing the line.

### Scenario 3: Consulting-Style Internal Service Line
Situation: A consulting firm's back office processes laptop swaps for 120 employees after a client rollout. Requests arrive unevenly, and the team wants the process to feel more like a production line than a ticket queue.
Applicable framework/metric: Line Efficiency and Idle-Time Tradeoff.
Analysis: The available time per day is 28,800 seconds and the demand is 60 swaps per day, so cycle time is 480 seconds. The work content is 3,900 seconds. Minimum stations = ceil(3,900 / 480) = 9. Line efficiency with 9 stations is 90.3%, which is strong but leaves little room for variation.
Decision rule: If efficiency is above 90% but complaints rise, the issue is variation, not headline capacity. If efficiency is below 80%, consolidate tasks. If idle time is high but cycle time is safe, move work instead of hiring.
Action: Pre-image devices overnight, separate asset inventory from user handoff, and use one control tower to route exceptions before they enter the line.

## 7. Implementation Playbook
1. List every task in the assembly line and record its precedence.
2. Time each task on a small sample of units to separate normal work from outliers.
3. Calculate demand, takt time, and cycle time for the shift or day.
4. Build a station-load table and assign tasks without breaking precedence.
5. Flag any workstation that exceeds cycle time and rebalance it before launch.
6. Pilot the line for one day, then compare output, idle time, and handoff errors against the design.
7. Lock the best version into a short SOP, visual board, and escalation rule.

## 8. Content Quality Audit
Covered well: The source gives a clean definition of an assembly line, explains why balance matters, and introduces the core vocabulary of workstation, line balancing, cycle time, and idle time.
Underplayed or missing: The chapter does not explain precedence constraints, takt time, line efficiency, balance delay, mixed-model lines, or the effect of variability on station choice. It also does not show how a manager actually reassigns work when the slowest station sets the line speed.
Supplement with: Monden, *Toyota Production System: Practical Approach to Management* (1983) [verified from model knowledge, not source]; Womack, Jones, and Roos, *The Machine That Changed the World* (1990) [verified from model knowledge, not source]; Hopp and Spearman, *Factory Physics* (1996; later editions) [verified from model knowledge, not source]; Womack and Jones, HBR, "From Lean Production to the Lean Enterprise" (1994) [verified from model knowledge, not source]; Mishina, *Toyota Motor Manufacturing, U.S.A., Inc.* HBS Case 9-693-019 (1992) [verified from model knowledge, not source]; Salveson (1955) on the assembly line balancing problem; and Scholl and Becker (2006) on exact and heuristic solution procedures for simple assembly line balancing.
Red flags in the source: The source is intentionally introductory, so it can make line balancing sound like equalizing time only. In practice, task order, ergonomic limits, quality checks, and variation can prevent a perfectly even assignment. It also does not distinguish a paced line from a more flexible service flow, which matters when you apply the idea to IT or AI operations.

## 9. Quick-Recall Card
```text
Topic: Assembly Line Design (Cycle Time, Line Balancing)
Core idea: Put the right work in the right station so the slowest station does not control the whole line.
Key metric/formula: Takt time = available production time / customer demand; line efficiency = total task time / (stations * cycle time).
Framework trigger: Use it when output is capped, one station is overloaded, or idle time is visibly uneven.
Watch out for: Equalizing time while breaking precedence or adding unnecessary movement.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which station or handoff is really setting the line speed, and what task move removes that constraint fastest?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:5, 10:5] Sections rewritten: [3, 4, 6, 8] Enrichments applied: [source-term coverage; IT/AI/Product/Consulting examples; model-knowledge formulas explicitly labeled; decision-rule thresholds; supporting references and case framing] Final scores: all 5/5 Pass 2 completed: 2026-04-18 19:49 IST Audited by: A6 -->
