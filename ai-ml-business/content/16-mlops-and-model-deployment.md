# MLOps and Model Deployment

## Overview

MLOps (Machine Learning Operations) is the set of practices that take an ML model from a data scientist's notebook to a reliable, monitored production system. It covers version control for data and models, automated training pipelines, testing, deployment, and ongoing monitoring. Without MLOps, models degrade silently, break when data changes, and never deliver their promised business value at scale.

---

## Why It Matters

Most ML models never make it to production. The gap between a working prototype and a dependable system is where projects stall. MLOps closes that gap by treating ML systems like software products — with CI/CD pipelines, automated testing, rollback capability, and performance dashboards. Companies with mature MLOps practices deploy models faster, catch drift early, and maintain trust in AI-driven decisions.

## Key Principles

- Version everything: code, data, model weights, and configuration, so any result can be reproduced
- Automate the training pipeline end-to-end: data ingestion, preprocessing, training, evaluation, and deployment
- Monitor model performance in production — accuracy can decay as real-world data shifts (concept drift or data drift)
- Build a rollback mechanism so you can revert to the previous model instantly if the new version underperforms

## Key Terms

| Term | Definition |
|------|------------|
| **MLOps** | The discipline of deploying, monitoring, and maintaining ML models in production reliably |
| **CI/CD for ML** | Continuous integration and continuous deployment pipelines adapted for model training and release |
| **Model Drift** | A decline in model performance over time caused by changes in the underlying data distribution |
| **Feature Store** | A centralized repository of precomputed features that ensures consistency between training and serving |

## Use Case

A fintech company retrains its credit risk model monthly as new loan outcomes become available. An MLOps pipeline automatically ingests fresh data, retrains the model, runs evaluation tests against a holdout set, and deploys the new version behind a canary release that serves 5% of traffic. If key metrics hold, the rollout extends to 100% within a week.

## Scenario

> An online travel agency deployed a price-prediction model that worked well for six months, then started giving inaccurate estimates. Investigation showed that post-pandemic travel patterns had shifted the data distribution (concept drift). After implementing automated drift detection with weekly statistical tests comparing training and live data distributions, the team caught similar shifts within days and triggered retraining automatically.

## Examples

- A retail company uses MLflow to track experiments, log model artifacts, and compare model versions before promoting the best one to production
- A healthcare AI startup stores curated patient features in a feature store so that the same transformations used during training are applied identically at inference time, eliminating train-serve skew

---

## Audited Appendix

# MLOps and Model Deployment
**Course:** AI and ML for Business  
**Module:** Foundations  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** `ai-ml-business/content/16-mlops-and-model-deployment.md`

---

## 1. Topic Snapshot
MLOps is the operating system that turns an ML notebook into a production service that can be trusted, monitored, and updated.  
For IT, AI, Product, and Consulting leaders, it answers a practical question: how do we deploy models safely, detect drift early, and keep business decisions reproducible?

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| MLOps | Machine Learning Operations | The discipline of shipping and maintaining ML systems in production. | To move from notebook demos to reliable services. | Deployment frequency, uptime, incident rate. | Platform engineering, AI ops reviews. |
| CI/CD for ML | Continuous Integration / Continuous Deployment | Automated build, test, and release pipelines for ML. | To make model releases repeatable and less error-prone. | Lead time, deployment success rate. | DevOps, ML platform teams. |
| Model Drift | N/A | Model quality declines over time as real data changes. | To explain why a once-good model can fail later. | Accuracy decay, error rate, calibration. | Monitoring dashboards, model governance. |
| Feature Store | N/A | A shared place to store reusable model inputs. | To keep training and serving consistent. | Feature freshness, reuse rate, skew reduction. | Data platform, ML engineering. |
| Concept Drift | N/A | The relationship between inputs and outcomes changes. | To explain why the business pattern changed, not just the data. | Statistical distance, performance decay. | Fraud, pricing, forecasting. |
| Data Drift | N/A | The distribution of input data changes. | To detect input shifts before performance collapses. | Population statistics, PSI, KL-style shift. | Monitoring and alerting. |
| Canary Release | N/A | Roll out a model to a small slice of traffic first. | To reduce production risk. | Traffic share, canary success rate. | Deployment, SRE, release management. |
| Holdout Set | N/A | Data held back for evaluation. | To test whether the model generalizes. | Validation metrics, holdout score. | Model review, experimentation. |
| Train-Serve Skew | N/A | Training and inference use different transformations or data. | To prevent silent production bugs. | Difference in feature values or predictions. | ML platform audits. |
| Rollback | N/A | Revert to a prior model or version. | To recover quickly when a release fails. | Time to revert, incident recovery time. | Incident response, release ops. |

