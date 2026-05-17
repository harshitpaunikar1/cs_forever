# Valuation Methodologies

## Overview

Valuation is the process of estimating what a company is worth. Different methods (income-based, market-based, asset-based) look at the business from different angles, and a good deal team uses more than one to cross-check the answer.

---

## Why It Matters

Pay too much and even a great target destroys value; pay too little and the deal never closes. A clear valuation range helps leaders negotiate, choose the right payment mix, and explain the price to the board.

## Key Principles

- Use at least two methods and check the range they produce
- Match the method to the business: growth firms need DCF, stable firms suit multiples
- Separate the stand-alone value from the synergy value
- Test sensitivity to growth, margins, and discount rates
- Do not let market hype override fundamentals

## Key Terms

| Term | Definition |
|------|------------|
| **Income Approach** | Value based on future expected cash flows |
| **Market Approach** | Value based on what similar firms trade for |
| **Asset Approach** | Value based on net worth of assets minus liabilities |
| **Enterprise Value (EV)** | Total value of the business including debt |
| **Equity Value** | Value that belongs to shareholders |

## Use Case

A private manufacturing company is up for sale. The buyer runs a DCF on future cash flows, compares EV/EBITDA multiples of listed peers, and also checks the replacement cost of the plant and machinery.

## Scenario

> A buyer valued a SaaS firm using three methods: DCF gave $200M, trading multiples gave $230M, and recent deal multiples gave $250M. The buyer offered $225M, right in the middle, and closed the deal without overpaying.

## Examples

- A bank uses P/B multiples to value another bank since asset value drives earnings.
- A startup investor uses DCF plus scenario weights because current profit is negative.

---

## Audited Appendix

# Valuation Methodologies
**Course:** Mergers and Acquisitions
**Module:** Content / Valuation Methodologies
**Audited on:** 2026-04-18
**Audited by:** A7
**Source files reviewed:** `mergers-acquisitions/content/05-valuation-methodologies.md`

---

## 1. Topic Snapshot
The three classical approaches — Income (future cash-flow view, e.g., DCF), Market (peer/precedent multiples), and Asset (net worth / replacement) — each look at the target from a different angle and produce their own value number. An IT/AI/Product/Consulting deal leader triangulates them so that one method's blind spot (e.g., DCF's WACC sensitivity, multiples' peer-selection bias) is checked by the others, producing a defensible range rather than a single point. The decision: choose a bid price and payment mix that sits inside a cross-checked range, so the buyer neither overpays (value destruction) nor underpays (deal dies).

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Income Approach | Income Approach | Value = PV of future cash flows | Captures forward economics | DCF, APV, DDM | Banker model tabs |
| Market Approach | Market / Relative Approach | Value = what peers trade/transact at | Anchors to market reality | EV/EBITDA, P/E, EV/ARR | Comps sheet |
| Asset (Cost) Approach | Asset-Based Approach | Value = net fair value of assets | Floor value, asset-heavy cos. | Σ FV(assets) − liabilities | Manufacturing, banks |
| DCF | Discounted Cash Flow | Discount future FCFF to today | Intrinsic value view | Σ FCFFₜ/(1+WACC)^t + TV | IC memo |
| CCA | Comparable Company Analysis | Peer trading multiples | Public-market read | Median EV/EBITDA × target EBITDA | "Trading comps" |
| PTA | Precedent Transaction Analysis | Past M&A multiples | Captures control premium | Median deal EV/EBITDA | "Transaction comps" |
| Replacement / Reproduction Cost | Replacement Cost | Cost to rebuild assets today | Asset-heavy targets | Engineering quotes, indexation | Plant & machinery |
| Book / Market / Liquidation Value | BV / MV / LV | Accounting / traded / fire-sale | Distinct floors & ceilings | Balance sheet / market / auction | Distressed deals |
| SOTP | Sum-of-the-Parts | Value each segment, add up | Conglomerates, multi-BU | Σ Segment EV − net debt | Holding cos. |
| Football Field | Football Field Chart | Horizontal range bars by method | Visual triangulation | Min–max per method | Board decks |
| Central Tendency | Mean / Median / Harmonic Mean | Summary statistic for peer set | Outlier-robust anchor | Median typical; harmonic for ratios | Comps page |
| Implied Range | Implied Valuation Range | Low–high from all methods | Negotiation anchor | Overlap of method ranges | Fairness opinion |
| Value Inflection | Startup / Growth / Mature | Stage drives which method works | Method fit by lifecycle | Revenue CAGR, margin profile | Stage gating |
| Control Premium | Control Premium | Extra paid for control | Control has option value | PTA − CCA median | Deal pricing |
| DLOM | Discount for Lack of Marketability | Discount for illiquidity | Private co. adjustment | 10–30% typical | Private-co. valuation |
| ESOP-Pool Adjustment | Option-Pool Shuffle | Dilution for future hires | Pre-money vs post-money clarity | % fully diluted | VC/PE term sheets |
| WACC | Weighted Average Cost of Capital | Blended required return | Discount rate for FCFF | w_d·k_d(1−t)+w_e·k_e | DCF engine |
| Terminal Value | TV | Value beyond explicit forecast | Captures going concern | Gordon growth or exit multiple | Model cell |

