# Portfolio Performance Evaluation

## Overview
Portfolio performance evaluation is the process of measuring how well an investment portfolio has done relative to its objectives, benchmarks, and the risks taken. It goes beyond simply looking at raw returns by adjusting for risk, comparing against appropriate benchmarks, and breaking down the sources of performance. This discipline ensures that investment decisions are accountable and that managers are rewarded for skill rather than luck.

---

## Why It Matters
Without rigorous performance evaluation, it is impossible to know whether a portfolio manager is adding value or simply riding a bull market. Investors need to distinguish between returns earned through genuine skill and those resulting from taking on excessive risk. Performance evaluation also identifies areas for improvement, validates the investment strategy, and builds trust between managers and their clients.

## Key Principles
- Raw returns must be adjusted for risk to provide a fair comparison across portfolios with different risk levels
- Benchmarks should be appropriate and investable so that comparisons are meaningful
- Attribution analysis decomposes returns into components such as asset allocation decisions and security selection to identify the sources of outperformance or underperformance
- Consistent evaluation over multiple periods is more informative than focusing on a single quarter or year

## Key Terms
| Term | Definition |
|------|------------|
| **Alpha** | The excess return of a portfolio relative to its benchmark after adjusting for risk, representing manager skill |
| **Treynor Ratio** | A risk-adjusted performance measure that divides excess return by beta, focusing on systematic risk |
| **Jensen's Alpha** | A measure of the portfolio's return above or below the return predicted by CAPM for its level of systematic risk |
| **Information Ratio** | The ratio of a portfolio's excess return over a benchmark to the variability of that excess return, measuring consistency of outperformance |

## Use Case
An institutional investor reviews the quarterly performance reports of five equity managers, comparing their alphas and information ratios to determine which managers are consistently adding value and which should be replaced.

## Scenario
> A nonprofit endowment board meets to review its investment portfolio. The investment consultant presents a report showing the portfolio returned 9 percent over the past year, compared to the benchmark's 8 percent. After adjusting for the slightly higher risk taken, the consultant shows a positive Jensen's alpha of 0.5 percent, confirming that the manager's security selection decisions genuinely added value rather than just reflecting extra risk.

## Examples
- Using the Sharpe ratio to compare a hedge fund's performance against a simple index fund to determine if the hedge fund's higher fees are justified by superior risk-adjusted returns
- Conducting attribution analysis to discover that a portfolio's outperformance came primarily from overweighting the healthcare sector rather than from picking individual winning stocks

---

## Audited Appendix

# Portfolio Performance Evaluation
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Portfolio Performance Evaluation
**Audited on:** 2026-04-18
**Audited by:** A3
**Source files reviewed:** `investment-analysis-portfolio/content/12-portfolio-performance-evaluation.md`

---

## 1. Topic Snapshot
Portfolio performance evaluation is the discipline of measuring realised returns against objectives, benchmarks and risks taken — adjusting raw returns for volatility, selecting the right yardstick, and decomposing returns into skill vs luck vs market beta. An IT/AI/Product/Consulting leader (sitting on an endowment board, reviewing a family-office advisor, or overseeing a treasury/fund manager) must demand risk-adjusted + attribution reports — not just raw returns — because a 9% vs 8% benchmark win can hide either true alpha (+0.5% Jensen) or smuggled-in beta/leverage. The decision: keep, replace, resize, or renegotiate fees for every manager on the roster.

---

## 2. Jargon & Terminology

| # | Term | One-line Definition | Where It Matters |
|---|------|---------------------|------------------|
| 1 | Alpha | Excess return over benchmark after adjusting for risk | Core skill measure |
| 2 | Jensen's Alpha | Rp − [Rf + βp·(Rm − Rf)] — CAPM-adjusted alpha | Manager screening |
| 3 | Sharpe Ratio | (Rp − Rf) / σp — reward per unit of total risk | Cross-strategy ranking |
| 4 | Sortino Ratio | (Rp − Rf) / σ_downside — punishes only downside vol | Asymmetric return funds |
| 5 | Treynor Ratio | (Rp − Rf) / βp — reward per unit of systematic risk | Diversified portfolios only |
| 6 | Information Ratio (IR) | (Rp − Rb) / Tracking Error | Active manager evaluation |
| 7 | Tracking Error | Std dev of (Rp − Rb) | Active risk budget |
| 8 | Active Return | Rp − Rb | Manager contribution |
| 9 | Beta (β) | Sensitivity to market | CAPM decomposition |
| 10 | Benchmark Selection | Picking an investable, style-matched index ex-ante | Guards against post-hoc gaming |
| 11 | Brinson Attribution | Allocation + Selection + Interaction = Total Active | Decompose sources of alpha |
| 12 | Time-Weighted Return (TWR) | Geometric chain; removes cashflow-timing | GIPS manager comparison |
| 13 | Money-Weighted Return (MWR/IRR) | IRR of flows; reflects investor's actual $ experience | Individual outcome |
| 14 | GIPS Standards | CFA Institute global standard for return reporting | Institutional mandates |
| 15 | Drawdown | Peak-to-trough % loss | Path-dependent risk |
| 16 | Maximum Drawdown (MDD) | Worst peak-to-trough across history | Tail/behaviour risk |
| 17 | Calmar Ratio | Annualised Return / |MDD| | Trend/CTA evaluation |
| 18 | Upside / Downside Capture | % of benchmark's up-moves / down-moves captured | Defensive vs aggressive style |
| 19 | M² (Modigliani-Modigliani) | Sharpe re-scaled to market-risk units (in % terms) | Client-friendly Sharpe |
| 20 | Style Analysis (Sharpe 1992) | Regression of returns on style indices | Detecting style drift |
| 21 | Factor Attribution (Fama-French) | Decomposes α into value/size/momentum/quality factors | Modern manager due-diligence |

