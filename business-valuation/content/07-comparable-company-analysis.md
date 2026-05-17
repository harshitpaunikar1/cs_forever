# Comparable Company Analysis

## Overview

Comparable company analysis — "comps" — values a business by looking at how similar listed companies are priced in the market. The idea: if peers trade at 10x earnings, your company should trade near that too, adjusted for size and growth. It is a market-based cross-check on any DCF.

---

## Why It Matters

Comps reflect what buyers will actually pay right now, not what a model says. Bankers, investors, and managers use them to sanity-check valuations and set price expectations. Misapplied comps — wrong peers, wrong multiple — give false confidence and expensive mistakes.

## Key Principles

- Peer selection is everything — match industry, size, growth, and geography.
- Use forward multiples where possible (next-year EBITDA or earnings).
- EV/EBITDA is the workhorse multiple; P/E works for stable-leverage comparisons.
- Adjust for non-recurring items in both target and peer financials.
- Apply a control or illiquidity discount when valuing private companies.

## Key Terms

| Term | Definition |
|------|------------|
| **EV/EBITDA** | Enterprise value divided by earnings before interest, tax, depreciation, amortization. |
| **P/E Ratio** | Share price divided by earnings per share. |
| **Peer Group** | Listed companies with similar business models and financial profiles. |
| **Liquidity Discount** | Valuation haircut applied when shares cannot be easily sold. |

## Use Case

A private company preparing for an IPO builds a comp table of listed peers to set an initial price range for the offering document.

## Scenario

> A food-delivery start-up planning a private round looked at three listed peers trading at 4–6x revenue. Applying 5x to its own 800 crore revenue gave an indicative 4,000 crore valuation. The round closed at 3,800 crore after a small private-company discount — exactly where the comps predicted.

## Examples

- A cement company is valued at the sector median EV/EBITDA of 9x.
- A niche luxury brand is valued at a 30% premium to the broader apparel peer group.

---

## Audited Appendix

# Comparable Company Analysis
**Course:** Business Valuation
**Module:** Content / Comparable Company Analysis
**Audited on:** 2026-04-18
**Audited by:** A4
**Source files reviewed:** `business-valuation/content/07-comparable-company-analysis.md`

---

## 1. Topic Snapshot
Trading comps value a business by benchmarking it against how similar listed companies are priced today — if peers trade at 10x forward earnings, the target should trade near that, adjusted for size, growth, and geography. For an IT/AI/Product/Consulting leader benchmarking own firm, preparing a fundraise/IPO, or advising a client, comps reflect what buyers will actually pay now, not what a DCF model asserts. Decision: anchor a defensible price range (floor, midpoint, ceiling) that survives investor scrutiny and aligns with market reality.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|------|-----------|---------------|---------------|--------------|-------------------|
| EV/EBITDA | Enterprise Value / EBITDA | Price of the whole business vs cash earnings | Capital-structure neutral workhorse | EV ÷ LTM or NTM EBITDA | IT services, mid-cap industrials |
| EV/Revenue | Enterprise Value / Revenue | Price per rupee of sales | Works when EBITDA is negative | EV ÷ Revenue | Early-stage SaaS, marketplaces |
| EV/ARR | Enterprise Value / Annual Recurring Revenue | Price per rupee of recurring SaaS revenue | SaaS quality of revenue matters | EV ÷ ARR | Cloud SaaS, Bessemer Cloud Index |
| P/E (Trailing) | Price / Earnings (LTM) | Market price per ₹1 of past earnings | Quick stable-company check | Share price ÷ trailing EPS | Listed IT majors, consulting roll-ups |
| P/E (Forward) | Price / Earnings (NTM) | Price per ₹1 of next-year earnings | Captures growth expectations | Share price ÷ forecast EPS | Sell-side research |
| PEG Ratio | Price/Earnings-to-Growth | P/E adjusted for growth rate | Compares firms at different growth stages | P/E ÷ earnings growth % | Growth-tech coverage |
| Price/Sales | Price / Sales per share | Equity price per rupee of revenue | Simple, no EBITDA required | Market cap ÷ revenue | Consumer tech, retail |
| Price/Book | Price / Book Value | Equity price vs accounting net assets | Asset-heavy / financial firms | Market cap ÷ book equity | Banks, BFSI |
| Peer Group | — | Set of listed comparables | Single stock is noise; set is signal | 4–8 curated names | Every comps deck |
| Pure-Play Peer | — | Company in one clean business line | Avoids conglomerate distortion | Revenue mix >80% in segment | SaaS sub-segment coverage |
| Forward Multiple | NTM multiple | Based on next-year forecast | Valuation is forward-looking | EV ÷ forecast metric | Equity research |
| Trailing Multiple | LTM multiple | Based on last-12-month actuals | Anchored in audited reality | EV ÷ LTM metric | Annual reports |
| Control Premium | — | Uplift for buying control | Control = synergies + cash-flow rights | ~20–30% over trading price | M&A advisory |
| Liquidity/Marketability Discount (DLOM) | Discount for Lack of Marketability | Haircut for shares not easily sold | Private shares lack exits | ~15–30% off public multiple | Private placements, 409A |
| Size Premium/Discount | — | Adjustment for scale difference | Small firms riskier | 10–25% haircut | Small/mid-cap valuation |
| Harmonic Mean | — | Reciprocal-based average of multiples | Prevents outliers from skewing | n ÷ Σ(1/xi) | Academic + practitioner comps |
| EV/GMV | EV / Gross Merchandise Value | Price per rupee of platform volume | Marketplaces don't keep GMV | EV ÷ GMV | Food delivery, e-commerce |
| EV/Customer | EV / number of customers | Price per subscriber/user | Consumer-scale businesses | EV ÷ paid customer count | Telecom, D2C |
| Rule of 40 | Growth % + EBITDA margin % ≥ 40 | SaaS quality threshold | Balances growth vs profit | Growth + margin | Cloud SaaS investor decks |
| Magic Number | Net New ARR / Prior Q S&M spend | Sales efficiency ratio | Is GTM spend productive? | ΔARR ÷ S&M | SaaS board reviews |
| LTV/CAC | Lifetime Value / Customer Acquisition Cost | Unit economics ratio | Is the funnel profitable? | LTV ÷ CAC (target ≥3×) | PLG and SaaS boards |

