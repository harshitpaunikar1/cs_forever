# Introduction to Investment Analysis

## Overview
Investment analysis is the process of evaluating financial assets to determine whether they are suitable for a particular investor or portfolio. It involves examining an asset's potential return, its associated risks, and how it fits within a broader financial plan. Whether you are looking at stocks, bonds, real estate, or alternative investments, the goal is always to make informed decisions that align with your financial objectives.

---

## Why It Matters
Every financial decision involves trade-offs between risk and reward. Without a structured approach to analyzing investments, individuals and institutions risk losing capital, missing opportunities, or building portfolios that do not match their goals. Investment analysis provides the framework to evaluate options systematically, compare alternatives, and make choices grounded in evidence rather than guesswork.

## Key Principles
- All investments carry some degree of risk, and higher potential returns generally come with higher risk
- Diversification across asset classes reduces the impact of any single investment's poor performance
- Investment decisions should be driven by clearly defined objectives, time horizons, and risk tolerance
- Markets are influenced by economic conditions, interest rates, corporate earnings, and investor sentiment

## Key Terms
| Term | Definition |
|------|------------|
| **Asset Class** | A category of investments that share similar characteristics, such as stocks, bonds, or real estate |
| **Risk Tolerance** | The degree of variability in returns that an investor is willing to accept |
| **Liquidity** | How quickly and easily an asset can be converted to cash without significantly affecting its price |
| **Fundamental Analysis** | A method of evaluating securities by examining financial statements, industry conditions, and economic factors |

## Use Case
A financial advisor uses investment analysis to build a retirement portfolio for a client who is 30 years from retirement, selecting a mix of growth stocks and bonds that matches the client's risk tolerance and long-term goals.

## Scenario
> Maria just received a bonus and wants to invest it wisely. She compares several mutual funds by looking at their past performance, expense ratios, and the sectors they invest in. After analyzing the options, she picks a diversified fund that balances growth potential with manageable risk, giving her confidence that her money is working toward her retirement.

## Examples
- Comparing the price-to-earnings ratios of two technology companies to decide which stock offers better value
- Reviewing a bond's credit rating and yield to maturity before adding it to a fixed-income portfolio

---

## Audited Appendix

# Introduction to Investment Analysis
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Introduction to Investment Analysis
**Audited on:** 2026-04-18
**Audited by:** A2
**Source files reviewed:** `investment-analysis-portfolio/content/01-introduction-investment-analysis.md`

---

## 1. Topic Snapshot
Investment analysis is the structured evaluation of financial assets (stocks, bonds, real estate, alternatives) against an investor's return objectives, risk tolerance, and time horizon — converting gut-feel "should I buy this?" into a defensible decision.
An IT/AI/Product/Consulting professional needs it because RSU vesting, ESOP liquidity events, post-tax bonus allocation, founder liquidity at exit, and advising a CFO on treasury mix are all capital-allocation problems where the default (leaving cash idle, or over-concentrating in employer stock) destroys real wealth.
The decision this framework forces: "Given my goals, horizon, and risk capacity, what is the right asset mix and which specific securities satisfy a written Investment Policy Statement — versus chasing last year's winner?"

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Asset Class | Asset Class | Bucket of instruments with similar risk/return behaviour (equity, debt, real estate, commodities, cash) | Diversification requires uncorrelated buckets | Correlation matrix vs other classes | IPS, allocation reviews |
| Risk Tolerance | Risk Tolerance | How much volatility you can stomach emotionally | Separates panic-sellers from holders | Questionnaire score, drawdown tested | Advisor onboarding |
| Risk Capacity | Risk Capacity | How much loss your balance sheet can *afford* (different from tolerance) | Tolerance lies; capacity is math | Net worth × horizon × income stability | CFP planning |
| Liquidity | Liquidity | Speed to convert to cash without haircut | Emergencies and opportunities need cash | Bid-ask spread, T+n settlement, lock-in | Treasury, fund factsheet |
| Fundamental Analysis | Fundamental Analysis | Valuing from financials (earnings, cashflow, moat) | Price ≠ value; find mis-pricing | DCF, P/E, P/B, EV/EBITDA | Equity research |
| Technical Analysis | Technical Analysis | Valuing from price/volume patterns | Behaviour repeats; momentum exists | RSI, MACD, moving averages | Trading desks |
| Quantitative Analysis | Quantitative Analysis | Rules-based, statistical factor models | Remove human bias | Factor loadings, backtest Sharpe | Quant funds, robo-advisors |
| Top-Down vs Bottom-Up | — | Macro-first vs security-first research flow | Two valid entry points | Allocation→sector→stock vs stock→sector→macro | Asset-mgmt style notes |
| Strategic vs Tactical Allocation | — | Long-run policy mix vs short-run tilts | Discipline plus opportunism | SAA band %, TAA deviation % | IPS, quarterly review |
| Time Horizon | — | Years until money is needed | Determines volatility capacity | Years to goal | Retirement, goal planning |
| Investment Policy Statement (IPS) | IPS | Written contract: goals, constraints, allocation, review cadence | Prevents emotional drift | Document adherence audit | CFA, private banking |
| Benchmark | Benchmark | Reference index to judge performance | "Good vs what?" | Nifty 50, S&P 500, CRISIL Composite Bond | Fund factsheet |
| Alpha | Alpha | Return above benchmark adjusted for risk | Measures skill | Regression intercept vs benchmark | Fund reviews |
| Beta | Beta | Sensitivity of asset to market moves | Systematic risk gauge | Cov(asset,mkt)/Var(mkt) | CAPM, equity research |
| Expense Ratio | TER | Annual fund running cost as % of AUM | Silent CAGR killer | % per year | Mutual fund KID |
| Passive vs Active Investing | — | Index-tracking vs manager-picking | Fees vs alpha debate | TER spread, tracking error, IR | Boglehead vs PMS debate |
| ETF vs Mutual Fund | Exchange-Traded Fund vs MF | Exchange-traded basket vs AMC-priced basket | Intraday liquidity vs end-of-day NAV | Ticker price vs NAV; spread | Zerodha, Groww |
| Closed-End vs Open-End | — | Fixed units traded on exchange vs continuous creation/redemption | Different liquidity mechanics | Discount/premium to NAV | CEF markets |
| Net Asset Value (NAV) | NAV | Per-unit fund value | Fair price for MF units | (Assets − Liabilities) / Units | Daily fund reports |

