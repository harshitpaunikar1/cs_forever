# Comparable Company Analysis

## Overview

Comparable company analysis, often called trading comps, values a business by comparing it to similar publicly traded companies. The analyst selects a peer group, calculates valuation multiples like EV/EBITDA or P/E for each peer, and applies those multiples to the target company's financial metrics. The result is a market-based valuation range that reflects what investors are currently willing to pay for similar businesses.

---

## Why It Matters

Comps provide a reality check against DCF valuations by showing what the market actually pays for comparable businesses right now. If a DCF says a company is worth $10 billion but every comparable peer trades at a valuation implying $6 billion, something needs explaining. Bankers use comps in virtually every pitch book, fairness opinion, and IPO pricing exercise because clients and boards want to see where a company stands relative to its peers.

## Key Principles

- Peer selection is the most subjective and important step because the wrong peers produce misleading multiples
- Enterprise value multiples like EV/EBITDA are preferred over equity multiples because they are capital-structure neutral
- Calendarization adjusts for different fiscal year ends so all companies are compared on the same time period
- Outliers should be identified and potentially excluded or explained rather than blindly averaged

## Key Terms

| Term | Definition |
|------|------------|
| **Trading Comps** | A valuation method that compares a target to similar publicly traded companies using market multiples |
| **EV/EBITDA** | Enterprise value divided by earnings before interest, taxes, depreciation, and amortization, the most common comp multiple |
| **Peer Group** | A set of publicly traded companies selected for comparison based on industry, size, growth, and margins |
| **Calendarization** | Adjusting financial data from different fiscal year ends to a common time period for accurate comparison |

## Use Case

A bank advising on the sale of a regional hospital chain identifies eight publicly traded healthcare services companies as peers. The peers trade at 10x to 14x forward EV/EBITDA. Applying the median multiple of 12x to the target's projected $400 million EBITDA yields an enterprise value of $4.8 billion, which the bank uses to set the asking price.

## Scenario

> An investment bank was pitching to advise a mid-cap software company on a potential sale. The team selected 15 SaaS peers and found they traded at 8x to 20x forward revenue, with a median of 12x. The target's faster-than-peer growth rate of 40% versus the median 25% justified a premium multiple of 15x, implying a $6 billion valuation. The client agreed the premium was defensible and hired the bank.

## Examples

- Morgan Stanley using EV/EBITDA comps of six luxury goods companies to value a fashion house at 18x EBITDA, well above the industrial average of 10x, reflecting brand premium and margin profile
- An analyst excluding one peer from a seven-company comp set because its recent bankruptcy filing depressed its multiples and would have unfairly dragged down the target's implied valuation

---

## Audited Appendix

# Comparable Company Analysis
**Course:** Investment Banking  
**Module:** Valuation / Comparable Company Analysis  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `investment-banking/content/06-comparable-company-analysis.md`

---

## 1. Topic Snapshot
Comparable company analysis, or trading comps, estimates value by asking what the public market is currently paying for similar businesses.
For IT, AI, product, and consulting leaders, the point is not just to copy a peer multiple. The real decision is which peers are genuinely comparable, which multiple best reflects the business model, and how much judgment is still being baked into the range.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Trading comps | Trading comparables | Valuing a business by comparing public peers | To anchor value in market reality | Implied valuation range | M&A, IPOs, fairness opinions |
| Peer group | N/A | Set of comparable public companies | To create a clean benchmark set | Number and quality of peers | Equity research, banking |
| EV | Enterprise Value | Total value of the operating business | To compare firms regardless of capital structure | Market cap + debt - cash | Valuation, comps, DCF |
| EBITDA | Earnings Before Interest, Taxes, Depreciation, and Amortization | Operating profit proxy | To normalize operating performance | EBITDA margin, growth | Banking, board decks |
| EV/EBITDA | Enterprise Value / EBITDA | Common operating multiple | To compare firms on operating cash generation | Multiple level, median, mean | M&A, public comps |
| P/E | Price/Earnings ratio | Equity value relative to earnings | To compare equity returns | Share price / EPS | Public markets, investors |
| Calendarization | N/A | Aligning fiscal periods across companies | To compare peers on the same time window | Adjusted LTM/FY numbers | Banking models, research |
| LTM | Last Twelve Months | Trailing annual financials | To reflect current performance | Trailing revenue/EBITDA | Trading comps, analysis |
| Forward multiple | N/A | Multiple based on future year estimates | To reflect market expectations | NTM EV/EBITDA, NTM revenue | Sell-side, IPOs |
| Outlier | N/A | A peer with unusual metrics or events | To avoid distorted averages | Std. dev., range, judgment | Comps selection, diligence |
| Median | N/A | Middle value in a peer set | To reduce distortion from extremes | Median multiple | Valuation tables |
| Premium / discount | N/A | Higher or lower multiple than peers | To reflect quality differences | % above or below peer median | Deal discussions |
| Forward EBITDA | N/A | Expected EBITDA in a future period | To price growth and quality into valuation | Estimate from model | SaaS, industrials, healthcare |
| Revenue multiple | N/A | Value relative to sales | To value high-growth or low-profit businesses | EV/revenue | SaaS, consumer, tech |
| Implied valuation | N/A | Value derived from a peer multiple | To translate the market multiple into dollars | Multiple × metric | Pitch books, fairness opinions |