---

## 3. Frameworks & Matrices

### 3.1 Peer Selection Funnel
**Purpose:** narrow ~200 listed names to 4–8 credible comps.

```
[Industry universe ~200]
          |
   Industry / sub-sector filter
          v
     [~50 names]
          |
   Size filter (revenue ±2x target)
          v
     [~25 names]
          |
   Growth band (±10 pts of target CAGR)
          v
     [~12 names]
          |
   Geography / regulation
          v
     [~8 names]
          |
   Business model (pure-play)
          v
  [4–8 final comps] -> compute multiples
```

**Components:** sector, size, growth, geography, business model, float/liquidity.
**IT/AI/Product/Consulting example:** AI-SaaS target (₹80 cr ARR, 50% growth, India+US) → filter to pure-play AI/data SaaS between ₹400–2,000 cr revenue, 30–70% growth → 6 peers (3 US, 2 India-listed, 1 global).
**Trigger:** any new valuation deck or 409A refresh.

### 3.2 Multiple Selection Matrix

| Profitability ↓ / Model → | Recurring (SaaS) | Transaction/Marketplace | Services/Consulting | Capital-intensive |
|---|---|---|---|---|
| Profitable, stable | EV/EBITDA + P/E | EV/EBITDA + EV/GMV | EV/EBITDA | EV/EBITDA, P/B |
| Profitable, growth | EV/ARR + Rule-of-40 | EV/Revenue + EV/GMV | EV/EBITDA + PEG | EV/EBITDA |
| Unprofitable, growth | EV/ARR, EV/Revenue | EV/GMV, EV/Revenue | EV/Revenue | EV/Revenue |
| Unprofitable, slow | avoid multiples, use DCF | EV/GMV with caveats | EV/Revenue + margin bridge | P/B + replacement cost |

**Trigger:** before picking a headline multiple — never default to "what looks reasonable."

### 3.3 Comps Football Field

```
Valuation (₹ cr)   2,000   3,000   4,000   5,000   6,000
                    |-------|-------|-------|-------|
EV/ARR (peers 8-12x)          [====================]
EV/Revenue (4-6x)       [================]
Precedent txns                        [===========]
DCF base-case                 [==============]
52-week high/low (if listed)        [=========]
                    |-------|-------|-------|-------|
Concluded range: ₹3,500–4,500 cr; midpoint ₹4,000 cr
```

**Components:** each method as a horizontal bar; overlap zone = defensible range.
**Example:** Series C AI-SaaS target lands at ₹3,500–4,500 cr pre-money, anchored by EV/ARR + DCF cross-check.
**Trigger:** fairness opinions, board price-range approval, IC memo.

### 3.4 SaaS Growth-Profit 2x2 (Optional)

```
                High Growth (>40%)
                       |
   EV/ARR premium      |   EV/ARR + Rule-of-40
   (land-grab mode)    |   premium (best quadrant)
  ---------------------+---------------------
   Avoid multiples;    |   EV/EBITDA standard
   fix unit economics  |   (mature SaaS)
                       |
                Low Growth (<20%)
        Low Margin <--- | ---> High Margin
```

**Trigger:** chooses which multiple anchors value for a SaaS target.

---

