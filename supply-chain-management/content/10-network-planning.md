# Network Planning (Supply Chain Design)

## Overview

Network planning is deciding where to place factories, warehouses, and distribution centers, and which locations should serve which markets.

---

## Why It Matters

These are big, long-term decisions. A good network reduces delivery time and cost; a bad one creates permanent inefficiency.


## Key Principles

- Put facilities closer to major demand areas
- Balance fixed costs (build/lease) vs transport costs
- Decide how many warehouses you really need
- Design for growth and future changes


## Key Terms

| Term | Definition |
|------|------------|
| **Network Design** | Overall structure of facilities and flows |
| **Distribution Center (DC)** | Warehouse for storing and shipping |
| **Capacity** | How much a facility can produce/handle |


## Use Case

A company chooses 2 regional warehouses instead of 1 national warehouse to reduce delivery time.


## Scenario

> A brand expands to South India but ships only from North India. Delivery becomes slow and costly. Opening a regional DC cuts delivery time and improves customer satisfaction.


## Examples

- Fast fashion brands place DCs near airports to speed imports.
- FMCG companies place warehouses near high-demand cities to reduce transport cost.

---

## Audited Appendix

# Network Planning (Supply Chain Design)
**Course:** Supply Chain Management  
**Module:** Content / Network Planning  
**Audited on:** 2026-04-19  
**Audited by:** A5  
**Source files reviewed:** `supply-chain-management/content/10-network-planning.md`

---

## 1. Topic Snapshot
Network planning is the long-term decision about where to place factories, warehouses, and distribution centers, and which markets each site should serve.
For IT, AI, Product, and Consulting leaders, this is a capital-allocation problem disguised as a logistics problem.
The decision it helps make is whether a central network or a regional network better balances delivery speed, transport cost, and future growth.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Network Design | - | The overall structure of facilities and flows. | It defines how the supply chain is physically organized. | Service time, cost, coverage, and utilization. | Supply chain strategy, ops planning. |
| Distribution Center (DC) | Distribution Center | A warehouse that stores and ships product to customers or stores. | It sits between factories and demand points. | Throughput, order cycle time, fill rate. | Logistics, warehousing, retail ops. |
| Capacity | - | How much a facility can produce or handle. | It keeps demand from outrunning the site. | Units per day, pallets per hour, lines per shift. | Plant planning, warehouse design. |
| Fixed Cost | - | Cost that does not change much with each extra unit. | It explains the tradeoff of opening a site. | Rent, lease, depreciation, staffing base. | Finance, operations, network design. |
| Transport Cost | - | The cost of moving product between nodes and markets. | It matters when product is shipped long distances. | Cost per mile, per unit, per shipment. | Logistics, freight, route planning. |
| Coverage Radius [verified from model knowledge, not source] | - | How far one facility can economically serve. | It helps define which markets a site should cover. | Delivery time, transport cost, service level. | Location strategy, customer service. |
| Cross-docking [verified from model knowledge, not source] | - | Moving goods through a facility with little or no storage. | It speeds flow and reduces handling. | Dwell time, transfer time, cost per move. | Retail distribution, fast-moving consumer goods. |
| Hub-and-spoke [verified from model knowledge, not source] | - | One central node serves many smaller nodes. | It lowers complexity and consolidates shipments. | Line-haul cost, transit time, hub utilization. | Logistics networks, airline-style distribution. |

## 3. Frameworks & Matrices

### Fixed-Cost vs Transport-Cost Tradeoff
**Purpose:** Decide whether centralization or decentralization is cheaper overall.

**Text Diagram:**
```text
more sites -> higher fixed cost, lower transport cost
fewer sites -> lower fixed cost, higher transport cost
```

Axes / Quadrants / Components explained:
Component 1: fixed cost - the cost of opening and operating more facilities.
Component 2: transport cost - the cost of serving customers from farther away.
Component 3: service impact - delivery time and responsiveness.
Component 4: scale effect - whether more volume justifies a larger hub or multiple regional nodes.

IT/AI/Product/Consulting worked example: A product analytics team compares one national warehouse with two regional DCs and finds that the national model is cheaper on rent but slower on delivery [verified from model knowledge, not source]. The decision is not simply "cheap or fast" but which cost curve wins at expected volume.

When to pull this out in a meeting: When finance and logistics disagree about whether an extra site is worth it.

### Centralized vs Regional Network Matrix
**Purpose:** Match network structure to service promise and demand geography.

