# Risk and Information (Expected Value/Utility, Insurance, Moral Hazard, Adverse Selection, Auctions, Decision Trees)


## Overview

This topic explains decision-making under uncertainty. It covers how people value risky outcomes and how lack of information creates market problems.


## Why It Matters

Managers face uncertain demand, costs, and competitor moves. Better risk thinking improves pricing, warranties, insurance, bidding, and investment decisions.


## Key Principles

- Expected value summarizes average outcome.
- Risk-averse people prefer certainty.
- Insurance reduces risk but creates moral hazard/adverse selection.
- Information has value; decision trees help structure choices.
- Auctions require smart bidding (avoid winner’s curse).


## Key Terms

| Term | Definition |
|------|------------|
| **Expected Value** | Probability-weighted average. |
| **Expected Utility** | Utility-weighted evaluation of risky choices. |
| **Risk Premium** | Extra amount someone pays to avoid risk. |
| **Moral Hazard** | Risky behavior after being insured. |
| **Adverse Selection** | High-risk people more likely to buy insurance. |
| **Winner’s Curse** | Overpaying in common-value auctions. |


## Use Case

A firm bids for a government contract using a decision tree.


## Scenario

> Two companies bid for a mining block. True value is uncertain. The winner might have been overly optimistic—winner’s curse risk.


## Examples

- Warranty programs reduce customer risk but may increase careless usage.
- Using market research can be worth it if it prevents a wrong launch.

---

## Audited Appendix

# Risk and Information (Expected Value/Utility, Insurance, Moral Hazard, Adverse Selection, Auctions, Decision Trees)
**Course:** Microeconomics for Managers  
**Module:** Content  
**Audited on:** 2026-04-19  
**Audited by:** A1  
**Source files reviewed:** `microeconomics-for-managers/content/16-risk-and-information.md`

---

## 1. Topic Snapshot
Risk and information explain how to choose when outcomes are uncertain and when other people know more than you do.
For IT/AI/Product/Consulting leaders, this is the logic behind launch gating, insurance design, warranty policy, bidding, and evidence-based decision making. [verified from model knowledge, not source]
The decision it helps make is whether to pay to reduce risk, redesign incentives, or bid conservatively when information is incomplete.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| expected value | EV | The average outcome after weighting each result by its probability. | Gives a baseline for comparing risky options. | `sum(p_i x_i)` across outcomes. | Finance, bidding, launch planning. |
| expected utility | EU | A risk-adjusted way to evaluate uncertain outcomes. | Captures that people care about risk, not just averages. | `sum(p_i U(x_i))`. | Insurance, economics, decision science. |
| utility | - | A satisfaction score used to rank risky and safe choices. | Lets managers compare choices with different risk levels. | Utility units or utility functions. | Microeconomics, product trade-offs. |
| risk premium | - | The extra amount someone will pay to avoid risk. | Shows how much risk aversion matters in real decisions. | `EV - certainty equivalent`. | Insurance, contract design, treasury. |
| certainty equivalent | CE | The guaranteed amount that feels as good as the risky option. | Converts a gamble into a comparable cash value. | Monetary amount. | Pricing, negotiation, capital budgeting. |
| risk-averse | - | A person who prefers a sure outcome to a fair gamble. | Explains why insurance and hedging exist. | Compare CE to EV. | Executive decision making, economics. |
| moral hazard | - | Riskier behavior after protection is in place. | Warns that insurance can change incentives. | Claims frequency, usage patterns, loss rates. | Insurance, SaaS guarantees, warranties. |
| adverse selection | - | High-risk people are more likely to buy coverage. | Explains why pooled markets can break without screening. | Claims mix, enrollment mix, churn mix. | Insurance, lending, hiring. |
| winner's curse | - | Paying too much in an auction because the winner is the most optimistic bidder. | Prevents overbidding when the true value is uncertain. | Bid vs realized value gap. | Auctions, M&A, vendor selection. |
| decision tree | - | A structured map of choices, chance events, and payoffs. | Makes uncertainty visible and comparable. | Branch probabilities and expected payoff. | Strategy, product launches, capital projects. |
| common-value auction | - | An auction where the item has one true value, but bidders estimate it differently. | Explains why information quality matters in bidding. | Bid shading, post-auction value. | Spectrum sales, contracts, commodities. |
| insurance | - | A transfer that reduces downside loss in exchange for a premium. | Helps firms smooth risk and protect continuity. | Premium, deductible, coverage limit. | Risk management, operations, HR benefits. |

## 3. Frameworks & Matrices

### Risk-Choice Triangle
**Purpose:** Separate average payoff, downside risk, and risk attitude before making a decision. [verified from model knowledge, not source]

