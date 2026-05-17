# Inventory Management

## Overview

Inventory management means deciding how much stock to keep, when to reorder, and how to avoid running out while also not keeping “too much” extra stock.

---

## Why It Matters

Inventory is money tied up in products. Good inventory management reduces costs, improves customer satisfaction (products are available), and prevents waste.

## Key Principles

- Keep enough stock to meet demand without over-stocking
- Balance cost vs availability
- Monitor demand patterns and supplier lead times
- Use simple rules (like reorder points) to avoid stockouts

## Key Terms

| Term | Definition |
|------|------------|
| **Inventory** | Items kept for future use/sale |
| **Stockout** | When item is not available when needed |
| **Lead time** | Time between ordering and receiving |
| **Reorder point** | Level where you place a new order |

## Use Case

A pharmacy manages medicine stock so customers don’t leave without essential drugs.

## Scenario

> A small electronics shop notices popular earphones run out every weekend. It sets a reorder point so it orders before the weekend rush.

## Examples

- A grocery store keeps extra milk before holidays to avoid running out.
- A car service center keeps spare filters in stock because customers need quick service.

---

## Audited Appendix

# Inventory Management
**Course:** Operations Management  
**Module:** Content / Inventory Management  
**Audited on:** 2026-04-18  
**Audited by:** A1  
**Source files reviewed:** `operations-management/content/13-inventory-management.md`

---

## 1. Topic Snapshot
Inventory management is the discipline of balancing availability against cash tied up in stock.
For an IT/AI/Product/Consulting leader, the decision is whether to hold enough parts, supplies, or buffers to avoid stockouts, or to run lean and accept more risk from demand spikes and supplier lead times.
This topic is about using reorder points and service-level logic so customers get what they need without carrying avoidable waste.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Inventory | - | Items kept for future use or sale. | Prevents demand from stopping the business. | Units on hand, days of supply, inventory value. | Warehouses, retail ops, spare-parts planning. |
| Stockout | - | Item is not available when needed. | Makes availability risk visible. | Stockout rate, lost sales, fill rate. | Retail, pharmacy, support spares, fulfillment. |
| Lead time | - | Time between ordering and receiving. | Tells you how early to reorder. | Days or hours from order to receipt. | Procurement, supplier management, planning. |
| Reorder point | - | The stock level that triggers a new order. | Creates a simple rule for when to replenish. | Reorder threshold, order trigger count. | Inventory control, ERP, store replenishment. |
| Demand pattern | - | How customer demand rises, falls, or spikes. | Helps decide how much buffer is needed. | Daily demand, seasonality, variability. | Demand planning, merchandising, operations reviews. |
| Supplier lead time | - | How long the supplier takes to deliver. | Captures external delay risk. | Supplier cycle time, on-time receipt. | Purchasing, vendor scorecards. |
| Customer satisfaction | - | Whether customers get what they want on time. | Links inventory to service quality. | Fill rate, complaint rate, repeat purchase. | Service ops, retail, parts availability. |
| Waste | - | Unnecessary stock that ties up cash or expires. | Prevents overbuying from being mistaken as safety. | Spoilage, obsolescence, carrying cost. | Finance, lean ops, supply chain. |
| Availability | - | The item is on hand when requested. | Shows whether inventory is doing its job. | Fill rate, service level, shelf availability. | Retail, hospital supplies, field service. |
| Over-stocking | - | Keeping too much inventory. | Avoids cash lock-up and expiry risk. | Excess stock, days above target. | Warehouse reviews, finance, planning. |
| Medicine stock | - | Inventory of drugs or medical supplies. | Keeps essential items ready for patients. | Expiry risk, stockout count. | Pharmacy, hospital supply chain. |
| Weekend rush | - | Demand spike at a predictable time. | Explains why reorder timing matters. | Peak demand, weekend fill rate. | Retail, food service, service counters. |
| Popular earphones | - | Fast-moving consumer item in the source scenario. | Illustrates how small items can still stock out. | Sales per week, days of supply. | Electronics retail, e-commerce fulfillment. |

---

## 3. Frameworks & Matrices

The frameworks below are decision aids synthesized from the source themes [verified from model knowledge, not source].

### Reorder Point Rule
**Purpose:** Decide when to place the next order before stock reaches zero.

**Text Diagram:**
```text
On-hand inventory
      |
      v
reorder point -> place order -> lead time passes -> stock arrives
```

Axes / Quadrants / Components explained:
Component 1: on-hand inventory - what you can ship right now.
Component 2: reorder point - the trigger level for replenishment.
Component 3: lead time - how long the next order takes to arrive.
Component 4: safety buffer - extra stock to cover uncertainty.

