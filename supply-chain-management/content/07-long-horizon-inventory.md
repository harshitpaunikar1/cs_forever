# Inventory Management Over a Longer Horizon

## Overview

This is about managing stock for products that sell continuously over time (like soap, rice, spare parts). The focus is deciding when to reorder and how much.

---

## Why It Matters

It reduces daily firefighting. Good models help keep products available while controlling storage cost.


## Key Principles

- Set reorder points (when to reorder)
- Decide order quantity (how much to reorder)
- Keep safety stock for uncertainty
- Balance holding cost vs stockout cost


## Key Terms

| Term | Definition |
|------|------------|
| **Reorder Point (ROP)** | Inventory level that triggers a new order |
| **Safety Stock** | Extra stock kept to handle uncertainty |
| **Holding Cost** | Cost of storing inventory |


## Use Case

A supermarket uses reorder points for staples like sugar and flour to avoid empty shelves.


## Scenario

> A store waits too long to reorder. Delivery takes 10 days. Shelves go empty for a week. With a reorder point and safety stock, this wouldn’t happen.


## Examples

- Pharmacies keep safety stock for critical medicines.
- A hardware store uses reorder points for fast-moving screws and tools.

---

## Audited Appendix

# Inventory Management Over a Longer Horizon
**Course:** Supply Chain Management  
**Module:** Content / Long-Horizon Inventory Management  
**Audited on:** 2026-04-19  
**Audited by:** A2  
**Source files reviewed:** `supply-chain-management/content/07-long-horizon-inventory.md`

---

## 1. Topic Snapshot
This topic is the control logic for keeping inventory available while not overbuying.
For an IT/AI/Product/Consulting leader, it is the decision framework for service spares, fulfillment inventory, and critical consumables. [verified from model knowledge, not source]
It helps decide when to reorder, how much buffer to hold, and how much stockout risk is acceptable.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| `reorder point` `ROP` `lead time` `inventory position` `reorder trigger` | Reorder control | The stock level or inventory state that tells you to place the next order. | Prevents stockouts from lead-time delays. | Units on hand, units on order, backlog, and the trigger level. | Replenishment planning, ERP screens, procurement reviews. |
| `safety stock` `demand uncertainty` `service level` `stockout risk` `fill rate` | Buffer against uncertainty | Extra stock kept so random demand or delay does not cause an empty shelf. | Converts uncertainty into a planned buffer. | Safety units, service level target, fill rate, stockout frequency. | Operations planning, retail replenishment, supply chain meetings. |
| `holding cost` `storage cost` `capital tied up` `working capital` | Cost of carrying stock | The money spent on storing and financing inventory. | Stops teams from treating inventory as free. | Carrying rate, warehousing cost, insurance, capital cost. | Finance, warehouse ops, inventory reviews. |
| `order quantity` `cycle stock` `average inventory` `trade-off` | Replenishment size | How much to buy each time you reorder. | Balances buying too often versus holding too much. | Order size, average inventory, cost per order, inventory turns. | Purchasing, category management, planning. |
| `stockout cost` `availability` `days of supply` `backorder` | Service risk and impact | The operational or customer damage when inventory runs out. | Forces the team to value availability, not just low cost. | Lost sales, delayed jobs, downtime, fill rate, days of supply. | Service ops, retail, field support, production planning. |
| `continuous review` `review cycle` `supplier reliability` `demand volatility` | Review discipline | How often the inventory state is checked and how stable the supplier and demand are. | Makes the control policy workable in real operations. | Review frequency, lead-time variance, demand variance, on-time delivery. | ERP planning, vendor management, operations dashboards. |

## 3. Frameworks & Matrices

### Reorder Control Loop
**Purpose:** Show how demand, lead time, and inventory position connect to a reorder decision.

**Text Diagram:**
```text
Demand -> inventory position -> reorder point -> order -> lead time -> receipt
```
Axes / Quadrants / Components explained:
Demand: how fast stock is consumed.
Inventory position: on-hand plus on-order minus backorders.
Reorder point: the trigger that protects against lead-time depletion.
Lead time: the delay between order and receipt.
Receipt: inventory arriving after the delay.
IT/AI/Product/Consulting worked example: A product team keeps laptop docking-station spares for remote employees. When inventory position falls to the reorder point, the team places an order before the next support wave hits. [verified from model knowledge, not source]
When to pull this out in a meeting: When people are arguing about whether to reorder now or wait for the next weekly review.

### Cost-to-Service Curve
**Purpose:** Show the trade-off between holding more stock and risking a stockout.

**Text Diagram:**
```text
Low stock -> low holding cost / high stockout risk
Balanced -> acceptable service / acceptable cost
High stock -> high holding cost / low stockout risk
```
Axes / Quadrants / Components explained:
Holding cost: money tied up in inventory.
Stockout risk: probability of running out before replenishment arrives.
Service level: how often demand is satisfied without a shortage.
Working capital: cash unavailable for other uses.
IT/AI/Product/Consulting worked example: A data-center team holding spare SSDs has cheap carrying cost compared with the cost of server downtime, so the curve justifies a higher buffer. [verified from model knowledge, not source]
When to pull this out in a meeting: When finance wants lower inventory but operations needs higher availability.

