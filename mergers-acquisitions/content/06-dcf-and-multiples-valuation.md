# DCF and Multiples-Based Valuation

## Overview

A DCF (discounted cash flow) adds up the future cash a business is expected to produce and brings those numbers back to today's value using a discount rate. Multiples valuation takes a market ratio (like EV/EBITDA) from similar firms and applies it to the target's numbers.

---

## Why It Matters

DCF is grounded in what the business can earn; multiples show what the market is paying right now. Using them together gives a realistic price range and protects buyers from both inflated markets and over-optimistic forecasts.

## Key Principles

- DCF is only as good as the forecast and the discount rate
- Always use a realistic terminal value, not a hopeful one
- For multiples, pick truly comparable firms by size, sector, and geography
- Adjust EBITDA for one-time items before applying multiples
- Triangulate DCF and multiples to narrow the range

## Key Terms

| Term | Definition |
|------|------------|
| **DCF** | Value = sum of future cash flows discounted to today |
| **WACC** | Weighted average cost of capital used as the discount rate |
| **Terminal Value** | Value of the business beyond the forecast period |
| **EV/EBITDA** | Common multiple comparing enterprise value to earnings |
| **Comparable Companies** | Listed peers used to benchmark multiples |

## Use Case

A buyer projects five years of free cash flow for a target, discounts them at 11% WACC, adds a terminal value, and then cross-checks the answer against EV/EBITDA multiples of three listed peers.

## Scenario

> A consumer goods buyer ran a DCF giving a value of Rs 800 crore. Listed peers were trading at 12x EBITDA, which gave Rs 900 crore. The buyer flagged the gap, negotiated earnouts for the upside, and signed at Rs 820 crore.

## Examples

- A PE fund uses a 5-year DCF with exit multiple to value a logistics acquisition.
- An analyst values a listed retailer at 1.5x sales based on peer multiples.

---

## Audited Appendix

# DCF and Multiples-Based Valuation
**Course:** Mergers and Acquisitions
**Module:** Content / DCF and Multiples Valuation
**Audited on:** 2026-04-18
**Audited by:** A8
**Source files reviewed:** `mergers-acquisitions/content/06-dcf-and-multiples-valuation.md`

---