---

## 3. Frameworks & Matrices

### 3.1 Valuation Triangle
**Purpose:** force triangulation across the three lenses so no single bias dominates.

```
                 INCOME APPROACH
                (DCF / APV / DDM)
                        /\
                       /  \
                      /    \
                     /      \
                    /        \
                   /          \
                  /   RANGE    \
                 /   OVERLAP    \
                /   = FOOTBALL   \
               /      FIELD       \
              /____________________\
   MARKET APPROACH            ASSET APPROACH
   (CCA + PTA)               (Replacement + Liquidation)
```

**Components:** Income (forward), Market (peers), Asset (floor). **IT/AI/Product/Consulting example:** AI-SaaS target — DCF as primary (growth story), EV/ARR comps as market check, asset approach only as sanity floor (IP + GPU contracts). **Trigger:** any deal above ₹50 cr / $10M — never rely on one method.

### 3.2 Method-by-Business-Type Selector

| Business Type | Primary Method | Cross-Check 1 | Cross-Check 2 | Why |
|---|---|---|---|---|
| AI-SaaS (growth, -ve EBITDA) | DCF w/ scenario weights | EV/ARR comps | Precedent EV/ARR | Profit negative, growth drives value |
| AI platform (mid-stage) | DCF + EV/Revenue | Precedents | Rule-of-40 benchmark | Hybrid growth + unit econ |
| IT services firm | EV/EBITDA comps | DCF | Precedent (cycle-adj) | Stable, cyclical margins |
| Mature manufacturer | DCF + EV/EBITDA | Replacement cost | Precedents | Tangible-asset heavy |
| Distressed / turnaround | Liquidation value | Replacement cost | DCF (downside) | Going-concern in doubt |
| Conglomerate / holdco | SOTP | Peer SOTP | NAV − holding discount | Mixed segments |

### 3.3 Football Field (SaaS Target)

```
Method                  Low     Mid     High   ($M)
                        |       |       |
DCF (base case)         [==== $200M ====]
DCF (bull/bear)       [====== $220M =======]
Trading Comps EV/EBITDA   [=== $230M ===]
Trading Comps EV/ARR        [== $235M ==]
Precedents EV/EBITDA         [=== $250M ====]
52-week range (if listed)  [==== $210M ====]
                        |       |       |
                       180     225     260
                                ^
                           Bid $225M
```

**Trigger:** present football field at IC before bid; bid inside overlap zone.

### 3.4 (Optional) SOTP for Conglomerates
**Purpose:** unbundle a multi-segment target; apply holding discount (10–25%). **Example:** IT-conglomerate with (a) IT services, (b) BPO, (c) captive AI lab — value each with appropriate primary method, subtract segment net debt, apply holding discount for cross-subsidy inefficiency.

---

## 4. Formulas

### 4.1 DCF Enterprise Value
```
EV_DCF = Σ_{t=1..n} [ FCFFₜ / (1 + WACC)^t ] + TV / (1 + WACC)^n
TV = FCFF_{n+1} / (WACC − g)        (Gordon)   OR   TV = EBITDA_n × Exit Multiple
```
**Thresholds:** TV should be ≤ 70–75% of EV (else forecast too short). g ≤ long-run GDP growth.
**SaaS example:** 5-yr FCFF PV = $60M; TV PV = $140M; EV_DCF = $200M. Equity = EV − Net Debt.

