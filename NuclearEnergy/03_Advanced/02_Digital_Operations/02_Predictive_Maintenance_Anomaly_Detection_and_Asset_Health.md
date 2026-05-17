# Predictive Maintenance, Anomaly Detection, and Asset Health

## Overview

Predictive maintenance in plant environments usually sits as an advisory layer around equipment health. It uses time-series data to detect abnormal patterns before they become failures or forced outages.

## Why This Topic Matters

This is one of the highest-value intersections of plant systems, data, and software, and it is highly relevant in 2026.

## Main Concepts / Core Concepts

- trend baselining
- anomaly detection
- thresholds versus model-based detection
- maintenance decision support
- false positives and operator trust

## Mental Model / Big Picture

```text
historian data
    -> cleaning and features
    -> baseline or model
    -> anomaly score / health indicator
    -> maintenance action or further review
```

## Practical / Design / Operational Sections

Good starter use cases:

- pump vibration
- bearing temperature
- lube-oil temperature
- motor current
- valve stroke time

## Hands-On Example / Mini Project

Train a simple outlier or novelty model on synthetic pump data and compare the model output with hand-built rule thresholds.

## Best Practices

- start with explainable features
- compare model output against engineering expectation
- optimize for trust, not model novelty

## Common Pitfalls

- no baseline period
- no handling of operating-mode changes
- model scores with no action guidance

## Metrics / KPIs / What to Measure

- precision of anomaly flags
- false-alarm rate
- lead time before failure
- maintenance savings or avoided downtime

## Tools Commonly Used Around This Topic

- `Python`
- `scikit-learn`
- `sktime`
- historian exports
- dashboards

## Recommended Resources

- scikit-learn outlier detection docs
- sktime docs
- plant historian and reliability references

## Interview Questions

- Why is predictive maintenance usually advisory rather than safety-critical?
- What makes a plant anomaly model trustworthy?
- How do you prevent model output from becoming nuisance noise?

## Portfolio / Resume Application

This is one of the best project areas for showing direct business value and plant relevance.

## 2026+ Focus Areas

- asset-health scoring
- human-readable anomaly explanations
- hybrid rules-plus-model approaches

## Next Step

Continue to [Functional Safety, Validation, and OT Cybersecurity](../03_Safety_Security_and_Regulation/01_Functional_Safety_Validation_and_OT_Cybersecurity.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

In plant environments, predictive maintenance usually starts with equipment classes that already generate useful signals: pumps, motors, bearings, valves, fans, exchangers, and electrical assets. The real workflow is not "model predicts failure." It is "model or rules show an abnormal pattern early enough that reliability, maintenance, and operations can decide whether to inspect, defer, or intervene."

That difference matters because trust and actionability matter more than model sophistication.

### Industry Tool Stack

- historian trend archives
- vibration, temperature, current, pressure, and stroke-time signals
- `Python`, `scikit-learn`, `sktime`, and feature engineering notebooks
- dashboards for health score and evidence review
- CMMS and work-order records for feedback

### Step-by-Step Applied Workflow

1. Choose one asset class with consistent signals and known failure patterns.
2. Build a baseline for healthy behavior across operating modes.
3. Compare rules, thresholds, and model-based anomaly scores instead of assuming ML is better by default.
4. Review anomalies with maintenance history and operator context before escalating them.
5. Feed the outcome back into the model or rules so nuisance patterns are reduced over time.

### AI Integration

This page is itself an AI page, but the strongest pattern is still hybrid:

- physics or rules constrain the search space
- anomaly models rank suspicious behavior
- human review determines whether the condition is real, urgent, or mode-related

### Case Studies

- `EPRI`: strong benchmark for asset-health and reliability-centered plant work.
- `IAEA`: useful benchmark for advisory digital support and conservative maintenance decision discipline.
- `Ignition` or historian-centered workflows: useful benchmark for how plant teams actually surface evidence to users.

### Failure Modes & Safety

- training on mixed operating modes without labeling them
- alerting on every unusual pattern until operators stop believing the system
- no feedback loop from work orders back to the analytics team
- allowing an advisory score to be interpreted as a safety-critical command

### Business & Commercial Layer

This is one of the clearest commercial opportunities in the entire nuclear folder:

- avoided forced outages
- better maintenance timing
- reduced inspection waste
- plant digitalization consulting
- asset-health software products and dashboard services

### Hiring Signal

High-value evidence includes:

- feature tables tied to engineering meaning
- comparison of threshold and model methods
- false-positive discussion
- clear statement of why the output stays advisory

### Portfolio Projects

- Beginner: `pump-anomaly-baseline`
  Deliverables: synthetic pump trends, thresholds, anomaly plots, review note.
- Intermediate: `asset-health-scorecard`
  Deliverables: multi-signal health score, evidence panel, maintenance recommendation categories.
- Advanced: `maintenance-decision-support-lab`
  Deliverables: hybrid rules-plus-model pipeline, CMMS-style feedback loop, alert rationalization note.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: hybrid rules-plus-model workflows are more credible than black-box novelty.
- `2030`: stronger integration of health analytics with outage planning and spares.
- `2035`: better human-readable explanation layers for plant users.
- `2045`: asset-health analytics remain useful wherever physical equipment ages under consequence.

### Interview Questions

1. Why is predictive maintenance usually advisory rather than safety-critical?
   Short answer: because uncertainty, false positives, and operating-mode effects require engineering review.
2. What makes a plant anomaly model trustworthy?
   Short answer: good data quality, mode awareness, explainable features, and feedback from real outcomes.
3. How do you prevent model output from becoming nuisance noise?
   Short answer: threshold discipline, alert rationalization, and closed-loop feedback.
4. Why compare models with simple rules?
   Short answer: because rules are often easier to trust and sometimes good enough.
5. What is the commercial value here?
   Short answer: fewer forced outages and better maintenance timing.

### Further Depth

- scikit-learn outlier detection docs
- sktime docs
- EPRI reliability references
- historian analytics references