---

## 3. Frameworks & Matrices

### 3.1 Investment Analysis Pyramid
**Purpose:** Sequence research from macro to micro so you don't buy a great stock in a doomed sector.
```
            ┌──────────────┐
            │   SECURITY   │   Pick this stock/bond
            ├──────────────┤
            │   COMPANY    │   Financials, moat, mgmt
            ├──────────────┤
            │   INDUSTRY   │   Structure, margins, cycle
            ├──────────────┤
            │   ECONOMIC   │   GDP, rates, inflation, FX
            └──────────────┘
```
**Components:** Macro drivers → sector tailwinds → firm moat → security pricing.
**IT/AI/Product/Consulting example:** AI-SaaS founder with ₹2 cr surplus first sees India real-rate ~1.5% (macro favours equity), picks IT-services (industry still growing 9% CAGR), shortlists mid-cap IT with >20% ROCE, buys when P/E < 5-yr median.
**Trigger:** Any time horizon ≥5 years and allocation ≥ ₹10 L.

### 3.2 Risk-Return Spectrum
**Purpose:** Visual sanity check before adding an asset — does the expected return justify the added risk?
```
Return ^
       |                                         Crypto ●
       |                               Alts ●
       |                      Equity ●
       |            Bonds ●
       |   Cash ●
       +--------------------------------------------->  Risk / Volatility
Typical  3-6%    5-8%         11-13%       10-15%     80-100% σ
CAGR
```
**Components:** Each band = historical CAGR and approximate annual σ.
**IT/AI/Product/Consulting example:** Consulting senior with ₹50 L post-tax — anchors 20% cash, 30% bonds, 40% equity, 8% alternatives (REIT/gold), 2% crypto — declines a "sure 30%" unlisted-equity pitch because the return falls off the spectrum band.
**Trigger:** Whenever a new asset class is pitched.

### 3.3 IPS Construction Framework
**Purpose:** Turn goals, risk, horizon, constraints into an enforceable allocation band.
```
 Goals  ──┐
 Risk   ──┤
 Horizon ─┼──►  IPS  ──►  Strategic Asset Allocation (with ± bands)
 Constr ──┘                │
                           └──►  Rebalance rule + Review cadence
```
**Components:** Goals (retirement corpus, home, child ed.); Risk (tolerance + capacity); Horizon (short/med/long buckets); Constraints (tax, liquidity, ESG, regulatory).
**IT/AI/Product/Consulting example:** Product Director, age 38, 22-yr horizon, high risk capacity — SAA = 70% equity (50% domestic index + 20% US index) / 20% debt / 10% gold-REIT. Rebalance ±5% band, annual review, ESOP cap 15% of net worth.
**Trigger:** New job, major liquidity event, or no IPS on file.

### 3.4 Top-Down vs Bottom-Up Decision Flow (Optional)
```
TOP-DOWN:  Macro → Sector → Stock       (good for tactical rotation)
BOTTOM-UP: Stock → Sector → Macro check (good for conviction picks)
```
**Trigger:** Top-down when rates/cycle are the dominant story; bottom-up when a specific firm has a durable edge.