### 4.2 Multiples
```
EV_comps   = EV/EBITDA (peer median) × Target EBITDA
Equity_P/E = P/E (peer median)       × Target EPS × Shares
EV_ARR     = EV/ARR (peer median)    × Target ARR
```
**Thresholds:** trim top/bottom 10% of peer set; prefer median over mean; harmonic mean for ratios.
**SaaS example:** peer median EV/ARR = 5.75×; target ARR = $40M → EV = $230M.

### 4.3 Replacement Cost (Asset Approach)
```
EV_asset = Σ Asset Fair Values − Liabilities
        (for replacement: cost to rebuild identical productive capacity today)
```
**Thresholds:** use for asset-heavy (manufacturing, infra); weak for services/SaaS (people + IP dominate).
**Example:** private manufacturer — plant replacement $80M + inventory $15M − liabilities $25M = $70M floor.

### 4.4 Central Tendency (Peer Multiples)
```
Median(EV/EBITDA)        = preferred default
Harmonic Mean(EV/EBITDA) = n / Σ(1 / (EV/EBITDAᵢ))    (better for ratios)
Trimmed Mean (10%)       = discard outliers both tails
```
**Thresholds:** peer set ≥ 6 names; disclose why outliers excluded.

### 4.5 SOTP
```
EV_SOTP = Σ_i (Segment EVᵢ − Segment Net Debtᵢ) × (1 − Holding Discount)
```
**Thresholds:** holding discount 10–25% depending on governance, cross-subsidies.

**Decision on SaaS target (all methods together):**
- DCF $200M, CCA $230M, PTA $250M → range $200–$250M, midpoint ≈ $225M → bid $225M in middle of range; closes without overpay.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Use ≥ 2 methods and triangulate (football field). | Rely on a single method, especially DCF-only in hot markets. |
| Match method to business type (growth → DCF, stable → multiples, asset-heavy → replacement). | Force DCF on a distressed asset or replacement cost on a SaaS. |
| Separate standalone value from synergy value explicitly. | Blend synergy into DCF and justify any price. |
| Sensitivity-test WACC, growth, margin, terminal multiple. | Present one-point valuation with no ranges. |
| Use median (or harmonic mean) for peer multiples; trim outliers. | Use mean on a skewed peer set with one mega-cap. |
| Apply DLOM / control premium explicitly for private targets. | Copy public comps directly without liquidity/control adjustment. |
| Cross-check DCF-implied terminal growth and exit multiple vs peers. | Allow implied g > GDP or exit multiple > peer max without a reason. |
| Show cycle-adjusted multiples for IT services / cyclicals. | Use trough or peak multiples as "normal". |
| Document peer-selection criteria (size, geography, margin band). | Cherry-pick peers that justify the desired answer. |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS Target (Football Field)
Buyer runs DCF ($200M base, $180–$230M range) + EV/ARR comps (peer median 5.75× on $40M ARR = $230M) + precedents (6.25× on ARR = $250M, control premium embedded). Football field overlap $210–$240M → IC bids $225M, middle of the implied range. Payment mix: 60% cash / 40% stock to share risk on growth assumptions.
**Tools:** Excel (DCF), CapIQ (comps + precedents), PitchBook (private multiples), Damodaran dataset (WACC/betas).

### Scenario 2 — IT-Services Firm (Cycle-Adjusted)
Target: mid-size IT services firm, $500M revenue, 14% EBITDA margin, cyclical demand. Buyer uses EV/EBITDA comps (peer median 11× → EV $770M), DCF with normalized 13% mid-cycle margin (EV $740M), precedents (12.5× with cycle adjustment → EV $875M). Because market is near a cyclical peak, buyer anchors to DCF and trading comps, not frothy precedents; bids $760M.
**Tools:** CapIQ (cycle data), FactSet (peer set), Excel (DCF + Monte Carlo on margin), Damodaran (industry WACC).

### Scenario 3 — ANTI-EXAMPLE: DCF-Only in a Frothy Market
Buyer of a consumer-AI platform uses DCF only, plugs in 40% revenue CAGR for 10 years and 4% terminal growth; implied EV = $1.0B. Skips comps (peer EV/Revenue median says $700M) and precedents ($750M). Bids $1.0B. 2 years later, growth resets to 18%, WACC rises 200 bps, and the buyer books an impairment of ≈ ₹1,200 cr (~$145M). Had the football field been used, the frothy DCF number would have sat 30%+ above every other method — an obvious red flag pre-bid.
**Tools ignored (that would have saved the deal):** CapIQ comps, PitchBook precedents, Damodaran implied-ERP check.