## 3. Frameworks & Matrices

### Peer Selection Matrix
**Purpose:** Decide whether a company should be in the comp set.

**Text Diagram:**
```text
                         Similarity
                 High                      Low
Business model  Include                   Exclude or flag
Size/growth      Include if close          Exclude or normalize
Margins          Include if comparable     Exclude or explain
Geography        Include if relevant       Exclude if market differs materially
```

Axes / Quadrants / Components explained:
Component 1: business model, meaning how the firm makes money.
Component 2: size and growth, meaning revenue scale and growth profile.
Component 3: margins, meaning profitability and operating leverage.
Component 4: geography, meaning market structure and valuation regime.

IT/AI/Product/Consulting worked example: A SaaS company should compare itself to public software peers, not to a hardware distributor just because both “sell technology.” If the target has 40% growth and the peer group averages 20%, a premium may be warranted, but only if the rest of the similarity criteria hold.
When to pull this out in a meeting: When someone wants to force a convenient but weak peer into the set.

### Multiple Choice Matrix
**Purpose:** Decide which valuation multiple best fits the business.

**Text Diagram:**
```text
High growth / low current profit -> revenue multiple
Stable profit / mature business   -> EV/EBITDA or P/E
Capital-intensive business        -> EV-based multiple with caution
Early-stage or messy earnings     -> use revenue, bookings, or ARR proxy
```

Axes / Quadrants / Components explained:
Component 1: profitability, meaning whether earnings are meaningful today.
Component 2: growth, meaning whether the market is paying for future expansion.
Component 3: capital intensity, meaning whether debt and depreciation distort earnings.
Component 4: predictability, meaning how reliable the operating metrics are.

IT/AI/Product/Consulting worked example: A subscription software business with strong ARR growth may deserve a revenue multiple rather than a P/E ratio, while a consulting firm with stable margins is better compared on EV/EBITDA.
When to pull this out in a meeting: When the team is arguing over one multiple that does not fit the company.

### Valuation Bridge
**Purpose:** Move from public market multiples to a target valuation range.

**Text Diagram:**
```text
select peers -> clean metrics -> choose median -> apply premium/discount -> derive implied value
```

Axes / Quadrants / Components explained:
Component 1: peer quality, meaning the starting universe.
Component 2: metric quality, meaning whether numbers are calendarized and normalized.
Component 3: judgment, meaning the premium or discount for differences.
Component 4: output, meaning the valuation range used in the deal.

IT/AI/Product/Consulting worked example: A target with higher gross margin and faster revenue growth than peers may justify a modest premium, but the analyst should explain why the premium is defensible rather than simply more optimistic.
When to pull this out in a meeting: When the client asks how the headline multiple becomes a number they can use.

## 4. Formulas

The formulas below are practical valuation tools [verified from model knowledge, not source].

### Formula 1: EV/EBITDA [verified from model knowledge, not source]
Formula: `EV/EBITDA = Enterprise Value / EBITDA`

Why this formula exists: It compares firms on operating value while reducing capital-structure noise.
How to interpret the output:
Lower multiple -> market is assigning less value per unit of EBITDA
Higher multiple -> market expects stronger growth, quality, or scarcity
Worked example with numbers: If EV is $4.8B and EBITDA is $400M, EV/EBITDA is 12.0x. Decision: compare that result to the peer median and explain any premium or discount.

### Formula 2: P/E Ratio [verified from model knowledge, not source]
Formula: `P/E = Share Price / Earnings per Share`

Why this formula exists: It shows what the public market is paying for each dollar of earnings.
How to interpret the output:
Lower P/E -> lower earnings valuation or lower growth expectation
Higher P/E -> higher growth or higher confidence
Worked example with numbers: If share price is $60 and EPS is $3, P/E is 20x. Decision: use only when the company has meaningful earnings and a stable capital structure.

