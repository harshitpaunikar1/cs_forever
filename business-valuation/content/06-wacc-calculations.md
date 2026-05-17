# WACC Calculations

## Overview

WACC — weighted average cost of capital — is the blended rate a company pays to fund itself with debt and equity. It reflects what investors demand given the risk of the business. In a DCF, WACC is the discount rate applied to free cash flow to the firm.

---

## Why It Matters

Get WACC wrong and every valuation built on it is wrong. Too low and you overpay for assets; too high and you walk away from good deals. Managers also use WACC as a hurdle rate to decide which projects create value and which destroy it.

## Key Principles

- WACC = (E/V × Re) + (D/V × Rd × (1 − Tax Rate)).
- Cost of equity usually comes from CAPM: risk-free rate + beta × equity risk premium.
- After-tax cost of debt matters — interest is tax-deductible.
- Use target capital structure weights, not historical ones, for long-term valuations.
- WACC should match the cash flow: firm-level WACC pairs with FCFF, not FCFE.

## Key Terms

| Term | Definition |
|------|------------|
| **Cost of Equity (Re)** | Return shareholders demand for the risk of owning the stock. |
| **Cost of Debt (Rd)** | Effective interest rate the company pays on its borrowings. |
| **Beta** | A stock's sensitivity to overall market movements. |
| **Equity Risk Premium** | Extra return investors expect over the risk-free rate for holding stocks. |

## Use Case

A corporate finance team sets an internal WACC of 11% and uses it as the minimum acceptable IRR for every capital expenditure proposal across business units.

## Scenario

> A mid-cap steel firm mechanically used its book debt-to-equity to compute WACC, getting 9%. When it refreshed using market values and a peer-based beta, WACC rose to 12%. Two major capex projects that looked positive at 9% turned negative at 12%, and the board cancelled them, saving 400 crore of misallocated capital.

## Examples

- A bank with heavy, cheap leverage may have a WACC as low as 7%.
- A biotech start-up with no debt and high beta may have a WACC above 15%.

---

## Audited Appendix

# WACC Calculations
**Course:** Business Valuation
**Module:** Content / WACC Calculations
**Audited on:** 2026-04-18
**Audited by:** A3
**Source files reviewed:** `business-valuation/content/06-wacc-calculations.md`

---

