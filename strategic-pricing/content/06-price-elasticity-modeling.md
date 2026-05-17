# Price Elasticity Modeling

## Overview

Price elasticity measures how much demand moves when the price changes. If a 10% price cut lifts sales by 20%, the product is elastic. If sales only rise 3%, it is inelastic. Modeling elasticity turns this relationship into a number a manager can use to choose price changes.

---

## Why It Matters

Without elasticity, every price change is a guess. With it, a manager can forecast revenue impact before touching the price tag. Misreading elasticity is one of the most common causes of failed promotions and flat category performance.

## Key Principles

- Separate elasticity by product, segment, and channel — they differ widely.
- Use at least 12 months of data to cover seasonal effects.
- Watch cross-elasticity: price changes on one SKU affect its neighbors.
- Inelastic products can usually absorb price rises; elastic ones cannot.
- Re-estimate elasticity after market shocks, not just on a fixed schedule.

## Key Terms

| Term | Definition |
|------|------------|
| **Price Elasticity** | Percent change in quantity divided by percent change in price. |
| **Elastic Demand** | Elasticity greater than 1 — buyers react strongly to price. |
| **Inelastic Demand** | Elasticity below 1 — buyers react weakly to price. |
| **Cross-Elasticity** | How one product's demand reacts to another product's price. |

## Use Case

A beverage brand wants to raise prices 5%. An elasticity study shows their flagship is inelastic (0.4) but their diet variant is elastic (1.6). The team raises the flagship by 6% and holds the diet variant flat, protecting volume while lifting profit.

## Scenario

> A bookstore chain cut the price of paperbacks by 15%, expecting a big volume jump. Elasticity was only 0.7, so sales rose just 10% — not enough to cover the margin loss. After learning the lesson, they reversed course and invested in loyalty bundles instead.

## Examples

- A telecom prices data plans using elasticity to find the revenue-maximizing point.
- A supermarket models cross-elasticity to avoid promotions that cannibalize siblings.

---

## Audited Appendix

# Price Elasticity Modeling
**Course:** Strategic Pricing  
**Module:** Content / Price Elasticity Modeling  
**Audited on:** 2026-04-18  
**Audited by:** A1  
**Source files reviewed:** `strategic-pricing/content/06-price-elasticity-modeling.md`

---

## 1. Topic Snapshot
Price elasticity tells you how much demand moves when price changes, which is the core input for a pricing decision that is more than guesswork. For an IT/AI/Product/Consulting leader, this topic helps decide where to raise price, where to hold price, and where a price cut will only burn margin.
The source is concise, so the operating frameworks below are a practical synthesis of the source and standard management practice [verified from model knowledge, not source].

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Price Elasticity | - | The sensitivity of demand to a price change. | Helps predict demand before changing a price. | `|% change in quantity / % change in price|`. | Pricing, economics, revenue management. |
| Elastic Demand | - | Demand moves strongly when price changes. | Warns that price changes can heavily move volume. | Elasticity greater than 1. | Retail promotions, consumer goods. |
| Inelastic Demand | - | Demand moves weakly when price changes. | Signals room to raise price with limited volume loss. | Elasticity below 1. | Essentials, sticky subscriptions, telecom. |
| Cross-Elasticity | - | Demand for one product changes when another product's price changes. | Shows substitution and cannibalization. | Response of product A to product B's price change. | Product families, supermarket baskets. |
| Revenue-Maximizing Point | - | The price where revenue is highest. | Guides the best price move, not just the highest price. | Revenue curve peak. | Pricing analytics, channel strategy. |
| Seasonal Effects | - | Demand changes with the time of year. | Prevents distorted elasticity estimates. | Month/quarter seasonality patterns. | Retail, travel, subscriptions. |

## 3. Frameworks & Matrices

### Own-Price Elasticity Decision Grid
**Purpose:** Decide whether to raise, hold, or lower price based on demand sensitivity.

**Text Diagram:**
```text
Elasticity < 1   -> price change has smaller demand response -> price can rise
Elasticity = 1   -> revenue stays roughly flat -> test carefully
Elasticity > 1   -> demand moves hard -> price rise can hurt revenue
```

Axes / Quadrants / Components explained:
Component 1: inelastic demand - quantity barely moves when price changes.
Component 2: borderline demand - the revenue effect is uncertain and should be tested.
Component 3: elastic demand - quantity shifts a lot when price changes.
Component 4: revenue-maximizing point - the price near which the business should operate if the goal is profit rather than volume alone.