---

## 3. Frameworks & Matrices

### 3.1 Risk-Adjusted Metric Ladder
**Purpose:** Pick the right metric for the right question; no single ratio is sufficient.

```
                           WHAT QUESTION?
                                |
   +-------+-------+-------+-------+-------+-------+
   |       |       |       |       |       |       |
Total    Down    Systemic Active   CAPM    Tail
risk?    risk?   risk?    vs Bench skill?  risk?
   |       |       |       |       |       |
 Sharpe Sortino Treynor    IR    Jensen α Calmar
```
**Components:** Sharpe (broad), Sortino (asymmetric strategies), Treynor (well-diversified), IR (active mgmt), Jensen α (CAPM residual), Calmar (trend/path-sensitive).
**Worked example (Consulting lens):** Due-diligence on an AI-thematic long-only fund: Sharpe 0.9, IR 0.55, Jensen α +1.2%, Calmar 0.7 — ladder passes → shortlist.
**Trigger:** Any new manager onboarding or quarterly review.

### 3.2 Brinson Attribution Waterfall
**Purpose:** Decompose active return into allocation skill vs security-selection skill.

```
 Total Active Return (Rp - Rb) = +1.00%
  |
  |-- Allocation Effect  : Σ (wp - wb) x Rb          = +0.70%   <- sector/asset bets
  |-- Selection Effect   : Σ wb x (Rp_sector - Rb)   = +0.20%   <- stock picks within sector
  |-- Interaction Effect : Σ (wp - wb) x (Rp - Rb)   = +0.10%
  =====================================================
  Total                                              = +1.00%
```
**Components:** Allocation (top-down), Selection (bottom-up), Interaction (cross-term).
**Worked example (Product/AI lens):** Endowment's 12% vs 11% benchmark — Brinson reveals 0.7% from healthcare overweight (allocation), only 0.2% from stock selection → mandate is an "asset-allocator", not a "stock-picker"; renegotiate fees accordingly.
**Trigger:** Any time outperformance > 50 bps — always ask "from where?".

### 3.3 TWR vs MWR Decision Tree
**Purpose:** Pick the right return definition for the right audience.

```
Who is being evaluated?
      |
   +--+-----------------------+
   |                          |
Manager skill            Individual investor
(external cashflows        (own behaviour,
 out of mgr control)        timing, contributions)
   |                          |
  TWR                         MWR (IRR)
(GIPS-compliant)          (reflects $ outcome)
```
**Components:** TWR = geometric chain of sub-period returns; MWR = IRR that discounts flows to zero.
**Worked example (PM lens):** Founder's family office — show TWR to compare against peer managers; show MWR to founder to reveal behavioural drag from chasing returns.
**Trigger:** Any manager review (TWR) or personal wealth review (MWR).

### 3.4 Up / Down Capture Ratio Matrix (Optional)
```
                  Down-Capture
                 Low        High
              +----------+----------+
     High     | Ideal    | High-beta|
Up-           | (alpha)  |  aggress.|
Capture       +----------+----------+
     Low      | Defensive| Avoid    |
              | (bonds-  | (drag)   |
              |  like)   |          |
              +----------+----------+
```
**Trigger:** Style classification + regime-sensitivity check.

---

## 4. Formulas