### Buffer Allocation Matrix
**Purpose:** Decide which items deserve more safety stock than others.

**Text Diagram:**
```text
                High demand uncertainty
                 ^              ^
                 |              |
High criticality |  heavy buffer |  heavy buffer + monitoring
                 |              |
-----------------+--------------+-----------------> Low criticality
                 |              |
Low criticality  |  lean buffer  |  lean buffer
                 |              |
                 +--------------> High supplier reliability
```
Axes / Quadrants / Components explained:
Criticality: how painful a stockout would be.
Demand uncertainty: how variable demand is.
Supplier reliability: how likely the vendor is to hit the promised date.
Safety stock: the buffer added when the risk is high.
IT/AI/Product/Consulting worked example: A consulting office can carry low buffers for printer paper, but a hospital or field engineering team should hold a larger buffer for mission-critical items. [verified from model knowledge, not source]
When to pull this out in a meeting: When multiple SKUs compete for the same cash budget.

### Reorder Policy Ladder
**Purpose:** Escalate from monitoring to expediting when inventory trouble worsens.

**Text Diagram:**
```text
Monitor -> signal -> reorder -> expedite -> root-cause review
```
Axes / Quadrants / Components explained:
Monitor: track days of supply and expected depletion.
Signal: detect when inventory is approaching the trigger.
Reorder: place the normal replenishment order.
Expedite: use premium freight or alternate supply if lead time slips.
Root-cause review: investigate forecast error, supplier miss, or abnormal demand.
IT/AI/Product/Consulting worked example: A managed IT provider keeps spare routers in regional hubs. When an outage consumes the buffer faster than expected, the team expedites the next replenishment and then reviews whether the forecast or supplier promise was wrong. [verified from model knowledge, not source]
When to pull this out in a meeting: When a shortage is no longer theoretical and service levels are already slipping.

## 4. Formulas

The source gives the decision logic but not the math, so the formulas below are the standard control rules that make reorder-point planning operational. [verified from model knowledge, not source]

### Formula 1: Reorder Point
Formula: `ROP = demand during lead time + safety stock`
Variables:
`demand during lead time` = expected usage while waiting for replenishment
`safety stock` = buffer for uncertainty
Why this formula exists: It answers when to reorder so the stock does not hit zero before the next delivery arrives.
How to interpret the output:
Value below current inventory position -> reorder now
Value roughly equal to current inventory position -> monitor closely
Value far above current inventory position -> no action yet
Worked example with numbers: If demand during a 10-day lead time is 1,000 units and safety stock is 200 units, ROP = 1,200. Decision: reorder once inventory position reaches 1,200.

### Formula 2: Safety Stock
Formula: `safety stock = z × σ_LT`
Variables:
`z` = service factor for the desired service level
`σ_LT` = standard deviation of demand during lead time
Why this formula exists: It converts service-level ambition into an actual buffer.
How to interpret the output:
Low value -> lean inventory, higher shortage risk
Moderate value -> balanced cost and service
High value -> stronger protection, higher holding cost
Worked example with numbers: If the team wants about a 95% service level (`z = 1.65`) and lead-time demand standard deviation is 120 units, safety stock = 198 units. Decision: hold roughly 200 units of buffer for that SKU.

### Formula 3: Inventory Position
Formula: `inventory position = on_hand + on_order - backorders`
Variables:
`on_hand` = physical units available now
`on_order` = units already ordered but not yet received
`backorders` = demand already promised but not yet filled
Why this formula exists: It answers whether the true stock state is already below the reorder trigger.
How to interpret the output:
Value above ROP -> keep monitoring
Value near ROP -> prepare the next order
Value below ROP -> reorder or expedite
Worked example with numbers: If on hand = 700, on order = 400, and backorders = 0, inventory position = 1,100. Decision: if the ROP is 1,200, the team should order now.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Reorder only after the shelf is already empty. | Use the reorder point as a trigger before the lead-time gap opens. |
| Treat safety stock as waste with no business value. | Value safety stock against the cost of a stockout or downtime. |
| Focus only on unit price and ignore holding cost. | Compare purchase cost, storage cost, and capital tied up. |
| Use the same buffer for every item. | Allocate more buffer to critical or uncertain items. |
| Ignore backorders when calculating true inventory state. | Track inventory position, not just physical stock. |

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Grocery Replenishment for Staples
Situation: A grocery chain sells rice continuously and wants to stop running out during a busy promotion week. The item is cheap, but the customer cost of empty shelves is high because shoppers switch to a competitor. [verified from model knowledge, not source]
Applicable framework/metric: Reorder Control Loop + Reorder Point.
Analysis: Average demand during lead time is 1,000 bags and safety stock is 200 bags, so ROP is 1,200. The current inventory position is 1,150, which means the reorder trigger has already been reached.
Decision rule: If inventory position falls below ROP, reorder immediately; if it stays above ROP, keep monitoring; if the supplier is late, expedite.
Action: Place the replenishment order today, add a short-term promotion forecast adjustment, and track daily depletion until the delivery arrives.

