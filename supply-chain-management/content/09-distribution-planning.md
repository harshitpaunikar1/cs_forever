# Distribution Planning

## Overview

Distribution planning is deciding how products move from warehouses to customers or stores—how often, how much, and through which routes.

---

## Why It Matters

Distribution impacts delivery speed and cost directly. Poor planning leads to late deliveries, high transport costs, and empty shelves.


## Key Principles

- Choose delivery frequency (daily/weekly)
- Consolidate shipments to reduce cost
- Match distribution method to product needs (fragile, cold, urgent)
- Plan routes and warehouse replenishment together


## Key Terms

| Term | Definition |
|------|------------|
| **Last-Mile Delivery** | Final delivery to customer/store |
| **Consolidation** | Combining orders to ship together |
| **Fulfillment** | Completing an order (pick-pack-ship) |


## Use Case

A beverage company plans weekly deliveries to small shops and daily deliveries to big supermarkets.


## Scenario

> A company sends half-empty trucks daily. Cost becomes very high. By consolidating shipments and delivering on fixed routes, cost drops without hurting service.


## Examples

- Milk distributors use early-morning fixed routes to supply many retailers efficiently.
- E-commerce companies use city hubs to speed up last-mile delivery.

---

## Audited Appendix

# Distribution Planning
**Course:** Supply Chain Management  
**Module:** Content / Distribution Planning  
**Audited on:** 2026-04-19  
**Audited by:** A4  
**Source files reviewed:** `supply-chain-management/content/09-distribution-planning.md`, `supply-chain-management/content/08-multi-echelon-inventory.md`, `supply-chain-management/content/10-network-planning.md`

---

## 1. Topic Snapshot
Distribution planning decides how products move from warehouses to stores or customers: how often, how much, and through which routes.  
For IT/AI/Product/Consulting leaders, it is the operating layer that turns a network design into actual service levels, transport cost, and customer experience.  
The decision it supports is whether to consolidate, route differently, add a hub, or change fulfillment cadence to hit service targets without overspending.

## 2. Jargon & Terminology

Definitions below are synthesized from the source plus standard supply-chain practice [verified from model knowledge, not source].

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Distribution planning | None | Choosing how goods move through the network | Balances service speed and logistics cost | Cost per delivered unit, on-time delivery, route efficiency | S&OP, logistics reviews, operating model design |
| Last-mile delivery | None | Final delivery step to the customer or store | Usually the most expensive and visible part of the journey | Delivery lead time, first-attempt success, cost per drop | E-commerce, grocery, courier operations |
| Consolidation | None | Combining smaller orders into larger shipments | Reduces empty space and transport cost | Truck load factor, shipment frequency, transport cost per unit | Freight planning, warehouse dispatch |
| Fulfillment | None | Pick-pack-ship execution of an order | Converts demand into delivered service | Order cycle time, fill rate, pick accuracy | Warehouse management, e-commerce ops |
| Distribution center (DC) | None | A warehouse designed to store and ship product [verified from model knowledge, not source] | Speeds regional delivery and reduces line-haul distance | Throughput, throughput per square foot, service level | Network planning, fulfillment engineering |
| Network design | None | Overall structure of factories, warehouses, and flows [verified from model knowledge, not source] | Makes the long-term service-cost tradeoff explicit | Total landed cost, delivery time, capacity utilization | Supply-chain strategy, capex planning |
| Capacity | None | How much a facility or vehicle can handle [verified from model knowledge, not source] | Prevents overloaded routes and backlogs | Utilization rate, bottleneck rate, throughput | Operations planning, warehouse design |
| Echelon | None | A level in the supply chain such as factory or store [verified from model knowledge, not source] | Lets teams plan across the whole chain | Inventory by level, service by level | Multi-echelon inventory reviews |
| Risk pooling | None | Combining demand across locations to reduce variability [verified from model knowledge, not source] | Supports central stock and lower safety inventory | Variability reduction, stockout probability | Inventory strategy, DC planning |
| Centralization | None | Keeping stock in fewer locations [verified from model knowledge, not source] | Improves pooling and control | Central stock share, average ship distance | Network and inventory design |

## 3. Frameworks & Matrices

The selection logic below is [verified from model knowledge, not source]; the source gives the basic ideas, and these frameworks turn them into decisions.

### Service-Cost Tradeoff Ladder
**Purpose:** Decide whether you should ship more often, ship larger lots, or redesign the route.

**Text Diagram:**
```text
Customer promise
   -> Delivery frequency
      -> Shipment size
         -> Route design
            -> Fulfillment cost
```

Axes / Quadrants / Components explained:
Customer promise: speed and reliability required by the market.
Delivery frequency: daily, weekly, or fixed-route cadence.
Shipment size: how much is loaded on each trip.
Route design: which stops belong together and in what sequence.
Fulfillment cost: the resulting transport and handling burden.