### 4.1 Sharpe & Sortino
- **Sharpe = (Rp − Rf) / σp**; threshold: > 1.0 good, > 2.0 excellent, < 0.5 weak.
- **Sortino = (Rp − Rf) / σ_downside**; preferred for asymmetric/option-like funds.
- *Example:* AI-thematic fund Rp 14%, Rf 5%, σ 10% → Sharpe = 0.9 (acceptable for concentrated thematic).

### 4.2 Treynor
- **Treynor = (Rp − Rf) / βp**; use only if portfolio is well-diversified.
- *Example:* β = 1.1, Rp 12%, Rf 5% → Treynor = 6.36%.

### 4.3 Jensen's Alpha
- **α_J = Rp − [Rf + βp · (Rm − Rf)]**; threshold: +1% after fees is meaningful; statistical significance needs 3+ yrs.
- *Example:* Manager A: Rp 10%, Rf 5%, β 0.9, Rm 9% → α = 10% − [5 + 0.9·4] = +1.4% → retain.

### 4.4 Information Ratio
- **IR = (Rp − Rb) / Tracking Error**; threshold: 0.4 average, 0.6 good, 1.0 elite.
- *Example:* Active return 2%, TE 3.6% → IR = 0.55 → keep.

### 4.5 M² (Modigliani-Modigliani)
- **M² = Rf + Sharpe_p × σ_m**; re-scales Sharpe to market-risk units, reads in % return terms — board-friendly.
- *Example:* Sharpe 0.9, σ_m 15%, Rf 5% → M² = 5 + 0.9·15 = 18.5% → fund equivalent to 18.5% market-risk return.

### 4.6 Brinson Attribution
- **Allocation = Σ (wp − wb) × Rb**
- **Selection = Σ wb × (Rp_sector − Rb_sector)**
- **Interaction = Σ (wp − wb) × (Rp_sector − Rb_sector)**

### 4.7 TWR vs MWR
- **TWR:** (1 + R1)·(1 + R2)·...·(1 + Rn) − 1 (geometric chain of sub-period returns between cashflows).
- **MWR:** solve for IRR such that Σ CFt / (1+IRR)^t = 0.
- *Example:* Large inflow right before drawdown → MWR < TWR (investor timing penalty); don't punish manager.

### 4.8 Calmar
- **Calmar = Annualised Return / |MDD|**; threshold: > 0.5 acceptable, > 1 strong.

---

## 5. Do vs Don't

| Do | Don't |
|----|-------|
| Adjust all returns for risk (Sharpe/Sortino/Jensen) | Don't compare managers on raw returns alone |
| Pick benchmarks ex-ante, investable, style-matched | Don't pick/switch benchmarks post-hoc to flatter numbers |
| Report TWR for manager skill evaluation | Don't compare MWR across managers — cashflow timing is not their skill |
| Always report MDD alongside return | Don't ignore drawdowns; a 30% MDD may break the investor behaviourally |
| Evaluate over ≥ 3-yr rolling windows and full market cycles | Don't cherry-pick 1-yr windows or rolling since-inception favourable starts |
| Decompose alpha via Brinson + factor attribution | Don't credit "alpha" that is actually small-cap/value/momentum factor beta |
| Fee-adjust (net of fees) before ranking | Don't compare gross returns when fee structures differ |
| Test for style drift annually (Sharpe 1992) | Don't assume the strategy today = strategy at mandate |

---

## 6. Real-Life Scenarios

### Scenario 1 — HNI Reviewing 3 Wealth Managers (PM/Founder lens)
A tech founder with ₹80 cr spread across 3 PMS managers commissions a 3-yr rolling review. Metrics: Sharpe, IR, Brinson, MDD. Manager X: Sharpe 1.1, IR 0.7, MDD −12% → keep and top up. Manager Y: Sharpe 0.6, IR 0.1, MDD −24% → replace. Manager Z: Sharpe 0.9 but 80% of alpha is value-factor beta (via Fama-French) → renegotiate fees to smart-beta pricing.

### Scenario 2 — Endowment Board Brinson Decomposition (Board/Consulting lens)
A nonprofit endowment board sees 12% return vs 11% benchmark. Brinson decomposition: +0.7% allocation, +0.2% selection, +0.1% interaction. Board realises outperformance came from sector allocation, not security selection. Decision: re-scope mandate to "tactical allocator", shrink security-selection fee, hire a passive sleeve for core equity. Saves ~25 bps on ₹500 cr = ₹1.25 cr/yr.

### Scenario 3 — ANTI-EXAMPLE: Founder Fires Low-Vol Manager after 1-yr (What Not To Do)
A SaaS founder fires Manager M after 1-yr underperformance of 200 bps vs S&P 500. Actual strategy: low-vol, sized for drawdown resilience. MDD −15% vs benchmark −28%. In year 2, manager returns +24% vs benchmark +14% — but founder is out. Quantified cost of firing: ~₹6 cr missed return on ₹50 cr corpus + ₹40 lakh transition/tax costs. Root cause: no risk-adjusted evaluation, no MDD tracking, 1-yr window. Fix retro: mandate 3-yr rolling Sharpe + up/down capture before any fire decision.