## 1. Topic Snapshot
DCF discounts a target's projected free cash flows at its cost of capital and adds a terminal value to derive intrinsic enterprise value, while multiples (EV/EBITDA, EV/ARR, EV/Revenue, P/E) lift a market-implied ratio from truly comparable peers or precedents and apply it to the target's normalized metric. An IT/AI/Product/Consulting leader triangulates both because DCF anchors price to forecast economics (unit economics, SBC, churn) while multiples anchor price to what the market is actually paying right now for SaaS, GCC, or services assets. The decision being made: what offer range to put on the table, how to structure earnouts when DCF and multiples diverge, and when to walk away because the peer set is trading at a cyclical peak.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|------|-----------|---------------|---------------|--------------|-------------------|
| DCF | Discounted Cash Flow | Value = sum of future cash, pulled back to today | Anchors price in earnings, not sentiment | Σ FCFF/(1+WACC)^t + TV | IC memos, CFO decks |
| WACC | Weighted Avg Cost of Capital | Blended cost of debt + equity | Single discount rate across capital stack | (E/V)Re + (D/V)Rd(1−t) | Valuation models |
| Terminal Value | TV (Gordon vs Exit Multiple) | Value beyond forecast horizon | 60–80% of DCF sits here | FCFF_{n+1}/(WACC−g) or EBITDA_n × m | DCF tab row 30 |
| Implied Perpetuity Growth | Implied g | Growth rate baked into exit multiple | Sanity-checks terminal aggressiveness | g = WACC − FCFF_{n+1}/TV | Cross-check step |
| FCFF | Free Cash Flow to Firm | Cash for all capital providers | Matches enterprise-level WACC | EBIT(1−t) + D&A − Capex − ΔWC | DCF builds |
| FCFE | Free Cash Flow to Equity | Cash left for shareholders | Used with cost of equity, not WACC | FCFF − Interest(1−t) + Net Borrowing | LBO / equity DCF |
| Enterprise Value | EV | Value of operating business | Capital-structure neutral | Equity + Debt − Cash + Minority + Prefs | All multiples |
| Equity Value | Market Cap / Offer Value | Value to shareholders | What buyer actually pays for stock | EV − Net Debt − Prefs | Term sheets |
| EV/EBITDA | Enterprise Value / EBITDA | How many years of EBITDA to recoup EV | Core multiple for mature firms | EV ÷ LTM or NTM EBITDA | Banker pitches |
| EV/Revenue | EV / Revenue | Top-line anchor when EBITDA < 0 | Needed for loss-making growth | EV ÷ LTM Revenue | Early-stage tech |
| EV/ARR | EV / Annual Recurring Revenue | SaaS-native multiple | Recognizes subscription predictability | EV ÷ committed ARR | SaaS M&A |
| P/E (Trailing / Forward) | Price / Earnings | Price per rupee of net income | Equity-level quick read | Price ÷ EPS (LTM or NTM) | Public comps |
| Harmonic Mean | HM of multiples | Inverse-averaged multiple | Avoids upward bias of arithmetic mean | n / Σ(1/x_i) | Rigorous comp tables |
| Forward vs Trailing Multiple | NTM vs LTM | Next-12 vs last-12 months | Adjusts for growth direction | NTM uses forecast denominator | Equity research |
| Rule of 40 (SaaS) | Growth% + FCF Margin% ≥ 40 | SaaS health gate | Explains multiple dispersion | Growth + FCF margin | SaaS diligence |
| Peer Group | Comparable Companies | Truly similar firms | Multiples only mean something vs peers | Size, sector, geo, growth filter | Comp tables |
| Cycle-Adjusted Multiple | Normalized Multiple | Multiple smoothed over cycle | Removes peak/trough distortion | Median of 5–7 yr multiples | Cyclical deals |
| Synergy-Adjusted Multiple | EV / (EBITDA + Synergies) | Multiple if synergies realized | Reveals "price to buyer" vs "price to seller" | EV ÷ (EBITDA + NPV synergies/yr) | Bid modelling |
| One-Time Adjustments | Non-recurring items | Strip legal, restructuring, COVID | Clean run-rate EBITDA | Add back / take out items | QoE reports |
| Pro-Forma EBITDA | Adjusted EBITDA | EBITDA after normalisation + run-rate | Basis for multiple application | Reported + adjustments | SPA schedules |

---

## 3. Frameworks & Matrices

### 3.1 DCF Architecture
**Purpose:** Show the anatomy of a DCF so nothing hides in terminal value.
```
          +-------------------------------------------------+
          |                DCF BUILD                        |
          +-------------------------------------------------+
 Yr1..Yr5 |  Revenue -> EBITDA -> EBIT -> NOPAT -> FCFF     |
          |         discounted at WACC                      |
          +-------------------------------------------------+
          |              TERMINAL VALUE                     |
          |  Gordon: FCFF_{n+1}/(WACC-g)                    |
          |  Exit:   EBITDA_n * m                           |
          |         discounted at WACC                      |
          +-------------------------------------------------+
                          | sum
                          v
                 Enterprise Value (EV)
                  - Net Debt - Prefs + Cash
                          v
                    Equity Value
```
**Components:** explicit forecast, WACC, TV method, sensitivity on WACC × g.
**IT/AI/Consulting worked example:** AI-SaaS target, 5-yr FCFF projection with SBC as real cost, WACC 11%, exit multiple 10× ARR as TV check.
**Trigger:** any cross-border or control deal above $25M.

