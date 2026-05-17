# Python Programming Basics

## Overview

Python is the most widely used programming language for AI and ML work. Its simple syntax reads almost like English, and its ecosystem of libraries — NumPy for math, pandas for data tables, scikit-learn for models — means you rarely build from scratch. Knowing basic Python lets business professionals prototype ideas, automate repetitive tasks, and communicate more effectively with data science teams.

---

## Why It Matters

Managers who can read and write basic Python scripts close the gap between business questions and technical answers. Instead of waiting days for an analyst to pull numbers, a product manager can query a dataset in a Jupyter notebook, explore patterns, and bring sharper questions to the next sprint planning. Python literacy also helps leaders evaluate vendor tools, spot unrealistic promises, and estimate development effort.

## Key Principles

- Start with core constructs: variables, loops, conditionals, and functions
- Use libraries instead of writing math from scratch — they are tested, optimized, and documented
- Write readable code with clear variable names and comments; you will revisit it months later
- Jupyter notebooks let you mix code, output, and narrative in one document — ideal for exploratory analysis

## Key Terms

| Term | Definition |
|------|------------|
| **Variable** | A named container that stores a value such as a number, string, or list |
| **Library** | A reusable package of pre-written code (e.g., pandas, NumPy) |
| **Function** | A named block of code that takes inputs, performs a task, and returns an output |
| **Jupyter Notebook** | An interactive environment for writing and running Python code alongside visualizations |

## Use Case

A finance analyst writes a 20-line Python script that pulls daily exchange rates from an API, calculates rolling averages, and emails a summary table to the treasury team every morning — replacing a manual spreadsheet process that took 45 minutes.

## Scenario

> A retail chain's category manager learned basic pandas in a weekend workshop. She wrote a script that merged point-of-sale data with weather data, revealing that umbrella sales spiked two days before forecasted rain, not on rainy days. The insight shifted promotional timing and boosted umbrella revenue 18% over the next quarter.

## Examples

- A supply chain team uses a Python script with the PuLP library to solve a linear programming model that minimizes shipping costs across 12 warehouses
- An HR analyst uses matplotlib in a Jupyter notebook to visualize employee attrition trends by department, presenting the chart directly in a leadership meeting

---

## Audited Appendix

# Python Programming Basics
**Course:** AI and ML for Business  
**Module:** content  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `ai-ml-business/content/03-python-programming-basics.md`

---

## 1. Topic Snapshot
Python is the business-friendly language that connects data, analysis, and automation in AI/ML work.
This topic helps decide when a leader should prototype in code, automate repeatable analysis, or hand work to a specialist.
For IT, AI, product, and consulting teams, the practical value is faster answers, clearer problem framing, and less dependence on manual spreadsheets.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Python | Python programming language | The language used to write scripts and data workflows | To prototype and automate quickly | N/A | Analytics, engineering, AI |
| Variable | N/A | A named container for a value | To store intermediate results | N/A | Coding, notebooks |
| Library | N/A | Reusable pre-written code package | To avoid rebuilding common functions | Adoption, version, coverage | Data science, product analytics |
| NumPy | Numerical Python | Math-focused library for arrays and numerical work | To do fast computation on data | N/A | ML, scientific computing |
| pandas | N/A | Library for tabular data tables | To clean, join, and analyze business data | N/A | Reporting, analytics |
| scikit-learn | N/A | Library for common ML models | To build models without writing algorithms from scratch | Accuracy, F1, CV score | ML prototyping |
| Function | N/A | A reusable block of code with inputs and outputs | To keep logic organized | N/A | Scripting, software |
| Jupyter Notebook | N/A | Interactive coding document with code and narrative | To explore and explain data in one place | N/A | Analytics, workshops |
| API | Application Programming Interface | A way to pull data from another system | To automate data access | Latency, uptime, response success | Integration, data engineering |
| Rolling average | N/A | Average over a moving window | To smooth noisy data | Window size, trend stability | Forecasting, ops |
| Spreadsheet process | N/A | Manual Excel-style workflow | To compare automation against current work | Time per task, error rate | Finance, ops |
| Point-of-sale | POS | Transaction system at checkout | To capture sales behavior | Sales, basket size | Retail analytics |
| Weather data | N/A | Historical or forecast weather observations | To enrich demand analysis | Coverage, forecast accuracy | Retail, logistics |
| Promotional timing | N/A | When a promo is launched | To align offers with demand | Uplift, conversion | Growth, merchandising |
| PuLP | Python LP model library | Tool for building optimization models in Python | To solve resource allocation problems | Objective value, constraints met | Supply chain, OR |
| Linear programming | LP | Optimization method for best outcome under constraints | To minimize cost or maximize value | Objective value, feasibility | Operations, consulting |
| matplotlib | N/A | Plotting library for charts | To visualize trends and outliers | N/A | Reporting, notebooks |
| Attrition trends | N/A | Pattern of employees leaving over time | To detect workforce risk | Attrition rate | HR analytics |
| Department | N/A | Organizational unit | To compare performance across groups | Headcount, attrition, cost | HR, planning |

