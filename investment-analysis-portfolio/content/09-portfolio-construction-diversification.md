# Portfolio Construction and Diversification

## Overview
Portfolio construction is the practical process of selecting and weighting investments to build a portfolio that meets an investor's goals. Diversification is the strategy of spreading investments across different assets, sectors, and geographies to reduce risk. Together, these practices turn investment theory into real-world portfolios that balance growth, income, and capital preservation.

---

## Why It Matters
Even the best individual investment picks can lead to poor outcomes if a portfolio is poorly constructed. Concentration in a single stock, sector, or country exposes investors to catastrophic losses. Diversification does not guarantee profits, but it systematically reduces the impact of any one investment failing. Thoughtful portfolio construction ensures that the overall mix of assets is aligned with the investor's time horizon, risk appetite, and financial objectives.

## Key Principles
- Asset allocation, the split between stocks, bonds, cash, and alternatives, is the single biggest driver of long-term portfolio performance
- Diversification reduces unsystematic risk but cannot eliminate systematic risk that affects all markets
- Rebalancing periodically brings the portfolio back to its target allocation after market movements cause drift
- Constraints such as taxes, liquidity needs, and regulatory requirements must be factored into portfolio construction

## Key Terms
| Term | Definition |
|------|------------|
| **Asset Allocation** | The process of dividing a portfolio among different asset classes such as equities, bonds, and cash |
| **Rebalancing** | Periodically buying or selling assets to restore a portfolio to its original target allocation |
| **Diversification** | Spreading investments across various assets to reduce the impact of any single investment's poor performance |
| **Strategic vs. Tactical Allocation** | Strategic allocation sets long-term targets, while tactical allocation makes short-term adjustments based on market conditions |

## Use Case
A retirement plan provider designs target-date funds that automatically shift from a growth-oriented stock allocation toward a conservative bond allocation as the participant approaches retirement age, rebalancing quarterly to stay on track.

## Scenario
> Elena has her entire savings in technology stocks because they have performed well recently. When the tech sector drops 30 percent in a correction, her portfolio loses a third of its value. Her advisor helps her rebuild with a diversified mix of domestic stocks, international equities, bonds, and real estate investment trusts. The next time technology stocks decline, her portfolio barely moves because losses in one area are offset by gains in others.

## Examples
- A pension fund allocating 60 percent to equities, 30 percent to fixed income, and 10 percent to alternative investments based on its liability structure and risk budget
- An individual investor adding emerging market bonds to a portfolio of domestic stocks and treasuries to capture higher yields and further diversify across regions

---

## Audited Appendix

# Portfolio Construction and Diversification
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Portfolio Construction and Diversification
**Audited on:** 2026-04-18
**Audited by:** A10
**Source files reviewed:** `investment-analysis-portfolio/content/09-portfolio-construction-diversification.md`

---

## 1. Topic Snapshot
Portfolio construction is the disciplined selection and weighting of assets across classes, geographies, sectors, and factors so that the aggregate risk-return profile (not any single pick) matches the investor's goals, horizon, and constraints; diversification is the engine that neutralises unsystematic risk inside that construction.
An IT/AI/Product/Consulting leader — a founder sitting on illiquid ESOPs, a senior engineer whose RSUs have compounded into 60-70% single-stock concentration, or an HNI post-exit with a lumpsum — faces asymmetric wipe-out risk because their human capital, employer equity, and sector bets are already co-correlated; disciplined allocation is the only lever that converts lucky beta into durable net worth.
Decision: what is the target strategic allocation (by asset class, geography, factor, and liquidity bucket), what rebalancing rule governs drift, and what concentration-unwind glide path protects the next decade of compounding?

---

## 2. Jargon & Terminology