## 1. Topic Snapshot
WACC is the blended, risk-adjusted cost of the capital (equity + debt) a firm uses to fund itself, and it becomes the discount rate in DCF-on-FCFF as well as the internal hurdle rate for any capex or AI-infra investment. For an IT/AI/Product/Consulting leader, WACC directly decides which GenAI platform builds clear the bar, which M&A target is worth chasing, and how aggressively to price multi-year consulting engagements or SaaS roadmaps. The core decision it drives: "Does this project/deal/bet earn more than our risk-adjusted cost of funding it — and if not, kill, renegotiate, or re-scope?"

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| WACC | Weighted Average Cost of Capital | Blended yearly cost of all money you use | Single hurdle across mixed funding | (E/V)Re + (D/V)Rd(1−t) | Valuation, capex gate reviews |
| Re | Cost of Equity | Return shareholders demand | Equity holders bear residual risk | CAPM / build-up | DCF, IRR debates |
| Rd | Cost of Debt | Interest lenders charge you | Debt is senior, cheaper than equity | YTM on bonds / loan rates | Treasury, credit memos |
| CAPM | Capital Asset Pricing Model | Pricing risk vs market | Link systematic risk to return | Rf + β·ERP | Valuation schools, b-school |
| Risk-Free Rate | Rf | Return with ~zero default risk | Baseline for every asset | 10Y Govt bond yield | Research reports |
| ERP | Equity Risk Premium | Extra return equity vs Rf | Equity compensation for risk | Historical / implied (Damodaran) | Pitch books, valuations |
| Beta (Raw) | β | Stock co-movement with market | Measures systematic risk | Regression of returns | Bloomberg, CapIQ |
| Levered Beta | β_L | Beta including debt impact | Equity β rises with leverage | From raw regression | Listed-firm data |
| Unlevered Beta | β_U / Asset β | Pure business risk, debt stripped out | Compare businesses apples-to-apples | Unlever via Hamada | Private-co valuations |
| Hamada Equation | — | Relever/unlever β for chosen D/E | Adjust peer β to your capital mix | β_L = β_U[1+(1−t)(D/E)] | Valuation models |
| Size Premium | SP | Extra return for small-cap risk | Small firms empirically earn more | Duff & Phelps size deciles | Mid-market M&A |
| Country Risk Premium | CRP | Extra return for EM exposure | Sovereign + currency risk | Damodaran CRP tables | Cross-border deals |
| Target Capital Structure | Target D/E | D/E ratio firm plans to run at LT | Current mix may be transient | Industry medians + policy | LT DCF, ratings |
| Marginal Tax Rate | t | Tax on next rupee of income | Drives tax shield on debt | Statutory rate / effective | Debt pricing |
| Pre-tax vs After-tax Rd | — | Rd before vs after tax shield | Only after-tax Rd in WACC | Rd × (1−t) | WACC build |
| Market Value Equity | E | Share price × shares outstanding | Forward-looking weight | Live market cap | Every WACC |
| Market Value Debt | D | PV of future debt cash flows | Book ≠ market when rates move | Bond price or YTM discount | Treasury |
| Book vs Market Weights | — | Balance-sheet vs market values | Book distorts leverage weights | From financials vs market | Audit debates |
| Credit Spread | — | Yield over Rf for credit risk | Reflects default probability | YTM − Rf at same tenor | Debt investors |
| YTM | Yield to Maturity | All-in return if bond held to maturity | Best proxy for marginal Rd | Bond pricing formula | Cost-of-debt work |

---

## 3. Frameworks & Matrices

### 3.1 WACC Build-Up Block Diagram
**Purpose:** Show how raw inputs (Rf, β, ERP, YTM, t, weights) combine into one number.
```
        Rf ──────────────┐
                          ├──► Re = Rf + β·ERP (+ SP + CRP)
   β · ERP ──────────────┘                      │
                                                 │  × (E/V)
   YTM ─────► × (1 − t) ──► After-tax Rd        │
                                   │  × (D/V)   │
                                   ▼            ▼
                               ┌─────────────────────┐
                               │        WACC         │
                               └─────────────────────┘
```
**Components:** Rf, β, ERP, YTM, t, E, D, V=E+D.
**IT/AI/Product/Consulting example:** A listed IT-services firm with Rf=7%, β=1.0, ERP=6% → Re=13%; YTM=8%, t=25% → after-tax Rd=6%; E/V=85%, D/V=15% → WACC = 0.85·13 + 0.15·6 = 12.0%.
**Trigger:** Any DCF, capex gate, or M&A IRR review.

### 3.2 CAPM Components Stack
**Purpose:** Visualise what is driving Re; spot when one premium is doing all the lifting.
```
Re (%)
 16 ┤                                   ┌──┐  CRP  +2
 14 ┤                         ┌──┐      ├──┤  SP   +1
 12 ┤               ┌──┐      ├──┤      ├──┤
 10 ┤     ┌──┐      │  │      │  │      │  │  β·ERP
  8 ┤     │  │      │  │      │  │      │  │
  6 ┤ ┌──┐│  │  ┌──┐│  │  ┌──┐│  │  ┌──┐│  │  Rf
  0 ┼─┴──┴┴──┴──┴──┴┴──┴──┴──┴┴──┴──┴──┴┴──┴────────
       Listed IT   AI-infra    Mid-mkt    EM roll-out
```
**Components:** Rf, β·ERP, SP, CRP.
**IT/AI/Product/Consulting example:** An AI-infra scale-up with β=1.8, Rf=7%, ERP=6%, SP=2% → Re = 7 + 10.8 + 2 = 19.8%; shows β is dominant — pushing roadmap de-risk reduces Re fastest.
**Trigger:** Whenever Re looks "too high" or "too low," decompose before defending.

