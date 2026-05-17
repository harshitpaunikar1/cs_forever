# Discounted Cash Flow (DCF) Models

## Overview

A DCF model values a business as the sum of its future free cash flows, each discounted to today at the cost of capital. It is the most rigorous valuation method because it forces explicit assumptions on growth, margins, and risk. Done well, it reveals what a company is fundamentally worth, regardless of market mood.

---

## Why It Matters

Markets swing on sentiment; DCF anchors you to economics. Managers use it to test whether share prices, bids, or project returns make sense. A good DCF also tells you what you are implicitly assuming, which is often more useful than the final number.

## Key Principles

- Forecast 5–10 years of free cash flow, then add a terminal value.
- Use free cash flow to firm (FCFF) with WACC, or free cash flow to equity (FCFE) with cost of equity.
- Terminal value often drives 60–80% of the answer — stress-test it.
- Growth and discount rate assumptions must be internally consistent.
- Always run a sensitivity table; a single-point DCF answer is rarely trustworthy.

## Key Terms

| Term | Definition |
|------|------------|
| **FCFF** | Free cash flow available to all capital providers (debt and equity). |
| **WACC** | Weighted average cost of capital, used to discount FCFF. |
| **Terminal Value** | Value of cash flows beyond the forecast period, usually via Gordon growth. |
| **Enterprise Value** | Value of the whole business before subtracting net debt. |

## Use Case

An investment bank advising on a sale builds a DCF model to anchor the price range it will negotiate with bidders, alongside multiples-based cross-checks.

## Scenario

> A consumer brand was trading at 2,000 crore market cap. A DCF with 8% long-term growth and a 10% WACC implied a fair value of 2,700 crore. The fund took a stake, pushed for faster margin expansion, and exited 3 years later at 3,500 crore — roughly what the original DCF had already flagged.

## Examples

- A stable utility DCF uses a 3% perpetual growth rate and 7% WACC.
- A high-growth tech DCF uses a 2-stage model: 20% growth for 5 years, then 4% terminal.

---

## Audited Appendix

# Discounted Cash Flow (DCF) Models
**Course:** Business Valuation
**Module:** Content / DCF Models
**Audited on:** 2026-04-18
**Audited by:** A2
**Source files reviewed:** `business-valuation/content/05-discounted-cash-flow-dcf-models.md`

---

## 1. Topic Snapshot
DCF values a business as the sum of its future free cash flows, each discounted back to today at the cost of capital — the most rigorous method because it forces explicit assumptions on growth, margins, and risk. For an IT/AI/Product/Consulting leader evaluating a SaaS target, an AI-platform build-vs-buy, or a consulting-practice buyout, DCF anchors the conversation to underlying economics when market multiples swing wildly. The decision it supports: is the ask price / bid / internal project return defensible, or are we paying for someone else's optimistic story?

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|------|-----------|---------------|---------------|--------------|-------------------|
| FCFF | Free Cash Flow to Firm | Cash available to all capital providers (debt + equity) after reinvestment | Isolates operating economics from capital structure | EBIT(1-t) + D&A - Capex - ΔWC | i-bank pitch decks, CFO reviews |
| FCFE | Free Cash Flow to Equity | Cash available to equity holders after debt service | Needed when modelling levered returns | FCFF - Interest(1-t) - Net Debt Repayment | PE buyout models |
| WACC | Weighted Avg Cost of Capital | Blended hurdle rate across debt & equity | Discount rate matched to FCFF | (E/V)·Ke + (D/V)·Kd·(1-t) | Every DCF memo |
| Cost of Equity (Ke) | Ke | Return equity holders demand | Prices equity risk | CAPM: Rf + β·ERP | Fairness opinions |
| Terminal Value | TV | PV of cash flows beyond forecast horizon | Explicit forecast can't run forever | Gordon or Exit Multiple | 60–80% of DCF output |
| Gordon Growth Model | GGM | TV assuming constant perpetual growth | Closed-form perpetuity | FCFF_{n+1}/(WACC-g) | Stable businesses |
| Exit Multiple TV | EM-TV | TV via market multiple on terminal EBITDA | Market-anchored check | EBITDA_n × multiple | PE, sponsor models |
| Explicit Forecast Period | EFP | 5–10 yr projection window | Period where line-item forecasts are credible | Years chosen by analyst | Model structure |
| Implied Perpetuity Growth | Implied g | Back-solved g from an Exit Multiple TV | Sanity check | Reverse Gordon | Senior reviewer questions |
| Mid-Year Convention | MYC | Discounts assuming cash arrives mid-period | More realistic than year-end | Factor of 0.5 on t | Industry-standard models |
| Enterprise Value | EV | Whole-business value pre net-debt | Capital-structure neutral | Σ PV(FCFF) + PV(TV) | Every valuation doc |
| Equity Value | EqV | Value attributable to shareholders | What a buyer writes the cheque for | EV - Net Debt - Minority + Cash | SPA negotiations |
| NPV | Net Present Value | PV of flows minus upfront investment | Project-level go/no-go | ΣFCF/(1+r)^t - I₀ | Capex committee |
| IRR | Internal Rate of Return | Discount rate at which NPV = 0 | Compare to hurdle rate | Root-find on NPV=0 | Investment committees |
| Sensitivity / Tornado | Tornado | Single-variable impact ranking | Shows which inputs matter | Vary ±x%, rank ΔEV | Board-ready decks |
| Scenario Analysis | Scenarios | Coherent input bundles (base/bull/bear) | Captures correlated moves | Probability-weight EVs | Strategy reviews |
| 2-Stage Model | 2-Stage | High-growth stage + stable perpetuity | Most early-stage/tech valuations | Explicit EFP + GGM TV | SaaS / AI deals |
| 3-Stage Model | 3-Stage | Growth + fade + stable | Models competitive-advantage decay | EFP + fade + GGM | Mature franchise valuations |
| Implied Terminal EV/EBITDA | Implied Multiple | EV/EBITDA hiding inside a Gordon TV | Cross-check vs trading comps | TV / EBITDA_n | Every DCF review |