## 3. Frameworks & Matrices

### MLOps Release Pipeline [verified from model knowledge, not source]
**Purpose:** Show the path from model development to safe production deployment.

**Text Diagram:**
```text
data ingestion -> preprocessing -> training -> evaluation -> approval -> deployment -> monitoring -> retraining
```

Axes / Quadrants / Components explained:
Component 1: data ingestion and preprocessing - prepare reliable inputs.
Component 2: training and evaluation - prove the model works before release.
Component 3: approval and deployment - push the model to users safely.
Component 4: monitoring and retraining - keep the model healthy over time.

IT/AI/Product/Consulting worked example: An internal IT team deploys a ticket-routing model behind a canary release. The model handles a small traffic slice, the dashboard checks accuracy and latency, and the team promotes it only after the service desk confirms the routed tickets are resolving faster.
When to pull this out in a meeting: When a model works in a notebook but the team needs a plan for production.

### Drift Response Matrix [verified from model knowledge, not source]
**Purpose:** Decide whether to ignore, monitor, retrain, or rollback when model performance changes.

**Text Diagram:**
```text
Low drift + stable performance   -> monitor
High drift + stable performance  -> investigate inputs
Low drift + falling performance  -> inspect labels / pipeline
High drift + falling performance -> rollback or retrain immediately
```

Axes / Quadrants / Components explained:
Component 1: drift level - whether the data distribution changed.
Component 2: performance level - whether the business metric is still acceptable.
Component 3: response action - monitor, investigate, retrain, or rollback.

IT/AI/Product/Consulting worked example: A product pricing model starts missing on competitive offers after a market shift. Data drift appears in the feature distribution and prediction error rises, so the team triggers retraining and temporarily falls back to the previous version.
When to pull this out in a meeting: When a production model starts behaving oddly and the team must decide whether to patch, retrain, or revert.

## 4. Formulas

Formula: `Accuracy decay % = (baseline accuracy - current accuracy) / baseline accuracy × 100` [verified from model knowledge, not source]  
Variables:
baseline accuracy = performance before deployment or drift
current accuracy = performance after live data shifts
Why this formula exists: It answers how much model quality has degraded.
How to interpret the output:
Value < 5% -> normal drift watch -> keep monitoring
Value 5%–15% -> meaningful decay -> investigate features and data quality
Value > 15% -> severe degradation -> retrain or rollback
Worked example with numbers: If a lead-scoring model falls from 80% to 68% accuracy, decay is 15%. That is large enough to trigger a release review, not just passive monitoring.