## 3. Frameworks & Matrices

### Python Usefulness Ladder
**Purpose:** Decide whether Python is the right tool for the task.

**Text Diagram:**
```text
Manual spreadsheet work
        |
        +-- Repeatable or formula-heavy? --> Python script
        |
        +-- Needs data wrangling, charts, or model prototyping? --> Python + notebook
        |
        +-- Needs production integration? --> Python service / pipeline
```

Axes / Quadrants / Components explained:
Component 1: Manual work, meaning ad hoc tasks with high human effort.
Component 2: Python script, meaning repeatable automation and data processing.
Component 3: Notebook, meaning exploration plus explanation for stakeholders.
Component 4: Production pipeline, meaning reusable code that runs reliably in a workflow.

IT/AI/Product/Consulting worked example: A product manager moves a weekly churn report from Excel into a Python notebook, then hands the same logic to engineering for a scheduled pipeline once the metrics are stable.
When to pull this out in a meeting: When a team asks whether the analysis should stay in Excel or become code.

### Library vs Build Matrix
**Purpose:** Decide whether to use a library or custom code.

**Text Diagram:**
```text
Need math / data table / model routine?
   |
   +-- Existing library available --> Use it
   |
   +-- No reliable library or special logic --> Build carefully
```

Axes / Quadrants / Components explained:
Component 1: Reuse, meaning libraries like NumPy, pandas, and scikit-learn.
Component 2: Custom build, meaning specialized logic that libraries do not cover.
Component 3: Risk, meaning maintenance burden if you rebuild standard functions.

IT/AI/Product/Consulting worked example: A consulting team uses pandas for cleaning client sales data and scikit-learn for a quick baseline model instead of writing a custom regression engine.
When to pull this out in a meeting: When someone proposes building something that already exists in a standard package.

### Notebook-to-Production Matrix
**Purpose:** Decide whether the work should remain exploratory or be operationalized.

**Text Diagram:**
```text
Exploration only ---> Jupyter Notebook
Validated repeatability ---> Script
Business-critical automation ---> Scheduled pipeline/service
```

Axes / Quadrants / Components explained:
Component 1: Exploration, meaning the team is still learning.
Component 2: Repeatability, meaning the logic should run the same way every time.
Component 3: Business criticality, meaning failure would affect operations or revenue.

IT/AI/Product/Consulting worked example: An HR analyst starts with a Jupyter notebook to visualize attrition by department, then turns the workflow into a scheduled report once leadership starts using it monthly.
When to pull this out in a meeting: When the question is whether a notebook is “good enough” for ongoing use.

## 4. Formulas

The source does not include explicit formulas; the following are added for practical business use [verified from model knowledge, not source].

Formula: `Time Saved (%) = (Manual Time - Automated Time) / Manual Time`
Variables:
Manual Time = time required before Python automation
Automated Time = time after script or pipeline
Why this formula exists: It answers whether automation is worth the setup effort.
How to interpret the output:
Value < 0.25 → small gain, automate only if the task is frequent
Value 0.25–0.60 → strong candidate for scripting
Value > 0.60 → high-priority automation
Worked example with numbers: If a treasury report drops from 45 minutes to 10 minutes, time saved = (45-10)/45 = 0.78, which justifies automation.

