# Observability Telemetry and Fleet Diagnostics

## Overview

This page covers how to know what your robots are doing once they leave the development bench. In a serious robotics program, deployment is not the finish line. It is the point where the team has to observe behavior across real networks, real operators, real buildings, and real hardware drift without attaching a laptop to every robot. That is the job of observability. In robotics, observability means three complementary things: logs that explain what happened, metrics that show how the system is trending, and traces that reveal where latency or blocking appears across a distributed stack. It also means recorded data that can be replayed later against a known software version.

This topic matters because many robot failures are not clean crashes. They are slow degradations: SLAM quality worsens after a mapping update, a camera pipeline drops frames only on one robot class, QoS mismatches appear under one Wi-Fi condition, or battery behavior drifts across a fleet long before a hard fault. Without structured observability, those failures turn into anecdotes. With it, the team can see the problem, correlate it, reproduce it, and feed it back into tests. This page turns “we deployed the stack” into “we can operate and support the stack.”

## Logs Metrics and Traces on Real Robots

Logs, metrics, and traces solve different problems and they should not be confused. Logs answer “what happened?” They are event records: controller switched, planner failed, map update rejected, battery warning raised, behavior tree entered recovery, inference node exceeded latency threshold. In ROS 2 systems, this usually starts with `rclcpp` or `rclpy` logging and `/rosout`, but production systems rarely stop there. Teams add structured fields such as robot ID, mission ID, map version, sensor serial numbers, and error categories so the logs can be searched later instead of just read locally. Severity matters too. If every transient event is logged as an error, operators stop trusting the stream. Good robot logging distinguishes between expected recoverable events, degraded-but-manageable conditions, and states that really require action.

Metrics answer a different question: “how healthy is the system over time?” CPU saturation, topic rates, dropped frames, battery discharge slope, localization covariance, planner cycle time, QoS deadline misses, and mission success rate all belong here. Prometheus-style metrics are useful for scraping robot and infrastructure health. InfluxDB-style time-series systems are helpful when the data is high-cardinality or mission-tagged. The important point is that metrics are not substitutes for logs. They summarize the state of the system, but they do not explain one specific failure by themselves.

Traces solve the third problem: “where did the time go?” Robotics systems are distributed and asynchronous. A perception message may move from a camera driver to an image rectifier to a detector to a tracker to a planner to a controller. When the end-to-end loop becomes too slow, the team needs timing evidence across nodes, executors, callbacks, and middleware hops. That is where OpenTelemetry-style ideas, `ros2_tracing`, and LTTng matter.

## Bagging Replay and Edge-to-Cloud Data Flow

Robot observability always hits a bandwidth wall. It is easy to say “record everything.” It is much harder to do that on an edge computer with finite SSD life, limited uplink, and multiple high-rate sensors. That is why rosbag strategy matters. `ros2 bag` with MCAP is useful because it gives a practical recorded-data path for debugging and replay, but the team still has to decide what to record continuously, what to sample, and what to retain only on trigger. A 3D LiDAR, multiple cameras, and full debug topics can fill storage very quickly. A professional bagging policy usually records enough to reconstruct the failure while leaving room for long operating windows. That often means recording key sensor topics, transforms, command paths, and system health topics all the time, while reserving very high-rate raw streams or extra debug topics for triggered capture.

The edge-to-cloud architecture then determines what leaves the robot. In practice, most fleets do not stream all raw data all the time. They record locally, upload summaries and metrics continuously, and fetch full bags only when a trigger condition or incident review requires it. This is where platforms such as Foxglove, Formant, InOrbit, and Freedom Robotics become useful as operations layers rather than as replacements for local recording. They help teams search cross-robot history, compare one robot to fleet baselines, and retrieve the right recordings when a problem crosses from “interesting” to “actionable.”

Replay is what makes this useful for engineering. If the team can replay a bag against a frozen stack version and reproduce the failure, observability has become development leverage instead of just operations overhead.

## Fleet Dashboards Alerting and Incident Review