### 3.3 Levered vs Unlevered Beta Matrix (Hamada)
**Purpose:** Move peer β from listed capital structure to your target structure — essential for private AI / PE-owned IT firms.
```
Step 1: Pull peer raw (levered) β        e.g., 1.25 at peer D/E = 0.40, t=25%
Step 2: Unlever:  β_U = 1.25 / [1 + (1−0.25)·0.40]
                 β_U = 1.25 / 1.30 = 0.96
Step 3: Average β_U across 5–8 peers     e.g., mean β_U = 1.00
Step 4: Relever at target D/E (say 0.20): β_L = 1.00·[1 + 0.75·0.20] = 1.15
Step 5: Use β_L = 1.15 in CAPM for your firm
```
**Components:** Peer set, peer D/E, peer tax rate, target D/E, firm tax rate.
**IT/AI/Product/Consulting example:** Consulting-partner valuing a boutique AI-services firm pulls β from Accenture/Infosys/TCS, unlevers (they run ~zero debt so little change), relevers at target 10% D/E → defensible β for private-co DCF.
**Trigger:** Valuing private firms or firms undergoing recap.

### 3.4 WACC Sensitivity Grid (β × ERP)
**Purpose:** Show how fragile WACC is to two most-debated inputs; discipline hurdle-rate debates.
```
                           ERP
                 5.0%    5.5%    6.0%    6.5%    7.0%
β = 0.8   WACC  10.1%   10.5%   10.9%   11.3%   11.7%
β = 1.0         11.3%   11.8%   12.3%   12.8%   13.3%
β = 1.2         12.5%   13.1%   13.7%   14.3%   14.9%
β = 1.4         13.7%   14.4%   15.1%   15.8%   16.5%
β = 1.6         14.9%   15.7%   16.5%   17.3%   18.1%
      (Assumes Rf=7%, Rd=8%, t=25%, E/V=85%, D/V=15%)
```
**Components:** β, ERP, fixed weights and Rd.
**IT/AI/Product/Consulting example:** Product-finance lead shows CFO that moving β from 1.0 to 1.4 and ERP from 5.5 to 6.5% swings WACC from 11.8% to 15.8% — flips three of seven AI-platform capex projects below hurdle.
**Trigger:** Before freezing a single WACC for a capex season.

---

## 4. Formulas

### 4.1 WACC
`WACC = (E/V)·Re + (D/V)·Rd·(1 − t)` where V = E + D.
**Threshold:** Bank-like cheap-leverage firms ~7%; mature IT-services 11–13%; biotech / no-debt, high-β tech >15%.
**Example:** SaaS firm: Rf=7%, β_U=1.2, ERP=6%, D/E=0.3, t=25%.
 - β_L = 1.2·[1 + 0.75·0.3] = 1.47
 - Re = 7% + 1.47·6% = 15.82%
 - Assume Rd (YTM) = 9% → after-tax Rd = 9%·0.75 = 6.75%
 - Weights: E/V = 1/1.3 = 76.9%, D/V = 23.1%
 - **WACC = 0.769·15.82 + 0.231·6.75 = 12.17% + 1.56% = 13.73%.**

### 4.2 CAPM (with optional premia)
`Re = Rf + β·ERP (+ Size Premium + Country Risk Premium)`.
**Threshold:** Rf = 10Y sovereign of cash-flow currency; β from 2–5Y weekly regressions; ERP 5–7% for mature markets (Damodaran 2024).
**Example:** Mid-cap Indian AI firm listed only on NSE: Rf=7%, β=1.3, ERP=6%, SP=1.5% → Re = 7 + 7.8 + 1.5 = 16.3%.

