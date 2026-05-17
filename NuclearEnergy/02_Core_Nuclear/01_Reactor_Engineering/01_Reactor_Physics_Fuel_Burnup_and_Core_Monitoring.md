# Reactor Physics, Fuel Burnup, and Core Monitoring

## Overview

Core monitoring is the operational face of reactor physics. It turns neutron behavior, fuel condition, and thermal limits into watchable indicators and decision points for operators and engineers.

## Why This Topic Matters

Plant decisions rely on knowing whether the core is within allowed state, how burnup affects current behavior, and whether a transient is moving the plant toward or away from margins.

## Core Terminology

- `Flux map`: representation of neutron distribution or power shape
- `Power peaking`: local concentration of power that affects thermal margins
- `Burnup`: fuel usage state across the cycle
- `Shutdown margin`: ability to make and keep the reactor subcritical

## Mental Model / Big Picture

```text
reactor state
    -> detectors and calculations
    -> core monitoring
    -> margin assessment
    -> operator / engineering decision
```

## Main Concepts / Core Concepts

- local power matters, not just total power
- burnup and poison state change allowable operating strategy
- monitoring combines measurement and model-based inference

## Architecture / Components / Building Blocks

- neutron detectors
- temperature and pressure instrumentation
- core-monitoring software
- surveillance tests and calibration processes

## Practical / Design / Operational Sections

Engineers track:

- power distribution
- axial and radial shape changes
- approach to limits
- detector consistency
- fuel-cycle progression

## Hands-On Example / Mini Project

Build a notebook that simulates a simplified power-shape change across burnup and flags when a chosen local margin is exceeded.

## Best Practices

- compare measurements across channels
- treat inconsistent instrumentation seriously
- connect monitoring output to actual operating decisions

## Common Pitfalls

- watching only gross power
- ignoring detector uncertainty
- forgetting that burnup changes the operating picture

## Metrics / KPIs / What to Measure

- flux trends
- local peaking factors
- burnup state
- shutdown margin

## Recommended Resources

- MIT OCW `22.05`
- MIT OCW `22.091`
- OpenMC examples for more advanced modeling

## Interview Questions

- Why does local power peaking matter?
- How does burnup change plant operations?
- Why is detector trustworthiness important?

## Portfolio / Resume Application

Core-state visualizations and margin dashboards make strong simulation portfolio artifacts.

## Next Step

Continue to [Thermal Hydraulics, Cooling Loops, and Heat Removal](02_Thermal_Hydraulics_Cooling_Loops_and_Heat_Removal.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

In operating plants, reactor physics becomes a shift-by-shift question of whether the measured core state still matches the expected one. Engineers watch flux behavior, detector agreement, burnup progression, xenon effects, shutdown margin, local power behavior, and thermal limits because those determine how safely and economically the unit can run.

This work is not just "physics." It drives startup planning, maneuver restrictions, surveillance decisions, reload planning, and when operations should slow down and call reactor engineering.

### Industry Tool Stack

- in-core and ex-core detector systems
- core monitoring software and engineering calculation packages
- cycle-history databases, burnup maps, and surveillance results
- startup test records and detector-calibration checks
- `OpenMC` and `PyNE` for open learning and study-scale modeling
- engineering notebooks and margin dashboards for review packages

### Step-by-Step Applied Workflow

1. Begin from the expected core state for the current cycle point, rod condition, and power level.
2. Compare detector signals and calculated distributions to see whether the core is behaving as predicted.
3. Check burnup progression, xenon condition, and any local peaking or detector disagreement that could reduce margin.
4. If measured behavior drifts, reconcile instrumentation, operating conditions, and physics assumptions before recommending action.
5. Issue a review note that tells operations what is normal, what requires caution, and what needs further engineering evaluation.

### AI Integration

AI fits here when it helps engineers rank what deserves attention first:

- detector-drift and sensor-health anomaly ranking
- surrogate models for repeated what-if studies
- optimization support for fuel-management scenarios

The model still needs engineering review because a neat score is not the same as a defendable core-state judgment.

### Case Studies

- `MIT CRPG / OpenMC`: strong benchmark for transparent reactor-analysis workflows that can be inspected and reproduced.
- `NPCIL`: useful benchmark for why cycle-wise reactor behavior, detector trust, and conservative monitoring matter in an operating fleet.
- `Westinghouse` and `Framatome`: useful vendor benchmarks because both publicly position core design and fuel-management services around reload analysis, monitoring, and margin management.

### Failure Modes & Safety

- detector drift can make the core look healthier or less stable than it really is
- xenon and burnup effects can be underestimated by inexperienced analysts
- local peaking or margin erosion can hide behind acceptable total power if only headline numbers are watched
- the safety failure is acting on a calculation without reconciling it against real detector behavior and operating condition

### Business & Commercial Layer

Better core monitoring protects:

- fuel utilization and cycle economics
- outage planning and reload quality
- capacity factor through fewer avoidable derates
- engineering workload by catching detector or model issues early

It also creates commercial demand for fuel services, analysis software, monitoring systems, and engineering consulting.

### Hiring Signal

Interviewers look for engineers who can explain:

- why detector agreement matters
- how burnup changes decision-making during a cycle
- what a conservative response looks like when model and measurement disagree

Good portfolio evidence includes a burnup visualization, a detector-comparison notebook, and one engineering note discussing margin rather than only plotting numbers.

### Portfolio Projects

- Beginner: `burnup-visualizer`
  Deliverables: synthetic burnup map, detector-trend plots, short note on what parameters should be checked each cycle step.
- Intermediate: `core-monitoring-review`
  Deliverables: OpenMC-style toy model, detector-comparison dashboard, mismatch triage note.
- Advanced: `reload-margin-study`
  Deliverables: scenario study with assumptions, uncertainty notes, margin plots, and operator-facing summary language.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: open tools make reactor-analysis learning more accessible, but review discipline remains the hard part.
- `2030`: stronger coupling between fleet data, digital twins, and core-performance studies.
- `2035`: more value in hybrid workflows where fast models screen cases before deeper analysis.
- `2045`: the enduring skill is not one code; it is conservative interpretation of core behavior under uncertainty.

### Interview Questions

1. Why is total power alone not enough for core monitoring?
   Short answer: local power distribution and detector agreement can reveal margin issues that total power hides.
2. How does burnup affect operation?
   Short answer: it changes reactivity behavior, power shape, margins, and the decisions around rods and cycle planning.
3. What should you do if detector signals and calculations disagree?
   Short answer: check instrumentation quality, operating condition, and model assumptions before recommending action.
4. Why does xenon matter operationally?
   Short answer: it changes reactivity and can distort expected power behavior after maneuvers.
5. Where can AI help without replacing reactor engineering?
   Short answer: anomaly ranking, detector health checks, and repeated scenario screening.

### Further Depth

- MIT OCW `22.05` and `22.091`
- OpenMC documentation and examples
- PyNE documentation
- IAEA reactor physics training material