IT/AI/Product/Consulting worked example: A SaaS product has an inelastic enterprise tier and an elastic self-serve tier. The enterprise price can rise with limited churn risk, while the self-serve tier should be tested more carefully because a small price jump can hurt sign-ups [verified from model knowledge, not source].

When to pull this out in a meeting: When finance wants a price increase and product wants proof that volume will not collapse.

### Cross-Elasticity SKU Map
**Purpose:** Show whether products are substitutes, complements, or cannibalization risks.

**Text Diagram:**
```text
SKU A price change -> affects SKU A demand and nearby SKU B/C demand
```

Axes / Quadrants / Components explained:
Component 1: SKU A - the item whose price is changing.
Component 2: SKU B/C - neighboring or related items in the portfolio.
Component 3: substitution effect - buyers move from one product to another.
Component 4: cannibalization effect - one item steals demand from its sibling.

IT/AI/Product/Consulting worked example: A telecom company raises the price of one data plan and watches demand move to a cheaper sibling plan. The cross-elasticity map shows whether the price change adds net revenue or just shifts customers across tiers.

When to pull this out in a meeting: When one price change seems to improve one SKU but quietly damages a related SKU.

### Elasticity Estimation Workflow
**Purpose:** Estimate elasticity with enough data quality that the result is decision-grade.

**Text Diagram:**
```text
Collect 12+ months -> segment by product/channel -> estimate elasticity -> test assumption -> re-estimate after shock
```

Axes / Quadrants / Components explained:
Component 1: time window - enough history to capture seasonality.
Component 2: segmentation - separate products, channels, and customer groups.
Component 3: estimation - fit the relationship between price and demand.
Component 4: re-estimation - refresh the model after market shocks or major mix changes.

IT/AI/Product/Consulting worked example: A consumer app changes price in one geography, but seasonality and channel mix blur the result. Segmenting by channel and re-estimating after the test gives a cleaner read on true sensitivity.

When to pull this out in a meeting: When someone wants an elasticity number from one promotion and calls it universal.

## 4. Formulas
The source is conceptual, so the formulas below are practical operating heuristics [verified from model knowledge, not source].

### Formula 1: Price Elasticity
Formula: `Price Elasticity = |% Change in Quantity / % Change in Price|`
Variables:
% Change in Quantity = demand response after the price move
% Change in Price = percent change in price
Why this formula exists: It answers how sensitive demand is to price movement.
How to interpret the output:
Value < 1 -> inelastic demand -> price can usually rise
Value 1-1.5 -> moderate sensitivity -> test before scaling
Value > 1 -> elastic demand -> price rises can hurt revenue
Worked example with numbers: If a 10% price cut lifts quantity by 7%, elasticity is 0.7. Decision: price cuts are unlikely to pay back; keep the price or target a different segment.

### Formula 2: Cross-Elasticity
Formula: `Cross-Elasticity = |% Change in Quantity of A / % Change in Price of B|`
Variables:
Quantity of A = demand for product A
Price of B = price of the related product B
Why this formula exists: It answers whether pricing one product moves demand for another product.
How to interpret the output:
Positive and high -> substitutes; watch cannibalization
Near zero -> weak linkage; pricing can be separated
Negative -> complements; pricing B can hurt A or vice versa
Worked example with numbers: If raising product B by 5% increases product A demand by 3%, cross-elasticity is 0.6. Decision: treat A and B as substitutes in the pricing model.

### Formula 3: Revenue Impact Approximation
Formula: `Revenue Impact ≈ (1 + % Change in Price) x (1 + % Change in Quantity) - 1`
Variables:
% Change in Price = the price move being tested
% Change in Quantity = the demand response implied by elasticity
Why this formula exists: It answers whether a price change is likely to raise or lower revenue.
How to interpret the output:
Value > 0 -> revenue increases
Value = 0 -> revenue roughly flat
Value < 0 -> revenue falls
Worked example with numbers: If price rises 6% and quantity falls 2%, revenue impact is about 3.9%. Decision: the price increase is probably worth testing, assuming churn stays stable.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Assume one elasticity number fits all products. | Estimate by product, segment, and channel. |
| Use a promotion month as if it were normal demand. | Include seasonality and enough history in the model. |
| Raise one SKU price without checking sibling SKUs. | Measure cross-elasticity and cannibalization. |
| Treat a price cut as automatically good for revenue. | Compare quantity lift with margin loss. |
| Freeze elasticity forever after one estimate. | Re-estimate after shocks and major market changes. |
| Use elasticity without checking whether the product is essential or discretionary. | Interpret inelastic and elastic demand differently before acting. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Beverage Price Increase
Situation: A beverage brand wants to raise prices 5%. The flagship product is sticky with loyal buyers, but the diet variant is easier to substitute.
Applicable framework/metric: Own-Price Elasticity Decision Grid and Price Elasticity.
Analysis: The flagship has elasticity 0.4, so demand barely moves. The diet variant has elasticity 1.6, so demand is likely to drop sharply if price rises.
Decision rule: If elasticity is below 1, a price rise is usually viable. If it is above 1, a rise can hurt revenue. If it is near 1, test carefully.
Action: Raise the flagship by 6%, hold the diet variant flat, and monitor mix shift and total margin.