## 4. Formulas

### 4.1 EV/EBITDA
`EV/EBITDA = Enterprise Value / EBITDA`
**Threshold:** IT services 12–18x; cement 8–10x; luxury consumer 20–30x.
**Example:** listed cement peer EV ₹9,000 cr, EBITDA ₹1,000 cr → 9x. Apply 9x to target EBITDA of ₹300 cr → EV ₹2,700 cr.

### 4.2 EV/ARR (SaaS)
`EV/ARR = Enterprise Value / Annual Recurring Revenue`
**Threshold:** 2024–2026 range 5–10x for median SaaS; 10–15x for Rule-of-40 leaders.
**Example:** AI SaaS target ARR ₹80 cr, growth 50% → peers trade 8–12x forward ARR → EV range ₹640–960 cr.

### 4.3 PEG
`PEG = (P/E) / (Earnings Growth %)`
**Threshold:** PEG < 1 generally undervalued; > 2 rich.
**Example:** IT peer P/E 30, growth 20% → PEG 1.5. Target P/E 25, growth 25% → PEG 1.0 → cheaper on growth-adjusted basis.

### 4.4 Harmonic Mean of Multiples
`Harmonic Mean = n / Σ(1/xi)`
**Why preferred:** aggregates price/value ratios consistently; damps high-multiple outliers.
**Example:** peer EV/EBITDA = {8, 10, 12, 25}. Arithmetic mean = 13.75 (skewed by 25). Harmonic mean = 4 / (1/8 + 1/10 + 1/12 + 1/25) = 4 / 0.3583 = 11.16 → a more defensible central multiple.

### 4.5 Peer Median + IQR Range (Optional)
`Low = 25th percentile multiple; High = 75th percentile; Mid = median`
**Example:** 8 peers, EV/Revenue IQR 4.2x–5.8x, median 4.9x. Target revenue ₹800 cr → range ₹3,360–4,640 cr, mid ₹3,920 cr. After 15% private liquidity discount → concluded ₹3,300–3,950 cr (consistent with the food-delivery closed-at-₹3,800 cr case).

---

## 5. Do vs Don't

| Do | Don't |
|----|-------|
| Curate 4–8 pure-play peers by industry, size, growth, geography | Don't throw 20 dissimilar names into a peer set to look thorough |
| Prefer NTM/forward multiples for valuation decisions | Don't mix trailing multiples for one peer with forward for another |
| Apply liquidity/marketability discount (15–30%) for private targets | Don't forget DLOM — inflates private valuation by 20%+ |
| Use harmonic mean or median when one peer is an outlier | Don't use arithmetic mean blindly when range is skewed |
| Use EV/EBITDA when peers have differing leverage | Don't use P/E across companies with very different debt loads |
| Normalize for size and growth differences (regression or tiering) | Don't ignore that a ₹500 cr firm cannot trade like a ₹50,000 cr firm |
| Pick the multiple before looking at the answer | Don't reverse-engineer: pick the multiple that "looks reasonable" |
| Strip non-recurring items (litigation, COVID-relief, one-time grants) in target AND peers | Don't compare cleaned target EBITDA to peers' reported EBITDA |
| Refresh comps at least quarterly; note cycle-sensitivity | Don't use 2021 cloud multiples in 2024 — tech multiples compressed ~50% |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS Series C Fundraise
Indian AI-SaaS company, ARR ₹80 cr, 50% YoY growth, EBITDA margin -10% (Rule-of-40 = 40). Build peer set: 6 listed global AI/data SaaS (Snowflake-like, Datadog-like, MongoDB-like, plus 2 India-listed SaaS). Median forward EV/ARR = 10x, Rule-of-40 leaders premium at 12x. Target sits at the median → EV ₹800 cr, apply 15% DLOM for late-stage private → ₹680 cr concluded; pre-money anchor for Series C term sheet.

### Scenario 2 — IT-Services Consulting Firm Benchmarking
Mid-size IT consulting firm, ₹1,200 cr revenue, EBITDA ₹240 cr (20% margin), 18% growth. Peers: listed Indian mid-cap IT (Mphasis-tier, Coforge-tier, Persistent-tier). Median forward EV/EBITDA = 15x → EV ₹3,600 cr. Cross-check with EV/Revenue 3x → ₹3,600 cr (consistent). Decision: board sets ₹3,400–3,800 cr as strategic-sale reservation price.

### Scenario 3 — ANTI-EXAMPLE: Stale Multiples (Cost Quantified)
US-India tech product startup in early 2024 anchored its pre-money at 18x ARR citing 2021 cloud comps. Actual 2024 median was ~7x. Target ARR ₹100 cr → they asked ₹1,800 cr; market would pay ₹700 cr. Overvaluation ~40% of ask. Round failed; 9-month delay burned ₹45 cr of cash runway, forced a down-round at ₹600 cr, ~67% dilution to founders vs. original plan. Quantified cost: ₹45 cr cash + ~25 pts extra dilution — a direct result of ignoring multiple compression.