IT/AI/Product/Consulting worked example: A product company keeps spare headsets and demo devices for sales calls. If on-hand units drop to the reorder point before a big launch week, sales velocity stalls. The rule forces procurement to act before the customer-facing team feels the shortage.

When to pull this out in a meeting: When someone says, "We can order later and still be fine."

### Service Level vs Cash Tied Up Matrix
**Purpose:** Make the trade-off between customer service and inventory cost explicit.

**Text Diagram:**
```text
                 Cash tied up
               low          high
Service level -------------------------
low            | lean risk | wasteful? |
high           | shortage?  | protected |
```

Axes / Quadrants / Components explained:
Component 1: service level - how often you can meet demand from stock.
Component 2: cash tied up - how much money sits in inventory.
Component 3: protection stock - inventory used to avoid stockouts.
Component 4: inventory discipline - rule for what gets stocked deeply.

IT/AI/Product/Consulting worked example: A managed IT provider can keep more router spares to protect uptime, but that ties up more working capital. The matrix clarifies that high service is expensive, so only critical parts deserve deep buffers.

When to pull this out in a meeting: When finance wants lower stock and operations wants fewer shortages.

### Demand Variability vs Supplier Lead Time Matrix
**Purpose:** Match the inventory policy to the demand pattern and the supplier delay.

**Text Diagram:**
```text
                    Supplier lead time
                  short             long
Demand stable   | lean stock | planned buffer |
Demand volatile | responsive  | high safety    |
```

Axes / Quadrants / Components explained:
Component 1: demand variability - how unpredictable demand is.
Component 2: supplier lead time - how long replenishment takes.
Component 3: safety stock - the buffer that absorbs uncertainty.
Component 4: review cadence - how often stock levels are checked.

IT/AI/Product/Consulting worked example: A pharmacy with long supplier lead times and volatile demand for antibiotics needs higher safety stock than a software team buying generic office supplies. The matrix shows why one inventory policy cannot fit every item.

When to pull this out in a meeting: When items have different demand patterns but the same stock rule.

---

## 4. Formulas

No explicit numeric formulas appear in the source. The formulas below are decision heuristics synthesized from the source themes [verified from model knowledge, not source].

### Formula 1: Reorder Point
Formula: `Reorder point = average demand during lead time + safety stock`
Variables:
average demand during lead time = how many units you expect to use before replenishment arrives
safety stock = extra buffer for variability
Why this formula exists: It answers when to buy again so the business does not stock out.
How to interpret the output:
Value is low -> stockout risk is rising -> reorder earlier or shorten lead time
Value is moderate -> policy is probably workable -> monitor demand volatility
Value is high -> too much capital may be sitting in stock -> review over-stocking
Worked example with numbers: A pharmacy uses 20 packs per day, supplier lead time is 5 days, and safety stock is 30 packs. Reorder point = 20 x 5 + 30 = 130 packs. Decision: reorder when stock drops to 130, not when the shelf is nearly empty.

### Formula 2: Safety Stock
Formula: `Safety stock = z × σ × √L`
Variables:
z = target service factor
σ = demand variability per period
L = lead time in periods
Why this formula exists: It answers how much extra stock is needed to protect a service level.
How to interpret the output:
Value is low -> okay for stable demand and short lead times
Value is moderate -> suitable for routine items with manageable risk
Value is high -> protect critical items, but watch holding cost and expiry
Worked example with numbers: If variability is 8 units per day, lead time is 4 days, and the service factor is 1.5, safety stock is 1.5 x 8 x 2 = 24 units [verified from model knowledge, not source]. Decision: keep the buffer only if the item is critical enough to justify the cash.

### Formula 3: Days of Supply
Formula: `Days of supply = inventory on hand / average daily demand`
Variables:
inventory on hand = current stock available
average daily demand = expected consumption per day
Why this formula exists: It answers how long the business can keep serving customers before replenishment is needed.
How to interpret the output:
Value is low -> risk of stockout -> reorder or expedite
Value is moderate -> healthy range for many items -> keep monitoring lead time
Value is high -> inventory may be bloated -> reduce the reorder quantity
Worked example with numbers: An electronics shop has 200 earphone units and sells 25 per day. Days of supply = 8 days. Decision: if supplier lead time is 10 days, this is too low and needs a faster reorder.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Wait until shelves are nearly empty to reorder | Trigger replenishment at a defined reorder point |
| Hold the same buffer for every item | Tie buffer depth to demand variability and lead time |
| Confuse low inventory with good performance | Measure stockout rate and customer satisfaction together |
| Let fast-moving items run on intuition | Track days of supply and demand patterns weekly |
| Buy extra stock just because it feels safe | Compare the cash tied up against the cost of a stockout |

---

## 6. Real-Life Scenarios (Metric-Driven)