IT/AI/Product/Consulting worked example: A retail analytics team is deciding whether a regional hub should serve city stores daily and smaller towns weekly. The ladder shows the real question is not "faster or cheaper" but "what service promise justifies which cadence and route structure."

When to pull this out in a meeting: When a team is debating delivery speed without quantifying the cost of that promise.

### Consolidation vs Frequency Matrix
**Purpose:** Show the tradeoff between more frequent deliveries and lower transport cost through larger loads.

**Text Diagram:**
```text
                     DELIVERY FREQUENCY
                 High                           Low
CONSOLIDATION
High        Fast service, higher cost     Balanced service-cost
Low         Small, expensive trips        Cheapest per trip, slower service
```

Axes / Quadrants / Components explained:
High frequency: better service, more trips.
Low frequency: cheaper per trip, slower response.
High consolidation: fuller trucks and lower unit cost.
Low consolidation: more partial loads and higher unit cost.

IT/AI/Product/Consulting worked example: A beverage distributor can deliver daily to supermarkets and weekly to small shops. Supermarkets sit in the high-frequency/high-consolidation quadrant because their volume fills trucks. Small shops usually need a low-frequency but consolidated route to stay profitable.

When to pull this out in a meeting: When service teams want daily delivery everywhere and finance wants every route to be cheap.

### Centralized vs Distributed Fulfillment Matrix
**Purpose:** Decide whether stock should sit in one hub or many locations.

**Text Diagram:**
```text
                      CUSTOMER REACH
                 Localized                 Broad
STOCK LOCATION
Centralized   Lower inventory, longer     Best for risk pooling and scale
              distance to some customers
Distributed   Faster local response,      Best for hot SKUs and urgent service
              more total stock
```

Axes / Quadrants / Components explained:
Centralized stock: supports risk pooling and lower inventory.
Distributed stock: supports faster local response.
Localized demand: suits a single-area hub.
Broad demand: suits a regional or national network.

IT/AI/Product/Consulting worked example: A direct-to-consumer brand keeps slow-moving SKUs in a single DC but places hot items in a regional node. That mix keeps service acceptable while avoiding duplicated inventory everywhere.

When to pull this out in a meeting: When deciding whether a new warehouse will improve service enough to justify the extra fixed cost.

## 4. Formulas

The formulas below are [verified from model knowledge, not source]; they turn the planning tradeoff into measurable unit economics.

### Formula 1: Cost per Delivered Unit
Formula: `Cost per Delivered Unit = Total Distribution Cost / Units Delivered`

Variables:
Total Distribution Cost = transport, handling, and delivery overhead
Units Delivered = successful units delivered to customer or store

Why this formula exists: It shows whether consolidation or route redesign is actually reducing unit cost.

How to interpret the output:
Value < target -> efficient distribution -> keep cadence
Value at target -> acceptable -> optimize service level or route density
Value > target -> too expensive -> consolidate, reroute, or change network

Worked example with numbers: If a route costs $600 and delivers 500 units, cost per unit is $1.20. If the same route is consolidated into 1,000 units for $800 total, cost per unit falls to $0.80. That is the economic case for consolidation, assuming service remains acceptable.

### Formula 2: Truck Load Factor
Formula: `Load Factor = Units Loaded / Truck Capacity`

Variables:
Units Loaded = actual product loaded on the vehicle
Truck Capacity = maximum useful capacity of the vehicle

Why this formula exists: It tells you whether you are sending half-empty trucks or using capacity well.

How to interpret the output:
Value < 0.60 -> underfilled -> consolidate more or adjust route frequency
Value 0.60-0.85 -> healthy -> keep monitoring service and spoilage risk
Value > 0.85 -> near full -> good for cost, but check service flexibility

Worked example with numbers: A truck can carry 1,000 cases, but a route only loads 450. The load factor is 45%, which is a red flag for over-frequent delivery. If route consolidation raises the load to 800 cases, load factor becomes 80% and unit cost drops sharply.

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Don't send half-empty trucks just because the schedule is familiar. | Do consolidate shipments until the service promise is still met at an acceptable load factor. |
| Don't design routes before checking demand density. | Do align route frequency and stop sequence with actual order volume. |
| Don't treat all products the same. | Do match distribution method to the product's urgency, fragility, and temperature needs. |
| Don't centralize or decentralize stock by instinct. | Do compare service speed, risk pooling, and total inventory before choosing the stock location. |
| Don't optimize a warehouse in isolation. | Do plan fulfillment, transport, and replenishment together. |

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: FMCG Company with Half-Empty Trucks
**Situation:** A beverage company delivers 500 cases daily on a truck that can carry 1,000 cases. Each trip costs $600, and delivery demand is stable enough to allow fixed routes.

**Applicable framework/metric:** Consolidation vs Frequency Matrix + Cost per Delivered Unit + Load Factor.

**Analysis:** Current cost per delivered unit = $600 / 500 = $1.20. If the company consolidates to 1,000 cases every two days and the trip cost rises to $800, cost per unit drops to $0.80. Load factor improves from 50% to 100%, assuming no service loss.