---

## 3. Frameworks & Matrices

### 3.1 2-Stage DCF Structure
**Purpose:** Standard workhorse for IT/SaaS/AI targets with a high-growth runway fading to a stable tail.

```
  Year:   1    2    3    4    5    |   Terminal
  FCFF:  F1   F2   F3   F4   F5    |   F5·(1+g)/(WACC-g)
         |    |    |    |    |         |
   ÷   (1+w) (1+w)² …          (1+w)^5  ÷ (1+w)^5
         ↓    ↓    ↓    ↓    ↓         ↓
        PV₁  PV₂  PV₃  PV₄  PV₅       PV(TV)
                   \\___________+___________/
                                |
                               EV
```
**Components:** explicit FCFF forecast, WACC, terminal growth g, discount factors, TV.
**Worked example — SaaS target:** ARR ₹500 cr, FCFF Y1–5 = 60, 85, 115, 145, 175 (₹ cr); WACC 12%; g 3%. PV of explicit FCFFs ≈ ₹410 cr. TV = 175·1.03/(0.12-0.03) ≈ ₹2,003 cr; PV(TV) ≈ ₹1,137 cr. EV ≈ ₹1,547 cr.
**Trigger:** any single-bet SaaS/AI acquisition or internal platform NPV.

### 3.2 TV Method Selector (Gordon vs Exit Multiple)
**Purpose:** Choose TV approach without flipping a coin.

```
                Is terminal year steady-state?
                       /            \
                     Yes             No → extend forecast
                      |
          Are comparable exit multiples reliable?
                   /          \
                 Yes           No
                  |             |
         Use BOTH; cross-check  Use Gordon only;
         implied g vs implied   stress g and WACC
         multiple; explain gap
```
**Components:** steady-state test, comp availability, reasonableness bands.
**Worked example — AI platform:** no clean public comps at terminal state → Gordon with g = 3% (long-run GDP proxy) + sensitivity band 2–4%.
**Trigger:** before finalising any TV number.

### 3.3 Sensitivity Tornado / Grid — WACC × g
**Purpose:** Communicate uncertainty; no point estimates in boardrooms.

```
            g = 2.0%   2.5%   3.0%   3.5%   4.0%
WACC 10%     1,710   1,820   1,950   2,110   2,310
WACC 11%     1,510   1,595   1,695   1,810   1,950
WACC 12%     1,360   1,430   1,510   1,600   1,705  ← base
WACC 13%     1,240   1,295   1,360   1,430   1,510
WACC 14%     1,140   1,185   1,240   1,295   1,360
                                             (₹ cr EV)

Tornado (base EV ₹1,510 cr):
  WACC ±1pp       ████████████████  ±₹190 cr
  Terminal g ±1pp ██████████        ±₹115 cr
  Y5 margin ±2pp  ████████          ±₹95 cr
  Revenue CAGR ±3pp ██████          ±₹70 cr
  Capex intensity ±1pp ████         ±₹45 cr
```
**Components:** ranked input shocks, EV deltas, base highlighted.
**Worked example:** above table for the same SaaS target shows WACC dominates — focus diligence on beta and capital structure assumption.
**Trigger:** every committee memo.

### 3.4 (Optional) DCF Sanity-Check Triangle
```
                DCF (intrinsic)
                      /\
                     /  \
                    /    \
        Trading Comps ── Precedent Transactions
```
All three ranges should overlap within ±15% or you owe the committee an explanation.

