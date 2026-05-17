# EOQ Model (Economic Order Quantity)

## Overview

EOQ is a method to find the best order size that keeps total inventory cost low—by balancing ordering cost and holding cost.

---

## Why It Matters

Ordering too often increases ordering cost; ordering too much increases holding cost. EOQ gives a practical “sweet spot.”

## Key Principles

- Demand is assumed steady (in basic EOQ)
- Lead time is known (in basic EOQ)
- Ordering cost and holding cost are key drivers
- Goal: minimize total cost

## Key Terms

| Term | Definition |
|------|------------|
| **EOQ** | Best quantity to order each time |
| **Annual demand (D)** | Units needed per year |
| **Ordering cost (S)** | Cost per order |
| **Holding cost (H)** | Cost to hold one unit for a year |

## Use Case

A stationery shop decides how many notebooks to order per delivery to reduce storage and delivery expenses.

## Scenario

> A café orders coffee beans. If it orders tiny quantities daily, delivery cost rises. If it orders huge quantities monthly, beans lose freshness. EOQ helps choose a balanced order size.

## Examples

- A bookstore uses EOQ for popular exam guides with steady demand.
- A factory uses EOQ for nuts/bolts used regularly in assembly.

---

## Audited Appendix

# EOQ Model (Economic Order Quantity)
**Course:** Operations Management  
**Module:** Operations Management  
**Audited on:** 2026-04-18  
**Audited by:** A3  
**Source files reviewed:** operations-management/content/16-eoq-model.md

---

## 1. Topic Snapshot
EOQ is the order quantity that minimizes the tradeoff between ordering cost and holding cost.  
For an IT/AI/Product/Consulting leader, this is the decision lens for how much to buy, when to buy it, and whether current demand is stable enough for a deterministic inventory policy.  
The question it answers is: what order size keeps total inventory cost near the sweet spot without starving the business?

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| EOQ | Economic Order Quantity | The best quantity to order each time. | To minimize total inventory cost. | Units per order. | Inventory planning, procurement, operations reviews. |
| Annual demand (D) | Annual Demand | Units needed per year. | To size the annual replenishment pattern. | Units/year. | Forecasting, supply planning, SKU reviews. |
| Ordering cost (S) | Ordering Cost | Cost incurred every time an order is placed. | To capture admin, transport, and setup overhead. | Cost per order. | Purchasing, supplier management, replenishment. |
| Holding cost (H) | Holding Cost | Cost of carrying one unit for a year. | To price storage, capital, obsolescence, and damage. | Cost/unit/year. | Warehouse finance, inventory control, working capital. |
| Lead time | N/A | Time between order placement and receipt. | To know when inventory will arrive. | Days, weeks, or months. | Reorder planning, supplier SLAs, operations. |
| Steady demand | N/A | Demand that does not swing wildly in the basic EOQ model. | To make the model solvable with one stable number. | Demand variance, forecast error. | Basic inventory theory, classroom examples. |
| Total cost | N/A | Sum of ordering and holding cost in the basic model. | To identify the cost-minimizing order size. | Annual cost. | Business cases, working-capital discussions. |

## 3. Frameworks & Matrices

### EOQ Tradeoff Curve
**Purpose:** Show why total cost falls at first and then rises as order size grows.

**Text Diagram:**
```text
Cost
 ^            holding cost
 |              /
 |             /
 |     total  /\
 |    cost   /  \   <- EOQ at the bottom
 |          /    \
 |         /      \ ordering cost
 +----------------------------------> Order quantity
                Q*
```

Axes / Quadrants / Components explained:
Ordering cost: falls as order quantity increases because fewer orders are placed.
Holding cost: rises as order quantity increases because more inventory sits in stock.
Total cost: the sum of the two in the basic model.
EOQ point: the order size where the two forces are in balance. [verified from model knowledge, not source]

IT/AI/Product/Consulting worked example: A procurement manager sets a replenishment policy for exam notebooks. If the team orders too often, admin and freight waste money; if it orders too much, cash gets stuck in inventory. EOQ picks the middle ground. [verified from model knowledge, not source]

When to pull this out in a meeting: When procurement and finance disagree about whether to buy more now or more often.

### Demand-Sensitivity Matrix
**Purpose:** Show how EOQ reacts when the demand or cost structure changes.