**Decision rule:** If load factor is below 60% and service level stays above target after consolidation, reduce trip frequency. If load factor is 60-85%, keep the route and only tune the schedule. If service falls below the target, restore frequency even if cost rises.

**Action:** Move the route to a fixed every-other-day schedule, inform stores in advance, and measure on-time delivery and spoilage after the change.

### Scenario 2: E-Commerce Brand Choosing a Regional Hub
**Situation:** A DTC brand ships all orders from one national warehouse. Average delivery time to South India is 4.5 days, while the target is under 2.5 days. The operations team is considering a regional DC.

**Applicable framework/metric:** Centralized vs Distributed Fulfillment Matrix + cost per delivered unit.

**Analysis:** The current model is cheap on inventory but slow on service. A regional hub would add fixed cost, but it could reduce delivery time by 2 days and improve conversion on urgent items. If the incremental fixed cost is $180,000 per year and the regional hub improves gross margin by $260,000 through higher conversion and lower refunds, the hub is justified.

**Decision rule:** If service gaps are above target by more than 1 day and the incremental margin exceeds fixed cost by at least 25%, open the regional node. If service is already within target, keep centralization.

**Action:** Run a six-month pilot with a 20-SKU regional node and measure promise-date accuracy, cost per delivered unit, and return rates.

### Scenario 3: Consulting Client Rebalancing Store Replenishment
**Situation:** A retail chain has stock both in a central warehouse and at every store. Fast-moving items stock out in metro stores, while slow-moving items pile up in small towns.

**Applicable framework/metric:** Centralized vs Distributed Fulfillment Matrix + risk pooling.

**Analysis:** Centralizing the slow movers reduces total safety stock, while keeping a small local buffer for fast movers protects service. If centralization cuts inventory from 90 days of cover to 55 days and service stays above 97%, the network has become leaner without harming customers.

**Decision rule:** If a SKU has low velocity and stable demand, centralize it. If it has high velocity or urgent demand, keep it close to the customer. If service drops below 95%, reintroduce local stock.

**Action:** Segment the assortment, move slow SKUs to the hub, and set a weekly replenishment cadence for the high-velocity items.

## 7. Implementation Playbook

1. Map the current flow from warehouse to store/customer so the team sees the actual route and stop sequence.
2. Measure demand density, load factor, and delivery frequency for each route.
3. Separate products by urgency, fragility, and temperature needs so one distribution rule does not govern the whole portfolio.
4. Test whether route consolidation keeps service levels within target before changing the full network.
5. Compare centralized versus distributed inventory using total inventory, delivery lead time, and fixed cost.
6. Build a shared distribution dashboard that combines route performance, on-time delivery, and cost per delivered unit.
7. Review the network monthly and change cadence or location only when the metrics show a durable benefit.

## 8. Content Quality Audit

Covered well: the source explains the core distribution choices simply and correctly. It gives a clear bridge from planning intent to practical levers such as delivery frequency, consolidation, product fit, and route planning.

Underplayed or missing: service-level segmentation, vehicle-routing constraints, demand density, stop time, time windows, and the coupling between inventory location and distribution cost. The source also does not explain how distribution planning links back to network planning and multi-echelon inventory design.

Supplement with: Chopra and Meindl, *Supply Chain Management: Strategy, Planning, and Operation* [verified from model knowledge, not source]; Simchi-Levi, Kaminsky, and Simchi-Levi, *Designing and Managing the Supply Chain* [verified from model knowledge, not source]; Fisher, "What Is the Right Supply Chain for Your Product?" HBR (1997) [verified from model knowledge, not source]; and the vehicle-routing literature on route optimization and service windows [verified from model knowledge, not source]. A consulting-style network redesign case is also useful for seeing the fixed-cost versus service-speed tradeoff in practice [verified from model knowledge, not source].

Red flags in the source: it can make consolidation look universally good even when urgent products need more frequency. It also treats last-mile delivery as a simple endpoint rather than the most service-sensitive and cost-sensitive part of the system.

## 9. Quick-Recall Card

```text
Topic: Distribution Planning
Core idea: Decide how often, how much, and through which route product should move so service stays high and unit cost stays controlled.
Key metric/formula: Cost per Delivered Unit = total distribution cost / units delivered; Load Factor = units loaded / truck capacity.
Framework trigger: Use the service-cost ladder when deciding cadence, the consolidation matrix when balancing service against cost, and the centralization matrix when choosing warehouse location.
Watch out for: half-empty trucks, one-size-fits-all service rules, and centralizing or decentralizing without measuring demand density and inventory impact.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Where should the next unit move, and how often, to hit service without paying for waste?
```

<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:4, 7:4, 8:4, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 6, 8, 9] Enrichments applied: [full source-term inventory, route and hub examples, IT/AI/Product/Consulting lens, cost-per-unit math, load-factor logic, literature supplements] Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:42 Audited by: A4 -->