---

## 4. Formulas

1. **Enterprise Value**
   EV = Σₜ₌₁ⁿ [FCFFₜ / (1+WACC)ᵗ] + TV / (1+WACC)ⁿ
   *Threshold:* TV share 60–80% is typical; >85% → forecast too short.
   *Example:* ₹410 cr explicit + ₹1,137 cr TV = ₹1,547 cr (TV share 73%).

2. **Gordon Growth TV**
   TV = FCFF_{n+1} / (WACC − g)
   *Threshold:* g < long-run nominal GDP (≈ 5–6% India, 3–4% US); WACC − g ≥ 3pp to avoid instability.
   *Example:* 175·1.03 / (0.12 − 0.03) = ₹2,003 cr.

3. **Exit Multiple TV**
   TV = EBITDA_n × multiple
   *Threshold:* multiple ≤ current trading comps median; avoid peak-cycle multiples on terminal year.
   *Example:* SaaS target Y5 EBITDA ₹220 cr × 10x = ₹2,200 cr.

4. **Implied Terminal Growth (reverse Gordon from Exit Multiple)**
   g_implied = WACC − (FCFF_{n+1} / TV_ExitMultiple)
   *Threshold:* If g_implied > 4–5% you're smuggling in growth.
   *Example:* TV ₹2,200 cr, FCFF_{n+1} ₹180 cr, WACC 12% → g_implied = 12% − 180/2,200 = 3.8%. Just-about defensible.

5. **Equity Value Bridge**
   EqV = EV − Net Debt − Minority Interest − Preferred + Cash (+ non-operating assets)
   *Threshold:* reconcile to target's latest balance sheet date; adjust for deal-close cash.
   *Example:* EV ₹1,547 cr − Debt ₹200 cr − Minority ₹30 cr + Cash ₹80 cr = ₹1,397 cr equity.

6. **(Optional) Mid-Year Convention**
   Discount factor = 1 / (1+WACC)^(t − 0.5)
   *Threshold:* lifts EV by ~(WACC/2); document convention in model notes.
   *Example:* WACC 12% → EV lifts ~5.8%; our ₹1,547 cr → ~₹1,637 cr.

---

## 5. Do vs Don't

| Do | Don't |
|----|-------|
| Discount FCFF with WACC and FCFE with Cost of Equity — keep them matched. | Don't mix FCFF with Cost of Equity (double-counts leverage). |
| Cap terminal g at long-run nominal GDP. | Don't set g ≥ LT GDP; no company outgrows the economy forever. |
| Expense Stock-Based Compensation in FCF for SaaS/AI targets. | Don't treat SBC as non-cash "add-back"; it's real dilution. |
| Always present a WACC × g grid and tornado. | Don't hand over a point-estimate EV without sensitivity. |
| Use a *target* capital structure for WACC weights. | Don't lock in today's (possibly distorted) leverage if the plan is to re-capitalise. |
| Limit explicit forecast to the competitive-advantage period (CAP); fade thereafter. | Don't forecast 15 years of 30% growth — market will compete it away. |
| Cross-check Gordon TV vs implied exit multiple (and vice-versa). | Don't rely on one TV method without triangulating the other. |
| Normalise terminal-year margin, capex, and working capital to steady-state. | Don't anchor TV on a peak-margin year. |

---

## 6. Real-Life Scenarios

### Scenario 1 — Valuing a SaaS Target (Product/M&A lens)
₹500 cr ARR, 85% GRR, 115% NRR. Build 2-stage DCF: Y1–5 FCFF grows 45% → 18%; WACC 12%; g 3%; mid-year convention. EV ≈ ₹1,600 cr. Cross-check: trading comps 8–11x ARR → ₹4,000–5,500 cr range (they value growth optionality). Precedent deals at 6x ARR → ₹3,000 cr. Gap forces a story: are you paying for intrinsic cash or market-implied optionality? Outcome: bid anchored at ₹2,800 cr with earn-out closing the gap.

### Scenario 2 — Internal AI Platform Build vs Buy (AI Lead/Consulting lens)
In-house AI inference platform: ₹60 cr upfront, ₹8 cr annual opex, projected margin-expansion FCFs Y1–5 = 5, 15, 28, 40, 55 (₹ cr). TV via Exit Multiple on Y5 run-rate benefit (8x) = ₹440 cr. WACC 14% (risk-adjusted for execution). NPV ≈ ₹185 cr; IRR ≈ 38%. Build wins vs buy-license quote of ₹280 cr NPV. Caveat: tornado shows adoption rate is the swing variable → gate spend on a 12-month pilot KPI.