| # | Term | Plain-English Meaning | IT/AI/Product/Consulting Lens |
|---|------|----------------------|-------------------------------|
| 1 | Strategic Asset Allocation (SAA) | Long-term target mix across equities/bonds/alternatives tied to goals | The "architecture diagram" of your wealth — rarely changed, always referenced |
| 2 | Tactical Asset Allocation (TAA) | Short-term tilts away from SAA to exploit valuation/cycle views | Feature-flag on top of core platform; reversible, bounded |
| 3 | Dynamic Asset Allocation | Rule-based continuous adjustment to risk/volatility regime | Auto-scaling group for portfolios — responds to measured signals |
| 4 | Rebalancing (Threshold) | Trigger trades when weight drifts beyond ±band (e.g., 5%) | Alert-driven ops, lower turnover, higher discipline |
| 5 | Rebalancing (Calendar) | Trade on fixed schedule (monthly/quarterly/annual) | Cron job — predictable, may over/under-trade |
| 6 | Rebalancing (Hybrid) | Calendar check + threshold gate | Scheduled review, conditional execution — best of both |
| 7 | Diversification (Asset-Class) | Spread across equity/debt/real-estate/gold/cash | Microservices vs monolith — isolate blast radius |
| 8 | Diversification (Geography) | Domestic + developed + emerging exposure | Multi-region deployment for currency/political risk |
| 9 | Diversification (Sector) | No single industry > cap (e.g., 25%) | Avoid "all-in on one vertical" portfolio concentration |
| 10 | Diversification (Factor) | Blend value/size/momentum/quality/low-vol factors | Ensemble model vs single classifier |
| 11 | Diversification (Currency) | INR + USD + other reserve exposure | Natural hedge for dollar-earning consultants |
| 12 | Correlation Drift | Historically low correlations rise in crises | Cascading failure — dependencies surface under load |
| 13 | Home Bias | Over-allocation to domestic market | Local knowledge bias; caps global opportunity set |
| 14 | Concentration Risk | Single asset/issuer > prudential limit | RSU in employer = double-exposure to job + stock |
| 15 | Rule-of-110 / Age-Based | Equity % = 110 − Age (heuristic glide) | Default config for retail glide path |
| 16 | Glide Path (Target-Date Fund) | Pre-set equity-to-bond transition with age | Roadmap milestones baked into fund |
| 17 | Core-Satellite | Passive low-cost core + active/thematic satellites | 70% stable infra + 30% bets (AI/EV themes) |
| 18 | Risk Parity | Weight assets so each contributes equal risk | Load-balanced risk budget, not dollar-balanced |
| 19 | Factor Investing | Systematic tilts to documented premia | Style beta as a product SKU |
| 20 | ESG Integration | Environmental/Social/Governance screens in weighting | Compliance + values overlay |
| 21 | Tax Location (Asset Placement) | Put tax-inefficient assets in tax-advantaged accounts | Sharded storage by query cost profile |
| 22 | Tax-Loss Harvesting | Realise losses to offset gains; maintain exposure via proxy | Periodic cleanup job with wash-sale guard |
| 23 | Rebalancing Bonus | Return pickup from disciplined buy-low/sell-high | Compounding edge from ops hygiene |
| 24 | Liquidity Budget | % of portfolio accessible within N days | SLA for emergency/opportunistic capital |
| 25 | Private Allocation (VC/PE/Private Credit) | Illiquid high-risk/return sleeve | Long-horizon bets with lock-up cost |
| 26 | Alternatives (Gold/REITs/Crypto) | Non-traditional assets for diversification | Heterogeneous compute — different return drivers |
| 27 | Goal-Bucketing | Separate portfolios per goal/horizon | Namespace-per-tenant isolation |
| 28 | Wash-Sale Rule | Disallows loss if repurchased within 30 days | Cooldown window to keep tax-benefit valid |

---

## 3. Frameworks & Matrices

### 3.1 Asset-Allocation Glide Path
**Purpose:** Illustrate how equity risk should decline as the investor approaches goal date (retirement/liquidity event).
```
Equity %
 100 |*
  90 |  *
  80 |    *                            Rule: Equity = max(20, 110 - Age)
  70 |      *
  60 |        *  <- age 50
  50 |          *
  40 |            *
  30 |              *  <- age 70 (retirement)
  20 |________________*_______________
      25  35  45  55  65  75  Age
```
**Components:** age/horizon axis, equity/bond/alt weights, floor (never below 20% equity to beat inflation), custom overlay for human-capital stage.
**Worked example (IT/AI Lead, age 38):** Equity = 110 − 38 = 72% → 65% public equity (split 40% India / 20% US / 5% EM) + 7% private/VC sleeve; 23% debt; 5% gold/REITs; revisit glide annually.
**Trigger:** Every birthday, every major life event (marriage, child, exit, inheritance), every 10% net-worth jump.

