# Plant Data Validation, Model Governance, and Decision Support

## Overview

Nuclear plants generate continuous streams of operational data: process historian tags sampled every second, protection system signals logged at millisecond intervals, manual operator entries, laboratory analysis results, and maintenance records spanning decades. The temptation, on encountering this abundance, is to treat it as a ready-made dataset for analytics. The reality is that historian data looks clean until you examine it closely — and then you find calibration drift, tag renaming events that created silent discontinuities, time-synchronization errors from server clock resets, decimation artifacts from compression algorithms, and sensor ranges that were changed without updating the metadata.

Data validation is the discipline of converting raw historian data into quantities that can actually be trusted for engineering analysis. Model governance is the discipline of ensuring that analytics models — process performance calculators, anomaly detectors, advisory decision support tools — behave as intended throughout their operational lifetime, not just on the day they were commissioned. Together, these disciplines define the difference between a plant analytics program that improves decisions and one that creates confident wrong answers.

This page covers the practical reality of nuclear plant data quality, the validation techniques that address it, the governance frameworks that maintain model trustworthiness over time, and the regulatory boundary between advisory AI systems (which are permissible and growing) and safety-function AI systems (which are essentially prohibited today by the structure of nuclear safety qualification requirements).

---

## Historian Data Quality: What Goes Wrong and Why

Nuclear plant process historians — OSIsoft PI, Honeywell PHD, Emerson DeltaV historian, AVEVA Process Data Manager — store time-series data from thousands of measurement points. Each tag corresponds to a physical sensor transmitter with a specific range, engineering unit, and sampling rate. The historian records what the transmitter reports. The problems are in the gap between what the transmitter reports and what the physical quantity actually is.

**Calibration drift**: Instruments have calibrated ranges and accuracies established during periodic surveillance testing. Between surveillance intervals (typically 18–24 months for many nuclear instrument calibrations), an instrument's output can drift. A pressure transmitter nominally calibrated to ±0.1% of span may be reading 0.5% high for six months before the next calibration catches it. Historical data from that period contains a systematic bias that is invisible unless you overlay calibration records with historian time series. For analytics models trained on uncorrected historian data, calibration drift introduces unknown bias into the training signal.

**Tag renaming and engineering unit changes**: Plant configuration changes — instrument replacement, I&C upgrades, DCS migrations — frequently cause tag names to be changed, signal ranges to be rescaled, or engineering units to be modified. In a poorly documented change, the new tag appears in the historian as a new measurement starting on a specific date; the old tag stops updating. A naive join between old and new data creates a discontinuity at the change date that looks like a physical plant event. Detecting these discontinuities requires comparing historian data against the plant configuration change log — which is typically maintained in a separate document management system and not automatically linked to historian metadata.

**Time-synchronization errors**: When a DCS server clock drifts or is reset by an NTP synchronization event, timestamps in the historian may jump backward or forward, creating duplicate entries, negative time deltas between consecutive samples, or gaps. These errors are especially problematic for analytics that rely on change detection or rate-of-change calculations, where a false time jump produces a spurious spike in the derived signal.

**Compression artifacts**: Most historians use exception reporting or swinging door compression to reduce storage requirements. Instead of recording every sample, the historian records only when the value changes by more than a deadband threshold or when the rate of change changes significantly. The reconstructed time series is not a faithful record of the actual measurement — it is a piecewise linear approximation. Fast transients narrower than the deadband are invisible in the stored data. Slow drift smaller than the deadband is recorded as flat-lined data until the deadband is crossed, masking the true gradual trend.

**Out-of-range and saturated readings**: When a sensor fails or a process parameter exceeds the transmitter range, the historian often records the last valid value, the transmitter's high- or low-range saturation value, a NaN, or a system-defined sentinel value depending on the historian configuration. If downstream analytics treat a saturation value as a valid process reading, the results can be severely distorted. Validation pipelines must define explicit rules for handling out-of-range data.

---

## Validation Pipelines for Historian Data

A validation pipeline transforms raw historian exports into an analysis-ready dataset with known quality characteristics. The pipeline structure for nuclear plant data typically includes:

**Completeness check**: For each tag and time range, verify that the fraction of expected samples that are present exceeds a threshold (typically > 95% for critical process measurements). Flag tags with systematic gaps for root-cause investigation.

**Range validation**: Verify that each value falls within the physically realizable range for the measurement (process pressure cannot be negative; temperature cannot exceed the known physical bounds). Values outside the range are flagged as invalid regardless of the historian's quality code.

**Temporal consistency**: Verify that timestamps are monotonically increasing and that time deltas between consecutive samples are consistent with the expected sample rate. Flag duplicate timestamps and anomalous time jumps.

**Cross-tag consistency (sensor fusion validation)**: Redundant instrumentation — multiple transmitters measuring the same process parameter — provides independent observations that should agree within a known measurement uncertainty. If Transmitter A reads 150°C and Transmitter B reads 152°C, the 2°C difference is within expected uncertainty. If Transmitter A reads 150°C and Transmitter B reads 175°C, one of them is likely faulty or miscalibrated. Heat balance closures, flow conservation checks (total inlet flow ≈ total outlet flow + change in inventory), and instrument comparison reports are the standard tools for cross-tag consistency validation in nuclear plants.

**Calibration record overlay**: Validation pipelines at mature plant analytics programs automatically retrieve the calibration record for each instrument (from the CMMS) and flag historian periods where the instrument's as-found error exceeded its calibration tolerance. This allows analysts to apply correction factors or exclude periods of known measurement bias.

---

## Model Governance for Advisory Analytics

An analytics model deployed in a nuclear plant — a process performance calculator, a vibration anomaly detector, an equipment health index — is not a static artifact. It is a living software component that must be maintained as the plant, the data environment, and the models themselves change over time. Model governance is the framework that manages this lifecycle.

**Training and validation split discipline**: Models trained on nuclear plant historian data are subject to temporal autocorrelation — the plant's operating state at time T is similar to its state at T+1 second. A random 80/20 split will produce overly optimistic validation metrics because training and validation sets will include near-identical observations. Correct practice for time-series models is temporal splitting: train on years 1–4, validate on year 5, test on year 6. This ensures the validation metric reflects the model's ability to generalize to future operating conditions it has not seen.

**Concept drift monitoring**: Plant operating conditions change over time as fuel burnup progresses, equipment ages, seasonal heat sink temperatures vary, and operational practices evolve. A model trained on data from years 1–3 of operation may produce systematically biased predictions when applied to data from years 8–10. Monitoring for concept drift requires tracking model residuals (prediction error) over time and triggering model review when the residual distribution shifts significantly from the training baseline.

**Rollback protocols**: When a model update degrades performance, the governance framework must enable rapid rollback to the previous version. This requires version-controlled model artifacts, documented performance baselines for each version, and a defined reversion procedure. In a nuclear plant context, this is especially important because operators may be using model outputs to inform decisions — a degraded model producing incorrect outputs must be identified and corrected or rolled back before it influences consequential actions.

**Operator trust thresholds**: Even advisory models (those not connected to any safety function) require explicit agreements with plant operators about when to follow model recommendations and when to override. An anomaly detection system that generates dozens of false-positive alerts per week will be ignored — the operators will route around it. Governance frameworks define precision and recall thresholds that the model must achieve in validation before deployment, and track false-positive rates in production to ensure they stay within the operator trust envelope.

---

## The Regulatory Boundary: Advisory AI vs. Safety-Function AI

The most important data governance concept for engineers entering nuclear analytics is the distinction between advisory systems and safety systems, because they are governed by entirely different regulatory frameworks.

**Advisory systems** provide information, trends, or recommendations to operators and engineers who make the final decision. An operator advisory system that displays a predicted optimal turbine back-pressure setpoint is advisory — the operator decides whether to act on it. The operator remains in the decision loop. Advisory systems are not subject to 10 CFR 50 Appendix B (Quality Assurance Criteria) in the same way safety systems are, though they are still subject to rigorous V&V requirements under 10 CFR 50.59 for changes to the facility.