### 3.2 Multiple Selection Matrix
**Purpose:** Use the right multiple for the right business model.
```
Business Type           | Primary Multiple | Secondary       | Watch-out
------------------------+------------------+-----------------+-------------------------
Mature IT Services      | EV/EBITDA        | EV/Revenue      | Utilisation, pyramid mix
GCC / BPM               | EV/EBITDA        | EV/FTE          | Wage inflation
SaaS (>$10M ARR)        | EV/ARR           | Rule of 40      | Net Retention, CAC payback
Early-stage / loss-mak. | EV/Revenue       | EV/Gross Profit | Burn multiple
Marketplace / Platform  | EV/GMV or Take   | EV/Revenue      | Take-rate sustainability
Consumer / Retail       | EV/EBITDA        | EV/Sales        | Cyclicality
Telecom / Infra         | EV/Customer      | EV/EBITDA       | Capex intensity
AI tooling / copilots   | EV/ARR           | EV/Seat         | Usage-based rev volatility
```
**Worked example:** Logistics SaaS with $25M ARR, 45% growth, 70% gross margin → EV/ARR 10× peer median = $250M; cross-check Rule of 40 at 50% supports premium band.
**Trigger:** before pulling any comp table, fix the primary multiple per business model.

### 3.3 DCF-vs-Multiples Triangulation (Football Field)
**Purpose:** Converge on an offer range, not a single number.
```
                       Low    Base    High
DCF (WACC 10-12%)      |--------X-----|        800 - 950 cr
Trading Comps EV/EBITDA        |-------X-----| 880 - 1050 cr
Precedent Transactions         |---------X---| 950 - 1150 cr
Exit-Multiple DCF      |--------X-----|        820 - 980 cr
52-wk trading range    |---X---|                700 -  900 cr
                       ------------------------->
                              Offer band: 880-980 cr
```
**Reconciliation rules:** if multiples > DCF by >20%, test for market froth or synergy pricing; if DCF > multiples, test forecast optimism (growth, margin, TV g).
**Worked example:** Consumer-goods target DCF = ₹800 cr, peers 12× EBITDA = ₹900 cr → flagged gap, structured earnouts tied to EBITDA, closed at ₹820 cr base + ₹120 cr earnout.
**Trigger:** investment committee pre-read.

### 3.4 (Optional) Implied Terminal Growth from Exit Multiple
**Purpose:** Catch TV optimism baked into exit multiples.
```
g_implied = WACC - FCFF_{n+1} / TV
If g_implied > long-run GDP (2-3% DM, 5-6% India) -> re-underwrite TV.
```

---

## 4. Formulas

1. **DCF Enterprise Value**
   `EV = Σ [FCFF_t / (1+WACC)^t]  +  TV / (1+WACC)^n`
   Threshold: TV share of EV should be 55–75%; >85% = TV-driven valuation, push back.
   Example: AI-SaaS 5-yr PV of FCFF = $60M, TV PV = $140M → EV = $200M.

2. **Terminal Value (two methods)**
   `Gordon: TV = FCFF_{n+1} / (WACC − g)`
   `Exit Multiple: TV = EBITDA_n × m`
   Threshold: Gordon g ≤ long-run nominal GDP. Exit m ≤ entry m (no multiple expansion assumed).
   Example: FCFF_{n+1}=$18M, WACC=11%, g=3% → Gordon TV = $225M.

3. **Implied Growth from Exit Multiple**
   `g = WACC − FCFF_{n+1} / TV`
   Threshold: flag if g > 5% for DM or > 7% for India.
   Example: exit m = 12× on EBITDA $22M = TV $264M; FCFF_{n+1}=$18M, WACC=11% → g = 11% − 18/264 = 4.2% (acceptable).

4. **Trading / Transaction Multiples**
   `EV/EBITDA = EV / EBITDA`  ·  `EV/ARR = EV / ARR`  ·  `P/E = Price / EPS`
   Threshold: SaaS EV/ARR cluster 6–12× post-2023 reset; IT services EV/EBITDA 10–14×.
   Example: $25M ARR × 10× = $250M; precedents at 12× = $300M; DCF base $200M → bid $235M mid.

5. **Harmonic Mean of Multiples (preferred)**
   `HM = n / Σ (1/x_i)`
   Threshold: use HM, not arithmetic, to avoid upward skew; gap between HM and AM > 15% signals outliers → trim set.
   Example: peer EV/EBITDA 8, 10, 12, 25 → AM = 13.75, HM = 11.4 → use 11.4 for valuation.

6. **Synergy-Adjusted Multiple (buyer lens)**
   `m_adj = EV_offer / (EBITDA_target + run-rate synergy)`
   Threshold: m_adj should be ≤ peer median; if not, buyer is overpaying even with synergies.
   Example: Offer $600M, EBITDA $40M, synergy $20M → m_adj = 10× vs standalone 15×.

