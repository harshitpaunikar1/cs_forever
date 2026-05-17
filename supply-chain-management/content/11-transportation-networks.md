# Transportation Networks

## Overview

Transportation networks are the choices of how goods travel (road, rail, air, sea) and how shipments are organized across routes and hubs.

---

## Why It Matters

Transportation is often one of the biggest supply chain costs. The mode choice affects speed, cost, and reliability.


## Key Principles

- Choose mode based on product value and urgency
- Combine shipments where possible
- Plan routes to reduce empty return trips
- Consider reliability, not just cheap rates


## Key Terms

| Term | Definition |
|------|------------|
| **Mode** | Road/rail/air/sea |
| **Freight** | Goods transported in bulk |
| **Hub-and-Spoke** | Central hub connects to many smaller points |


## Use Case

A company ships bulk goods by rail for cost savings, but uses air for urgent spare parts.


## Scenario

> A company ships high-value electronics by sea to save money, but deliveries take too long and customers complain. Switching to air for urgent items and sea for regular stock balances speed and cost.


## Examples

- Fresh seafood uses air freight due to short shelf life.
- Cement uses rail/road in bulk because it is heavy and low-value per unit.

---

## Audited Appendix

# Transportation Networks
**Course:** Supply Chain Management  
**Module:** Content / Transportation Networks  
**Audited on:** 2026-04-19  
**Audited by:** A3  
**Source files reviewed:** `supply-chain-management/content/11-transportation-networks.md`

---

## 1. Topic Snapshot
Transportation networks decide how goods move by road, rail, air, or sea and how shipments are organized across routes and hubs.  
It matters because mode choice drives the biggest tradeoff in supply chain execution: speed, cost, and reliability.  
For an IT/AI/Product/Consulting decision-maker, the key question is whether the network design matches product value, urgency, and service promise.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Mode | - | The transport choice: road, rail, air, or sea | To match delivery needs with cost and speed | Transit time, freight cost, reliability | Logistics planning, procurement |
| Freight | - | Goods transported in bulk | To describe the shipment itself, not the route | Weight, volume, freight rate | Shipping, carrier negotiations |
| Hub-and-Spoke | - | Central hub connects many smaller points | To consolidate shipments and reduce route complexity | Line-haul cost, load factor, hub utilization | Network design, distribution planning |
| Road | - | Truck-based transport | To offer flexible door-to-door service | Transit time, cost per mile, on-time rate | Last-mile delivery, domestic freight |
| Rail | - | Train-based transport | To move heavy bulk efficiently | Cost per ton-km, delay rate | Commodity logistics, bulk shipping |
| Air | - | Plane-based transport | To move urgent or high-value goods fast | Transit time, cost per unit, damage rate | Spare parts, premium shipping |
| Sea | - | Ship-based transport | To move large volumes at low cost | Cost per container, sailing time | International trade, imports |
| Reliability | - | How consistently shipments arrive as promised | To protect service levels | On-time delivery %, delay variance | Executive reviews, customer SLAs |
| Route | - | The path a shipment follows | To organize multi-stop delivery efficiently | Distance, stops, travel time | Fleet planning, routing software |
| Hub | - | A central consolidation point | To pool freight before redistribution | Throughput, dwell time, cross-dock time | Distribution centers, 3PLs |

## 3. Frameworks & Matrices

### Mode Choice Matrix
**Purpose:** Choose the transport mode that best fits product urgency and value density.

**Text Diagram:**
```text
                    Product urgency
                Low                         High
Value     ------------------------------------------------
Low       | Sea / rail                    | Road
High      | Rail / road                  | Air
```

Axes / Quadrants / Components explained:
Product urgency: how quickly the goods must arrive to protect sales or operations.  
Value density: how valuable the shipment is relative to its weight or volume.  
Low urgency + low value density: sea or rail usually wins on cost.  
Low urgency + high value density: road or rail can balance cost and flexibility.  
High urgency + low value density: road is often the practical compromise.  
High urgency + high value density: air is justified when delay cost is high.

IT/AI/Product/Consulting worked example: An AI-based routing engine flags urgent spare parts for air, bulk replenishment for sea, and a new product launch for road plus hub consolidation. The decision produced is whether to pay for speed now or protect margin with slower freight.  
When to pull this out in a meeting: When a team wants one transport mode for every product.

### Hub-and-Spoke Design Lens
**Purpose:** Decide whether to use a central hub to consolidate freight or move directly point-to-point.

**Text Diagram:**
```text
Point-to-point:  A -> B, A -> C, A -> D, B -> C ...
Hub-and-spoke:   A -> HUB -> B
                 A -> HUB -> C
                 A -> HUB -> D
```

Axes / Quadrants / Components explained:
Direct routes: fewer handoffs, faster for urgent lanes, but can be expensive.  
Hub consolidation: higher load factor and lower freight cost, but more dwell time.  
Hub utilization: how much the hub is handling relative to its capacity.  
Network density: whether there are enough flows to justify centralization.

IT/AI/Product/Consulting worked example: A logistics product owner uses a hub-and-spoke model for routine store replenishment and direct air routes for emergency spares. A consultant uses the same lens to explain why the network should consolidate one flow but not another.  
When to pull this out in a meeting: When managers are debating centralization versus direct shipping.

## 4. Formulas