**Tools:** Bloomberg PORT, Morningstar Direct, eVestment, FactSet, Backstop; Python (`pyfolio`, `riskfolio-lib`, `empyrical`); Power BI attribution dashboards; Addepar/Canoe for family-office aggregation.

---

## 7. Implementation Playbook

1. **Define** the investment policy statement (IPS) objectives + benchmark(s) ex-ante — artifact: signed IPS.
2. **Instrument** return and cashflow capture (TWR engine) — artifact: GIPS-compliant return series in Python/Excel.
3. **Compute** the risk-adjusted ladder (Sharpe, Sortino, Treynor, IR, Jensen α, Calmar) on 1/3/5-yr windows — artifact: quarterly metric dashboard.
4. **Decompose** active return via Brinson (allocation/selection/interaction) + factor attribution (FF5) — artifact: attribution report.
5. **Track** drawdowns, MDD, up/down capture — artifact: rolling drawdown chart + regime table.
6. **Benchmark-audit** yearly: confirm benchmark still investable and style-matched; run Sharpe-1992 style-drift regression — artifact: benchmark-integrity memo.
7. **Review** quarterly with manager; escalate (watchlist → replace) per pre-agreed thresholds — artifact: manager-scorecard + decision log.
8. **Close the loop:** annual IC presentation with keep/replace/resize decisions and fee-renegotiation list — artifact: IC deck + fee schedule update.

---

## 8. Content Quality Audit
- **Covered well:** Definition of performance evaluation, raw-vs-risk-adjusted distinction, benchmark rationale, skill-vs-luck framing, terms (Alpha, Treynor, Jensen, IR), quarterly review use case, endowment-board scenario, hedge-fund-fee justification, attribution insight (sector overweight vs stock picks).
- **Underplayed in source (supplemented above):** Brinson attribution rigor (allocation/selection/interaction math); TWR-vs-MWR distinction and GIPS implications; benchmark-selection discipline (ex-ante, investable, style-matched); factor attribution (Fama-French) to distinguish alpha from factor beta; drawdown-based metrics (MDD, Calmar); GIPS Standards; style-drift detection (Sharpe 1992); up/down capture; M² ratio; anti-example with quantified cost of firing.
- **Supplementary sources:**
  1. Sharpe, W. F. (1992). "Asset Allocation: Management Style and Performance Measurement." *Journal of Portfolio Management*.
  2. Brinson, G. P., Hood, L. R., & Beebower, G. L. (1986/1991). "Determinants of Portfolio Performance." *Financial Analysts Journal*.
  3. Bodie, Z., Kane, A., & Marcus, A. J. (2020). *Investments*, 12th ed.
  4. CFA Institute (2020). *GIPS Standards Handbook*.
  5. Ang, A. (2014). *Asset Management: A Systematic Approach to Factor Investing*.
- **Red flags:** Source lacks TWR/MWR rigor, no Brinson math, no drawdown metrics, no factor-attribution mention, no style-drift test, and no anti-example illustrating cost of evaluation errors.

---

## 9. Quick-Recall Card
- Raw return is noise; risk-adjusted return is signal — always divide by the risk taken.
- Pick the benchmark ex-ante, make it investable, and freeze it — re-benchmarking post-hoc is self-deception.
- Use TWR for managers (removes cashflow timing); use MWR for investors (reveals behavioural drag).
- Brinson decomposes "from where" alpha came — allocation, selection, or interaction.
- MDD, Calmar, and up/down capture tell you whether the investor can actually *hold* the strategy.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Is this manager delivering risk-adjusted, attribution-verified alpha net of fees over a full cycle — or am I paying active fees for smuggled-in beta and luck?"

---

**Connects to:** [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [08-capital-asset-pricing-model.md](08-capital-asset-pricing-model.md), [07-modern-portfolio-theory.md](07-modern-portfolio-theory.md), [../business-valuation/](../business-valuation/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [1 Topic Snapshot tightened to role-lens; 2 Jargon expanded to 21 rows; 3 added TWR/MWR tree + Up/Down matrix; 4 added Brinson + M² + Calmar with thresholds; 5 Do/Don't expanded to 8; 6 added anti-example w/ cost; 8 supplements + red flags]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ quantified cost; IT tooling (pyfolio/riskfolio-lib/Power BI/Addepar); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A3
-->