**Safety systems** perform protective functions: scram initiation, emergency core cooling system actuation, containment isolation. These systems must meet the requirements of IEEE Std 603 (Criteria for Safety Systems for Nuclear Power Generating Stations), which mandates deterministic, qualified hardware and software with a demonstrated design basis. Current AI/ML systems cannot satisfy these requirements because their behavior is not deterministic and cannot be formally verified against a design basis specification. This is not a gap that is likely to be closed in the near term — it reflects a fundamental incompatibility between how neural networks work and how safety systems must be qualified.

The practical implication: in 2026, legitimate AI applications in nuclear analytics are all advisory. Any proposal to connect a machine learning model output directly to a protective action (bypassing operator review) is inconsistent with the current regulatory framework and should be treated with extreme caution.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

The gap between having a process historian and having trustworthy analytics data is larger than most engineers who have not worked in plant operations expect. A typical large nuclear plant historian holds data for 5,000–20,000 process tags stretching back 10–20 years. A fraction of those tags have complete, correctly calibrated, consistently named historical records. The rest require varying degrees of remediation before they can support engineering analysis.

OSIsoft PI (now AVEVA PI System) is the dominant historian platform at US and European nuclear utilities. PI's Asset Framework (AF) layer adds context to raw tags — defining equipment hierarchies, unit conversions, calculated attributes, and event frames — that transforms a flat tag list into a structured data model. The data governance challenge at plants with mature PI implementations is maintaining the AF model as the physical plant changes: when an instrument is replaced, the new tag must be mapped into the AF hierarchy with correct metadata, and the historical context for the old tag must be preserved with documentation of the change.

EPRI's Plant Modernization Program has published extensive technical reports on plant historian data quality and analytics validation frameworks, covering the specific failure modes described above and the remediation techniques used at leading US utilities. Their work provides the most detailed public documentation of what mature nuclear plant data governance looks like in practice.

The regulatory framework for advisory analytics in US nuclear plants is 10 CFR 50.59, which governs changes to the facility. A new analytics tool that provides operator guidance but does not perform a safety function may or may not require a formal 50.59 evaluation and NRC notification, depending on the tool's scope and the plant's licensing basis. Plants with aggressive analytics programs typically have a dedicated licensing group that evaluates each new tool against 50.59 criteria before deployment.

### Industry Tool Stack

- **OSIsoft PI / AVEVA PI System** — the dominant nuclear plant historian; PI Data Archive for time-series storage, PI Asset Framework (PI AF) for equipment hierarchy and calculated attributes, PI Vision for dashboards, PI Data Access API (PI Web API, AFSDK) for programmatic data retrieval
- **Honeywell PHD / Experion historian** — alternative historian platform at plants using Honeywell DCS; similar architecture to PI; less widely used in nuclear than PI but present at several fleets
- **AVEVA Process Data Manager (formerly Wonderware Historian)** — another historian platform; present at some nuclear and heavy industrial facilities
- **Cognite Data Fusion** — industrial data integration platform that can ingest from multiple historian sources, apply transformations, and expose a unified API; being evaluated at several utilities for cross-site fleet analytics
- **Python with PI Web API / AFSDK** — `requests` library for PI Web API REST calls; Cognite's `cognite-sdk-python` for Cognite; pandas for time-series analysis; the standard programmatic data access stack for plant analytics
- **OSIsoft PI Notifications / PI Event Frames** — PI's native event detection and alerting framework; can trigger notifications when tag values exceed thresholds; used for rule-based anomaly detection without ML models
- **EPRI Plant Modernization Program technical reports** — the primary reference library for nuclear plant data quality frameworks; requires EPRI membership; covers historian validation, AF model governance, and analytics deployment case studies
- **MLflow / DVC (Data Version Control)** — open-source model registry and experiment tracking tools; used by nuclear analytics teams building ML models to version training datasets, model artifacts, and performance metrics; supports rollback protocols
- **Grafana + InfluxDB or Prometheus** — open-source monitoring stack; used by some utilities for operational analytics dashboards; complements the historian by providing real-time visualization of derived metrics