---

## 5. Do vs Don't

| Do | Don't |
|----|-------|
| Build WACC bottom-up (peer beta, target capital structure) | Use borrower's own historical leverage for WACC |
| Cap Gordon g at long-run GDP | Let terminal g drift above 5% "because growth is strong" |
| Cross-check DCF TV via implied exit multiple and vice versa | Report DCF without showing TV % of EV |
| Use harmonic mean for peer multiples | Use arithmetic mean when outliers exist |
| Normalize EBITDA (one-times, SBC, founder salary) | Apply multiple to reported EBITDA for SaaS/tech |
| Use NTM multiples for growth businesses | Compare NTM target multiple to LTM peer multiple |
| Cycle-adjust for cyclical sectors (chemicals, autos, semis) | Anchor on 2021 SaaS peak multiples in 2026 |
| Sensitize WACC × g × exit multiple (tornado chart) | Present a single-point valuation |
| Separate standalone value from synergy value | Pay the seller for 100% of synergies upfront |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS target, 2-stage DCF + EV/ARR cross-check
Buyer (strategic CPaaS player) runs 5-yr explicit forecast on a $25M ARR AI-SaaS firm growing 45%, fades to 15% in yrs 6–10, then terminal at 3%. WACC 12% reflecting illiquidity + tech beta. SBC treated as real cash cost. DCF EV = $220M. EV/ARR peer comps (Bessemer Cloud Index public SaaS HM = 8×): $200M. Precedent AI-tooling deals at 12× ARR: $300M. Football field 200–300, offer $235M with $40M earnout tied to Net Retention ≥ 115%. Tools: Excel, CapIQ, PitchBook, Bessemer Cloud Index.

### Scenario 2 — IT-services rollup, pro-forma EBITDA + peer EV/EBITDA
PE platform acquires 3 mid-size IT services firms (₹200 cr revenue each). Each reports ₹40 cr EBITDA; QoE strips ₹6 cr of one-time COVID costs, adds ₹4 cr synergy run-rate in year 2. Pro-forma EBITDA per target ≈ ₹38–42 cr. Listed peers (Happiest Minds, Coforge, Persistent) trade 15–22× EV/EBITDA; private mid-cap rollups clear 8–11×. Buyer anchors offer at 9.5× on pro-forma EBITDA, structures 60% cash + 40% earnout on 3-yr growth > 18% CAGR. Tools: FactSet, CapIQ, proprietary QoE workpaper.

### Scenario 3 — ANTI-EXAMPLE: trailing multiples at cyclical peak
In mid-2021 a buyer paid 18× LTM EV/EBITDA for a D2C consumer brand citing "peer trading at 20×". No cycle adjustment. By 2023 peer median reverted to 11×, target EBITDA flat. Implied fair EV dropped ~40%. On a ₹1,200 cr purchase, impairment write-down of approximately ₹450–500 cr hit the acquirer's books within 18 months. Lesson: cycle-adjust multiples using 5–7 yr median, stress-test with NTM and forward multiples, cap TV g below long-run GDP.

**Tools across scenarios:** Excel/Google Sheets, CapIQ, Bloomberg, FactSet, Bessemer Cloud Index, PitchBook, Tegus/AlphaSense for primary research, Python/NumPy for Monte Carlo sensitivity.

---

## 7. Implementation Playbook

1. **Scope valuation charter** — artifact: one-page memo fixing primary multiple, WACC build, forecast horizon, TV method, peer set criteria (size/sector/geo/growth).
2. **Build bottom-up WACC** — artifact: WACC tab with unlevered peer betas, re-levered at target capital structure, after-tax cost of debt, country-risk premium if cross-border.
3. **Construct pro-forma EBITDA / FCFF** — artifact: QoE bridge from reported to adjusted, SBC treatment documented, one-time items signed off by CFO.
4. **Run DCF with dual TV** — artifact: model with both Gordon and Exit-Multiple TV, reconciliation of implied g, TV as % of EV flagged.
5. **Assemble peer comps table** — artifact: trading comps + precedent transactions, harmonic mean, cycle-adjusted median, filtered for size/sector/geo.
6. **Sensitize** — artifact: tornado chart on WACC × g × exit multiple × growth × margin; Monte Carlo if board-level deal.
7. **Triangulate football field** — artifact: one-slide range chart, reconciliation narrative when DCF and multiples diverge > 20%.
8. **Land offer logic + deal structure** — artifact: IC memo mapping base cash + earnout + escrow to valuation gap and confidence in forecast.