**Text Diagram:**
```text
                 Ordering cost S
               low           high
Demand D  low | small Q*   | medium Q*
          high | medium Q*  | large Q*

Holding cost H pushes Q* down as H rises.
```

Axes / Quadrants / Components explained:
Demand (D): annual volume the item must support.
Ordering cost (S): cost per replenishment event.
Holding cost (H): annual carrying cost per unit.
Decision effect: higher D or S pushes EOQ up; higher H pushes EOQ down. [verified from model knowledge, not source]

IT/AI/Product/Consulting worked example: A SaaS hardware bundle has stable demand but rising warehouse costs. The matrix says do not blindly increase the order size; higher H pulls EOQ down, so the team should order less often but more accurately. [verified from model knowledge, not source]

When to pull this out in a meeting: When one input changes and the team needs to know whether to reorder more, less, or the same.

## 4. Formulas
The source gives the intuition, but not the math. The formulas below are standard EOQ math used to turn that intuition into a decision rule. [verified from model knowledge, not source]

Formula: `EOQ = sqrt((2DS) / H)`
Variables:
D = annual demand.
S = ordering cost per order.
H = annual holding cost per unit.
Why this formula exists: It answers, "What order size minimizes the sum of ordering and holding cost?"
How to interpret the output:
Value below EOQ -> ordering too often -> consolidate orders.
Value at EOQ -> cost-minimizing sweet spot -> hold the policy.
Value above EOQ -> inventory too high -> reduce order size and release cash.
Worked example with numbers: If D = 24,000 units, S = 120 per order, and H = 2 per unit-year, then EOQ = sqrt((2 x 24,000 x 120) / 2) = sqrt(2,880,000) = 1,697 units, approximately. [verified from model knowledge, not source]

Formula: `Annual ordering cost = (D / Q) x S`
Variables:
Q = order quantity.
D = annual demand.
S = ordering cost per order.
Why this formula exists: It answers, "What does the ordering pattern cost per year?"
How to interpret the output:
Value high -> too many small orders.
Value low -> fewer, larger orders.
Value matching holding cost at EOQ -> the model is balanced. [verified from model knowledge, not source]
Worked example with numbers: At Q = 1,697, ordering cost is (24,000 / 1,697) x 120 = about 1,698 per year. [verified from model knowledge, not source]

Formula: `Annual holding cost = (Q / 2) x H`
Variables:
Q = order quantity.
H = annual holding cost per unit.
Why this formula exists: It answers, "What does the average inventory sitting in stock cost?"
How to interpret the output:
Value high -> too much stock on hand.
Value low -> stock is leaner.
Value matching ordering cost at EOQ -> inventory is near the sweet spot. [verified from model knowledge, not source]
Worked example with numbers: At Q = 1,697 and H = 2, holding cost is (1,697 / 2) x 2 = about 1,697 per year. [verified from model knowledge, not source]

Formula: `Total annual cost = (D / Q) x S + (Q / 2) x H`
Variables:
D = annual demand.
Q = order quantity.
S = ordering cost per order.
H = annual holding cost per unit.
Why this formula exists: It answers, "What is the full inventory carrying and ordering burden?"
How to interpret the output:
Value drops as Q rises at first, then rises as holding cost dominates.
Value minimum -> best order size.
Value far from minimum -> reorder policy needs review. [verified from model knowledge, not source]
Worked example with numbers: At Q = 1,697, total annual cost is about 3,395, split almost evenly between ordering and holding. [verified from model knowledge, not source]

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Order tiny quantities just to keep shelves visually empty. | Use EOQ to balance shipment frequency against carrying cost. |
| Assume the largest order is cheapest because it lowers ordering frequency. | Check holding cost, because cash and storage get more expensive. |
| Use EOQ without checking whether demand is actually stable. | Confirm demand is steady enough for the basic model. |
| Ignore lead time when stockouts matter operationally. | Align EOQ with replenishment timing and reorder planning. |
| Treat one SKU the same as every other SKU. | Separate fast movers, slow movers, and irregular items before applying EOQ. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Stationery shop replenishment
Situation: A stationery shop sells notebooks with predictable annual demand and wants to avoid both delivery churn and storage pileups. The owner, finance lead, and operations consultant need a simple order policy.  
Applicable framework/metric: EOQ tradeoff curve.  
Analysis: With D = 12,000 notebooks, S = 80, and H = 1.5, EOQ = sqrt((2 x 12,000 x 80) / 1.5) = about 1,131 notebooks.  
Decision rule: If the current order size is below EOQ, place fewer larger orders. If it is above EOQ, reduce order size. If demand is unstable, pause and rebuild the forecast first. [verified from model knowledge, not source]  
Action: Set the replenishment rule to roughly 1,100 notebooks per order and review quarterly.

