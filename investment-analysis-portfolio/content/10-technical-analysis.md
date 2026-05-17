# Technical Analysis

## Overview
Technical analysis is a method of evaluating securities by studying historical price and volume data to forecast future price movements. Unlike fundamental analysis, which looks at financial statements and economic factors, technical analysis focuses entirely on market data and chart patterns. Practitioners believe that price movements follow identifiable trends and patterns that tend to repeat over time.

---

## Why It Matters
Technical analysis provides tools for timing investment decisions, helping traders and investors decide when to buy or sell. Even fundamental investors often use technical analysis to refine their entry and exit points. While no method can predict the future with certainty, technical analysis offers a disciplined framework for interpreting market behavior, identifying trends, and managing the timing of trades.

## Key Principles
- Price movements tend to follow trends, and once a trend is established it is more likely to continue than to reverse
- Historical price patterns and chart formations often repeat because they reflect consistent human behavior
- Volume confirms price trends: a price move accompanied by high volume is considered more significant than one on low volume
- Support and resistance levels act as psychological price floors and ceilings where buying or selling pressure tends to concentrate

## Key Terms
| Term | Definition |
|------|------------|
| **Support Level** | A price level where buying interest is strong enough to prevent the price from falling further |
| **Resistance Level** | A price level where selling pressure is strong enough to prevent the price from rising further |
| **Moving Average** | An indicator that smooths price data over a specified period to reveal the underlying trend direction |
| **Relative Strength Index** | A momentum oscillator that measures the speed and magnitude of price changes on a scale of zero to one hundred |

## Use Case
A swing trader uses a combination of moving average crossovers and relative strength index readings to identify stocks that are beginning a new uptrend, entering positions when the short-term moving average crosses above the long-term average and the RSI confirms upward momentum.

## Scenario
> Tom notices that a stock has bounced off the same support level of 50 dollars three times over the past year. When the stock approaches 50 dollars again and the trading volume starts to increase, he buys shares expecting the support to hold once more. The stock rebounds to 60 dollars within weeks, and Tom sells at a profit near the known resistance level.

## Examples
- Using a 50-day and 200-day moving average crossover, known as a golden cross, as a signal that a long-term uptrend is beginning
- Watching for a head-and-shoulders chart pattern to signal that a stock's uptrend is about to reverse into a downtrend

---

## Audited Appendix

# Technical Analysis
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Technical Analysis
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `investment-analysis-portfolio/content/10-technical-analysis.md`

---