### Scenario 2: IT Hardware Spares for Remote Employees
Situation: A product company supports remote staff with docking stations, chargers, and replacement headsets. The items do not cost much to hold, but a shortage causes lost productivity and helpdesk churn. [verified from model knowledge, not source]
Applicable framework/metric: Cost-to-Service Curve + Safety Stock.
Analysis: Demand uncertainty is moderate and lead-time demand standard deviation is 120 units. At a 95% service level, safety stock is about 198 units, which is far cheaper than repeated expediting and downtime.
Decision rule: If stockout cost is much larger than holding cost, raise the buffer; if holding cost dominates and service impact is low, reduce the buffer.
Action: Increase safety stock for high-impact spares, keep leaner buffers for low-impact accessories, and review the policy monthly.

### Scenario 3: Multi-Site Field Operations
Situation: A consulting firm runs field kits across several offices and only some items are mission critical. The team has limited working capital and wants to avoid locking cash into low-value stock. [verified from model knowledge, not source]
Applicable framework/metric: Buffer Allocation Matrix + Inventory Position.
Analysis: Critical items with high demand uncertainty get heavier buffers, while low-criticality items like printer paper stay lean. One office shows on-hand 450, on-order 300, and backorders 100, so inventory position is 650 and may already be below the reorder point.
Decision rule: If criticality and uncertainty are both high, keep a larger buffer; if supplier reliability is strong and usage is stable, reduce safety stock; if inventory position drops below the trigger, reorder before the next site visit.
Action: Rank the SKUs by criticality, assign buffer tiers, and review the top 20 items every week.

## 7. Implementation Playbook

1. Define the SKU list and separate critical items from non-critical items.
2. Estimate demand during lead time from history, promotions, and obvious seasonality.
3. Set a service level for each item based on the cost of a stockout.
4. Compute reorder point, safety stock, and inventory position for the live dashboard.
5. Review supplier reliability and lead-time variance before locking the policy.
6. Pilot the policy on a small set of items and compare actual stockouts against the target.
7. Revisit the buffer monthly and tighten or relax it when demand or supplier behavior changes.

## 8. Content Quality Audit

**Covered well:** The source gives the core intuition correctly: reorder points, safety stock, and holding cost are the three levers that keep long-horizon inventory under control. It is simple enough to teach the idea quickly and to connect the policy to everyday store or warehouse decisions.

**Underplayed or missing:** The chapter does not explain how to compute the reorder point, how to size safety stock, how service level maps to stockout risk, or how to treat inventory position versus on-hand stock. It also omits lead-time variability, supplier reliability, and item criticality, which are usually the real drivers of the policy.

**Supplement with:** Silver, Pyke, and Peterson, *Inventory Management and Production Planning and Scheduling* [verified from model knowledge, not source]; Zipkin, *Foundations of Inventory Management* [verified from model knowledge, not source]; Axsäter, *Inventory Control* [verified from model knowledge, not source]; Simchi-Levi, Kaminsky, and Simchi-Levi, *Designing and Managing the Supply Chain* [verified from model knowledge, not source]; Fisher, Hammond, Obermeyer, and Raman, 1994, HBR, *Making Supply Meet Demand in an Uncertain World* [verified from model knowledge, not source]; and HBS case material on Zara and fast-replenishment retail models [verified from model knowledge, not source].

**Red flags in the source:** It is intentionally introductory, so it can make inventory control sound like a simple reorder-point rule. In practice, the harder problem is estimating demand under uncertainty, choosing the right service level, and keeping the policy updated when lead times or demand patterns change.

## 9. Quick-Recall Card
```text
Topic: Inventory Management Over a Longer Horizon
Core idea: Reorder before lead time runs out, and use safety stock to absorb demand and supply uncertainty.
Key metric/formula: ROP = demand during lead time + safety stock; inventory position = on_hand + on_order - backorders.
Framework trigger: Use it when stock needs to stay available without tying up too much cash.
Watch out for: treating on-hand inventory as the whole picture and ignoring lead-time variance.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: How much buffer do we need to protect service without wasting working capital?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:4, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:5, 10:5] Sections rewritten: [2, 3, 4, 6, 8] Enrichments applied: [source-term expansion; IT/AI/Product/Consulting lens throughout; reorder-point formulas explicitly labeled [verified from model knowledge, not source]; 3 metric-driven scenarios; service-level and working-capital framing; supplemental reading and case framing] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:39 Audited by: A2 -->