### 3.2 Core-Satellite Architecture
**Purpose:** Combine low-cost passive beta with conviction-driven alpha attempts, without letting satellites dominate risk.
```
+-------------------------------------------------+
|                 PORTFOLIO (100%)                |
|-------------------------------------------------|
|  CORE 70% (passive, broad, low-cost)            |
|  - Nifty 500 index        30%                   |
|  - S&P 500 / Nasdaq 100   20%                   |
|  - Global Aggregate Bond  15%                   |
|  - Gold / REIT             5%                   |
|-------------------------------------------------|
|  SATELLITE 30% (active / thematic / alt)        |
|  - AI/Semiconductor theme 10%                   |
|  - India small-cap / PMS   8%                   |
|  - Private credit / VC     7%                   |
|  - Crypto (BTC/ETH)        5%                   |
+-------------------------------------------------+
```
**Components:** core (cost < 20 bps, broad index), satellite (theme/factor/private), risk cap per satellite (≤10%), total satellite ≤30%.
**Worked example (Product Lead, HNI ₹15 cr):** Core ₹10.5 cr in low-cost index+debt; satellite ₹4.5 cr split across AI-theme ETF, India small-cap PMS, early-stage VC LP commitment (₹1 cr), and 5% crypto.
**Trigger:** Build core first; add satellite only after emergency fund + core funded; rebalance satellites harder than core.

### 3.3 Rebalancing Methodology Matrix
**Purpose:** Choose a rule that balances drift-risk against tax and transaction cost.
```
                   | DRIFT CONTROL | TURNOVER | TAX DRAG | BEST FOR
-------------------+---------------+----------+----------+---------------------
Calendar (Annual)  |     Low       |   Low    |   Low    | Tax-aware HNI
Calendar (Qtr/Mo)  |    Medium     |  Medium  |  Medium  | Retirement funds
Threshold (±5%)    |     High      |  Medium  |  Medium  | Concentrated wealth
Threshold (±10%)   |    Medium     |   Low    |   Low    | Low-turnover HNI
Hybrid (Qtr+±5%)   |     High      |   Low    |   Low    | Most disciplined
```
**Components:** trigger rule, band width, tax account selection, harvesting overlay, transaction-cost estimate.
**Worked example (Consultant, ₹3 cr):** Hybrid — review every quarter, rebalance only if any asset class drifts > 5% from target; pair with tax-loss harvest on losers.
**Trigger:** Any band breach, cash inflow (bonus/dividends), or regime change (rate cycle flip).

### 3.4 Goal-Bucket Framework
**Purpose:** Map capital to goals by horizon and risk tolerance, preventing short-term volatility from derailing long-term compounding.
```
+---------------+------------------+-------------------+
| BUCKET        | HORIZON          | TARGET ALLOCATION |
+---------------+------------------+-------------------+
| Liquidity     | 0-2 yrs          | 100% cash/liquid  |
| (emergency +  |                  | debt MF / FD      |
|  near spend)  |                  |                   |
+---------------+------------------+-------------------+
| Stability     | 3-7 yrs          | 30% eq / 60% debt |
| (kids school, |                  | / 10% gold        |
|  house down)  |                  |                   |
+---------------+------------------+-------------------+
| Growth        | 8-15 yrs         | 70% eq / 20% debt |
| (retirement,  |                  | / 10% alts        |
|  kids college)|                  |                   |
+---------------+------------------+-------------------+
| Legacy        | 15+ yrs          | 85% eq / 10% alts |
| (lifetime/    |                  | / 5% debt         |
|  generational)|                  |                   |
+---------------+------------------+-------------------+
```
**Components:** named goal, horizon, target corpus, SIP/lumpsum plan, sub-allocation, review cadence.
**Worked example (Founder post-exit, ₹50 cr):** Liquidity ₹5 cr (2-yr burn) / Stability ₹10 cr (kids education + parents care) / Growth ₹20 cr (retirement + diversified global) / Legacy ₹15 cr (VC LP + long-duration equity + philanthropy endowment).
**Trigger:** Life event or each goal moving one horizon-bucket closer.

### 3.5 (Optional) Factor-Tilt Matrix for Satellite
**Purpose:** Within satellite sleeve, allocate across documented premia instead of single-stock picks.
```
Factor      | Evidence | Tilt Vehicle                 | Cycle Sensitivity
------------+----------+------------------------------+------------------
Value       |  Strong  | Nifty 200 Value 30 / ETF     | Pro-cyclical
Momentum    |  Strong  | Nifty Momentum 30 index      | Trend-dependent
Quality     |  Strong  | Nifty Quality 30             | Defensive
Low-Vol     |  Strong  | Low-Vol 50 ETF               | Defensive
Size        | Moderate | Small-cap / S&P SmallCap 600 | Pro-cyclical
```
**Trigger:** Use when satellite budget > ₹1 cr and investor has 7+ yr horizon; cap single factor at 10%.

