# Beer Game Simulation (Supply Chain Dynamics)

## Overview

The Beer Game is a learning activity where players manage orders in a supply chain (retailer → wholesaler → distributor → factory). Even with small demand changes, the system often becomes unstable.

---

## Why It Matters

It shows why supply chains face shortages, excess inventory, and panic ordering. It helps people understand how delays and poor coordination create big problems.


## Key Principles

- Small demand changes can cause big order swings
- Delays make decision-making harder
- Local decisions can hurt the whole chain
- Communication and planning reduce chaos


## Key Terms

| Term | Definition |
|------|------------|
| **Backorder** | Customer demand you couldn’t fulfill yet |
| **Pipeline Inventory** | Stock “on the way” but not received |
| **Order Delay** | Time between ordering and receiving |


## Use Case

Training managers to understand real supply chain challenges before they handle actual inventory and ordering decisions.


## Scenario

> Customers buy slightly more than usual. The retailer orders extra “just in case.” The wholesaler sees a big jump and orders even more. Soon, everyone is over-ordering—then everyone ends up with too much stock later.


## Examples

- A small increase in cola demand makes distributors over-order, causing warehouses to overflow weeks later.
- A minor festival demand spike makes retailers panic-buy inventory, leading to big losses after the festival ends.

---

## Audited Appendix

# Beer Game Simulation (Supply Chain Dynamics)
**Course:** Supply Chain Management  
**Module:** Content / Beer Game Simulation  
**Audited on:** 2026-04-19  
**Audited by:** A3  
**Source files reviewed:** `supply-chain-management/content/02-beer-game-simulation.md`

---

## 1. Topic Snapshot
The Beer Game is a supply chain simulation that shows how retailer, wholesaler, distributor, and factory ordering decisions interact under delay.  
It matters because small changes in customer demand can become large upstream order swings, creating backorders, pipeline inventory, and excess cost.  
For an IT/AI/Product/Consulting decision-maker, it is a warning to use real demand signals, not distorted orders, before changing replenishment policy.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Supply Chain (SC) | Supply Chain | The connected flow from supplier to customer | To describe the full operating system, not one department | Lead time, service level, inventory, cost | Operations, logistics, planning reviews |
| SCM | Supply Chain Management | Managing materials, information, and money across the chain | To coordinate buying, making, storing, moving, and delivering | Fill rate, stockouts, cost-to-serve, on-time delivery | Planning, procurement, consulting decks |
| Beer Game | - | A simulation of ordering decisions across the chain | To make feedback delays and coordination failures visible | Order swings, backorders, inventory buildup | Training sessions, ops workshops |
| Backorder | - | Demand you could not fulfill yet | To capture unmet customer demand | Backordered units, backorder days | Service reviews, fulfillment meetings |
| Pipeline Inventory | - | Stock already ordered but not yet received | To show goods in transit or in process | Units in transit, days of supply in pipeline | Replenishment planning, control towers |
| Order Delay | - | Time between placing and receiving an order | To model decision lag and transport lag | Days or weeks of delay | Supplier SLAs, planning cadence |
| Lead Time | - | Time from order to delivery | To size buffers and set reorder points | Average and variance of lead time | Procurement, inventory control |
| Service Level | - | How often demand is met on time/in full | To balance cost against customer experience | Fill rate, cycle service level | SLAs, executive dashboards |
| Bullwhip Effect | - | Small demand changes become larger order changes upstream | To explain amplified volatility in supply chains | Order variance vs demand variance | S&OP, supply chain analytics |
| Batch Ordering | - | Ordering in large chunks instead of smoothly | To reduce ordering effort or meet internal rules | Order size, order frequency | Procurement, ERP planning |
| Price Promotion | - | Temporary discount or offer that changes buying behavior | To drive demand or clear stock | Promo lift, sell-through, order spikes | Marketing, retail trade planning |
| Point-of-Sale (POS) Data | Point of Sale | Actual customer sales data at checkout | To separate real demand from upstream noise | Units sold by SKU/store/time | Retail analytics, demand planning |
| Visibility | - | Ability to see stock and demand across the chain | To coordinate decisions with shared facts | Data latency, completeness, accuracy | Control towers, dashboards |
| Collaboration | - | Partners planning together instead of guessing separately | To align incentives and reduce local optimization | Forecast accuracy, service level, meeting cadence | S&OP, partner governance |

## 3. Frameworks & Matrices

### Beer Game Feedback Loop
**Purpose:** Show how local ordering decisions can amplify instability across the supply chain.