---

## 8. Content Quality Audit

**Covered well in source:** DCF intuition, WACC basics, EV/EBITDA mechanics, triangulation habit, use of earnouts to bridge valuation gap, realistic TV warning.

**Underplayed / needs supplement:**
- Harmonic mean vs arithmetic mean of multiples (source silent).
- Cycle-adjusted / normalized multiples for cyclical and post-bubble sectors.
- Implied perpetuity growth cross-check from exit multiples.
- SaaS-specific multiples (EV/ARR, Rule of 40, NRR-based premium).
- Forward vs trailing multiples and how to match numerator/denominator timing.
- Sensitivity / tornado on WACC × g; Monte Carlo for complex deals.
- Stock-Based Compensation treatment inside FCF (especially for AI/SaaS).
- Synergy-adjusted multiple ("price to buyer" lens).

**Supplement with ≥5 sources:**
1. Damodaran, *Investment Valuation*, 3rd ed., Wiley (2012) — DCF, WACC, relative valuation rigor.
2. Koller, Goedhart & Wessels (McKinsey), *Valuation: Measuring and Managing the Value of Companies*, 7th ed. (2020) — continuing value, ROIC-growth framework.
3. Rosenbaum & Pearl, *Investment Banking: Valuation, LBOs, M&A, IPOs*, 3rd ed. (2020) — comps construction, precedent transactions mechanics.
4. Bessemer Venture Partners, *State of the Cloud Report* (2024) — SaaS multiple benchmarks, Rule of 40, NRR tiers.
5. Mauboussin & Callahan, HBR/Morgan Stanley *"What Does a Price-Earnings Multiple Mean?"* / *"The Right Way to Use a Multiple"* (2014) — implied expectations from multiples.

**Red flags:**
- TV > 80% of DCF EV with g near WACC.
- Peer set not filtered for size/growth/geo; 3 cherry-picked high comps.
- Using reported EBITDA without QoE.
- Trailing multiples applied at cyclical peak with no normalization.
- Synergies baked into standalone DCF and again into offer multiple (double-count).

---

## 9. Quick-Recall Card
- DCF = intrinsic (forecast + WACC + TV); Multiples = market (peer ratio × target metric).
- Triangulate DCF + trading comps + precedents on a football field; offer sits in the overlap.
- Always check TV % of EV, implied g, harmonic mean of multiples, and cycle adjustment.
- Pick the right multiple for the model: EV/EBITDA mature, EV/ARR SaaS, EV/Revenue early-stage, EV/GMV marketplace.
- Bridge valuation gaps with earnouts, escrows, and synergy sharing — not with optimistic WACC or g.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: what is the defensible offer range for this target and how do I structure the deal so I do not pay the seller for synergies and forecasts I have not yet earned?

---

**Connects to:** [05-valuation-methodologies.md](05-valuation-methodologies.md), [../business-valuation/05-discounted-cash-flow-dcf-models.md](../business-valuation/05-discounted-cash-flow-dcf-models.md), [../business-valuation/07-comparable-company-analysis.md](../business-valuation/07-comparable-company-analysis.md), [../business-valuation/08-precedent-transaction-analysis.md](../business-valuation/08-precedent-transaction-analysis.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:5, 10:4]
Sections rewritten: [3.3 football field numbers tightened; 4 thresholds added; 6.3 impairment quantified; 8 supplements expanded to 5]
Enrichments applied: [cross-course links; 5 supplements; anti-example with ₹450-500 cr impairment; IT/AI/SaaS tooling — CapIQ/Bessemer/PitchBook/FactSet; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:20
Audited by: A8
-->