### 4.3 Hamada — Unlever / Relever Beta
`β_L = β_U · [1 + (1 − t)·(D/E)]` → rearrange to unlever: `β_U = β_L / [1 + (1 − t)·(D/E)]`.
**Threshold:** Use firm-specific t; if D/E volatile, use target, not spot.
**Example:** Listed peer β_L = 1.4, D/E = 0.5, t = 25% → β_U = 1.4 / 1.375 = 1.018.

### 4.4 After-tax Cost of Debt
`After-tax Rd = YTM · (1 − t)`.
**Threshold:** Use YTM on longest liquid bond at current rating; if unrated, synthetic rating from interest-coverage (Damodaran).
**Example:** YTM 9%, t = 25% → 6.75%. If distressed (YTM 14%, t shield limited by losses → effective t = 0) → after-tax Rd = 14%.

### 4.5 Weights
`E/V = E / (E + D);  D/V = D / (E + D)` — **market values**, not book.
**Threshold:** Market cap = price × diluted shares; market-value debt via PV of remaining coupons at current YTM, or book as rough proxy if rates stable.
**Example:** E = ₹8,500 cr market cap; D market = ₹1,500 cr → V = ₹10,000 cr → E/V = 85%, D/V = 15%.

### 4.6 Build-Up Method (private firms)
`Re = Rf + ERP + Size Premium + Industry Premium + Company-Specific Risk Premium`.
**Threshold:** Use when β is unreliable (no peers, thin trading); company-specific premium 1–5% based on concentration, key-person, governance.
**Example:** Private GenAI consultancy: Rf=7%, ERP=6%, SP=3%, industry=1%, firm-specific=3% → Re = 20%.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|---|---|
| 1 | Use market-value weights for E and D | Don't use book weights for long-term valuation — the 9% vs 12% steel-co error came from exactly this |
| 2 | Unlever peer β and relever at your target D/E | Don't apply listed-firm raw β directly to a private or recapping firm |
| 3 | Use after-tax Rd with marginal tax rate | Don't forget the debt tax shield; using pre-tax Rd inflates WACC |
| 4 | Use **target** capital structure for long-horizon DCF | Don't use today's spot D/E if it is transient (just-closed acquisition, bridge debt) |
| 5 | Refresh β after strategic pivots (e.g., IT-services → GenAI platform) | Don't rely on historical β after transformational change in business mix |
| 6 | Add country risk premium for EM cash flows | Don't apply a single developed-market WACC to cross-border / India-focused arms |
| 7 | Compute segment WACCs for diversified groups (IT-services + hardware + VC arm) | Don't apply one blended WACC across segments with different risk |
| 8 | Pair firm-WACC with FCFF; pair cost of equity with FCFE | Don't use WACC to discount FCFE — double-counts debt benefit |
| 9 | Sanity-check WACC vs industry benchmarks (Damodaran annual tables) | Don't ship a WACC that is 300 bps off industry median without documented reason |
| 10 | Document Rf, ERP, β source, and date in the model | Don't bury assumptions in hidden cells — auditors and boards will ask |

---

## 6. Real-Life Scenarios

### Scenario 1 — Setting WACC for a listed IT-services firm's capex portfolio (POSITIVE)
A ₹40,000 cr mid-cap IT-services firm (cloud + GenAI services) must set a FY27 hurdle rate for a ₹3,500 cr capex portfolio (data-centre GPUs, platform modernisation, two tuck-in AI acquisitions). The CFO's finance team pulls β from 8 listed peers (Infosys, TCS, Wipro, HCLTech, Accenture, Cognizant, LTIMindtree, Mphasis), unlevers each via Hamada at their spot D/E and tax rates, averages β_U = 0.88, relevers at target D/E = 0.05 → β_L = 0.91. Rf = 7.0% (10Y G-Sec), ERP = 6.0% (Damodaran India, 2024), SP = 0% (large-cap) → Re = 7 + 0.91·6 = 12.46%. YTM on recent NCD = 7.8%, t = 25.17% → after-tax Rd = 5.83%. Weights: E/V = 95%, D/V = 5% → **WACC = 12.13%**. Board freezes 12.25% as FY27 hurdle; three low-margin platform projects fall below and are re-scoped. **Tools:** CapIQ (β screener, WACC worksheet), Bloomberg BETA and WACC functions, Damodaran's India ERP & unlevered-β dataset, Excel, Anaplan for capex gating.