Fleet dashboards should not try to show everything. They should show the few signals that reliably predict degraded mission quality or support load. Good robotics dashboards often include CPU and memory headroom, network quality, battery health, localization confidence, topic-rate health, planner or controller timing, mission state, and fault counters. They do not page the team for every node restart if the node restarts cleanly and the mission keeps running. They do page or alert on sustained SLAM divergence, repeated actuator faults, rising QoS deadline misses, or a battery pack whose behavior is drifting across multiple shifts.

Alerting quality matters because robots live in noisy environments. If the fleet generates constant low-value alerts, operators learn to ignore the system. That makes observability worse than useless. The correct approach is to alert on signals that imply real customer, safety, or uptime risk, then use richer logs and traces to drill down. This is especially important in AMR fleets and service robots operating in hospitals, warehouses, or public buildings where the system may spend long periods in recoverable edge cases.

Incident review is the final step. After an event, the team needs the bag or logs, the robot build and config version, the map or scene version, the operator context, and a trace of what changed. Then it needs to turn the incident into a reproducible test or a new alert rule. Observability is complete only when it feeds back into engineering and operations, not when it ends as a dashboard screenshot.

## Running Observability as an Operational Capability

The hardest part of observability is not choosing tools. It is deciding what the organization considers evidence. A robotics team needs conventions: log fields that are always present, metric names that do not drift by repo, trace points around critical callback chains, bagging policies that engineers and operators both understand, and an incident-review ritual that produces action items instead of folklore. This is why observability often sits close to platform engineering or SRE rather than inside one autonomy team. Someone has to define the common language.

When that language is good, fleet support gets faster. Developers can compare one robot against ten similar robots. Operations teams can tell the difference between a one-off Wi-Fi glitch and a systemic QoS regression. Managers can see whether a new release improved route completion or only moved the failures to a different layer. This page exists to make that capability explicit. A deployable robot is useful. A robot fleet you can actually see, debug, and improve is a business.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Observability in robotics is what lets a team operate machines across buildings, customers, or cities without turning every support event into a site visit. In a single robot demo, an engineer can watch RViz, print debug output, and re-run the stack locally. In a fleet, that breaks immediately. The team needs remote evidence that explains whether the problem is a map issue, a battery issue, a compute issue, a middleware issue, or an environment issue. That evidence usually comes from structured logs, scraped health metrics, trace instrumentation for timing-sensitive paths, and recorded bags that can be pulled on demand for the robots that actually misbehaved.

What makes robotics observability distinct from web-style observability is the amount of multimodal state involved. You are not only watching request latency. You are watching camera timing, LiDAR throughput, TF age, navigation confidence, controller lag, mission state, and battery behavior, often across flaky wireless links. This is why the tooling stack matters but the data model matters even more. A useful robotics telemetry system is one where you can correlate “the robot hesitated at 14:32” with a bag segment, a planner timeout, a QoS drop spike, a Wi-Fi RSSI dip, and a version change on the localization node.

### Industry Tool Stack

- `ros2_tracing` and `LTTng` — used for low-overhead tracing of callback execution, executor behavior, and message-flow latency across ROS 2 nodes.
- `Prometheus node_exporter` — used to collect CPU, memory, disk, and host-level metrics from robot computers and edge gateways.
- `custom ROS 2 exporters` — used to expose topic rates, QoS deadline misses, localization-health metrics, and planner timing as scrapeable metrics.
- `Grafana` — used to build operational dashboards for fleet health, mission success, battery drift, and subsystem-specific timing trends.
- `InfluxDB` — used when high-cardinality robotics time-series data or per-mission tagging makes a TSDB workflow more useful than pure Prometheus retention.
- `ros2 bag` with `MCAP` — used for efficient local recording, selective capture, replay, and frozen-stack debugging after a field incident.
- `Foxglove Studio / Foxglove Data Platform` — used for live and recorded robot-data visualization, cross-robot search, and multimodal debugging.
- `Formant`, `InOrbit`, `Freedom Robotics` — used for fleet operations, remote diagnostics, event review, and per-robot history in deployed fleets.
- `OpenTelemetry` — used where teams need trace IDs and distributed-event correlation outside pure ROS boundaries.

### Step-by-Step Applied Workflow