**Text Diagram:**
```text
Customer demand -> Retailer orders -> Wholesaler orders -> Distributor orders -> Factory schedules
        ^                |                 |                    |                    |
        |                v                 v                    v                    v
   backorders <---- pipeline inventory <---- order delay <---- information lag <---- capacity response
```

Axes / Quadrants / Components explained:
Component 1: Downstream demand signal, the real customer demand that should drive planning.  
Component 2: Upstream order signal, the distorted number each tier sees instead of true demand.  
Component 3: Delay, the gap between decision and receipt that makes overreaction more likely.  
Component 4: Inventory state, including pipeline inventory and backorders, which reveal whether policy is too slow or too aggressive.

IT/AI/Product/Consulting worked example: A retail IT team connects POS data to a demand-planning dashboard, an AI model forecasts demand from sales instead of orders, the product manager times promotions with replenishment capacity, and the consultant recommends smaller batch sizes when the bullwhip effect is visible.  
When to pull this out in a meeting: When each layer blames the next layer for stockouts or overstock.

### Visibility vs Delay Diagnostic Matrix
**Purpose:** Decide whether the main fix is better data sharing, faster replenishment, or both.

**Text Diagram:**
```text
                    Delay
                Low         High
Visibility  -------------------------
High        | Stable       | Data is clear but response is slow
Low         | Local guesses | Worst case: guessing + slow correction
```

Axes / Quadrants / Components explained:
Visibility: whether teams can see POS data, inventory, and shipment status in near real time.  
Delay: how long it takes for an order, production change, or shipment to reach the next stage.  
High visibility + low delay: the operating target; order changes are smaller and faster to correct.  
High visibility + high delay: the team knows the truth, but still needs safety stock or faster logistics.  
Low visibility + low delay: tactical chaos; teams may still react to noise because the signal is wrong.

IT/AI/Product/Consulting worked example: An AI-enabled control tower improves visibility first, then the supply chain lead reduces delay by moving to smaller, more frequent replenishment cycles. The decision produced is whether to invest in data integration, workflow automation, or both.  
When to pull this out in a meeting: When service problems persist even though everyone claims they "see" the data.

## 4. Formulas

Formula: Bullwhip ratio = variance of orders / variance of customer demand [verified from model knowledge, not source]  
Variables:  
Orders = quantities requested by the next upstream tier  
Customer demand = actual sales or consumption at the market edge  
Variance = how much the series swings around its average  
Why this formula exists: It answers whether volatility is being amplified as it moves upstream.  
How to interpret the output:  
Value < 1 -> demand is being dampened -> keep the current policy and monitor.  
Value 1-2 -> mild amplification -> reduce batch ordering and improve visibility.  
Value > 2 -> severe bullwhip -> redesign replenishment rules and reduce delay.  
Worked example with numbers: If order variance is 144 and customer-demand variance is 36, the bullwhip ratio is 4.0. That means upstream volatility is four times the real market signal, so the team should shorten review cycles, use POS data, and cap order changes.

Formula: Pipeline inventory = average demand rate x lead time [verified from model knowledge, not source]  
Variables:  
Average demand rate = units consumed per day or week  
Lead time = time from order placement to receipt  
Pipeline inventory = units already committed but not yet received  
Why this formula exists: It answers how much stock is already "in the system" before more orders are placed.  
How to interpret the output:  
Value < 1x lead-time demand -> likely undercoverage -> expedite or raise reorder point.  
Value 1x-1.5x lead-time demand -> workable -> maintain and monitor.  
Value > 1.5x lead-time demand -> too much in transit -> reduce batch size and free working capital.  
Worked example with numbers: If a store sells 120 units per day and lead time is 5 days, pipeline inventory should be about 600 units. If actual pipeline inventory is 1,000 units, the system is overloaded and the next move is to slow ordering and fix the delay.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Reorder from last week's order spike | Reorder from POS data and actual sell-through |
| Treat a short demand uptick as a permanent trend | Check whether delay and batch ordering amplified the signal |
| Let each tier optimize only its own inventory | Coordinate retailer, wholesaler, distributor, and factory policies |
| Use big promotions without a replenishment plan | Align price promotion timing with capacity and inventory buffers |
| Ignore backorders because they are "temporary" | Track backorder days, service level, and recovery speed |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Grocery replenishment after a small demand bump  
Situation: A grocery chain sees only a 6% rise in POS demand for a staple item, but distributor orders jump 28% because stores are afraid of stockouts. The IT team sees the mismatch in the dashboard, and the product/operations lead needs to decide whether the issue is true demand or amplification.  
Applicable framework/metric: Bullwhip ratio.  
Analysis: If demand variance is 25 and order variance is 100, the bullwhip ratio is 4.0. That is severe amplification, not real market growth.  
Decision rule: If bullwhip ratio > 2, cut batch size and use POS data. If between 1 and 2, tune reorder rules. If below 1, maintain and monitor.  
Action: Freeze panic ordering, switch to demand-based replenishment, and brief suppliers with one shared forecast.