### Step-by-Step Applied Workflow

1. **Extract a raw historian time series and assess quality** — using PI Web API or a CSV export from a plant training system, retrieve 6 months of data for a pressure transmitter and a redundant pressure transmitter measuring the same process; compute: (a) fraction of expected samples present, (b) min/max range check against the known instrument range, (c) correlation between the two transmitters; flag any anomalies.

2. **Build a compression artifact detector** — apply OSIsoft PI's default swinging door compression (deadband = 0.2% of span) to a synthetic pressure signal that includes a slow 0.1%/day drift; compare the compressed and original signals; quantify how much drift is invisible in the compressed historian record; document the limitation.

3. **Overlay calibration records with historian data** — obtain a sample calibration record (IAEA training materials or a plant simulator export) showing instrument as-found error at successive surveillance intervals; write a Python function that takes as-found error and surveillance date as inputs and returns a corrected time series that adjusts historian values by the measured drift between calibration intervals.

4. **Implement a cross-tag consistency check** — for a heat exchanger with inlet and outlet temperature measurements and a known heat duty calculation, implement an energy balance check: compute Q = ṁ × Cp × ΔT from measured flow and temperatures; compare against the expected duty from design; flag periods where the measured heat balance deviates more than 5% as potentially indicative of sensor error.

5. **Build a simple anomaly detector with concept drift monitoring** — train an isolation forest on 12 months of historian data from a feed pump (3 features: flow, inlet pressure, bearing temperature); generate anomaly scores for the next 6 months; plot the anomaly score distribution over the 6-month test period; compute a moving 30-day mean of the anomaly score and flag any period where the mean exceeds 1.5× its training baseline (indicating possible concept drift).

6. **Define a model governance document** — for the anomaly detector above, write a one-page governance document covering: (a) training data time range and exclusions, (b) performance metrics on the validation set (precision, recall at a defined threshold), (c) drift monitoring procedure (check monthly mean anomaly score against baseline), (d) rollback procedure (retain the previous model artifact; revert if drift is detected), (e) operator communication protocol (alert routing, false-positive reporting mechanism).

7. **Map the 10 CFR 50.59 applicability question** — for a hypothetical advisory system that recommends operator adjustment of a non-safety-related parameter, work through the 50.59 screening checklist: does this change the frequency of initiating events? Does it affect safety system function? Does it affect described methodology in the FSAR? This exercise builds the regulatory literacy needed to deploy plant analytics compliantly.

8. **Document the advisory/safety-function boundary for a specific use case** — choose a plant subsystem (e.g., reactor coolant pump vibration monitoring) and document: what an advisory model would look like for that system (alert operators to investigate, no automatic action), and why a directly actuating control response (automatically reduce power if vibration exceeds model-predicted threshold) would require a different regulatory treatment.

### AI Integration

AI/ML applications in nuclear plant data and analytics are growing rapidly in the advisory domain. The most mature current deployments fall into three categories.

**Anomaly detection for predictive maintenance**: ML models (isolation forests, LSTM autoencoders, one-class SVMs) trained on normal operating data from plant process historians can identify deviations that precede equipment failures. Cognite and EPRI have documented deployments at US and European utilities where these models provided 2–8 weeks of advance warning before bearing failures, valve degradation, and heat exchanger fouling that would otherwise have been detected only at the next scheduled inspection or after a forced outage.

**Performance monitoring and efficiency optimization**: Models that calculate equipment performance against design curves — pump efficiency vs. design hydraulic curve, heat exchanger effectiveness vs. clean-surface benchmark — provide continuous condition monitoring without manual engineering analysis. These models are relatively robust because they are based on established thermodynamic and hydraulic relationships; the ML component (if any) is used for pattern matching to diagnose which degradation mode is occurring, not for computing the performance index itself.

**Natural language processing for corrective action program analytics**: CAP databases at large plants contain hundreds of thousands of condition reports written over decades. NLP models can classify incoming CRs, identify recurring themes, and surface related historical events that the author may not have searched for. EPRI has published research on this application; several US utilities are in pilot phases.