1. Define the operational questions first: navigation regressions, compute saturation, localization drift, mission failure clustering, or actuator anomalies. Instrumentation should answer those, not generic curiosity.
2. Add structured logging to critical nodes with stable fields such as robot ID, mission ID, software version, map version, and subsystem name so logs are searchable across the fleet.
3. Export a small, high-value metrics set from each robot: compute headroom, bag recorder status, topic rates, key QoS violations, localization confidence, battery state, and mission state.
4. Trace the most latency-sensitive chains, such as perception-to-actuation or planner-to-controller, using `ros2_tracing`, LTTng, or an equivalent timing strategy rather than inferring latency from intuition.
5. Define a bagging policy: always-on topics, event-triggered high-rate topics, retention duration, upload policy, and how to freeze a bag against the exact software version that produced it.
6. Build dashboards for operators and separate deeper dashboards for engineers; the operational view should emphasize actionable health signals, not every internal metric.
7. Alert only on persistent or mission-impacting signals such as sustained SLAM divergence, repeated QoS misses, or unusual battery behavior, not on self-healed process restarts.
8. After every significant incident, pull the bag and logs, reproduce the issue if possible, and convert the finding into either a new regression test, a new alert, or a changed operating procedure.

### AI Integration

AI fits this topic around summarization, anomaly detection, and triage rather than as the core observability mechanism. Large models can summarize a long flight or mission log into a first-pass narrative, cluster similar incidents across a fleet, and suggest which metrics or traces best explain a failure pattern. Time-series anomaly detection can also help identify robots that are drifting away from fleet norms in battery behavior, planner timing, or perception latency. This is especially useful when the fleet is large enough that operators cannot visually inspect trend charts for every machine.

The limit is that observability still depends on structured signals. If the team does not record the right metrics, version tags, traces, or bag slices, AI has very little trustworthy material to work with. On this page, the adjacent AI role is therefore “amplify the evidence that already exists.” It is not a substitute for correct instrumentation, stable naming, or disciplined incident review. A good robotics observability stack becomes more useful with AI, but only after the engineers have made the system observable in plain deterministic terms.

### Case Studies

Foxglove is a strong benchmark because it focuses directly on multimodal robotics data rather than generic software logs, and because its tooling makes live plus recorded robot data searchable and explainable. Formant and InOrbit are also useful references because they are explicitly built around deployed robot fleets and the operational questions those fleets create. On the open-source side, Open Robotics matters here because `rosbag2` and `ros2_tracing` are foundational pieces of the practical debugging and tracing workflow that many robotics teams build on top of.

### Failure Modes & Safety

Bad observability creates blind robots in an organizational sense. The robot may still move, but the team cannot explain why it failed or whether the same failure is spreading. A common failure mode is recording too little: only nominal logs, no timing traces, and no bag when the issue is rare. The opposite failure also exists: recording everything at such a high rate that the robot fills its disk, burns CPU on telemetry, or floods the network with data no one can analyze. Another common trap is alert fatigue. Teams wire alerts to every node restart, every transient sensor timeout, and every log error, then learn to ignore the system when real problems appear.

Safety matters because some robotics failures degrade gradually before they become physically risky. SLAM divergence, stale transforms, battery sag, and rising control latency may all show up in telemetry before a near-collision or stuck event occurs. If the team cannot see those signals, the robot’s operational risk is effectively higher even if the controller code is unchanged. Good observability therefore acts as a safety amplifier: it helps teams intervene earlier and with more confidence.

### Business & Commercial Layer

This capability is close to operating cost. Fleet observability reduces truck rolls, shortens mean time to repair, and makes remote support viable. For AMRs in warehouses, hospitals, or retail, that means fewer site visits and fewer unresolved “the robot felt weird” reports. For service-robot companies, it means the support team can compare one incident against fleet baselines and decide whether the problem is environmental, mechanical, or software. For robotics startups, it also means new releases can be evaluated against real mission outcomes instead of hope. That is a direct margin effect.

In India, this skill is increasingly relevant to warehouse automation, service robotics, field robots, and robotics operations teams that support distributed deployments with limited on-site engineering coverage. In the US and Europe, it maps to AMR fleets, hospital robots, logistics robots, inspection fleets, and consumer robotics telemetry backends. Remote work is especially strong here because much of the job is data systems, platform design, incident review, and fleet analytics. Commercially, this page is about turning one robot into an operable product line.