**Text Diagram:**
```text
          certainty equivalent
                 /\
                /  \
               /    \
        expected value  risk premium
```

Axes / Quadrants / Components explained:
Component 1: expected value, which tells you the average monetary outcome.
Component 2: certainty equivalent, which tells you what a person would accept for sure.
Component 3: risk premium, which tells you the amount paid to avoid uncertainty.
Component 4: risk attitude, which tells you whether the business should insure, hedge, or accept the gamble.

IT/AI/Product/Consulting worked example: A product team considers delaying launch to reduce uncertainty. If the certainty equivalent of waiting is higher than the expected value of launching now, the team should pause and buy more information first. [verified from model knowledge, not source]

When to pull this out in a meeting: When the team is arguing about "average upside" without pricing the downside.

### Decision Tree for Launch or Bid
**Purpose:** Turn uncertain choices into branch-by-branch expected payoffs. [verified from model knowledge, not source]

**Text Diagram:**
```text
Decision -> launch / wait / bid
    -> good outcome
    -> average outcome
    -> bad outcome
```

Axes / Quadrants / Components explained:
Component 1: decision nodes, where the manager chooses an action.
Component 2: chance nodes, where demand, cost, or competitor behavior is uncertain.
Component 3: payoff nodes, where profit, loss, or strategic value is realized.
Component 4: expected payoff, which identifies the best branch.

IT/AI/Product/Consulting worked example: An AI services team can bid low, bid high, or walk away from a government contract. A decision tree forces the team to attach probabilities to delivery risk, margin, and win rate instead of relying on intuition alone. [verified from model knowledge, not source]

When to pull this out in a meeting: When there are multiple uncertain branches and a gut feel is not enough.

### Information Problem Map
**Purpose:** Show whether the core risk is hidden quality, hidden behavior, or hidden value. [verified from model knowledge, not source]

**Text Diagram:**
```text
hidden quality -> adverse selection
hidden behavior -> moral hazard
hidden value -> winner's curse
```

Axes / Quadrants / Components explained:
Component 1: hidden quality, which distorts who enters or buys.
Component 2: hidden behavior, which changes what people do after coverage or a contract.
Component 3: hidden value, which makes auctions and bids dangerous.
Component 4: management response, which is screening, incentives, or bid shading.

IT/AI/Product/Consulting worked example: A software warranty can attract customers who expect more downtime, then increase support tickets after purchase. That is both adverse selection and moral hazard in one product design. [verified from model knowledge, not source]

When to pull this out in a meeting: When the business issue sounds like "we are not seeing the real signal."

## 4. Formulas

### Formula 1: Expected Value
Formula: `EV = sum(p_i x_i)`
Variables:
`p_i` = probability of outcome `i`
`x_i` = payoff for outcome `i`
Why this formula exists: It answers the average payoff question under uncertainty.
How to interpret the output:
Higher EV -> better average return -> candidate for investment or bid
Lower EV -> weaker average return -> consider a different choice
Negative EV -> unattractive gamble -> avoid unless there is strategic value
Worked example with numbers: If a project has a 50% chance of making $200,000, a 30% chance of making $50,000, and a 20% chance of losing $100,000, EV = $95,000. Decision: the average looks positive, but the downside still needs stress testing. [verified from model knowledge, not source]

### Formula 2: Expected Utility
Formula: `EU = sum(p_i U(x_i))`
Variables:
`U(x_i)` = utility from outcome `i`
`p_i` = probability of outcome `i`
Why this formula exists: It answers how a risk-averse decision-maker values the gamble after accounting for discomfort with downside.
How to interpret the output:
Higher EU -> preferred risky choice -> acceptable if downside is tolerable
Lower EU -> avoid or insure -> buy protection or redesign the exposure
Close EU values -> use secondary criteria -> strategy, cash flow, or optionality may decide
Worked example with numbers: If a risky contract has high upside but a painful downside, EU can be lower than the sure smaller contract even when EV is higher. Decision: choose the safer deal if the business cannot absorb the loss. [verified from model knowledge, not source]