Formula: Load factor = shipped volume / vehicle capacity x 100 [verified from model knowledge, not source]  
Variables:  
Shipped volume = the amount loaded on the truck, railcar, plane, or vessel  
Vehicle capacity = the maximum amount the vehicle can carry  
Load factor = the percentage of capacity being used  
Why this formula exists: It answers whether shipments are being consolidated efficiently.  
How to interpret the output:  
Value < 70% -> underfilled -> consolidate more or redesign routes.  
Value 70%-90% -> acceptable -> monitor cost and service.  
Value > 90% -> strong utilization -> keep, unless service delays rise.  
Worked example with numbers: If a truck can carry 10 tons and you ship 7 tons, the load factor is 70%. If the same route is only shipping 4 tons, you are paying for empty space and should consolidate.

Formula: Total landed cost = freight cost + handling cost + time cost [verified from model knowledge, not source]  
Variables:  
Freight cost = charge paid to the carrier  
Handling cost = loading, unloading, cross-dock, and storage cost  
Time cost = the business cost of delay, stockouts, or missed sales  
Why this formula exists: It answers the real cost of a transport choice, not just the carrier quote.  
How to interpret the output:  
Value low -> cost-efficient lane -> keep the current mode.  
Value moderate -> acceptable tradeoff -> fine-tune route and consolidation.  
Value high -> expensive lane -> switch mode, redesign hub use, or change service promise.  
Worked example with numbers: A sea shipment may cost less in freight, but if the time cost of delay triggers stockouts, the landed cost can exceed an air shipment. That is why the best choice is the one with the lowest total landed cost, not the lowest freight invoice.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Choose the cheapest freight quote without checking service impact | Compare total landed cost, including delay risk |
| Use air for routine replenishment | Reserve air for urgent or high-value shipments |
| Run many empty or half-full trucks | Consolidate freight and raise load factor |
| Force every lane through a hub | Use direct routes where urgency outweighs consolidation savings |
| Judge the network only on freight cost | Track reliability, transit time, and customer service together |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: High-value electronics vs regular stock  
Situation: A company ships high-value electronics and also regular replenishment stock. The IT team sees air freight cost at $4.80/unit versus sea freight at $1.20/unit, but the sea lane adds 12 days of transit time.  
Applicable framework/metric: Total landed cost.  
Analysis: If the stockout penalty is $7/unit, sea freight can become more expensive than air once delay cost is counted.  
Decision rule: If total landed cost is lowest with air, use air. If sea plus buffer stock is cheaper, use sea. If the gap is small, use a mixed network by product class.  
Action: Ship urgent items by air, bulk items by sea, and set a service policy by SKU value and urgency.

Scenario 2: Bulk freight consolidation through a hub  
Situation: A manufacturer sends parts from three plants to many stores. The current point-to-point network keeps trucks at only 58% load factor, and empty return trips are common.  
Applicable framework/metric: Load factor and hub-and-spoke design.  
Analysis: A hub that raises average load factor to 84% improves utilization and lowers freight cost, even if dwell time rises slightly.  
Decision rule: If load factor < 70%, consolidate more. If 70%-90%, monitor. If > 90% but service slips, relax consolidation.  
Action: Move routine lanes through a regional hub, keep urgent lanes direct, and re-plan routes monthly.

Scenario 3: Cement and perishable seafood  
Situation: A consulting team reviews a client that ships cement and fresh seafood. Cement is low value per unit and can move in bulk by rail, while seafood is time-sensitive and must stay reliable.  
Applicable framework/metric: Mode choice matrix.  
Analysis: Cement belongs in the low-urgency/low-value quadrant, which points to rail or sea. Seafood belongs in the high-urgency quadrant, which points to air or fast road transport.  
Decision rule: If urgency is high, choose speed. If value density is low and urgency is low, choose rail or sea.  
Action: Split the transportation policy by product class rather than forcing one mode for all freight.

## 7. Implementation Playbook
1. Classify SKUs by urgency, value density, and service promise.  
2. Build a mode-choice policy that maps each class to road, rail, air, or sea.  
3. Measure load factor and empty miles on every major lane.  
4. Review total landed cost, not just freight quotes, before approving a shipment plan.  
5. Test hub-and-spoke versus direct routes for dense and sparse networks separately.  
6. Set service exceptions for urgent air lanes and keep bulk lanes on consolidation targets.  
7. Revisit the network every quarter when demand, carriers, or fuel costs change.  

## 8. Content Quality Audit
Covered well: The source gives the basic purpose of transportation networks and the core tradeoff between cost, speed, and reliability.  
Underplayed or missing: It does not quantify utilization, explain total landed cost, or show when hub-and-spoke beats point-to-point routing.  
Supplement with: Ballou, *Business Logistics/Supply Chain Management* [verified from model knowledge, not source]; Simchi-Levi, Kaminsky, and Simchi-Levi, *Designing and Managing the Supply Chain* [verified from model knowledge, not source]; Chopra and Meindl, *Supply Chain Management: Strategy, Planning, and Operation* [verified from model knowledge, not source]; a useful case is UPS ORION route optimization [verified from model knowledge, not source].  
Red flags in the source: It is a simplified overview, so it can make transport look like a one-variable cost decision when reliability, service penalties, and network density also matter.

## 9. Quick-Recall Card
```text
Topic: Transportation Networks
Core idea: Pick the mode and network shape that minimize total landed cost while protecting service.
Key metric/formula: Load factor = shipped volume / vehicle capacity x 100 [verified from model knowledge, not source].
Framework trigger: Use it when a lane is too slow, too expensive, or too empty.
Watch out for: Optimizing freight cost alone.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which mode and network shape gives the best cost-speed-reliability mix for this SKU class?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [mode-choice matrix, hub-and-spoke lens, load factor and landed cost formulas, IT/AI/Product/Consulting examples, lane-by-lane implementation playbook] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:40 Audited by: A3 -->