### Scenario 3 — ANTI-EXAMPLE: Terminal-Value Abuse (Consulting review)
Target consumer-tech: WACC 11%, g set at 5% (analyst "because India grows fast"). TV = ₹4,000 cr; EV = ₹5,200 cr; deal closes at ₹5,000 cr. Recomputing with g capped at 3.5%: TV falls to ₹2,700 cr, EV to ₹3,850 cr — a **~35% inflation** in the bid. At exit 3 years later, competitive fade lands the business at ₹3,500 cr EV → buyer realises ~₹1,500 cr of value destruction (quantified: ₹5,000 cr paid − ₹3,500 cr exit). Root cause: single-input TV abuse with no sensitivity or implied-multiple cross-check.

**Tools:** Excel / Google Sheets, Capital IQ, FactSet, Bloomberg, Anaplan, Looker, Python (numpy / scipy for Monte Carlo), @Risk, PitchBook.

---

## 7. Implementation Playbook

1. **Define** the decision (bid, build/buy, fairness opinion) and the unit of value (EV or Equity).
2. **Build** a 5–10 yr FCFF model tied to a revenue / cohort / unit-economics driver tree.
3. **Estimate** WACC with a target capital structure, industry beta, and Rf/ERP sourced from Damodaran updates.
4. **Construct** TV via Gordon and cross-check the implied exit multiple against trading comps; disclose both.
5. **Bridge** EV to Equity with a dated net-debt schedule; flag off-balance-sheet items (leases, earn-outs, pension).
6. **Stress-test** via tornado (≥5 variables) and 3 coherent scenarios; report a range, not a point.
7. **Triangulate** DCF vs trading comps vs precedent transactions; write the football-field chart.
8. **Document** assumptions, sources, and reviewer sign-offs in a model-audit log.

---

## 8. Content Quality Audit

**Covered well:** core DCF mechanics, 2-stage structure, TV as dominant driver, sensitivity requirement, EV-to-Equity bridge, FCFF/WACC vs FCFE/Ke matching.

**Underplayed in source:**
- Terminal-value abuse and the implied-multiple cross-check.
- Competitive-advantage period (CAP) and explicit fade modelling.
- Normalisation of terminal-year margins, capex, and working capital.
- SBC treatment in SaaS/AI FCF (non-trivial for high-growth targets).
- Monte Carlo simulation on correlated inputs (not just 1-D tornado).
- Real-options overlay for optionality-heavy AI / platform bets.

**Supplementary sources (≥5):**
1. Damodaran, *Investment Valuation*, 3rd ed., 2012 — especially chapters on growth patterns and TV.
2. Koller, Goedhart & Wessels (McKinsey), *Valuation: Measuring and Managing the Value of Companies*, 7th ed., 2020.
3. Pinto, Henry & Robinson (CFA Institute), *Equity Asset Valuation*, 4th ed., 2020.
4. Mauboussin & Callahan, *Expectations Investing*, updated ed., 2021 — reverse-DCF / market-implied expectations.
5. Luehrman, "Using APV: A Better Tool for Valuing Operations," *HBR*, 1997, and Luehrman, "Investment Opportunities as Real Options," *HBR*, 1998.

**Red flags in source:** ₹2,700 cr DCF on a brand with 8% LT growth + 10% WACC is arithmetically fine but 8% is perilously close to nominal GDP — should be framed as an aggressive growth case, not a base case. Source also conflates "LT growth" with "stage-1 growth" without distinguishing; readers may set g = 8% in Gordon by mistake.

---

## 9. Quick-Recall Card

- DCF = Σ PV(FCFF) + PV(TV), discounted at WACC; TV usually 60–80% of answer.
- Match numerators to denominators: FCFF ↔ WACC; FCFE ↔ Ke.
- Cap terminal g ≤ long-run nominal GDP; always cross-check implied exit multiple.
- Every DCF ships with a WACC × g grid, tornado, and 3 scenarios.
- Triangulate with trading comps and precedents — DCF alone is a story, not a proof.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: *what set of growth, margin, and risk assumptions must be true for the asking price (or my internal build case) to earn its cost of capital — and which of those assumptions is the least defensible?*

---

**Connects to:** [03-cash-flow-valuation.md](03-cash-flow-valuation.md), [04-time-value-of-money.md](04-time-value-of-money.md), [06-wacc-calculations.md](06-wacc-calculations.md), [09-valuation-for-m-and-a.md](09-valuation-for-m-and-a.md), [../mergers-acquisitions/06-dcf-and-multiples-valuation.md](../mergers-acquisitions/06-dcf-and-multiples-valuation.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [2 expanded to 19 terms; 3 added sanity-check triangle; 4 added mid-year; 6 quantified anti-example; 9 role-lens question]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ cost; IT tooling; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:32
Audited by: A2
-->