---

## 4. Formulas

### 4.1 Asset-Allocation Contribution
**Formula:** Portfolio Return Rₚ = Σᵢ (wᵢ × Rᵢ)
**Threshold:** Studies (Brinson 1986/1991, Ibbotson 2010) attribute 85-95% of time-series return variance to SAA.
**Example:** Portfolio weights 60% Eq / 30% Debt / 10% Gold. Realised: Eq +18%, Debt +7%, Gold +12% →
Rₚ = 0.60(18) + 0.30(7) + 0.10(12) = 10.8 + 2.1 + 1.2 = **14.1%**.

### 4.2 Rebalancing Threshold
**Formula:** Drift = |Current Weight − Target Weight| / Target Weight; trigger if Drift ≥ band (commonly 5%).
**Threshold:** ±5% relative or ±3% absolute is typical for HNI; tighter (±2%) for institutional.
**Example:** Target Eq = 60%; post-rally Eq = 68%. Drift = |68−60| / 60 = **13.3%** → exceeds 5% → rebalance: sell 8% of NAV from equity, redirect to debt/gold pro-rata.

### 4.3 Portfolio Risk Reduction from Diversification
**Formula:** σₚ² = Σᵢ wᵢ²σᵢ² + ΣᵢΣⱼ≠ᵢ wᵢwⱼσᵢσⱼρᵢⱼ ; and strictly σₚ ≤ Σᵢ |wᵢσᵢ| with equality only when all ρᵢⱼ = 1.
**Threshold:** Pairwise correlations < 0.3 deliver meaningful σ reduction; > 0.7 deliver almost none.
**Example (RSU unwind):** Concentrated: 70% tech RSU (σ = 35%) + 30% cash (σ = 0%) → σₚ = 0.70 × 35% = **24.5%**.
Diversified: 35% tech + 25% diversified India Eq (σ 20%, ρ 0.5) + 20% US Eq (σ 18%, ρ 0.4) + 15% debt (σ 5%) + 5% gold (σ 15%) →
σₚ² ≈ 0.35²(35)² + 0.25²(20)² + 0.20²(18)² + 0.15²(5)² + 0.05²(15)² + cross terms ≈ 150 + 25 + 13 + 0.6 + 0.6 + ~85 (cross) ≈ 274 → σₚ ≈ **16.5%**.
**Risk reduction: 24.5% → 16.5% (≈33% lower volatility) for similar expected return.**

### 4.4 Tax-Loss Harvesting Benefit
**Formula:** Benefit ≈ (Realised Losses × Marginal Tax Rate) − Transaction Costs − Wash-Sale Cost − Tracking-Error Cost of Proxy
**Threshold:** Worthwhile if realised loss ≥ ₹1 L and Benefit ≥ 0.2% of portfolio.
**Example:** Consultant has ₹12 L short-term losses in tech ETF; marginal tax 30%; transaction cost ₹3,000; buys proxy Nasdaq-100 fund avoiding wash sale.
Benefit = 12,00,000 × 0.30 − 3,000 = ₹3,60,000 − 3,000 = **₹3,57,000** saved in taxes this year, while maintaining market exposure.

### 4.5 (Optional) Glide-Path Equity %
**Formula:** Equity % = max(20, 110 − Age); Debt % = 100 − Equity − Alts
**Threshold:** Floor of 20% equity even at 90+ to counter longevity/inflation risk; US variants use 120-Age for aggressive.
**Example:** AI Lead, age 34 → Equity 76% (split 60 public / 16 private-themed); Debt 19%; Alts 5%. At 55 → Equity 55%; at 70 → Equity 40%.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|-----|-------|
| 1 | Fix SAA first; treat TAA as ≤10% overlay | Don't let TAA creep into SAA one tilt at a time |
| 2 | Unwind employer RSU to ≤10% of net worth on a scheduled glide | Don't hold 40%+ in employer stock "because it has momentum" |
| 3 | Use hybrid rebalancing (calendar + threshold) with written rules | Don't rebalance emotionally on headlines |
| 4 | Place tax-inefficient assets (debt, REIT) in tax-advantaged accounts | Don't hold growth equity in high-turnover taxable pockets |
| 5 | Diversify across class, geography, factor, and currency | Don't confuse 20 Indian large-cap funds with diversification |
| 6 | Maintain 2-year liquidity bucket separate from growth portfolio | Don't invade growth to fund short-term needs in drawdowns |
| 7 | Document IPS (Investment Policy Statement) with bands and triggers | Don't operate without written allocation and rebalancing rules |
| 8 | Harvest tax losses annually with wash-sale safeguards | Don't sell + repurchase inside 30-day window and lose the benefit |
| 9 | Cap private/illiquid sleeve to what you can lock for 7-10 years | Don't overload illiquid bets that force fire-sales later |