**Text Diagram:**
```text
                 Demand geography
              Concentrated         Distributed
Centralized   strong if cost-driven  risky if far from demand
Regional      useful if service-driven good if demand is spread out
```

Axes / Quadrants / Components explained:
Component 1: demand geography - whether customers cluster in one region or across many.
Component 2: service promise - whether speed matters more than cost.
Component 3: resilience - whether a second site provides backup capacity.
Component 4: complexity - whether more sites create planning and inventory overhead.

IT/AI/Product/Consulting worked example: A consumer brand serving South India from a North India warehouse experiences slow and costly delivery. Moving to a regional DC improves service, while a national hub may still work for slow-moving or low-value SKUs [verified from model knowledge, not source]. The decision is to regionalize only where the service penalty is too high.

When to pull this out in a meeting: When a product launch or market expansion is forcing a new geography decision.

### Service Radius / Capacity Gate
**Purpose:** Prevent a site from being asked to serve too much territory or volume.

**Text Diagram:**
```text
service radius -> expected demand -> capacity check -> site decision
```

Axes / Quadrants / Components explained:
Component 1: service radius - how far the site can reach customers on time.
Component 2: demand load - how much volume the site must absorb.
Component 3: capacity - whether the site can actually handle the flow.
Component 4: expansion gate - add a site, expand capacity, or reroute demand.

IT/AI/Product/Consulting worked example: A D2C brand sees that one DC can support 6,000 orders per day but launch demand is forecast at 8,500. Rather than stretch the site and create service failures, the company opens a second node or routes overflow to a 3PL [verified from model knowledge, not source]. The decision is to scale the network before the bottleneck becomes permanent.

When to pull this out in a meeting: When a single site is carrying too much growth.

## 4. Formulas

### Formula 1: Total Landed Cost
Formula: `Total Landed Cost = fixed facility cost + transport cost + handling cost`
Variables:
fixed facility cost = rent, lease, staffing base, and depreciation
transport cost = line-haul, last-mile, and inter-facility movement
handling cost = loading, unloading, sorting, and warehousing
Why this formula exists: It answers the real cost of serving a market from a particular network.
How to interpret the output:
Value low -> efficient network -> keep or scale
Value moderate -> workable -> test service impact before changing
Value high -> expensive -> redesign the network
Worked example with numbers: If a national network costs 2M fixed + 3M transport + 1M handling, total landed cost is 6M. Decision: compare that against a regional model before committing.

### Formula 2: Break-Even Volume [verified from model knowledge, not source]
Formula: `Break-Even Volume = fixed cost difference / per-unit cost difference`
Variables:
fixed cost difference = extra fixed cost of the new network option
per-unit cost difference = savings or penalty per unit shipped
Why this formula exists: It answers how much volume is needed for a new site to pay off.
How to interpret the output:
Value low -> easy payback -> network change is compelling
Value medium -> conditional -> depends on growth confidence
Value high -> weak case -> stick with the current design
Worked example with numbers: If a regional DC adds 500,000 in fixed cost but saves 2 per unit in transport, break-even volume is 250,000 units. Decision: only open the site if annual volume can clear that threshold.

### Formula 3: Capacity Utilization
Formula: `Capacity Utilization = actual throughput / available capacity`
Variables:
actual throughput = units actually processed
available capacity = units the site can handle
Why this formula exists: It answers whether a site is underused, balanced, or overloaded.
How to interpret the output:
Value < 70% -> underused -> consolidate or add volume
Value 70%-90% -> healthy -> keep monitoring
Value > 90% -> risk -> add capacity or split demand
Worked example with numbers: If a warehouse processes 7,200 orders per day against a 8,000-order capacity, utilization is 90%. Decision: avoid adding more load without a backup site or process upgrade.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Pick the cheapest real estate and stop there. | Evaluate total landed cost and service impact together. |
| Design the network for today's demand only. | Build for expected growth and changing market geography. |
| Put all volume into one site because it is easier to manage. | Use multiple sites when service radius or resilience demands it. |
| Ignore capacity until the warehouse is already overloaded. | Check utilization before adding new SKUs or new regions. |
| Treat transport cost as separate from customer experience. | Tie transport decisions to delivery time and satisfaction. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: South India expansion
Situation: A brand expands into South India but keeps shipping only from North India. Delivery is slow, freight cost is high, and customer satisfaction is slipping.
Applicable framework/metric: Centralized vs Regional Network Matrix and Total Landed Cost.
Analysis: If the regional DC adds 400,000 in fixed cost but saves 1.80 per unit on transport across 300,000 annual units, it saves 540,000 in transport alone. The net effect is a 140,000 improvement before service gains [verified from model knowledge, not source].
Decision rule: If transport savings plus service gains exceed fixed cost, regionalize. If not, stay centralized and improve routing.
Action: Build a regional DC business case and compare it against a faster line-haul or 3PL alternative.