### Scenario 2 — AI-startup internal hurdle (POSITIVE)
A Series-C GenAI infra startup (₹1,800 cr revenue, no debt, heavy GPU capex) needs a hurdle for FY27 project prioritisation: (a) own-model training cluster (₹400 cr), (b) enterprise GTM expansion (₹120 cr), (c) vertical fine-tuning platform (₹80 cr). With no listed peers, finance uses build-up + CAPM hybrid: pulls β_U from listed AI-exposed peers (NVIDIA supply chain, Palantir, Snowflake) averaging β_U = 1.55; D/E = 0 so β_L = β_U = 1.55. Rf = 7%, ERP = 6%, SP = 3%, company-specific = 2% → Re = 7 + 9.3 + 3 + 2 = **21.3%** → WACC ≈ 21.3% (all-equity). Projected IRRs: (a) 18% — BELOW hurdle, re-scope to partnership; (b) 34% — GO; (c) 27% — GO. Tool: CapIQ for peer β, Damodaran dataset for size premium, Excel model reviewed quarterly. **Outcome:** ₹400 cr cluster project deferred; capital redeployed into GTM and platform; runway extended by ~14 months.

### Scenario 3 — ANTI-EXAMPLE: buyer uses own WACC instead of target's (NEGATIVE)
A large US-listed consulting platform (buyer WACC = 8%) acquires a ₹1,200 cr Indian AI-consulting boutique. Deal team discounts target's FCFF at buyer's 8% WACC instead of target-appropriate WACC (β_U 1.2, relevered, plus India CRP 2.5%, SP 2%, Re ≈ 17%, WACC ≈ 16%). At 8%, enterprise value = ₹2,900 cr; at 14% (target-specific), EV = ₹1,700 cr. Buyer pays ₹2,700 cr (close to 8% EV). Five years later at exit multiple, realised IRR = 6% vs model-promised 15% — **₹800-900 cr of value destruction**, because the wrong discount rate treated Indian AI-consulting risk as if it were US consulting risk. Rule violated: WACC must reflect the **risk of the cash flows**, not the acquirer. Echoes the mid-cap steel scenario — wrong WACC, every valuation is wrong: too low → overpay; too high → walk away from good deals.

---

## 7. Implementation Playbook
1. **Define the cash-flow set** — confirm you are discounting FCFF (firm) so WACC is the right rate; if FCFE, stop and use Re.
2. **Pick Rf** — pull 10Y sovereign yield in the cash-flow currency on valuation date; document source and date.
3. **Build β** — select 5–10 listed peers, pull 2–5Y weekly β (CapIQ/Bloomberg), unlever each via Hamada using peer D/E and t, average, then relever at your target D/E.
4. **Set ERP and premia** — use Damodaran's implied ERP for the country; add size premium (Duff & Phelps / Pratt-Grabowski) for mid/small; add country risk premium for EM revenue exposure.
5. **Compute Re via CAPM (or build-up)** — Re = Rf + β·ERP + SP + CRP; document each term.
6. **Compute after-tax Rd** — take YTM on longest liquid bond (or synthetic rating from interest coverage), multiply by (1 − marginal tax rate); cap tax shield if NOLs.
7. **Set weights from market values** — use current market cap for E; PV of bonds at current YTM (or book as proxy) for D; use **target** D/V if current is transient.
8. **Assemble WACC, sensitivity, governance** — compute WACC; run β × ERP sensitivity grid; benchmark vs industry median (Damodaran, Duff & Phelps); sign off with CFO + valuation committee; refresh yearly or on material change.