### Hiring Signal

Job titles that match this page:

- Robotics Platform Engineer
- Fleet Operations Engineer
- Robotics SRE / DevOps Engineer
- Observability Engineer (Robotics)
- Technical Operations Engineer

Specific interview screens:

1. Design a telemetry schema for a mobile-robot fleet and explain which fields belong in structured logs, which belong in metrics, and which require tracing.
2. Given a robot incident with intermittent navigation hesitation, describe how you would use metrics, traces, and bags to distinguish Wi-Fi issues from planner latency.
3. Build an alert strategy for a fleet of AMRs and explain which signals should page operators immediately versus which should only create review tickets.
4. Explain how you would record rosbag data on a bandwidth-constrained robot without filling the disk or losing the evidence needed for replay.
5. Review a release rollout and describe how you would compare the new version against the old one using fleet telemetry instead of anecdotal operator feedback.

### Portfolio Projects

Beginner: `robot-observability-starter`
Deliverables: structured logging wrapper, one Prometheus exporter, one Grafana dashboard, one MCAP replay example.
Suggested repo tree:

```text
robot-observability-starter/
├── logging/
├── metrics/
├── dashboards/
├── bags/
└── README.md
```

Acceptance criteria:

- the project clearly separates logs, metrics, and replay artifacts
- one dashboard is tied to a concrete robot-health question
- a bag can be replayed against a documented stack version

Intermediate: `fleet-diagnostics-loop`
Deliverables: per-robot metrics pipeline, event-triggered bagging policy, incident-review template, latency trace for one critical path.
Suggested repo tree:

```text
fleet-diagnostics-loop/
├── exporters/
├── tracing/
├── incident_reviews/
├── retention_policy/
└── README.md
```

Acceptance criteria:

- at least one perception-to-actuation or planner-to-controller chain is traced
- the bagging policy includes retention and trigger rules
- one incident review produces a concrete engineering action item

Advanced: `robot-fleet-ops-platform-blueprint`
Deliverables: edge-to-cloud architecture, per-robot telemetry schema, alert rules, dashboard set, release-comparison playbook.
Suggested repo tree:

```text
robot-fleet-ops-platform-blueprint/
├── architecture/
├── schemas/
├── dashboards/
├── alerts/
├── release_analysis/
└── README.md
```

Acceptance criteria:

- the design supports both local recording and selective remote retrieval
- alerts are prioritized by mission impact rather than signal count
- another engineer could review the blueprint as the basis for a real fleet-ops system

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: more robotics teams are treating observability as platform infrastructure rather than as scattered debug scripts owned by individual autonomy teams.
- `2030`: fleet telemetry, bag indexing, and release evaluation will likely become much more automated, with stronger cross-robot regression detection after every deployment.
- `2035`: robotics observability will probably converge further with edge-cloud data systems, but multimodal replay and time-synchronized traces will remain distinctive requirements.
- `2045`: high-autonomy fleets will still need logs, metrics, traces, and replay, even if AI helps summarize them, because physical incidents still require auditable evidence and deterministic debugging.

### Interview Questions

1. Why are logs, metrics, and traces not interchangeable?
   Short answer: because logs explain discrete events, metrics summarize health over time, and traces reveal where latency and blocking appear through distributed execution paths.
2. Why is rosbag replay still important when you already have dashboards?
   Short answer: because dashboards summarize the system, while replay lets engineers reproduce the full sequence of sensor and control inputs against a frozen stack.
3. What makes a bad alert rule in robotics?
   Short answer: it fires on noisy but self-healing events and trains operators to ignore the observability system.
4. Why is selective recording necessary on robots?
   Short answer: because storage, compute, and bandwidth are limited, and recording everything continuously often harms the system without improving debugging proportionally.
5. How do you know observability is working?
   Short answer: when the team can explain incidents faster, reproduce regressions with evidence, and compare release impact across the fleet instead of relying on anecdotes.

### Further Depth

- `ros2_tracing` documentation
- `rosbag2` and MCAP documentation
- Foxglove documentation
- Formant developer and product materials
- InOrbit documentation
- OpenTelemetry documentation
- `Site Reliability Engineering` for operations principles adapted to physical systems