## 1. Topic Snapshot
Technical Analysis (TA) is the discipline of forecasting future price moves by studying historical price and volume data, chart patterns, and statistical indicators — it treats the market tape itself as the primary signal, independent of fundamentals. For an IT/AI/Product/Consulting leader, TA literacy matters because (a) quant/momentum vendors and fintech pitch decks lean heavily on TA claims that must be vetted, (b) your own RSU-exit and SIP-top-up decisions are easily hijacked by chart-driven behavioural biases, and (c) any ML-on-market-data product you build will inherit TA's pitfalls (overfitting, data-snooping, lookahead leakage). The decision TA helps you make: *when* to enter/exit a position you already believe in fundamentally, and *whether* a momentum/algo strategy marketed to you is statistically honest.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Support | Support Level | Price floor where buyers repeatedly step in | Captures psychological/order-book demand zone | Prior lows, trendline touches, volume nodes | "Nifty has support at 21,800" |
| Resistance | Resistance Level | Price ceiling where sellers appear | Captures supply/profit-taking zone | Prior highs, round numbers, MA confluence | "Stock facing resistance at 52-week high" |
| Trendline | — | Straight line joining swing lows (up) or highs (down) | Visualises trend direction and slope | 2+ touches on chart; break = trend change | "Trendline break confirms reversal" |
| SMA | Simple Moving Average | Average of last n closes | Smooths noise to show trend | Σ price / n | "50-day SMA is support" |
| EMA | Exponential Moving Average | Weighted MA favouring recent prices | Reacts faster than SMA | α·P + (1−α)·EMA_prev, α=2/(n+1) | "9 EMA crossed 21 EMA" |
| MA Crossover | Golden / Death Cross | Short MA crosses long MA up (golden) or down (death) | Classic trend-change signal | 50-day vs 200-day cross | "Golden cross on Nifty" |
| RSI | Relative Strength Index | Momentum oscillator 0–100 | Flags overbought/oversold | 100 − 100/(1+RS) | "RSI > 70, overbought" |
| MACD | Moving Average Convergence Divergence | Difference of two EMAs plus signal line | Shows momentum shifts and divergences | EMA12 − EMA26; signal = EMA9 | "MACD histogram turned positive" |
| Bollinger Bands | — | SMA ± k standard deviations | Captures volatility envelope | SMA(20) ± 2σ | "Price tagged upper band" |
| Stochastic Oscillator | — | Where close sits within recent high-low range | Momentum/overbought signal | %K, %D smoothing | "Stoch oversold at 15" |
| OBV | On-Balance Volume | Running volume total (+ up days, − down days) | Confirms trend with flow | Cumulative signed volume | "OBV diverging from price" |
| A/D Line | Accumulation/Distribution | Volume-weighted money flow | Detects stealth buying/selling | Money Flow Multiplier × Vol, cumulated | "Distribution on big caps" |
| Candlestick | Doji, Hammer, Engulfing | Single/multi-bar pattern from OHLC | Shows intrabar sentiment | Body, wick, prior context | "Bullish engulfing on daily" |
| Chart Pattern | Head-and-Shoulders, Double Top, Triangles, Flags | Multi-bar shapes implying continuation/reversal | Codifies repeated behaviour | Neckline/break + volume | "H&S top, ₹50 downside target" |
| Fibonacci Retracement | — | 23.6/38.2/50/61.8% pullback levels | Guesses where pullbacks end | Swing high to low × ratios | "Bounced off 61.8% fib" |
| Ichimoku Cloud | Ichimoku Kinko Hyo | Multi-line trend/support system | One-glance trend + S/R | Tenkan, Kijun, Senkou A/B, Chikou | "Price above the cloud" |
| VPA | Volume-Price Analysis | Reads price moves through volume lens | Separates conviction from noise | Volume vs range vs close location | "No volume, no trend" |
| Dow Theory | — | 6 tenets: trends, confirmation, volume | Foundational TA framework | Primary/secondary/minor trends | "Dow transports confirm industrials" |
| Elliott Wave | — | 5-up / 3-down wave structure | Maps crowd psychology cycles | Wave counts + Fibonacci | "We're in wave 3 of 5" |
| Momentum | — | Rate of price change | Captures trend strength | ROC = (P_t / P_{t−n}) − 1 | "12-1 momentum factor" |
| Mean Reversion | — | Prices pull back to average | Counter to momentum regime | z-score vs rolling mean | "Pairs trade mean-revert" |
| Backtesting | — | Simulating strategy on historical data | Estimate edge before risking capital | CAGR, Sharpe, Max DD on past data | "Backtest Sharpe 1.8" |
| Overfitting | Curve-fitting | Strategy tuned to noise, not signal | Destroys out-of-sample performance | Train-vs-test degradation | "It's overfit to 2020 COVID" |
| Data-Snooping Bias | p-hacking in markets | Finding "signal" by testing many rules | Inflated false positives | Deflated Sharpe, Bonferroni | "You snooped 10k indicators" |
| Walk-Forward Test | — | Rolling train/test windows | Mimics real deployment | Anchored or rolling windows | "Walk-forward held up" |

---

## 3. Frameworks & Matrices

### 3.1 Trend-Following vs Mean-Reversion Selector
**Purpose:** Decide *which family* of TA tools fits the current regime — momentum tools lose money in range-bound markets and vice versa.
```
                HIGH VOL / TRENDING
                       |
         Mean-Rev      |   Trend-Follow
         (fade spikes) |   (MA crossover, MACD, breakout)
   LOW  ---------------+---------------  HIGH
   ADX                 |                  ADX
         Mean-Rev      |   Consolidation
         (RSI, BB)     |   (wait / pattern setup)
                       |
                LOW VOL / RANGE-BOUND
```
**Components:** ADX (trend strength), realised vol, BB width, autocorrelation of returns.
**IT/AI lens:** Treat regime detection as a classifier upstream of your strategy — don't deploy one model across regimes. For a product analytics leader, same logic applies: a "growth-hack" that worked in a viral regime dies in steady-state.
**Trigger:** Apply at every portfolio review or before onboarding any momentum vendor.