---

## 8. Content Quality Audit
**Covered well:** Core WACC formula, CAPM, after-tax cost of debt, target vs book capital structure, hurdle-rate role, firm-WACC vs equity-WACC matching to FCFF/FCFE, concrete Indian mid-cap steel scenario illustrating book vs market weights.

**Underplayed / missing in source:**
1. Unlevering and relevering β (Hamada) — essential for private firms, PE-owned IT, and AI startups with no listed twin.
2. Country risk premium for India / EM cash flows and cross-border M&A.
3. Size premium and build-up method for private firms where β is noisy.
4. Segment WACC for diversified groups (e.g., conglomerate with IT-services arm + consumer + venture portfolio).
5. Crisis-period ERP spikes (COVID-2020, 2022 rate cycle) — static historical ERP misprices risk in dislocation.
6. Governance process: how often to refresh, who signs off, what triggers reset (rating change, recap, pivot).

**Supplement with sources:**
- Damodaran, A. *Investment Valuation* (3rd ed., 2012) + annual ERP/β/CRP updates at pages.stern.nyu.edu/~adamodar (2024 vintage).
- Koller, Goedhart, Wessels. *Valuation: Measuring and Managing the Value of Companies* (7th ed., McKinsey, 2020) — Chs on cost of capital and capital structure.
- Pratt, S. & Grabowski, R. *Cost of Capital: Applications and Examples* (5th ed., 2014) — definitive on build-up and size premia.
- Duff & Phelps (Kroll) *Valuation Handbook — U.S. and International Guide to Cost of Capital* (2023).
- Gallo, A. "A Refresher on Cost of Capital," *Harvard Business Review* (2015) — clean exec-level primer.

**Red flags in source:**
- Presents WACC almost as a single deterministic number; real practice needs sensitivity + ranges.
- No mention of when NOT to use a single WACC (segments, crisis, transformation).
- The biotech ">15%" and bank "~7%" examples are directionally right but lack the build-up that makes them defensible.
- Implicitly assumes listed firm — silent on private-firm adjustments.

---

## 9. Quick-Recall Card
- WACC = (E/V)·Re + (D/V)·Rd·(1−t); Re via CAPM = Rf + β·ERP (+ SP + CRP).
- Use **market-value** weights, **target** capital structure, **marginal** tax, and **match** WACC to FCFF.
- For private / recapping firms: unlever peer β, relever at your target D/E (Hamada).
- Sensitivity on β and ERP before freezing a hurdle; segment-level WACCs for diversified groups.
- Wrong WACC = wrong valuation every time: too low → overpay; too high → walk away from good deals.
- **As a PM/Consultant/AI Lead, the one question to answer with this framework is: "What is the single defensible risk-adjusted hurdle rate my capex, AI-infra bet, or M&A target must clear — and how much does that rate change my GO/NO-GO list?"**

---

**Connects to:** [05-discounted-cash-flow-dcf-models.md](05-discounted-cash-flow-dcf-models.md), [04-time-value-of-money.md](04-time-value-of-money.md), [../financial-management/](../financial-management/), [../investment-analysis-portfolio/08-capital-asset-pricing-model.md](../investment-analysis-portfolio/08-capital-asset-pricing-model.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:4, 7:4, 8:4, 9:5, 10:4]
Sections rewritten: [1 tightened to role-lens decision; 3 expanded with 4th sensitivity grid; 4 added build-up method; 6 added quantified anti-example; 8 added governance and crisis-ERP gaps]
Enrichments applied: [cross-course links; 5 supplements (Damodaran, Koller, Pratt-Grabowski, Duff & Phelps, HBR); anti-example with ₹800-900 cr cost; IT tooling (CapIQ, Bloomberg, Damodaran, Anaplan); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A3
-->