---

## 4. Formulas

### 4.1 Expected Return
`E(R) = Σ (pᵢ × Rᵢ)` or historical arithmetic mean.
**Threshold:** If E(R) − risk-free < 3%, equity risk premium is too thin.
**Example:** AI founder models Nifty next year — 40% chance +18%, 40% chance +6%, 20% chance −15%. E(R) = 0.4(18)+0.4(6)+0.2(−15) = 7.2+2.4−3 = **6.6%**. Versus 7% G-sec → under-compensated; keep debt weight.

### 4.2 Risk-Adjusted Return (Sharpe preview)
`RAR = (R_portfolio − R_f) / σ_portfolio`
**Threshold:** Sharpe <0.5 weak; 0.5–1 decent; >1 strong; >2 suspicious (check survivorship bias).
**Example:** Advisor compares two MFs for CFO treasury — Fund A 12%/σ 14%, Fund B 10%/σ 8%, R_f 7%. Sharpe A = (12−7)/14 = 0.36; Sharpe B = (10−7)/8 = 0.38. Fund B wins despite lower raw return.

### 4.3 TER Drag on Terminal Wealth
`Wealth loss fraction = 1 − (1 − TER)^n`
**Threshold:** Flag any equity fund TER >1.2%; index fund >0.3%.
**Example:** ₹2 cr over 25 years. At TER 1.5%: loss fraction = 1 − 0.985^25 = **31.4%** → ~₹62.8 L of terminal CAGR silently lost. At TER 0.2% (index): loss = 4.9% → ₹9.8 L. Switching saves ~₹53 L.

### 4.4 Real Return (Optional)
`R_real = (1 + R_nominal) / (1 + Inflation) − 1`
**Example:** FD at 7% with CPI 6% → real = 1.07/1.06 − 1 = **0.94%**. ₹50 L RSU parked in FD for 10 years grows only ~₹5 L in real terms — negative after tax.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Write a one-page IPS before investing any amount ≥3 months' salary | Don't start from "which stock is hot?" — start from goal & horizon |
| Cap single-security exposure (incl. employer RSU/ESOP) at 10–15% of net worth | Don't let vesting auto-accumulate employer stock past the cap |
| Compare funds on TER, tracking error, and 10-yr rolling returns | Don't rank funds by trailing 1-yr return alone |
| Separate risk *tolerance* (emotion) from risk *capacity* (math) | Don't let a bullish year inflate your stated tolerance |
| Rebalance on bands (±5%) or calendar (annual), whichever first | Don't rebalance on news headlines |
| Benchmark every active fund against a fair index after fees & tax | Don't judge a small-cap fund against Nifty 50 |
| Keep 6–12 months expenses in liquid/ultra-short before any equity | Don't invest emergency money in ELSS for tax savings |
| Document rationale + exit trigger for every position | Don't hold "because it will come back" without a written thesis |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI Founder with RSU Windfall
Priya, 34, AI-infra startup Head of Product, receives secondary liquidity of ₹3.2 cr (post-tax) plus ongoing RSUs vesting ~₹60 L/yr. She builds an IPS:
- **Emergency bucket:** ₹30 L in liquid fund + sweep-in FD (12 months burn).
- **Growth bucket:** ₹1.6 cr — 60% Nifty 500 index + 25% S&P 500 ETF + 15% mid-cap index.
- **Long-term bucket:** ₹80 L — NPS Tier-1 (equity-max) + PPF + sovereign gold.
- **Opportunistic bucket:** ₹50 L — angel/private credit, capped.
- Rule: vested employer stock sold to cap employer exposure at 15% of net worth.
**Tools:** Personal Capital / INDmoney (net-worth), Zerodha Coin (direct MFs), Carta (RSU/ESOP tracking), Morningstar Portfolio X-Ray (overlap check).

### Scenario 2 — Consulting Senior, Post-Tax Liquid Allocation
Arjun, 41, Partner-track at a strategy firm, takes home ₹95 L liquid after bonus + tax. Horizon 19 years to retirement, high capacity, moderate tolerance (2020 drawdown spooked him).
- 55% equity: 35% Nifty 500 index + 15% Nasdaq 100 ETF + 5% India mid-cap active (Sharpe-screened).
- 30% fixed income: 15% gilt fund + 10% corporate bond fund + 5% arbitrage.
- 10% alternatives: 5% gold ETF + 5% REIT.
- 5% tactical cash for bands.
- IPS rebalance band ±5%, annual review each April.
**Tools:** FundsIndia or Kuvera for goal tracking, KITE for ETFs, Value Research for TER/rolling return.