### 3.2 Indicator Stack (avoid redundancy)
**Purpose:** Combine *complementary* indicator families; don't stack three momentum oscillators and call it confirmation.
```
 +--------------+    +----------------+    +-------------+
 | TREND        |    | MOMENTUM       |    | VOLUME      |
 | MA / MACD    | +  | RSI / Stoch    | +  | OBV / A/D   |
 | Ichimoku     |    | ROC            |    | VPA         |
 +--------------+    +----------------+    +-------------+
        \___________________|___________________/
                    Signal fires only when
                 all three agree (2-of-3 min)
```
**Components:** one from each column; log correlation matrix of indicators.
**IT/AI lens:** Analogous to ensembling — diversity of *error modes* matters more than count of models. A consultant would call this triangulation.
**Trigger:** Every strategy spec and every pitch-deck critique.

### 3.3 Support/Resistance Decision Tree
**Purpose:** Separate real breakouts from false breaks.
```
           Price approaches S/R
                   |
          Volume rising into level?
            /                \
          No                 Yes
          |                   |
   Likely fail/fade      Close beyond level?
                            /        \
                         No           Yes
                         |             |
                    False break    Retest on lower vol?
                    (fade it)           /      \
                                      Yes       No
                                       |         |
                                 CONFIRMED   Wait / skip
                                 BREAKOUT
```
**IT/AI lens:** Same decision logic as feature-flag rollouts — launch only after a canary (retest) passes with low error rate (low volume on retest).
**Trigger:** Any breakout trade, any "stock crossed all-time high" headline.

### 3.4 Backtest Discipline Framework
**Purpose:** Keep research honest.
```
 Raw idea -> In-sample design -> Out-of-sample hold-out
                                       |
                                Walk-forward rolling test
                                       |
                        Apply transaction cost + slippage
                                       |
                        Deflated Sharpe / Bonferroni check
                                       |
                            Paper-trade 3 months
                                       |
                               Go live (small size)
```
**Components:** train/test split, walk-forward windows, costs (bps), multiple-testing correction, paper-trade gate.
**IT/AI lens:** Identical to MLOps promotion pipeline — dev → staging → canary → prod, with monitoring.
**Trigger:** Before any quant product ships or any TA vendor is procured.

---

## 4. Formulas

**4.1 Simple Moving Average**
SMA(n) = (P_1 + P_2 + ... + P_n) / n
*Example:* Last 5 closes 100,102,101,103,104 → SMA(5) = 102. Use: price below 200-SMA commonly flags long-term bear bias.

**4.2 Exponential Moving Average**
EMA(n) = α·P_today + (1 − α)·EMA_yesterday, α = 2/(n+1)
*Example:* n=10 → α ≈ 0.1818. If yesterday's EMA=100 and today P=110, EMA_today = 0.1818·110 + 0.8182·100 = 101.82. EMA reacts ~2× faster than SMA of same length.

**4.3 Relative Strength Index**
RSI = 100 − 100 / (1 + RS); RS = avg gain / avg loss over n (default 14)
*Example:* Avg gain 2.0, avg loss 1.0 → RS=2 → RSI = 100 − 100/3 = 66.7. Thresholds: RSI > 70 overbought (consider trim), < 30 oversold (consider add); bullish divergence = price lower low, RSI higher low.

**4.4 MACD**
MACD = EMA(12) − EMA(26); Signal = EMA(9) of MACD; Histogram = MACD − Signal
*Example:* EMA12=105, EMA26=102 → MACD=+3. MACD crossing above signal line = bullish momentum trigger; histogram shrinking = momentum fading even if trend intact.

**4.5 Bollinger Bands**
Upper = SMA(n) + k·σ(n); Lower = SMA(n) − k·σ(n); typical n=20, k=2
*Example:* SMA(20)=500, σ=10 → bands 480 / 520. BB "squeeze" (bandwidth at 6-month low) often precedes volatility expansion. Tags of upper band in an uptrend are continuation, not sell signals.