Formula: `Canary success rate = successful canary requests / total canary requests × 100` [verified from model knowledge, not source]  
Variables:
successful canary requests = requests handled without critical failure
total canary requests = requests sent to the limited release slice
Why this formula exists: It answers whether a limited rollout is safe to expand.
How to interpret the output:
Value < 95% -> stop and investigate
Value 95%–99% -> cautious continue, watch closely
Value > 99% -> strong signal to expand
Worked example with numbers: A credit-risk model handles 9,980 of 10,000 canary requests correctly and within latency limits, so the canary success rate is 99.8%. That supports wider release if business metrics also hold.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Deploy a model because it passed notebook tests. | Gate release on holdout evaluation and production checks. |
| Assume production data looks like training data forever. | Monitor drift and set alert thresholds. |
| Let training and serving use different feature logic. | Centralize features in a feature store or shared pipeline. |
| Roll out to everyone at once. | Use a canary release and expand gradually. |
| Keep a failing model online because rollback is inconvenient. | Build rollback into the deployment plan before launch. |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: IT ticket routing in an enterprise service desk  
Situation: An internal IT team wants to route incoming tickets with ML so agents spend less time triaging and more time resolving issues. The team is worried about production errors because the workflow directly affects employee productivity.  
Applicable framework/metric: Canary success rate and rollback readiness.  
Analysis: The model is deployed to 5% of traffic first. If latency stays within SLA and routing accuracy remains above the release threshold, the team expands; otherwise it reverts immediately.  
Decision rule: If canary success is above 99%, expand. If between 95% and 99%, watch and hold. If below 95%, rollback.  
Action: Launch behind a feature flag and keep the previous routing rule available.

Scenario 2: AI pricing model for a product team  
Situation: A product team ships a demand-based pricing model for a subscription feature. After two weeks, live performance drops because competitor pricing patterns changed.  
Applicable framework/metric: Accuracy decay % and drift level.  
Analysis: Accuracy falls from 82% to 71%, which is a 13.4% decay. That is enough to trigger investigation of drift, labels, and feature freshness.  
Decision rule: If decay is under 5%, monitor. If 5% to 15%, investigate and retrain. If above 15%, rollback or retrain fast.  
Action: Compare live features against training distributions and retrain the model if the drift is persistent.

Scenario 3: Consulting client model governance review  
Situation: A consulting team is helping a financial services client deploy an ML model for lead prioritization. The client wants business value fast, but the governance team needs auditability and reproducibility.  
Applicable framework/metric: MLOps release pipeline.  
Analysis: Versioning code, data, and model weights lets the team reproduce every score. A holdout test proves the model generalizes before the client approves a canary release.  
Decision rule: If the pipeline is reproducible and the canary is clean, expand. If not, stop the release.  
Action: Build a release checklist covering data version, approval owner, canary slice, and rollback owner.

## 7. Implementation Playbook
1. Version the code, data, model, and configuration together.
2. Automate the training and evaluation pipeline end to end.
3. Define release gates for holdout performance, latency, and business metrics.
4. Deploy with a canary slice and keep rollback one click away.
5. Monitor drift, accuracy, and service health in production dashboards.
6. Create alerts for feature skew, missing data, and threshold breaches.
7. Retrain or retire the model when drift becomes persistent.

## 8. Content Quality Audit
Covered well: The source correctly stresses that MLOps is the bridge from prototype to production and highlights versioning, automation, monitoring, and rollback.
Underplayed or missing: It does not go deep on observability, incident management, feature lineage, testing strategy, data contracts, model registries, or how to choose drift thresholds that reflect business risk.
Supplement with: *Designing Machine Learning Systems* (Chip Huyen, 2022), *Machine Learning Design Patterns* (Lakshmanan, Robinson, and Munn, 2020), peer-reviewed work on drift detection and concept drift, and HBS or IIM cases on enterprise AI operating models. [verified from model knowledge, not source]
Red flags in the source: "Model drift" is broad enough to hide multiple failure modes; teams need to separate label drift, data drift, and concept drift instead of treating all degradation the same way.

## 9. Quick-Recall Card
```text
Topic: MLOps and Model Deployment
Core idea: Production ML needs versioning, automated release, monitoring, and rollback.
Key metric/formula: Accuracy decay % = (baseline accuracy - current accuracy) / baseline accuracy × 100
Framework trigger: Use it when a model is leaving the notebook and entering production.
Watch out for: Drift, train-serve skew, and silent failures.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: How do we keep the model reliable after it goes live?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:4, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [release pipeline, drift matrix, accuracy and canary formulas, IT/product/consulting scenarios, deployment playbook, model governance audit] Final scores: all 5/5 Pass 2 completed: 2026-04-20 11:49 Audited by: A1 -->