### Scenario 2: Coffee beans in a cafe
Situation: A cafe buys coffee beans too often and delivery fees are creeping up, but larger orders risk freshness loss. This is a classic procurement-vs-quality tension.  
Applicable framework/metric: Total annual cost.  
Analysis: If ordering cost falls with larger Q but holding cost rises because beans age, the cost minimum is the order size that balances both. [verified from model knowledge, not source]  
Decision rule: If freshness risk is operationally critical, cap Q below the mathematical EOQ and treat quality as a hard constraint.  
Action: Split the item into a working stock policy and a freshness policy rather than forcing one number to solve both problems.

### Scenario 3: Factory nuts and bolts
Situation: A factory uses the same nuts and bolts every week in assembly. Procurement wants volume discounts, while operations wants to avoid overstocking slow-moving parts.  
Applicable framework/metric: Demand-sensitivity matrix.  
Analysis: If D is high and H is low, EOQ rises; if H rises because warehouse space is tight, EOQ falls. [verified from model knowledge, not source]  
Decision rule: If the supplier discount does not beat the extra holding cost, do not increase Q just to chase a unit price break.  
Action: Compare the discount savings against holding cost before signing a blanket purchase order.

## 7. Implementation Playbook
1. Pull 12 months of SKU-level demand, ordering cost, and holding cost estimates into one sheet.
2. Verify that the item is stable enough for the basic EOQ assumptions.
3. Calculate EOQ for each important SKU and rank the policy changes by cash impact.
4. Compare current order size with EOQ and flag items that are materially above or below target.
5. Add lead-time and service-level constraints where stockouts matter operationally.
6. Review supplier discounts, because they can override the pure EOQ result.
7. Publish the new replenishment rule in the procurement SOP or ERP master data.
8. Recompute EOQ whenever demand, freight, or storage cost changes materially.

## 8. Content Quality Audit
Covered well: The source explains the basic tradeoff clearly and gives a usable intuition for a balanced order size.  
Underplayed or missing: It omits the formula, the assumptions behind deterministic demand, the effect of lead time, and how discounts or service levels can change the answer.  
Supplement with: Silver, Pyke, and Peterson, *Inventory Management and Production Planning and Scheduling* [verified from model knowledge, not source]; Nahmias and Olsen, *Production and Operations Analysis* [verified from model knowledge, not source]; HBR article by Kraljic, 1983, "Purchasing Must Become Supply Management" [verified from model knowledge, not source]; HBS case *Zara: Fast Fashion* [verified from model knowledge, not source]; Harris, 1913, "How Many Parts to Make at Once" [verified from model knowledge, not source].  
Red flags in the source: It presents EOQ as a universal answer, but the model breaks if demand is volatile, stockouts are expensive, or supplier discounts dominate the cost structure.

## 9. Quick-Recall Card
```text
Topic: EOQ Model (Economic Order Quantity)
Core idea: Order enough to balance ordering cost and holding cost.
Key metric/formula: EOQ = sqrt((2DS) / H); total cost = (D / Q)S + (Q / 2)H.
Framework trigger: Use it when demand is steady and you need a base replenishment quantity.
Watch out for: Using EOQ before checking demand stability, lead time, and discount breaks.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What order size minimizes cost without harming service or freshness?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:4, 7:4, 8:4, 9:5, 10:4] Sections rewritten: [2, 3, 4, 6, 8] Enrichments applied: [added EOQ and total-cost formulas, tradeoff curve, sensitivity matrix, scenario math, sourcing caveats, procurement/finance decision lens] Final scores: all 5/5 Pass 2 completed: 2026-04-18 19:48 Audited by: A3 -->