**4.6 Rate of Change (Momentum)**
ROC(n) = (P_t / P_{t−n}) − 1
*Example:* 12-1 momentum = return over last 12 months skipping most recent month — the academic Jegadeesh–Titman factor.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Backtest on in-sample, validate on untouched out-of-sample + walk-forward | Don't tune on the full history and call the result a backtest |
| Combine one trend + one momentum + one volume indicator | Don't stack RSI, Stoch, CCI and claim three-way confirmation (they're all momentum) |
| Define stop-loss and position size *before* entry | Don't trade TA signals without a hard stop — a "setup" without risk control is gambling |
| Require volume confirmation at breakouts and retests | Don't chase breakouts on thin volume (majority are false) |
| Bake in realistic transaction costs, slippage, and taxes (STT/GST for IN) | Don't report gross returns from a high-turnover strategy — costs can flip Sharpe negative |
| Treat patterns as probabilistic, not deterministic | Don't confuse pareidolia (pattern-*seeing*) with pattern-*existence* |
| Keep a journal of trades, hypotheses, and outcomes | Don't rely on recall — hindsight memory is biased toward wins |
| Use TA to *time* positions you'd take anyway on fundamentals | Don't let a chart pattern override a broken thesis — price is not the full truth |
| Apply multiple-testing correction (deflated Sharpe) when screening indicators | Don't data-snoop 10,000 rule variants and publish the top one as "the strategy" |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-thematic ETF momentum play
A product leader wants exposure to an AI-thematic ETF (e.g., global robotics/AI index fund). Rather than lump-sum on a headline, she uses a disciplined TA overlay: wait for 50-DMA > 200-DMA (golden cross), RSI(14) between 50–65 (trending but not overbought), and weekly volume above 20-week average. Position size = 1% portfolio risk / (entry − stop), with stop at prior swing low. Exit rule: close < 50-DMA *or* RSI bearish divergence. Result: disciplined entries, fewer FOMO tops, drawdowns bounded by pre-committed stops.

### Scenario 2 — Tech-employee RSU vest exit
An AI engineer vests RSUs worth ₹40 L every quarter and tends to "wait for a better price", often ending up selling at lower levels. New rule: split each vest into 4 tranches; sell one tranche immediately (discipline floor); the remaining three sell on pre-declared technical triggers — (i) break of 50-DMA on daily close, (ii) RSI > 75 overbought fade, (iii) hit of prior resistance from Fibonacci 61.8% of the down-move. Removes emotion, diversifies exit timing, and converts a behavioural problem into a rules-based one.

### Scenario 3 — ANTI-EXAMPLE: retail overfit TA system
A retail investor in Bengaluru builds a "proprietary" system in Excel: 17 indicators, tuned on Nifty 2023 data. In-sample CAGR 42%, Sharpe 2.4. Deploys ₹25 L in Jan 2026. Out-of-sample (Jan–Apr 2026) the system delivers −34% drawdown = **₹8.5 L loss** before he halts. Post-mortem: (a) no out-of-sample hold-out, (b) no walk-forward, (c) transaction costs ignored (turnover 18×/yr → ~3.6% cost drag), (d) parameter grid of 10,000+ combinations = data-snooping, (e) 1-year in-sample = single regime (bull). Fix: deflated Sharpe test would have reduced effective Sharpe to ~0.3, below the paper-trade gate.

**Tools:** TradingView (charts + Pine Script), Python (backtrader, vectorbt, pandas-ta, zipline-reloaded), Zerodha Streak / Kite Connect, Bloomberg Terminal, Thinkorswim, QuantConnect, Amibroker.

---

## 7. Implementation Playbook