---

## 6. Real-Life Scenarios

### Scenario 1 — Tech Employee with 70% Single-Stock RSU
**Context:** Priya, Staff Engineer at a US-listed SaaS firm, Bengaluru, age 33. Net worth ₹6 cr of which ₹4.2 cr (70%) is vested employer RSU + unvested ESPP. Income is also 100% from the same employer.
**Risk:** Job + equity doubly correlated; 40% drawdown on the stock + layoff = wipe-out of next decade.
**Playbook:**
1. Compute long-term-capital-gains impact; use 10b5-1 plan to sell predictable quarterly lots.
2. Glide path: cut employer stock from 70% → 35% in Year 1 → 15% in Year 2 → 10% by Year 3.
3. Redeploy into 60% diversified public equity (India + US + EM), 20% debt, 10% gold/REIT, 10% satellite (AI theme + VC LP).
4. Harvest losses on any red RSU lots; use proceeds to seed the emergency bucket (18 months of expenses).
5. Resulting σₚ falls from ~24% to ~14% with similar expected return.
**Tools:** Personal Capital, Carta, Zerodha Coin, Morningstar X-Ray, Python (portfoliolab), Excel RSU unwind model.

### Scenario 2 — Founder Post-Exit, Goal-Bucket Framework
**Context:** Arjun, 42, sold AI-infra startup; ₹50 cr post-tax. Wants to (a) never work again under duress, (b) fund two kids' global education, (c) leave legacy / angel-invest.
**Playbook:**
1. Liquidity Bucket (5-yr living + contingencies) — ₹7 cr in liquid + ultra-short + arbitrage + FD ladder.
2. Stability Bucket (10-yr kids' education) — ₹12 cr in 30% equity / 60% debt / 10% gold; SIP-rebalanced annually.
3. Growth Bucket (15-yr retirement) — ₹20 cr at 70/20/10 (India+US+EM eq / debt / alts); hybrid rebalance.
4. Legacy Bucket (15+ yr + angel) — ₹11 cr split: ₹4 cr VC LP commitments over 4 years, ₹3 cr thematic AI/semi, ₹3 cr global quality/momentum factor tilt, ₹1 cr crypto (BTC/ETH only).
5. Written IPS with quarterly family-office review; tax-location optimised.
**Tools:** Morningstar X-Ray, Kuvera, Zerodha, Wealthsimple, Python (pyfolio, portfoliolab), family-office CRM.

### Scenario 3 — ANTI-EXAMPLE: PM Skips Rebalancing for 3 Years
**Context:** Rahul, Product Manager at a fintech, ₹4 cr portfolio started 2021 at target 55% eq / 35% debt / 10% gold. Inside equity, Indian tech + US tech = 40%.
**What happened:** 2021-2023 tech run-up; Rahul never rebalanced ("it's working, why touch it").
- By end-2023: Equity drifted to 78%, tech weight inside equity = 68% (≈ 53% of portfolio).
- 2024 tech correction: tech basket −42%, other equity −12%, debt +7%.
- Portfolio: before correction ₹6.8 cr; after correction ₹4.6 cr — **erased 5 years of gains, ₹2.2 cr lost**.
- If he had followed hybrid rebalancing (quarterly + ±5% band), drawdown would have been ≈ ₹0.9 cr (≈ ₹1.3 cr saved) — the rebalancing bonus and risk-control effect combined.
**Lesson:** A perfect SAA without governance is worse than a mediocre SAA with governance; drift is the silent tax on undisciplined portfolios.
**Tools:** Morningstar X-Ray (drift heatmap), Zerodha Console holdings report, Excel rebalancing template.

---

## 7. Implementation Playbook
1. **Draft** an Investment Policy Statement (IPS) — goals, horizon, risk tolerance, constraints, SAA bands (artifact: IPS v1 Google Doc).
2. **Compute** current allocation and concentration across class / sector / geography / employer-stock (artifact: Morningstar X-Ray + Excel concentration dashboard).
3. **Design** target SAA using glide path + goal-bucket framework; size satellite ≤30% (artifact: allocation.xlsx with SAA, bands, rebalance rule).
4. **Build** core with low-cost index ETFs/funds; stage satellite with factor tilts and private commitments (artifact: Zerodha/Kuvera basket + PMS onboarding).
5. **Unwind** concentration (employer RSU/single-stock) via 10b5-1 schedule or quarterly tax-aware lots (artifact: RSU glide schedule CSV with post-tax targets).
6. **Automate** rebalancing monitor (threshold alerts) and tax-loss harvest scan quarterly (artifact: Python portfoliolab notebook + calendar reminder).
7. **Review** quarterly vs IPS; annual deep-dive with CA for tax-location + harvest; trigger-based review on life events (artifact: quarterly review PDF).
8. **Document** every deviation from IPS with rationale and sunset clause (artifact: deviation log in IPS appendix).

---

## 8. Content Quality Audit
**Covered well:** asset allocation taxonomy, diversification across classes/geography, basic rebalancing, glide path, goal bucketing, core-satellite, RSU concentration case.
**Underplayed:**
- Tax-location / asset-placement optimisation across taxable vs tax-advantaged accounts.
- Quantification of rebalancing bonus (2% drag vs +0.5%/yr pickup depending on regime and cost).
- Factor tilt integration inside satellite — when and how much.
- ESG integration mechanics (exclusion vs best-in-class vs tilt).
- Private-market allocation constraints (illiquidity premium, J-curve, capital-call management).
- Custom glide-path vs off-the-shelf Target-Date Fund (human-capital overlay).
- Wash-sale rules (US) and Indian STCG/LTCG harvesting specifics.
- RSU concentration playbook (10b5-1, exchange funds, collars, direct indexing).
- Correlation drift under stress (2008, 2020) — diversification myth under tail events.

**Supplementary sources (≥5):**
1. David Swensen, *Unconventional Success* (2005) — individual-investor asset allocation.
2. Burton Malkiel, *A Random Walk Down Wall Street*, 12th ed. (2020) — index core + diversification.
3. Bodie, Kane, Marcus, *Investments*, 12th ed. (2020) — formal portfolio construction.
4. Andrew Ang, *Asset Management* (2014) — factor investing and risk budgeting.
5. William Bernstein, *The Four Pillars of Investing*, 2nd ed. (2023) — allocation and behavioural pillars.

**Red flags:**
- Advising fixed 60/40 regardless of age/human-capital stage.
- Treating diversification as "buy more funds" rather than low-correlation exposures.
- Ignoring currency exposure for dollar-earning Indian consultants.
- Oversold "private is always better" — ignores lock-up and capital-call risk.
- Using Rule-of-110 as the final answer instead of a starting heuristic.

---

## 9. Quick-Recall Card
- SAA drives 85-95% of long-term return variance; get it right, then leave it alone.
- Diversification cuts unsystematic risk only — hedge systematic risk via allocation and liquidity bucket, not more equity funds.
- Rebalance with written hybrid rule (calendar + ±5% band); automate the monitor.
- Unwind employer RSU to ≤10% on a glide path; concentrated wealth is bet, not a portfolio.
- Bucket by goal and horizon so drawdowns never touch the liquidity layer.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"What is my written target allocation, rebalancing rule, and 3-year unwind path for every concentrated position — and does my portfolio still stand if my employer/sector halves tomorrow?"**

---

**Connects to:** [07-modern-portfolio-theory.md](07-modern-portfolio-theory.md), [08-capital-asset-pricing-model.md](08-capital-asset-pricing-model.md), [12-portfolio-performance-evaluation.md](12-portfolio-performance-evaluation.md), [01-introduction-investment-analysis.md](01-introduction-investment-analysis.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:4, 4:4, 5:5, 6:5, 7:4, 8:5, 9:5, 10:5]
Sections rewritten: [3.3 rebalancing matrix expanded; 4.3 diversification math with numeric RSU unwind; 6.3 anti-example quantified with ₹2.2 cr loss]
Enrichments applied: [cross-course links; 5 supplements (Swensen, Malkiel, BKM, Ang, Bernstein); anti-example w/ ₹ cost; IT tooling (Personal Capital, Kuvera, Zerodha Coin, Morningstar X-Ray, Wealthsimple, Python portfoliolab, Excel); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A10
-->