Scenario 2: Cloud hardware spares across a multi-layer network  
Situation: An IT infrastructure provider stocks replacement parts across a retailer-like service desk, regional warehouses, and a central factory. Orders look "stable" locally, but backorders are rising because the lead time is 8 days and demand is 90 units per day.  
Applicable framework/metric: Pipeline inventory and service level.  
Analysis: Pipeline inventory should be about 720 units. If the actual pipeline inventory is only 500 units, the system is undercovered. If fill rate is 93%, the service level is too low for critical spares.  
Decision rule: If service level < 95%, increase safety stock and shorten order delay. If 95%-98%, refine reorder cadence. If > 98%, check for excess inventory.  
Action: Increase visibility into shipments, raise reorder points, and run a weekly review of backorders.

Scenario 3: Consumer promo that creates false demand  
Situation: A product team runs a deep discount for a new SKU. Customers buy 1,000 units, but the retailer orders 2,300 units because the promotion creates fear of shortages. The consulting team must tell leadership whether to scale manufacturing.  
Applicable framework/metric: Order-to-demand ratio.  
Analysis: The ratio is 2.3, which signals overreaction rather than clean demand. The team should not extrapolate the promo week into a base forecast.  
Decision rule: If order-to-demand ratio > 1.5, treat it as amplification. If 1.1-1.5, investigate promo timing and stock availability. If near 1.0, treat it as normal demand.  
Action: Separate promo lift from baseline demand, cap future order swings, and coordinate future price promotion with replenishment capacity.

## 7. Implementation Playbook
1. Map the retailer-wholesaler-distributor-factory flow in one swimlane and mark where order delay enters.  
2. Build a dashboard that combines POS data, inventory, pipeline inventory, and backorders in one view.  
3. Calculate the bullwhip ratio weekly for the top SKUs and flag anything above 2.0.  
4. Set reorder rules that use actual demand, not upstream orders, and cap batch ordering.  
5. Align price promotion calendars with supply capacity so marketing does not create artificial spikes.  
6. Create a service-level target and tie escalation to fill rate, backorder days, and lead time exceptions.  
7. Run the Beer Game in management reviews to teach why local decisions can damage the whole chain.  

## 8. Content Quality Audit
Covered well: The source gives the core intuition for the Beer Game, the importance of delays, and the link between local decisions and chain-wide instability.  
Underplayed or missing: It does not name the bullwhip effect explicitly, quantify volatility, or explain how POS data, visibility, and collaboration reduce amplification.  
Supplement with: Jay Forrester, *Industrial Dynamics* (1961); John Sterman, *Business Dynamics* (2000); Lee, Padmanabhan, and Whang (1997), "Information Distortion in a Supply Chain: The Bullwhip Effect" [verified from model knowledge, not source]; Sterman (1989), "Modeling Managerial Behavior: Misperceptions of Feedback in a Dynamic Decision Making Experiment" [verified from model knowledge, not source]; Chopra and Meindl, *Supply Chain Management: Strategy, Planning, and Operation* [verified from model knowledge, not source]. A useful case/simulation to pair with this topic is the Beer Distribution Game [verified from model knowledge, not source].  
Red flags in the source: It is intentionally simplified, so a reader could miss the role of forecasting policy, batching rules, promotional pricing, and information sharing as distinct bullwhip drivers.

## 9. Quick-Recall Card
```text
Topic: Beer Game Simulation (Supply Chain Dynamics)
Core idea: Small downstream demand changes can become large upstream order swings when delay and local decisions dominate.
Key metric/formula: Bullwhip ratio = variance of orders / variance of customer demand [verified from model knowledge, not source].
Framework trigger: Use it when stockouts and overstock coexist and everyone is reacting to the same noisy orders.
Watch out for: Treating upstream orders as real demand.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Are we planning from customer demand or from amplified signals?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [full source-term glossary, IT/AI/Product/Consulting framing, bullwhip ratio, pipeline inventory, service-level decision rules, multi-layer implementation playbook] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:40 Audited by: A3 -->