The frontier application — connecting ML model outputs to operator displays in the main control room — introduces human factors engineering requirements (10 CFR 50 Appendix A General Design Criterion 19, NUREG-0696 on functional criteria for emergency response facilities) that require extensive validation beyond normal software testing. This is an active area of NRC regulatory guidance development.

### Case Studies

**EPRI Fleet Analytics Validation Framework**: EPRI's Plant Modernization Program published a validation framework for fleet-scale analytics in nuclear plants that addresses exactly the historian data quality and model governance issues described in this page. Their framework establishes four validation levels: (1) data quality validation, (2) model performance validation on historical data, (3) shadow deployment (model runs in parallel with existing processes but does not influence decisions), (4) supervised deployment (model outputs are available to operators with defined escalation protocols). This four-stage approach is now used as a reference by several US utilities implementing analytics programs.

**IAEA NHSI — Nuclear Harmonization and Standardization Initiative**: The IAEA's Nuclear Harmonization and Standardization Initiative includes a work stream on nuclear plant data interoperability, addressing the challenge that plant historian data formats, tag naming conventions, and metadata schemas differ significantly across reactor designs and operators. Their work on common data exchange formats and metadata standards is directly relevant to multi-site fleet analytics programs. IAEA Technical Documents in this area provide the clearest public articulation of the data governance challenges facing the global nuclear fleet.

**Cognite Data Fusion at European Utilities**: Cognite's industrial data integration platform has been deployed at several European utilities and heavy industrial operators as a middleware layer between plant historians, CMMS systems, and analytics applications. Their published case studies describe the data quality challenges encountered — specifically tag mapping, unit conversion errors, and timestamp normalization — and the data pipeline architecture used to address them. The Cognite approach of treating industrial data integration as a software engineering problem (version-controlled transformation pipelines, unit test coverage, data lineage tracking) is directly applicable to nuclear plant analytics programs.

### Failure Modes & Safety

**Analytics model producing overconfident outputs on out-of-distribution data**: A vibration anomaly detector trained on data from normal operation at 100% power may produce confidently low anomaly scores during low-power operations (startup, power ascension testing) where the vibration signature is fundamentally different from the training distribution. If operators interpret the low anomaly score as confirmation of healthy equipment during these anomalous operating modes, the model has created a false sense of security. Robust models include an explicit out-of-distribution detector that flags when input data is outside the training envelope.

**Silent concept drift in a long-deployed model**: A pump health model that was accurate in year 1 of deployment may be producing systematically biased outputs in year 5 as the pump's operating characteristics have changed with aging. If no one is monitoring the model's residuals against confirmed outcomes, the drift is invisible. The model continues to be trusted because it was once accurate and no one has had reason to challenge it. Governance frameworks must include automated residual monitoring with explicit alerting thresholds.

**Data pipeline failure creating stale advisory outputs**: An analytics dashboard that displays "last updated: 4 hours ago" when operators expect real-time data may cause operators to make decisions based on stale information while believing it is current. Data pipeline monitoring — tracking the timestamp of the most recent successful historian query and alerting when it falls outside the expected update interval — is a required component of any production analytics deployment.

**Conflating advisory model output with safety-function verification**: An operator who interprets an anomaly detector's "normal" output as confirmation that a safety system is healthy has crossed the line between using an advisory tool appropriately and treating it as a substitute for required technical specification surveillance. Training and procedure controls must explicitly address this — advisory analytics are decision support tools, not surveillance substitutes.

**Training data contaminated by known-bad periods**: If the analyst does not exclude fault conditions, calibration-error periods, or plant transients from the training dataset, the model learns from corrupted data. A one-class anomaly detector trained on data that includes subtle faults will not identify those faults in production because they appear "normal" relative to the training distribution. Data quality validation and explicit exclusion of known-bad periods from training sets is a prerequisite for meaningful model validation.

### Business & Commercial Layer