**Tools:** S&P Capital IQ, PitchBook, Bloomberg, FactSet, Bessemer Cloud Index (public SaaS), Meritech Public Comps, Carta (private comps / 409A), Tracxn (India private deals), Refinitiv.

---

## 7. Implementation Playbook
1. **Define** target business model, growth, geography, profitability profile (one-page brief).
2. **Build** peer universe via Peer Selection Funnel → shortlist 4–8 pure-plays.
3. **Extract** LTM and NTM financials from CapIQ/Bloomberg; compute EV for each peer (market cap + debt − cash + minority interest + preferred).
4. **Compute** full multiple grid (EV/Revenue, EV/EBITDA, EV/ARR where applicable, P/E, PEG); flag outliers.
5. **Normalize** target and peer metrics — strip one-offs, align fiscal calendars, adjust for stock-based comp (SaaS).
6. **Apply** median, harmonic mean, and IQR; select the right multiple per Section 3.2 matrix.
7. **Adjust** for size, growth, control premium (if M&A), DLOM (if private); build Comps Football Field.
8. **Document** concluded range with sensitivity, committee memo, and refresh cadence (quarterly).

---

## 8. Content Quality Audit

**Covered well in source:** comps as a market cross-check; EV/EBITDA as workhorse; peer selection importance; forward-over-trailing preference; private-company liquidity discount; food-delivery and cement numeric examples.

**Underplayed / missing in source:**
- Harmonic mean vs arithmetic mean — source doesn't mention aggregation method, yet this changes conclusions when outliers exist.
- Forward vs trailing discipline — stated as preference but not operationalized.
- SaaS Rule-of-40 adjustment and EV/ARR banding (critical for AI/Product leaders today).
- Control premium rules for M&A (20–30%) separate from DLOM.
- Liquidity discount bands (15–30%) and when to use each.
- Cycle-sensitivity: 2021 vs 2024 multiple compression (~50% in cloud SaaS).
- Regression-based size/growth adjustment (Damodaran's approach).

**Supplements (≥5 sources):**
1. Damodaran, A. *Investment Valuation*, 3rd ed. (Wiley, 2012) — Ch. 17–19 on relative valuation.
2. Koller, Goedhart, Wessels. *Valuation: Measuring and Managing the Value of Companies*, 7th ed. (McKinsey/Wiley, 2020) — multiples chapter.
3. Rosenbaum & Pearl. *Investment Banking*, 3rd ed. (Wiley, 2020) — Ch. 1 Comparable Companies Analysis.
4. Bessemer Venture Partners. *BVP Cloud Index* — quarterly 2024 reports on EV/ARR bands and Rule-of-40.
5. Mauboussin, M. "What Does a Price-Earnings Multiple Mean?" (Credit Suisse / HBR-adjacent, 2014) — on when multiples mislead.
6. Meritech Capital. *Public SaaS Comps* (updated quarterly, 2024) — sector medians.

**Red flags in source:**
- No mention of harmonic mean.
- "4–6x revenue" cited for food delivery without period/context — multiples are cycle-sensitive.
- No guidance on size/growth regression adjustment.
- Private-discount magnitude not quantified (just "private discount").

---

## 9. Quick-Recall Card
- Comps = what the market will actually pay today; DCF = what the model says it should.
- Peer selection is 80% of the work: industry, size, growth, geography, model.
- Prefer forward multiples; EV/EBITDA is the workhorse; EV/ARR + Rule-of-40 for SaaS.
- Use harmonic mean/median; strip non-recurring on both sides; apply DLOM 15–30% for private.
- Refresh quarterly — tech multiples compressed ~50% from 2021 to 2024.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "What price range will the market actually support for my business today, and which peers and multiples defend that range?"

---

**Connects to:** [05-discounted-cash-flow-dcf-models.md](05-discounted-cash-flow-dcf-models.md), [08-precedent-transaction-analysis.md](08-precedent-transaction-analysis.md), [11-start-up-valuation.md](11-start-up-valuation.md), [../mergers-acquisitions/06-dcf-and-multiples-valuation.md](../mergers-acquisitions/06-dcf-and-multiples-valuation.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [2 (expanded to 20 terms), 3 (added football field + 2x2), 4 (added harmonic mean numeric), 6 (added quantified anti-example), 8 (added 6 supplements + red flags)]
Enrichments applied: [cross-course links; 6 supplements; anti-example w/ ₹45 cr + 25pt dilution cost; IT tooling (CapIQ, Bessemer, Meritech, Carta, Tracxn); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A4
-->
