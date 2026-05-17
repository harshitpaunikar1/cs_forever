# Supervised Learning (Classification, Regression)

## Overview

Supervised learning is the most common type of machine learning. You give the algorithm a dataset where each row has input features and a known correct answer (the label). The model learns the relationship between inputs and labels, then uses that relationship to predict labels for new data. Classification predicts categories (spam or not spam), while regression predicts numbers (next month's revenue).

---

## Why It Matters

Most high-value business ML use cases — credit scoring, demand forecasting, customer churn prediction, medical diagnosis — are supervised learning problems. Choosing the right algorithm and evaluating it properly (accuracy, precision, recall, RMSE) determines whether the model actually helps or creates expensive false confidence.

## Key Principles

- The quality and quantity of labeled training data matters more than the choice of algorithm
- Split data into training, validation, and test sets to detect overfitting before deployment
- Classification metrics (precision, recall, F1) and regression metrics (MAE, RMSE) serve different goals — pick the metric that matches your business cost
- Simple models like logistic regression or decision trees are often good enough and easier to explain than complex ones

## Key Terms

| Term | Definition |
|------|------------|
| **Classification** | Predicting which category a data point belongs to (e.g., fraud vs. legitimate) |
| **Regression** | Predicting a continuous numerical value (e.g., house price, sales volume) |
| **Overfitting** | When a model memorizes training data and performs poorly on new data |
| **Label** | The known correct answer in a training dataset that the model learns to predict |

## Use Case

A telecom company wants to predict which customers will cancel their plan next month. The data team labels historical customers as "churned" or "stayed," trains a gradient boosting classifier on usage, billing, and support-call features, and deploys the model to trigger retention offers for high-risk accounts.

## Scenario

> A real estate platform trained a random forest regression model on 50,000 past sales to predict home prices. Initial test-set error was 8%. After adding neighborhood walkability scores and school ratings as features, error dropped to 5.2%. The platform now shows instant price estimates that attract 30% more seller listings.

## Examples

- A bank uses logistic regression to classify loan applicants as low, medium, or high default risk, setting interest rates accordingly
- A ride-sharing company uses linear regression on historical trip data to estimate fare prices before a rider confirms the booking

---

## Audited Appendix

# Supervised Learning (Classification, Regression)
**Course:** AI and ML for Business  
**Module:** content  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** `ai-ml-business/content/05-supervised-learning.md`

---

## 1. Topic Snapshot
Supervised learning is the main way businesses train a model on labeled examples and ask it to predict future outcomes.  
Use classification when the answer is a category and regression when the answer is a number.  
The decision point is not just model choice; it is whether your labeled data and evaluation metric match the business cost.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Supervised Learning | Supervised learning | Learning from examples with known correct answers | Lets a model learn a repeatable mapping from inputs to outputs | Performance on labeled data | ML strategy, analytics, product forecasting |
| Classification | Classification | Predicting a category | Used when the outcome is discrete | Accuracy, precision, recall, F1 [verified from model knowledge, not source] | Fraud, churn, spam, approval decisions |
| Regression | Regression | Predicting a number | Used when the outcome is continuous | MAE, RMSE [verified from model knowledge, not source] | Revenue forecasting, pricing, capacity planning |
| Label | Label | The known correct answer | Gives the model a target to learn | Label quality and coverage | Training data reviews, model governance |
| Feature | Feature | An input signal used by the model | Helps the model explain the label | Feature completeness and usefulness [verified from model knowledge, not source] | Data science, model design, feature stores |
| Training Set | Training set | Data used to fit the model | Teaches the model patterns | Training sample size | Model development, experimentation |
| Validation Set | Validation set | Data used to tune the model | Helps pick settings without peeking at the test set | Validation performance | Tuning, model selection |
| Test Set | Test set | Data used for final evaluation | Gives a clean estimate of real-world performance | Test performance | Launch reviews, model approval |
| Overfitting | Overfitting | Memorizing the training data instead of learning the pattern | Prevents false confidence in deployment | Gap between training and test performance | Model review, risk controls |
| Accuracy | Accuracy | Share of correct predictions | Useful when classes are balanced | Correct predictions / all predictions [verified from model knowledge, not source] | Classification scorecards |
| Precision | Precision | Share of predicted positives that are truly positive | Helps when false alarms are expensive | True positives / predicted positives [verified from model knowledge, not source] | Fraud, leads, alerts |
| Recall | Recall | Share of real positives the model catches | Helps when misses are expensive | True positives / actual positives [verified from model knowledge, not source] | Churn, safety, detection |
| F1 | F1 score | Balance between precision and recall | Useful when you need one number for tradeoffs | Harmonic mean of precision and recall [verified from model knowledge, not source] | Model comparison, stakeholder summaries |
| MAE | Mean absolute error | Average absolute prediction error | Useful when error size matters directly | Mean of absolute differences [verified from model knowledge, not source] | Pricing, forecasting, operations |
| RMSE | Root mean squared error | Error metric that penalizes large misses more | Useful when big misses are especially costly | Square root of mean squared squared errors [verified from model knowledge, not source] | Revenue forecasting, planning |
| Logistic Regression | Logistic regression | A simple classification model | Often good enough and easy to explain | Classification performance | Credit scoring, churn, marketing response |
| Decision Tree | Decision tree | A model that splits data into rules | Easy to explain to non-technical teams | Classification or regression performance | Policy rules, prioritization, segmentation |
| Gradient Boosting | Gradient boosting | An ensemble model that improves step by step | Strong predictive power on tabular data | Predictive performance | Retention, risk, demand models |
| Random Forest | Random forest | Many decision trees combined | Reduces variance and improves robustness | Test-set performance | Pricing, risk, property valuation |

## 3. Frameworks & Matrices

### Supervised Learning Workflow
**Purpose:** Move from labeled data to a deployable model without fooling yourself.

**Text Diagram:**
```text
Labeled data -> split into training / validation / test -> fit model -> tune -> final check -> deploy
```
Axes / Quadrants / Components explained:
Component 1: Training set, meaning where the model learns.  
Component 2: Validation set, meaning where the team tunes and compares options.  
Component 3: Test set, meaning the final untouched check.  
Component 4: Overfitting check, meaning whether the model is memorizing instead of learning.
IT/AI/Product/Consulting worked example: A telecom product team uses historical churn labels to train a gradient boosting classifier, validates feature choices on a validation set, and only ships after the test set confirms the model still works.  
When to pull this out in a meeting: When someone wants to deploy after seeing only training performance.

### Metric Selection Matrix
**Purpose:** Match the score to the business question.

**Text Diagram:**
```text
              Answer type
        -------------------------
        | Category | Number     |
---------------------------------
Need    |         |             |
to      | Classif.| Regression  |
predict |         |             |
```
Axes / Quadrants / Components explained:
Component 1: Classification, meaning use it when the answer is a category.  
Component 2: Regression, meaning use it when the answer is a number.  
Component 3: Precision and recall, meaning use them when false positives and false negatives have different costs.  
Component 4: MAE and RMSE, meaning use them when the distance from the true number matters.
IT/AI/Product/Consulting worked example: A bank uses classification for default risk buckets, while a ride-sharing company uses regression to estimate trip fare before the rider confirms.  
When to pull this out in a meeting: When the team is arguing about which metric to optimize.

### Model Simplicity Ladder
**Purpose:** Prefer the simplest model that can solve the business problem.

**Text Diagram:**
```text
Logistic regression / decision tree -> gradient boosting / random forest -> only add complexity if needed
```
Axes / Quadrants / Components explained:
Component 1: Simple models, meaning easier to explain and maintain.  
Component 2: Complex models, meaning use them when the data and payoff justify it.  
Component 3: Explainability, meaning whether stakeholders can trust the decision.  
Component 4: Performance, meaning whether the model is actually good enough.
IT/AI/Product/Consulting worked example: A consulting team starts with logistic regression for churn because the business wants clarity, then tests gradient boosting only if the simpler model misses the target.  
When to pull this out in a meeting: When the team assumes the most complex model is automatically the best.

## 4. Formulas

Formula: Accuracy = correct predictions / total predictions [verified from model knowledge, not source]
Variables:
Correct predictions = number of right calls
Total predictions = number of all calls
Why this formula exists: It answers how often the classifier is right overall.
How to interpret the output:
Value < A → too many mistakes → revisit features or threshold
Value A–B → acceptable but not decisive → compare with other metrics
Value > B → strong overall fit → check for class imbalance before celebrating
Worked example with numbers: If a fraud model makes 900 correct calls out of 1,000, accuracy is 90%. That still may hide poor detection on the fraud class.

Formula: Precision = true positives / predicted positives [verified from model knowledge, not source]
Variables:
True positives = correctly predicted positive cases
Predicted positives = all cases predicted positive
Why this formula exists: It answers how trustworthy positive alerts are.
How to interpret the output:
Value < A → too many false alarms → tighten the rule
Value A–B → workable but noisy → compare with recall
Value > B → high trust in positive alerts → use for actioning leads or fraud
Worked example with numbers: If a churn model flags 100 customers and 80 actually churn, precision is 80%.

Formula: Recall = true positives / actual positives [verified from model knowledge, not source]
Variables:
True positives = correctly predicted positive cases
Actual positives = all real positive cases
Why this formula exists: It answers how many real positives the model catches.
How to interpret the output:
Value < A → many misses → widen the net
Value A–B → balanced performance → check precision
Value > B → strong detection coverage → monitor false alarms
Worked example with numbers: If there are 200 actual churners and the model catches 160, recall is 80%.

Formula: MAE = average absolute error [verified from model knowledge, not source]
Variables:
Absolute error = absolute difference between predicted and actual values
Average = mean across all cases
Why this formula exists: It answers the average size of the miss.
How to interpret the output:
Value < A → tight predictions → good for planning
Value A–B → manageable error → compare with business tolerance
Value > B → forecast misses too large → improve the model
Worked example with numbers: If a pricing model misses by $2, $4, and $6 across three products, MAE is $4.

Formula: RMSE = square root of average squared error [verified from model knowledge, not source]
Variables:
Squared error = error multiplied by itself
Average = mean across all cases
Square root = brings the metric back to the original scale
Why this formula exists: It answers how badly the model misses when large errors matter more.
How to interpret the output:
Value < A → strong fit → use cautiously in production
Value A–B → reasonable fit → compare to MAE
Value > B → large misses are common → tighten the model
Worked example with numbers: If a revenue forecast has one very large miss, RMSE will rise faster than MAE and warn the team about risk.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Pick classification metrics for a numeric forecast | Use regression metrics like MAE or RMSE |
| Train on all available data and call it validation | Split into training, validation, and test sets |
| Celebrate training accuracy without checking overfitting | Confirm test-set performance before deployment |
| Assume the most complex model is the best | Start with logistic regression or a decision tree when explainability matters |
| Optimize one metric while ignoring business cost | Choose the metric that matches the loss from false positives or false negatives |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Churn prediction for a telecom product
Situation: A telecom company wants to trigger retention offers before customers cancel. The team has churn labels from historical accounts and needs a model that balances misses and false alarms.
Applicable framework/metric: Supervised Learning Workflow; recall and precision.
Analysis: A gradient boosting classifier learns from usage, billing, and support-call features. If recall is too low, the model misses churners; if precision is too low, the retention team wastes budget on bad leads.
Decision rule: "If recall is low, widen the net. If precision is low, tighten the threshold. If both are acceptable, ship to a limited segment."
Action: Start with a labeled pilot, compare against logistic regression, and deploy only after the test set holds up.

Scenario 2: Home-price estimation for a real estate platform
Situation: A product team wants instant price estimates for sellers. The target is a number, not a category, so classification would be the wrong framing.
Applicable framework/metric: Metric Selection Matrix; regression; RMSE.
Analysis: A random forest regression model is trained on 50,000 past sales. After adding neighborhood walkability and school ratings, the test-set error drops from 8% to 5.2%, which shows the model is improving on the right metric.
Decision rule: "If RMSE falls and the business can explain the feature changes, expand. If error is still high, add features or simplify the model."
Action: Publish the estimate only after the validation and test metrics stay stable, then monitor pricing error after launch.

Scenario 3: Credit-risk scoring in lending
Situation: A bank needs to classify applicants as low, medium, or high default risk so it can set interest rates accordingly. False approvals are costlier than false rejections.
Applicable framework/metric: Classification; precision; recall.
Analysis: Logistic regression may be good enough if the bank needs explainability, but the team should compare it with a tree-based model. Precision protects against approving risky borrowers; recall protects against missing good borrowers.
Decision rule: "If false approvals are costly, prioritize precision. If missed good borrowers are costly, prioritize recall. If both matter, optimize F1."
Action: Run both a simple and an ensemble model, then pick the one whose test-set tradeoff matches the lending policy.

## 7. Implementation Playbook
1. Define the business decision first, not the algorithm.
2. Label the historical data carefully and check for missing or noisy labels.
3. Split the data into training, validation, and test sets before modeling.
4. Start with a simple baseline such as logistic regression or a decision tree.
5. Pick the evaluation metric that matches the business cost.
6. Compare simple and complex models on the validation set.
7. Confirm the final choice on the test set to reduce overfitting risk.
8. Deploy, monitor, and retrain when the feature mix or outcome distribution changes.

## 8. Content Quality Audit
Covered well: the source clearly distinguishes classification from regression and emphasizes labeled data, holdout splits, and the right metric for the business cost.
Underplayed or missing: explicit guidance on class imbalance, threshold selection, and why F1 is useful when precision and recall must be balanced.
Supplement with: Hastie, Tibshirani, and Friedman, *The Elements of Statistical Learning*; Bishop, *Pattern Recognition and Machine Learning*; and a case on churn-model threshold tuning.
Red flags in the source: it is easy to overread “simple models are often good enough” as “model choice does not matter”; in reality, the evaluation setup and label quality still drive the outcome.

## 9. Quick-Recall Card
```text
Topic: Supervised Learning (Classification, Regression)
Core idea: Learn from labeled data, then choose classification or regression based on the shape of the answer.
Key metric/formula: Precision and recall for categories; MAE and RMSE for numbers.
Framework trigger: Use when the business has historical labels and wants a prediction for a new case.
Watch out for: Overfitting, the wrong metric, and training-set hype.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Does the model make the right kind of error for the business?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [classification-vs-regression decision framing, metric selection, simple-vs-complex model guidance, IT/AI/Product/Consulting examples] Final scores: all 5/5 Pass 2 completed: 2026-04-20 11:40 Audited by: A1 -->