The commercial case for nuclear plant data analytics is compelling: the industry spends billions of dollars annually on unplanned outages and corrective maintenance that analytics could predict. EPRI estimates that fleet-wide deployment of predictive maintenance analytics for nuclear plant rotating equipment and heat exchangers could avoid 10–20% of unplanned forced outage days — a financial impact of hundreds of millions of dollars annually across the US fleet alone.

The business model for analytics in the nuclear industry has three implementation patterns: (1) utility-internal programs, where the plant operator builds and maintains its own analytics capability using in-house data engineering and data science staff; (2) vendor-supported programs, where companies like EPRI, Cognite, or specialized nuclear analytics vendors provide platforms and models with utility customization; (3) OEM-supplied monitoring packages, where reactor vendors (Westinghouse, EDF-GDF Suez, KEPCO E&C) include analytics for their specific equipment as part of service contracts.

In India, NPCIL has been building out digital plant analytics capability as part of a broader digitalization initiative. The data governance challenge at NPCIL is amplified by the fleet's heterogeneity: PHWRs of different vintage with different historian systems, DCS platforms, and data architectures. Building a unified fleet analytics program requires the data integration and governance frameworks described in this page, applied at scale across multiple sites.

### Hiring Signal

**Job titles in plant data governance and analytics:**
- **Plant Data Engineer** — designs and maintains historian integration pipelines, AF model structures, and data quality validation workflows; typically requires both process engineering knowledge (to understand what the tags represent) and software engineering skill (to build the pipelines)
- **Industrial Data Scientist (Nuclear)** — builds and validates ML models for anomaly detection, performance monitoring, and predictive maintenance; requires domain knowledge of nuclear plant systems alongside ML methodology
- **OT Data Governance Lead** — owns the policies and processes for how operational technology data is managed, validated, and made available for analytics; typically a senior role at a utility with a mature analytics program
- **Digital Twin Engineer** — builds physics-informed digital models of plant equipment integrated with historian data for real-time performance comparison; requires process engineering depth plus software integration skill
- **Advisory Analytics Engineer** — develops and deploys operator advisory tools within the regulatory framework; requires understanding of both the analytics technology and the 10 CFR 50.59 / licensing basis implications of deploying software in the plant environment
- **Reliability Analytics Engineer** — applies data analytics to equipment reliability programs; works at the intersection of CMMS data, historian data, and reliability engineering (FMEA, Weibull analysis, RCM)

**Specific interview screens for data governance and analytics roles:**
1. "You receive a historian export for a reactor coolant pump bearing temperature tag spanning 5 years. Describe your step-by-step process for validating this data before using it to train an anomaly detection model."
2. "An isolation forest anomaly detector deployed 18 months ago begins producing anomaly scores 2× higher than its historical baseline for a normally operating feed pump. What are the three most likely causes, and how do you distinguish between them?"
3. "What is the difference between a nuclear plant advisory analytics system and a nuclear safety system from a regulatory perspective? Why can a machine learning model be used in the former but essentially not in the latter today?"
4. "A calibration record shows that a feedwater flow transmitter was found 1.5% high at its most recent 24-month calibration. How does this affect your interpretation of 2 years of historical data from that transmitter? What would you do about it in your analysis?"
5. "Explain OSIsoft PI's swinging door compression algorithm. How does it affect the fidelity of historian data for fast transient analysis versus slow drift detection?"

### Portfolio Projects

**Beginner: `historian-data-quality-audit`**
- Deliverables: A Python notebook that performs a quality audit on a synthetic historian dataset (provided as CSV with 10 process tags over 12 months, containing deliberately introduced defects: 3% missing samples, 2 tags with range violations, 1 tag with a timestamp discontinuity, 1 tag pair that diverges by >5% after month 8); the notebook identifies and reports each defect type with count and severity
- Suggested repo tree: `README.md`, `data/synthetic_historian.csv`, `notebooks/data_quality_audit.ipynb`, `results/quality_report.md`
- Acceptance criteria: (1) the audit correctly identifies all 5 defect categories in the synthetic dataset with < 2 false positives; (2) the quality report specifies what analysis would be invalid using each defective tag and why; (3) the notebook runs end-to-end with a single `jupyter nbconvert --execute` command