### Scenario 3 — ANTI-EXAMPLE: Tech Employee, 90% Employer Stock
Ravi, 39, Engineering Director at a US-listed tech firm; RSUs auto-vest and sit unsold. Net worth ₹2.4 cr, of which ₹2.16 cr (90%) is employer stock. Sector correction halves the stock:
- Employer stock: ₹2.16 cr → ₹1.08 cr (−₹1.08 cr).
- Non-employer assets: ₹24 L unchanged.
- Net worth: ₹2.4 cr → ₹1.32 cr; **wealth loss ≈ ₹108 L**.
- Planned home purchase (₹1.5 cr) delayed ~4 years; had he held a 15% cap, loss would have been ~₹18 L and the home plan intact.
**Root cause:** no IPS, no concentration cap, no systematic vest-and-sell rule.
**Tools that would have helped:** Carta for RSU visibility, Morningstar X-Ray for overlap, a written IPS with a 15% single-security ceiling.

---

## 7. Implementation Playbook — Draft Personal IPS
1. **List goals** (artifact: 3-column sheet — goal, corpus needed in today's ₹, year).
2. **Compute risk capacity** (artifact: net-worth statement + income stability score).
3. **Score risk tolerance** (artifact: 10-question questionnaire, keep lower of capacity vs tolerance).
4. **Set Strategic Asset Allocation** (artifact: % table across equity/debt/alts/cash with ±5% bands).
5. **Define constraints** (artifact: one-pager on tax, liquidity, ESG, employer-stock cap).
6. **Pick instruments per bucket** (artifact: shortlist — index ETF, debt fund, gold/REIT — filtered on TER, tracking error, 10-yr rolling).
7. **Write rebalance + review rule** (artifact: IPS Section 7 — band-based trigger + annual April review).
8. **Automate execution** (artifact: SIP orders, RSU vest-and-sell standing instruction, quarterly dashboard in Personal Capital/INDmoney).

---

## 8. Content Quality Audit
**Covered well:** definition of investment analysis; core principles (risk, diversification, alignment); four key terms; two illustrative examples (P/E comparison, bond YTM + rating).
**Underplayed in source:**
- Formal IPS construction process (goals × capacity × horizon × constraints).
- Passive vs active debate and evidence on after-fee underperformance.
- TER drag compounding over 20–30 years (silent CAGR killer).
- Tax-loss harvesting and tax-efficient location (debt in tax-deferred, equity in taxable).
- RSU/ESOP concentration risk — structurally critical for tech employees.
- Alternatives framing: hedge funds, private credit, venture, crypto sizing rules.
- Risk capacity vs risk tolerance distinction.
- Benchmark selection and alpha measurement discipline.

**Supplement with:**
1. Bodie, Kane & Marcus, *Investments*, 12th ed. (McGraw-Hill, 2020) — canonical textbook.
2. Burton Malkiel, *A Random Walk Down Wall Street*, 12th ed. (W.W. Norton, 2020) — passive investing case.
3. William Bernstein, *The Four Pillars of Investing*, 2nd ed. (McGraw-Hill, 2023) — theory/history/psychology/business of investing.
4. CFA Institute, *Investment Policy Statement* readings (Level III curriculum) — IPS process.
5. David Swensen, *Unconventional Success* (Free Press, 2005) — individual-investor asset allocation.

**Red flags in source:**
- Maria scenario judges funds primarily on "past performance" — regulators and literature warn this is a weak predictor; should weight TER, tracking error, process.
- "Higher return = higher risk" stated as law; true on average, not per security — risk can exist without commensurate return.
- No mention of concentration risk, TER compounding, or IPS — the three highest-impact topics for a tech professional.

---

## 9. Quick-Recall Card
- Investment analysis = systematic match of assets to goals, horizon, and risk capacity — not stock-picking theatre.
- Sequence is Economic → Industry → Company → Security; skipping the macro layer is how sectors bury portfolios.
- Three silent wealth-killers: employer-stock concentration, TER drag, and inflation on "safe" FDs.
- An IPS (goals × capacity × horizon × constraints → SAA with bands) is the single highest-leverage artifact you can write this quarter.
- Risk *capacity* is math; risk *tolerance* is emotion — honour the smaller of the two.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Given my goals, horizon, and true risk capacity, what written IPS and asset allocation should govern every rupee — including vesting RSUs — for the next decade?"

---

**Connects to:** [02-time-value-of-money.md](02-time-value-of-money.md), [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [09-portfolio-construction-diversification.md](09-portfolio-construction-diversification.md), [../financial-management/](../financial-management/), [../business-valuation/](../business-valuation/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [1, 2, 3, 4, 6, 8, 9]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ cost; IT tooling; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A2
-->