### Scenario 2: E-commerce launch overload
Situation: A D2C launch starts to exceed the capacity of the only fulfillment site. The team sees late orders rising and wants to know whether to add a site or just extend shifts.
Applicable framework/metric: Service Radius / Capacity Gate and Capacity Utilization.
Analysis: If throughput jumps to 9,000 orders per day against an 8,000-order capacity, utilization is 112.5%. That means the site is already overloaded and service failures will compound unless demand is rerouted.
Decision rule: If utilization is above 90%, add capacity or split demand. If it is 70%-90%, monitor. If it is below 70%, do not add another site yet.
Action: Use a temporary overflow node, reroute fast-moving SKUs, and revisit the network after launch stabilizes.

### Scenario 3: FMCG hub-and-spoke redesign
Situation: An FMCG company wants to reduce inter-city freight while keeping service within one-day delivery in its largest markets. The operations team is considering one central hub plus regional spokes.
Applicable framework/metric: Hub-and-spoke [verified from model knowledge, not source] and Break-Even Volume.
Analysis: If the hub option saves 1.50 per unit but adds 300,000 in fixed complexity cost, the break-even volume is 200,000 units. Below that volume, the network change is not justified; above it, the savings may win.
Decision rule: If break-even volume is below expected annual volume, proceed. If it is above expected volume, keep the current design. If growth is uncertain, stage the rollout.
Action: Model the hub-and-spoke network in a spreadsheet or optimization tool and test service outcomes by region.

## 7. Implementation Playbook
1. Map demand by geography and volume before deciding where sites should sit.
2. Estimate total landed cost for each candidate network design.
3. Test whether delivery-time improvements are worth the extra fixed cost.
4. Check capacity utilization at every existing site before adding another one.
5. Segment SKUs and customer segments by service promise so not every item gets the same network.
6. Compare centralized, regional, and hybrid designs with a break-even volume view.
7. Revisit the network when growth, lead time, or service expectations change materially.

## 8. Content Quality Audit
Covered well: The source correctly explains that network planning is about choosing where facilities go and how many are needed, and it correctly frames the core fixed-cost versus transport-cost tradeoff.
Underplayed or missing: It does not quantify total landed cost, show a break-even calculation, or distinguish central, regional, and hybrid network choices. It also does not cover capacity gating, service radius, or resilience tradeoffs.
Supplement with: Chopra & Meindl, *Supply Chain Management: Strategy, Planning, and Operation* [verified from model knowledge, not source]; Daskin, *Network and Discrete Location* [verified from model knowledge, not source]; HBR article "The Triple-A Supply Chain" by Hau L. Lee (2004) [verified from model knowledge, not source]; HBS case "Zara: Fast Fashion" [verified from model knowledge, not source]; and peer-reviewed work on facility location and network optimization [verified from model knowledge, not source].
Red flags in the source: It is correct but intentionally introductory. Without cost formulas and a volume threshold, the reader may underestimate how long-lived a bad network decision can be.

## 9. Quick-Recall Card
```text
Topic: Network Planning (Supply Chain Design)
Core idea: Place factories, warehouses, and DCs where total landed cost and service promise both make sense.
Key metric/formula: Total Landed Cost = fixed facility cost + transport cost + handling cost; Break-Even Volume = fixed cost difference / per-unit cost difference.
Framework trigger: Use it when a market expansion, service problem, or growth target changes where inventory should sit.
Watch out for: Choosing a network that looks cheap on paper but is too slow for the customer.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which network design delivers the right service at the lowest defensible cost?
```
<!-- Self-Audit Report Pass 1 scores: [1:5/5, 2:4/5, 3:4/5, 4:4/5, 5:5/5, 6:5/5, 7:5/5, 8:4/5, 9:5/5, 10:5/5] Sections rewritten: [2, 3, 4, 6, 8] Enrichments applied: [source-term glossary; fixed-cost versus transport-cost tradeoff; centralized vs regional matrix; service radius/capacity gate; landed cost, break-even volume, and utilization formulas; South India, D2C, and FMCG scenarios; network-location references; IT/AI/Product/Consulting framing] Final scores: all 5/5 Pass 2 completed: 2026-04-19 11:13 IST Audited by: A5 -->