1. **Define objective & horizon** — write a one-page spec: asset universe, holding period (intraday / swing / position), target return, max drawdown, benchmark.
2. **Pick the indicator stack** — 1 trend + 1 momentum + 1 volume (e.g., 50/200 SMA + RSI(14) + OBV); justify *why* each adds information.
3. **Codify entry/exit/size rules** — machine-readable (Pine Script, Python, or even a CSV rulebook); no discretionary "I felt it" clauses.
4. **Backtest with discipline** — in-sample 60% / out-of-sample 20% / walk-forward 20%; include bid-ask, STT, brokerage, slippage (assume 5–10 bps/side for liquid equities).
5. **Stress-test regimes** — slice results into bull / bear / sideways / high-vol / low-vol buckets; a strategy that only works in one regime is brittle.
6. **Paper-trade 3 months** — run live on a simulator; compare realised to backtested slippage and fill rates.
7. **Deploy small, scale with evidence** — start at ≤25% of target capital; scale only if live Sharpe stays within 1 SE of backtested Sharpe.
8. **Monitor and review** — weekly dashboard of rolling Sharpe, drawdown, hit-rate, avg R-multiple; kill-switch if drawdown exceeds 1.5× backtest max.

---

## 8. Content Quality Audit

**Covered well:** core indicator list (MA, RSI), support/resistance intuition, golden cross, head-and-shoulders, scenario-driven framing (Tom at ₹50).

**Underplayed / missing:**
- *Backtest rigor*: no treatment of in-sample vs out-of-sample, walk-forward, or multiple-testing correction.
- *Data-snooping bias*: not mentioned; critical given retail access to 100s of indicators in TradingView.
- *Transaction-cost drag*: high-turnover TA strategies can lose 2–5% CAGR to costs; source ignores this.
- *EMH critique*: no discussion of why academic finance is skeptical of pure TA (weak-form efficiency) vs where momentum *does* survive (cross-sectional factor).
- *Momentum-factor academic evidence*: Jegadeesh–Titman (1993) shows 12-1 momentum earns a premium — this is the respectable cousin of charting and should be separated from pattern-reading.
- *Behavioural linkage*: S/R levels are psychological; connect to anchoring and herding in behavioural finance module.
- *Volatility-aware position sizing*: ATR-based stops, Kelly fraction — absent.

**Supplementary sources (≥5):**
1. Murphy, J. J. — *Technical Analysis of the Financial Markets* (NYIF, 1999). Canonical practitioner reference.
2. Pring, M. J. — *Technical Analysis Explained*, 5th ed. (McGraw-Hill, 2014). Indicator/chart-pattern depth.
3. Lo, A. W., & MacKinlay, A. C. — *A Non-Random Walk Down Wall Street* (Princeton, 1999). Academic evidence on predictability.
4. Aronson, D. — *Evidence-Based Technical Analysis* (Wiley, 2006). Statistical rigor, data-snooping, Monte Carlo permutation tests.
5. Jegadeesh, N., & Titman, S. — "Returns to Buying Winners and Selling Losers," *Journal of Finance* 48(1), 1993. Seminal momentum factor.
6. (Bonus) Bailey, D., Borwein, J., López de Prado, M., Zhu, Q. — "The Probability of Backtest Overfitting," *Journal of Computational Finance*, 2016.

**Red flags in typical TA content:** survivorship bias in chart examples (only winning patterns shown), cherry-picked entries without exit rules, zero mention of costs or taxes, "90% win rate" marketing (usually tiny wins / rare huge losses), unfalsifiable frameworks like some Elliott Wave counts.

---

## 9. Quick-Recall Card
- TA = price + volume + patterns; a *timing* layer, not a thesis replacement.
- Three families only: trend, momentum, volume — one indicator per family.
- Breakouts need volume; retests confirm; false breaks are the norm, not the exception.
- Backtest discipline > indicator choice: out-of-sample + walk-forward + costs + multiple-testing correction.
- Beware overfitting, data-snooping, and pattern-pareidolia; momentum (academic) ≠ charting (lore).
- **As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Does this chart/momentum/quant claim survive out-of-sample, walk-forward, and transaction costs — or am I being sold curve-fit noise?"**

---

**Connects to:** [11-behavioral-finance.md](11-behavioral-finance.md), [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [04-security-valuation.md](04-security-valuation.md), [../business-analytics/02-descriptive-analytics.md](../business-analytics/02-descriptive-analytics.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5]
Sections rewritten: [3 (added Backtest Discipline), 4 (added ROC + numeric examples), 6 (quantified anti-example drawdown), 8 (added Bailey/Lopez de Prado supplement)]
Enrichments applied: [cross-course links; 5+ supplements; anti-example with ₹8.5 L quantified cost; IT tooling stack; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A1
-->