**Intermediate: `anomaly-detector-with-governance`**
- Deliverables: An isolation forest anomaly detector trained on 9 months of synthetic plant historian data (feed pump: flow, inlet pressure, bearing temperature); tested on a holdout 3-month period containing one injected bearing degradation event; includes: a model governance document specifying training data, validation metrics, drift monitoring procedure, and rollback protocol; a drift detection implementation that raises an alert when the 30-day rolling mean anomaly score exceeds 1.5× the training baseline
- Suggested repo tree: `README.md`, `data/`, `models/`, `src/train.py`, `src/drift_monitor.py`, `docs/model_governance.md`, `results/validation_report.md`, `tests/`
- Acceptance criteria: (1) the injected degradation event is flagged at least 7 days before the defined fault threshold; (2) the drift monitor correctly triggers on a synthetic concept drift test case; (3) the governance document includes a rollback procedure that a new team member could execute without asking the author questions

**Advanced: `fleet-analytics-data-pipeline`**
- Deliverables: A data pipeline that ingests historian exports from 3 simulated plant units (different tag naming conventions, different sample rates, different compression settings), normalizes them to a common schema, applies cross-tag consistency checks (instrument redundancy comparison for 2 tag pairs per unit), computes a daily data quality score for each tag, and outputs an analysis-ready dataset with a provenance record documenting every transformation applied; a safety assumptions document covering what the pipeline does and does not validate
- Acceptance criteria: (1) the pipeline correctly maps all 3 simulated tag naming conventions to the common schema without manual intervention; (2) the cross-tag consistency checks correctly identify the 2 injected measurement discrepancies in the synthetic data; (3) the provenance record is machine-readable (JSON or YAML) and enables reconstruction of the exact transformation applied to any output value

### Future Trends

- **2026**: PI System (AVEVA) and Cognite Data Fusion achieve broad deployment across US and European nuclear fleets as the standard data integration layer between OT historians and analytics applications; the "data plumbing" problem is increasingly solved at the infrastructure level, allowing engineers to focus on model quality rather than data access
- **2030**: NRC regulatory guidance on digital I&C (NUREG-0800 Chapter 7 updates) begins to address advisory AI systems in the main control room environment more explicitly; formal guidance on acceptable validation methodologies for ML-based operator advisory tools reduces regulatory uncertainty and accelerates deployment
- **2035**: Physics-informed neural networks (PINNs) that embed thermodynamic and hydraulic constraints into their architecture are validated for nuclear plant performance monitoring; their interpretability and physical consistency addresses some of the regulatory concerns about black-box ML models, enabling more confident advisory deployments
- **2045**: Digital twin programs at leading utilities have accumulated 20+ years of operating data with validated data governance frameworks; the analytical models built on this foundation enable new operational strategies (flexible load-following, predictive maintenance-based outage scope optimization) that are not feasible today due to data quality limitations

### Interview Questions

1. **What is OSIsoft PI's swinging door compression algorithm and how does it affect the quality of historian data for engineering analysis?**
   *Answer*: Swinging door compression is an exception reporting algorithm that records a new data point only when the actual signal deviates from a linear interpolation of the last stored point by more than a specified deadband. The result is a piecewise-linear approximation of the actual signal rather than a faithful sample record. For slow process variables that change smoothly, this approximation is adequate. For fast transients narrower than the deadband (e.g., a brief pressure spike), the event is invisible in the compressed record. For slow drift smaller than the deadband, the historian records a flat line until the deadband is crossed, masking the true gradual trend. Engineers using historian data must understand the deadband settings for each tag and their implications for the analysis at hand.

2. **Why is a random 80/20 train-test split inappropriate for time-series models on plant historian data?**
   *Answer*: Because plant historian data is temporally autocorrelated — consecutive measurements are similar, so randomly sampling 20% of timesteps for the test set produces a test set that is highly similar to the training set (adjacent timesteps of the same measurement will be in both). The result is an overly optimistic validation metric that does not reflect the model's ability to generalize to future operating conditions. The correct approach is temporal splitting: train on an earlier time period, validate on a later time period that the model has not seen. This simulates the actual deployment scenario where the model is trained on historical data and applied to future data.