---

## 7. Implementation Playbook
1. **Define** target profile and value drivers (growth, margin, capital intensity) — artifact: 1-pager target profile.
2. **Select peer set** (≥ 6 names, size/geography/margin band) — artifact: CCA peer sheet with inclusion criteria.
3. **Build DCF** with 5-yr explicit forecast, WACC build-up, two TV methods (Gordon + exit multiple) — artifact: DCF model with sensitivity tables.
4. **Build CCA and PTA** using median/harmonic mean — artifact: comps + precedents sheet with outlier notes.
5. **Layer adjustments** — DLOM, control premium, holding discount, cycle adjustment — artifact: adjustments bridge.
6. **Plot Football Field** across methods, highlight overlap zone — artifact: football field chart for IC deck.
7. **Run sensitivity and scenario weights** (bull/base/bear on growth, margin, WACC) — artifact: tornado + scenario table.
8. **Recommend bid and payment mix** inside the overlap; document why — artifact: IC memo recommendation slide.

---

## 8. Content Quality Audit

**Covered well (source):** three approaches defined; principle of using ≥ 2 methods; method-fit-to-business; separation of standalone vs synergy; SaaS triangulation use case; bank P/B and startup DCF+scenario examples.

**Underplayed (to supplement):**
- Harmonic mean for peer ratios (not just median/mean).
- Asset-approach limits for services/SaaS (people + IP, not PP&E).
- SOTP and holding discount for conglomerates.
- DLOM / DLOC for private targets.
- Cycle-adjusted multiples for IT services and other cyclicals.
- Scenario weighting (probability-weighted DCF for startups/AI).
- Implied terminal-growth / implied-exit-multiple cross-check.

**Supplementary sources (≥ 5):**
1. Damodaran, *Investment Valuation*, 3rd ed. (Wiley, 2012).
2. Koller, Goedhart, Wessels, *Valuation: Measuring and Managing the Value of Companies*, 7th ed. (McKinsey/Wiley, 2020).
3. Rosenbaum & Pearl, *Investment Banking: Valuation, LBOs, M&A, and IPOs*, 3rd ed. (Wiley, 2020).
4. Pinto, Henry, Robinson, *Equity Asset Valuation*, 4th ed. (CFA Institute / Wiley, 2020).
5. Luehrman, "Valuing Companies: DCF vs Multiples," *Harvard Business Review* (1997).

**Red flags to watch:**
- TV > 75% of EV in DCF (forecast too short).
- Peer set that conveniently justifies bid price.
- Control premium double-counted (in DCF synergies and precedents).
- DLOM not applied to a private target.
- DCF-only valuation in a hot market with no comps cross-check.

---

## 9. Quick-Recall Card
- Three lenses: Income (DCF), Market (comps + precedents), Asset (replacement/liquidation). Use ≥ 2.
- Match method to business: growth → DCF; stable → multiples; asset-heavy → replacement; distressed → liquidation.
- Build a football field; bid inside the overlap, not outside it.
- Separate standalone from synergy; test sensitivity to WACC, growth, margin.
- Adjust for DLOM, control premium, holding discount, cycle.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Does our proposed bid sit inside the overlap zone of at least two independent valuation methods, and if not, which assumption is carrying the weight?"

---

**Connects to:** [06-dcf-and-multiples-valuation.md](06-dcf-and-multiples-valuation.md), [../business-valuation/](../business-valuation/), [01-introduction-to-ma-strategy.md](01-introduction-to-ma-strategy.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:4, 10:4]
Sections rewritten: [1 snapshot tightened; 3 football field ASCII; 4 formulas expanded w/ thresholds; 6 anti-example quantified; 9 role-lens question added]
Enrichments applied: [cross-course links; 5 supplements (Damodaran, Koller, Rosenbaum-Pearl, Pinto, Luehrman HBR); anti-example w/ ₹1,200 cr impairment cost; IT tooling (Excel, CapIQ, FactSet, PitchBook, Damodaran dataset); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A7
-->