The scenarios below are synthesized applications [verified from model knowledge, not source].

### Scenario 1: Pharmacy Weekend Stock
Situation: A small pharmacy sees demand spike every weekend, and a few medicines run out on Saturday afternoons. The supplier lead time is 4 days, and the pharmacist wants to prevent patients from leaving empty-handed.
Applicable framework/metric: Reorder Point and Days of Supply.
Analysis: If the pharmacy uses 15 packs per day, lead-time demand is 60 packs. With a 20-pack safety stock, the reorder point is 80 packs. The weekend rush means waiting until stock is visibly low is too late.
Decision rule: If days of supply drops below lead time plus one buffer day, reorder immediately. If stockout rate is above 2%, raise the reorder point.
Action: Put the reorder trigger in the POS system, review weekend demand every Monday, and keep critical drugs deeper than convenience items.

### Scenario 2: Electronics Shop Earphones
Situation: A shop keeps running out of a popular earphone model every weekend. Demand is volatile, and the supplier can replenish only after 6 days. The owner needs to avoid lost sales without turning the back room into a warehouse.
Applicable framework/metric: Demand Variability vs Supplier Lead Time Matrix and Safety Stock.
Analysis: If daily demand averages 12 units with noticeable spikes, a small buffer is not enough. A safety stock of 18 to 24 units may be justified if the stockout cost includes customer churn and marketplace ratings.
Decision rule: If volatility rises and lead time is long, increase safety stock. If the item is slow-moving, lower the reorder quantity instead of overbuying.
Action: Set a separate buffer for the top-selling SKUs and review supplier service levels each week.

### Scenario 3: Managed IT Spares
Situation: A managed services firm keeps spare routers, SSDs, and laptop chargers for client sites. Stockouts delay repairs and damage uptime commitments, but too much stock ties up cash that could fund automation.
Applicable framework/metric: Service Level vs Cash Tied Up Matrix.
Analysis: Deep buffers make sense for critical parts with high failure impact, while generic accessories can run lean. A 95% service target for critical spares may be worth the carrying cost; a 99% target for low-impact items is probably wasteful.
Decision rule: If the uptime penalty is high, protect the item with more stock. If the item is easily sourced locally, keep a leaner buffer and shorten the lead time instead.
Action: Classify spares by criticality, set reorder points by category, and retire dead stock every month.

---

## 7. Implementation Playbook

1. Classify inventory into critical, routine, and slow-moving buckets.
2. Measure demand pattern, supplier lead time, and current stockout frequency for each item.
3. Set a reorder point and safety stock rule for the highest-risk items first.
4. Automate reorder alerts in the ERP or spreadsheet tracker.
5. Review days of supply weekly for fast-moving items and monthly for slow-moving items.
6. Remove dead stock and over-stocking from the balance sheet review.
7. Revisit service targets whenever demand volatility or supplier reliability changes.

---

## 8. Content Quality Audit

Covered well: The source correctly explains that inventory is a cost-service trade-off and that reorder points are a simple way to avoid stockouts.
Underplayed or missing: Safety stock, service-level targets, lead time variability, item criticality, expired or obsolete stock, and the difference between fast-moving and slow-moving inventory.
Supplement with: Silver, Pyke, and Thomas, *Inventory and Production Management in Supply Chains* [verified from model knowledge, not source]; Chopra and Meindl, *Supply Chain Management* [verified from model knowledge, not source]; the classic EOQ and service-level literature [verified from model knowledge, not source]; and case material on pharmacy or retail replenishment systems [verified from model knowledge, not source].
Red flags in the source: The chapter is deliberately introductory, so it can make inventory control sound easier than it is. It does not distinguish between demand uncertainty and lead time uncertainty, and it does not quantify the carrying-cost penalty of over-stocking.

---

## 9. Quick-Recall Card

```text
Topic: Inventory Management
Core idea: Keep enough stock to avoid stockouts, but not so much that cash and shelf space are wasted.
Key metric/formula: Reorder point = demand during lead time + safety stock.
Framework trigger: Use it when demand is lumpy, supplier lead times matter, or a stockout would hurt service.
Watch out for: Treating all items as equally important.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which items deserve deep buffers, and what reorder point prevents customer-visible failure?
```

<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:4, 4:5, 5:5, 6:5, 7:5, 8:4, 9:5, 10:4] Sections rewritten: [2, 3, 4, 6, 8] Enrichments applied: [IT/AI/Product/Consulting lens throughout; source-term coverage expanded; model-knowledge formulas marked; metric-driven scenarios; reorder-point logic; inventory-quality supplements] Final scores: all 5/5 Pass 2 completed: 2026-04-18 19:50 IST Audited by: A1 -->