### Formula 3: Implied Enterprise Value [verified from model knowledge, not source]
Formula: `Implied EV = Selected Multiple × Target Metric`

Why this formula exists: It turns market multiples into an actual valuation range.
How to interpret the output:
Median multiple -> baseline value
Premium multiple -> stronger quality or growth
Discount multiple -> weaker growth, risk, or comparability
Worked example with numbers: If a software company’s peer median EV/revenue is 8x and the target has $750M revenue, implied EV = $6.0B. If a 10% premium is justified, value becomes $6.6B.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Compare the target to bad peers just to make the valuation look better | Build a defensible peer set first |
| Average multiples blindly | Use medians, outlier checks, and judgment |
| Mix fiscal periods without adjustment | Calendarize financials before comparison |
| Use one multiple for every business model | Pick the multiple that fits growth, margin, and capital intensity |
| Treat the result as objective truth | Present comps as a market-based estimate with assumptions |

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: SaaS Valuation With Growth Premium
Situation: A product-led SaaS business is being sold, and the owner believes it deserves more than the median peer multiple.
Applicable framework/metric: Peer Selection Matrix, revenue multiple, valuation bridge.
Analysis: If the target grows 40% versus a 25% peer median and has similar retention and margins, a premium can be justified. The premium should be anchored in clear operating differences, not enthusiasm.
Decision rule: If growth, retention, and margin are all above peer medians, allow a premium; if only growth is higher, keep the premium modest.
Action: Present the peer set, show normalized metrics, and explain the premium in one sentence.

### Scenario 2: Mature Service Business Using EV/EBITDA
Situation: A consulting-heavy services company wants to know whether EV/EBITDA or P/E is the better comp metric.
Applicable framework/metric: Multiple Choice Matrix, EV/EBITDA.
Analysis: Because earnings are meaningful and capital structure differences should not dominate the comparison, EV/EBITDA is more useful than P/E. It is also easier to compare across differently financed peers.
Decision rule: If EBITDA is stable and the business is not distorted by unusual leverage, use EV/EBITDA as the anchor.
Action: Normalize EBITDA, remove one-time items, and compare against a clean public peer set.

### Scenario 3: Weak Peer with Distorted Multiples
Situation: An analyst is tempted to include a peer that just filed bankruptcy because its market cap is tiny and its multiple looks low.
Applicable framework/metric: Peer Selection Matrix, outlier logic.
Analysis: The distressed peer will drag down the median and misrepresent the target’s value. If the peer is structurally different because of distress, it should be excluded or separately explained.
Decision rule: Exclude peers with unusual distress, accounting breaks, or non-comparable business models.
Action: Document the exclusion and preserve the integrity of the valuation range.

## 7. Implementation Playbook
1. Define the business model and operating profile of the target.
2. Build a peer universe based on business model, size, growth, and geography.
3. Calendarize and normalize the financial data.
4. Choose the multiple that best matches the economics of the business.
5. Remove or explain outliers before calculating the range.
6. Apply a defensible premium or discount based on visible differences.
7. Translate the multiple into implied value and compare it with other methods.

## 8. Content Quality Audit
Covered well: The source gives the core mechanics of trading comps, correctly emphasizes peer selection, and explains why EV/EBITDA is a common anchor.
Underplayed or missing: The chapter does not explain how to choose between revenue, EBITDA, and earnings multiples in different business models, nor does it quantify the impact of outliers, calendarization, or premium/discount logic.
Supplement with: public comps methodology from investment-banking valuation texts, normalization of financials, and market-specific multiple interpretation [verified from model knowledge, not source].
Red flags in the source: It can make comps look more mechanical than they are. The peer set and the adjustment judgment often matter more than the spreadsheet math.

## 9. Quick-Recall Card
```text
Topic: Comparable Company Analysis
Core idea: Value the target by comparing it to similar public companies and applying a defensible multiple.
Key metric/formula: EV/EBITDA = Enterprise Value / EBITDA; P/E = Share Price / EPS; Implied EV = Selected Multiple × Target Metric.
Framework trigger: Use the peer-selection matrix before trusting any valuation range.
Watch out for: bad peers, bad metrics, and outliers hiding in the average.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which public companies are truly comparable, and which multiple reflects the target’s economics best?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [peer selection matrix, multiple-choice matrix, valuation bridge, EV/EBITDA and P/E formulas, premium/discount logic, SaaS/services/distress scenarios] Final scores: all 5/5 Pass 2 completed: 2026-04-20 19:28 IST Audited by: A2 -->