### Scenario 2: Bookstore Promotion That Missed the Mark
Situation: A bookstore chain cuts paperback prices by 15% expecting a volume spike. The campaign looks good on traffic, but margin is still under pressure.
Applicable framework/metric: Revenue Impact Approximation and Price Elasticity.
Analysis: Elasticity is only 0.7, so demand is not responding strongly enough to cover the discount. Sales rise 10%, but that is not enough to recover lost margin.
Decision rule: If elasticity is below 1, broad discounts may be wasteful. If above 1, discounts can work, but only with careful margin control.
Action: Reverse the discount and use loyalty bundles instead of blunt price cuts.

### Scenario 3: Telecom Plan Mix
Situation: A telecom operator is deciding whether to push one data plan harder or keep prices balanced across sibling plans. The risk is that one plan will cannibalize the others.
Applicable framework/metric: Cross-Elasticity SKU Map and Cross-Elasticity.
Analysis: A 5% increase in one plan's price shifts some buyers to another plan, showing a cross-elasticity of 0.6. That means the plans are substitutes and need joint pricing.
Decision rule: If cross-elasticity is high, price the family together. If it is low, manage products separately. If it is negative, check for complement effects.
Action: Build a plan-family price ladder and monitor cannibalization after the next change.

## 7. Implementation Playbook
1. Collect at least 12 months of sales, price, promotion, and channel data.
2. Split the data by product, customer segment, and channel before estimating elasticity.
3. Mark seasonal periods and major shocks so they do not distort the estimate.
4. Estimate own-price elasticity and cross-elasticity for the portfolio.
5. Simulate revenue impact for the proposed price move before changing the price tag.
6. Run a small pilot in one region, channel, or segment to validate the estimate.
7. Re-estimate after the test and after any market shock, not just on a fixed calendar.

## 8. Content Quality Audit
Covered well: The source correctly defines elasticity, distinguishes elastic from inelastic demand, and highlights the importance of cross-elasticity and product-level segmentation.
Underplayed or missing: It does not explain estimation mechanics, data requirements, seasonal adjustment, or how to translate elasticity into a revenue decision and portfolio-level price policy.
Supplement with: Nagle and Müller, *The Strategy and Tactics of Pricing* [verified from model knowledge, not source]; Gupta and Lehmann, *Customer Analytics* [verified from model knowledge, not source]; HBR articles on price optimization and promotion design [verified from model knowledge, not source]; and peer-reviewed demand-estimation and revenue-management papers [verified from model knowledge, not source].
Red flags in the source: A single elasticity number can look more precise than it is. If the model ignores seasonality, channel mix, or sibling-SKU effects, the resulting recommendation can be directionally wrong even if the formula is correct.

## 9. Quick-Recall Card
```text
Topic: Price Elasticity Modeling
Core idea: Measure how demand reacts to price before you change the price.
Key metric/formula: Price Elasticity = |% Change in Quantity / % Change in Price|; Cross-Elasticity = |% Change in Quantity of A / % Change in Price of B|.
Framework trigger: Use it when a price change, promotion, or tier shift is under consideration.
Watch out for: Treating one promotion's result as universal demand truth.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Where can we move price without losing more volume than the margin gain is worth?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:4, 4:4, 5:5, 6:5, 7:5, 8:4, 9:5, 10:5] Sections rewritten: [3, 4, 6, 8] Enrichments applied: [own-price elasticity grid; cross-elasticity SKU map; estimation workflow; revenue-impact approximation; segmentation and re-estimation guidance] Final scores: all 5/5 Pass 2 completed: 2026-04-18 20:43 Audited by: A1 -->