### Formula 3: Risk Premium
Formula: `risk premium = EV - CE`
Variables:
`EV` = expected value of the risky option
`CE` = certainty equivalent
Why this formula exists: It answers how much the decision-maker will pay to eliminate uncertainty.
How to interpret the output:
Low premium -> risk tolerance is high -> self-insure or accept risk
Moderate premium -> partial hedging makes sense -> insure the worst case
High premium -> risk aversion is strong -> buy coverage or reduce exposure
Worked example with numbers: If a risky launch has EV of $120,000 and CE of $90,000, the risk premium is $30,000. Decision: spending up to that amount on insurance, delay, or testing can be rational. [verified from model knowledge, not source]

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Bid on average value alone. | Test expected value and downside separately. |
| Assume insurance removes all risk. | Check for moral hazard after coverage starts. |
| Sell a policy without screening. | Watch for adverse selection in the buyer pool. |
| Treat a winning bid as proof of good judgment. | Correct for winner's curse in common-value auctions. |
| Skip the decision tree because it looks slow. | Use a tree when uncertainty has branches that change the payoff. |

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Government contract bid
Situation: An AI consulting firm is deciding how aggressively to bid for a government modernization contract. The team has incomplete information on implementation risk, client responsiveness, and change requests. [verified from model knowledge, not source]
Applicable framework/metric: Decision Tree for Launch or Bid and Winner's Curse discipline.
Analysis: If the expected value of the contract is $1.2 million but a realistic downside adjustment cuts the certainty equivalent to $850,000, a bid that assumes the full EV would be too aggressive. [verified from model knowledge, not source]
Decision rule: If CE is far below EV, shade the bid. If CE is close to EV, bid normally. If CE is negative after risk adjustment, walk away.
Action: Build a decision tree with delivery risk, client delay risk, and bid-win probability before the final price is submitted.

### Scenario 2: Warranty and support offer
Situation: A hardware company wants to sell an extended warranty on a device used in field operations. Leadership expects the warranty to improve customer trust, but the support team fears misuse and higher claim volume. [verified from model knowledge, not source]
Applicable framework/metric: Information Problem Map and expected utility.
Analysis: If the warranty attracts higher-risk users, adverse selection will raise losses. If users become less careful after buying it, moral hazard will raise claims even if selection is neutral. [verified from model knowledge, not source]
Decision rule: If claim rates rise after launch, tighten screening or change deductibles. If claim rates stay stable, keep the offer.
Action: Add eligibility checks, usage thresholds, and an audit trail for claims.

### Scenario 3: Market research before launch
Situation: A product team is considering whether to spend $80,000 on research before a new feature launch. The feature could succeed, but a wrong launch would be expensive. [verified from model knowledge, not source]
Applicable framework/metric: Expected Value and Risk Premium.
Analysis: If the research prevents a decision that would have caused a $200,000 loss with moderate probability, the expected value of information can exceed the research cost. [verified from model knowledge, not source]
Decision rule: If the value of information exceeds its cost, research is justified. If not, ship with limited exposure. If the downside is catastrophic, delay until uncertainty falls.
Action: Run a small pilot, update probabilities, and only scale once the data changes the expected payoff.

## 7. Implementation Playbook
1. List every uncertain outcome that can change the business result.
2. Assign probabilities to outcomes instead of using a single optimistic forecast.
3. Compute expected value and then convert it into a certainty equivalent.
4. Build a decision tree for any bid, launch, or warranty decision with real downside.
5. Check whether insurance or guarantees will change user behavior after purchase.
6. Screen for hidden quality before offering pooled pricing or broad coverage.
7. Shade bids in common-value auctions to reduce winner's curse risk.

## 8. Content Quality Audit
Covered well: The source correctly frames uncertainty, risk aversion, insurance, information value, and auction discipline as connected managerial problems.
Underplayed or missing: It does not show the EV and EU math, the role of probability estimation, the difference between adverse selection and moral hazard in incentives, or how auction format changes optimal bidding. [verified from model knowledge, not source]
Supplement with: Varian, *Intermediate Microeconomics*; Pindyck and Rubinfeld, *Microeconomics*; and textbook chapters on expected utility and information economics [verified from model knowledge, not source]. For auction and bidding depth, use Kagel and Levin's auction research, Vickrey's classic work, and HBR-style cases on procurement and contract bidding [verified from model knowledge, not source].
Red flags in the source: The topic summary is accurate but compact, so it can hide how often the wrong bid or insurance design fails because the business misreads probabilities, incentives, or hidden information.

## 9. Quick-Recall Card
```text
Topic: Risk and Information
Core idea: Choose using expected value and expected utility, then correct for hidden information and distorted incentives.
Key metric/formula: EV = sum(p_i x_i); EU = sum(p_i U(x_i)); risk premium = EV - CE.
Framework trigger: Use it when outcomes are uncertain, users may change behavior, or bidders may overestimate value.
Watch out for: winner's curse, moral hazard, and adverse selection.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What is the risk-adjusted payoff once incentives and information gaps are included?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 6, 8, 9] Enrichments applied: [expected value and expected utility math; decision tree framework; information problem map; auction/winner's curse discipline; IT/AI/Product/Consulting scenarios; source-term coverage expansion] Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Pass 2 completed: 2026-04-19 11:55 IST Audited by: A1 -->