Formula: `Promo Lift (%) = (New Revenue - Baseline Revenue) / Baseline Revenue`
Variables:
New Revenue = revenue after a change
Baseline Revenue = revenue before the change
Why this formula exists: It answers whether a data-driven change actually improved performance.
How to interpret the output:
Value < 0.05 → not enough signal
Value 0.05–0.15 → useful pilot result
Value > 0.15 → strong business case
Worked example with numbers: If umbrella revenue rises from $100,000 to $118,000 after moving promotions earlier, lift = 18%, matching a meaningful product or retail impact.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Wait days for a simple data pull | Use Python to query and summarize repeatable data tasks |
| Rebuild standard math code from scratch | Use tested libraries like NumPy, pandas, and scikit-learn |
| Keep analysis trapped in one-off notebooks forever | Move stable logic into scripts or pipelines |
| Show only raw output with no narrative | Pair code with explanation so stakeholders can follow decisions |
| Treat a script as useful without measuring time saved | Compare automation against the spreadsheet baseline |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Weekly finance reporting
Situation: A treasury analyst is manually pulling exchange rates and building a summary every morning. Python can replace that repetitive spreadsheet work with an API-driven script.
Applicable framework/metric: Python Usefulness Ladder, Time Saved (%).
Analysis: The report falls from 45 minutes to 12 minutes. Time saved = (45-12)/45 = 73.3%, which is enough to justify automation and reduce operational risk.
Decision rule: If time saved > 50%, automate; if 25%–50%, pilot; if below 25%, keep manual.
Action: Build the script, add error handling, and schedule it with a delivery check.

Scenario 2: Retail demand insight
Situation: A product analytics team wants to understand why umbrella sales spike before rain rather than on rainy days. A Python notebook can merge POS and weather data and test the timing hypothesis.
Applicable framework/metric: Notebook-to-Production Matrix, promo lift.
Analysis: After shifting promotions two days earlier, umbrella revenue rises 18% over the next quarter.
Decision rule: If lift > 15%, scale the timing change; if 5%–15%, A/B test by region; if below 5%, revert.
Action: Run a segmented experiment and report the lift by store cluster.

Scenario 3: HR attrition dashboard
Situation: An HR analyst wants to show attrition trends by department to leadership. Python and matplotlib are the fastest path from raw data to an interpretable chart.
Applicable framework/metric: Library vs Build Matrix, attrition rate.
Analysis: The notebook reveals one department with 2x the company average attrition rate, which becomes the focus for deeper diagnosis.
Decision rule: If a department is > 1.5x the company average, prioritize intervention; if 1.0x–1.5x, monitor; if below 1.0x, keep current policy.
Action: Prepare a department-level retention review and share the chart in the next leadership meeting.

## 7. Implementation Playbook
1. Identify one repetitive business task that Python can shorten or standardize.
2. Pull the minimum dataset needed for a first pass.
3. Prototype in a notebook so analysis and explanation stay together.
4. Prefer a tested library over custom code whenever the library already solves the problem.
5. Measure time saved, error reduction, and stakeholder usefulness.
6. Convert stable analysis into a script or pipeline before it becomes mission-critical.
7. Package the result with plain-language notes so non-technical leaders can use it.

## 8. Content Quality Audit
Covered well: The source correctly positions Python as the bridge between business questions and data science execution, and it highlights libraries and notebooks in a useful business context.
Underplayed or missing: It does not distinguish exploratory analysis from production engineering, discuss testing/versioning, or mention failure modes like brittle notebooks.
Supplement with: *Automate the Boring Stuff with Python* by Al Sweigart (2019), *Python for Data Analysis* by Wes McKinney (2017) [verified from model knowledge, not source], and a short internal style guide for notebooks-to-production handoff.
Red flags in the source: The examples are helpful but imply that writing a script is enough; in practice, data quality, testing, and operational ownership decide whether the automation lasts.

## 9. Quick-Recall Card
```text
Topic: Python Programming Basics
Core idea: Python is the fastest path from business data to repeatable analysis and automation.
Key metric/formula: Time Saved (%) = (Manual Time - Automated Time) / Manual Time.
Framework trigger: Use when work is repetitive, data-heavy, or likely to move from notebook to production.
Watch out for: Leaving logic trapped in brittle notebooks or rebuilding standard libraries from scratch.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which repeating business task should become code first?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [IT/AI/Product/Consulting framing, time-saved and lift formulas, notebook-to-production gating] Final scores: all 5/5 Pass 2 completed: 2026-04-20 11:37 Audited by: A2 -->