3. **What is the regulatory distinction between an advisory analytics system and a safety function in US nuclear plants?**
   *Answer*: Safety systems perform protective actions (scram, ECCS actuation, containment isolation) based on plant state and must comply with IEEE Std 603 and 10 CFR 50 Appendix A GDC 21–24. They require deterministic, formally qualified hardware and software with a proven design basis. Advisory systems provide information or recommendations to operators who retain the decision authority; they do not perform protective actions. Advisory systems are subject to 10 CFR 50.59 (changes to the facility) and require rigorous validation, but not IEEE 603 safety system qualification. Current ML systems are compatible with the advisory framework because the operator remains in the decision loop. They are incompatible with the safety system framework because their behavior cannot be formally verified against a design basis specification.

4. **What is concept drift in a plant anomaly detection model and how do you detect it?**
   *Answer*: Concept drift occurs when the statistical relationship between input features and the target quantity changes over time — meaning the model's training distribution no longer matches the current operating distribution. In a nuclear plant context, this can occur as equipment ages, fuel burnup progresses, cooling water temperatures change seasonally, or operational practices evolve. Detection: monitor model residuals or anomaly scores over time using a rolling window; if the moving average diverges significantly from the training baseline, concept drift is the likely cause (assuming no physical anomaly explains the shift). Statistical tests such as the Kolmogorov-Smirnov test on the residual distribution or CUSUM (cumulative sum) control charts on rolling residual means are standard monitoring approaches.

5. **What is cross-tag consistency validation and why is it important for nuclear plant historian data?**
   *Answer*: Cross-tag consistency validation uses independent measurements of the same physical quantity — redundant transmitters, mass balance relationships, energy balance relationships — to verify that each measurement is consistent with what the physics of the process requires. If two redundant temperature transmitters disagree by more than their combined measurement uncertainty, one of them is likely faulty or miscalibrated. If the computed heat balance on a steam generator (Q = ṁ × Cp × ΔT) deviates from the expected duty by more than 5%, one of the contributing measurements (flow, temperature) may be in error. Cross-tag validation is important because a single-transmitter validation (is the value in range?) cannot detect a systematically biased transmitter that is reading consistently wrong within a plausible range. Only comparison against an independent measurement or physical relationship can detect this.

### Further Depth

- **EPRI Plant Modernization Program technical reports** (epri.com) — the primary reference for nuclear plant historian data governance and analytics deployment frameworks; EPRI membership required; search for "plant historian data quality" and "predictive maintenance analytics"
- **OSIsoft PI System documentation** (aveva.com/en/products/aveva-pi-system/) — official PI historian documentation; PI Web API reference, Asset Framework modeling guide, and PI Vision dashboard documentation
- **IAEA Nuclear Energy Series NP-T-1.6** — "Maintenance Optimization Programs for Nuclear Power Plants"; covers data-driven maintenance approaches and plant information system requirements
- **NUREG-0700 Rev. 3** — NRC guidance on human-system interface design; relevant for deploying analytics tools in the main control room environment; covers display design, alarm management, and operator decision support
- **10 CFR 50.59 rule text and NRC regulatory guide 1.187** — the regulatory basis for evaluating changes to the facility; required reading before deploying any new software in a nuclear plant environment
- **"Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow" — Aurélien Géron** — the standard ML practitioner reference; apply Chapters on anomaly detection, time-series analysis, and model deployment with nuclear plant data quality constraints in mind
- **Cognite Data Fusion documentation** (docs.cognite.com) — industrial data integration platform; REST API documentation, transformation pipeline patterns, and case studies applicable to multi-historian integration scenarios
- **IEEE Std 603-2018** — "Criteria for Safety Systems for Nuclear Power Generating Stations"; the foundational standard that defines why ML systems cannot currently perform safety functions; understanding this standard clarifies the regulatory boundary for all nuclear AI deployments
