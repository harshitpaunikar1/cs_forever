# PX4 ROS 2 and Offboard Control

## Overview

PX4 is one of the main open-source autopilot ecosystems for drone robotics. Its ROS 2 integration path is strong for engineers who want to work on offboard control, mission logic, state estimation interfaces, and companion-computer architectures.

This topic matters because aerial robotics has its own constraints: strict safety expectations, coordinate-frame conventions, communication layers, and autopilot separation of responsibilities.

## Core Concepts

### PX4 + ROS 2 Architecture
- autopilot on flight controller
- ROS 2 app on companion computer
- middleware bridge between the two

### Offboard Control
- ROS 2 application sends commands or setpoints
- autopilot handles low-level stabilization

### State and Frame Conventions
- NED and ENU differences
- telemetry topics and control topics

## Mental Model / Big Picture

```text
ROS 2 companion app -> bridge middleware -> PX4 autopilot -> vehicle behavior
```

## Hands-On Example / Mini Project

Build a `ROS 2 autonomous drone prototype` with:

- PX4 SITL
- one waypoint mission node
- one short note on safety assumptions and frame conversions

## Recommended Resources

- [PX4 ROS 2 User Guide](https://docs.px4.io/main/en/ros2/user_guide)
- [PX4 ROS 2 overview](https://docs.px4.io/main/en/ros2)

## Next Step

Continue to [LeRobot Isaac Lab and Modern Robot Learning](../04_Robot_Learning_and_Embodied_AI/01_LeRobot_Isaac_Lab_and_Modern_Robot_Learning.md).


<!-- FULL_TOPIC_EXPANSION_START -->
## Why This Topic Matters

Drone robotics roles require a clean understanding of autonomy versus low-level flight control responsibilities.

## Real-World Context / Industry Relevance

This appears in inspection drones, mapping platforms, and field robotics with aerial autonomy requirements.

## History / Evolution of the Topic

ROS 2 integration improved aerial robotics by making companion-computer workflows more consistent with the wider robotics ecosystem.

## Core Terminology

- `Autopilot`: The flight-control system that stabilizes and manages vehicle state.
- `Offboard control`: External control logic that provides higher-level commands.
- `SITL`: Software in the loop simulation of the flight stack.
- `NED`: North-East-Down coordinate convention commonly used in autopilot systems.

## Mental Model / Big Picture

```text
companion computer handles autonomy logic while the autopilot protects core flight behavior
```

## Main Concepts / Core Concepts

This page already contains the primary concept material above. The appended sections below extend it into industry and implementation context.

## Subtopics Breakdown

- architecture
- offboard control
- frame conventions
- safety

## Architecture / Components / Building Blocks

- PX4
- ROS 2 node
- bridge middleware
- simulator

## Process Flow / Lifecycle

```text
launch SITL -> connect ROS 2 -> read telemetry -> send setpoints -> validate behavior
```

## Practical / Design / Operational Sections

Treat frame conversion and safety logic as first-class concerns.

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

An offboard mission node works because telemetry QoS, frame handling, and command timing are all understood.

### Case Study 2 / Real Scenario

A drone experiment fails because the engineer mixes ENU and NED assumptions and blames the controller.

## Best Practices

- start in SITL
- document frame conventions
- keep safety fallbacks explicit

## Performance / Optimization Considerations

Telemetry rate, command rate, and bridge latency affect control quality.

## Security / Reliability Considerations

Flight systems require more conservative validation than many ground-robot demos.

## Scalability Considerations

Multi-vehicle or higher-level mission systems increase coordination complexity quickly.

## Common Pitfalls

- ignoring NED versus ENU
- unsafe offboard assumptions
- weak SITL validation

## Debugging / Troubleshooting Guide

- verify telemetry first
- confirm QoS compatibility
- inspect frame conversions and command timestamps

## Common Misconceptions

- ROS 2 replaces the autopilot
- waypoint demos equal robust drone autonomy
- drone stacks behave like mobile robots with propellers

## Tradeoffs / Decision Frameworks

The main trade-offs are autonomy flexibility versus safety constraints and rapid experimentation versus conservative validation.

## Metrics / KPIs / What to Measure

- mission completion rate
- frame correctness
- command latency
- safety event frequency

## Tools Commonly Used Around This Topic

- `PX4 SITL`
- `ROS 2`
- `QGroundControl`

## Ecosystem / Platforms / Vendors

- PX4
- ROS 2
- drone simulation tools

## Automation Opportunities

SITL mission tests and telemetry validation are good automation targets.

## AI Impact on This Topic

AI can help with mission logic, but flight-critical systems still demand careful deterministic validation.

## Recommended Resources

Use official PX4 ROS 2 docs first.

## Practice Exercises

- run one SITL mission
- explain NED versus ENU in your own words
- describe which control loop belongs to PX4 and which to ROS 2
-->
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

This page is about respecting the division of labor in aerial robotics. PX4 runs the low-level flight stack: attitude stabilization, state estimation, failsafes, mode handling, and the inner control loops that keep an aircraft flyable. ROS 2 on a companion computer is where mission logic, perception, high-level planning, and offboard behaviors usually live. In production, engineers use this split to keep flight-critical behavior on the autopilot while still gaining the flexibility of a richer compute stack for mapping, inspection logic, perception, or mission orchestration.

Offboard control is powerful because it allows a ROS 2 application to send setpoints, trajectories, or higher-level commands into PX4. It is also where many beginners make dangerous assumptions. If you misunderstand frame conventions, heartbeat or setpoint timing, estimator state, or mode transitions, the vehicle can reject commands or leave offboard mode. Real aerial robotics engineering therefore revolves around interfaces, timing, and bounded responsibility: PX4 owns stabilization and safety; the companion computer proposes behavior within those boundaries. The skill on this page is knowing how to integrate autonomy with flight control without pretending autonomy replaces flight control.

### Industry Tool Stack

- `PX4 Autopilot`: used for core flight control, estimator integration, mode handling, and safety logic.
- `PX4 SITL`: used to validate companion-computer logic and offboard flows before hardware tests.
- `ROS 2`: used for high-level mission nodes, perception, telemetry consumers, and orchestration around the aircraft.
- `QGroundControl`: used to inspect vehicle state, parameters, modes, and mission behavior during testing.
- `MAVLink` and PX4 ROS interfaces: used for telemetry, mode management, and setpoint/control exchange.
- `Gazebo` or compatible simulators: used to create repeatable flight scenarios and sensor conditions.
- `rosbag2`: used to capture telemetry and setpoint flows for post-flight or post-simulation analysis.

### Step-by-Step Applied Workflow

1. Start in PX4 SITL and verify the autopilot itself is healthy before adding any ROS 2 offboard logic.
2. Confirm the frame conventions and message semantics for every setpoint and telemetry path, especially NED versus ENU assumptions.
3. Build a minimal ROS 2 offboard node that sends one bounded command type, such as position setpoints, rather than a full mission stack immediately.
4. Validate mode transitions, arm logic, and required setpoint streaming behavior so the vehicle enters and maintains offboard mode correctly.
5. Observe telemetry, estimator status, and setpoint timing together in SITL or logs instead of judging behavior from motion alone.
6. Add one higher-level behavior, such as waypoint sequencing or camera-triggered positioning, only after the basic control contract is stable.
7. Test loss cases deliberately: stale setpoints, frame mismatch, dropped links, and estimator degradation should have predictable outcomes.
8. Keep hardware tests conservative and tightly scoped because the goal is to validate the interface boundary, not to improvise autonomy in the field.

### AI Integration

AI enters aerial robotics primarily above the flight-control layer. Vision models can support landing-target detection, obstacle interpretation, infrastructure inspection, and semantic mission triggers. Planning layers can optimize route selection or classify points of interest from onboard imagery. But the aircraft still depends on tightly bounded setpoints, estimator trust, and mode safety. That means AI belongs on the companion side with explicit outputs and fallback rules, not buried inside the flight-critical control loop without strong verification.

For this page, the honest AI message is that offboard control is what makes higher-level intelligence practical, but it does not relax safety discipline. A learned detector that tells the drone where to inspect is useful. A learned module that is allowed to violate flight-mode assumptions or frame semantics is not. The companion application must convert AI outputs into conservative commands PX4 can manage safely.

### Case Studies

PX4 itself is the strongest public benchmark because its documentation and ecosystem make the autopilot-versus-companion boundary explicit. Auterion is also a relevant named example because it has built commercial workflows around PX4-based autonomy stacks and companion-computer integration. More broadly, inspection and mapping UAV companies illustrate the same pattern: keep the autopilot authoritative over flight safety while using higher-level compute for mission intelligence.

### Failure Modes & Safety

The classic failure on this page is frame confusion. A ROS 2 node assumes ENU while the autopilot interface expects NED, and the drone appears to move correctly in one axis while behaving dangerously in another. Another common issue is setpoint timing: offboard mode may drop because the companion computer does not sustain the required stream or because latency spikes under load. Estimator quality is another hidden dependency. A high-level controller can be perfectly coded and still fail because the underlying state estimate is poor or not ready for offboard behavior.

Safety is stricter in aerial robotics than in many ground-robot demos because flight leaves less room for graceful error. That is why SITL, bounded commands, explicit mode handling, and conservative test envelopes matter. A strong engineer treats offboard control as a contract with the autopilot, not a replacement for it. The autopilot should always know how to recover if the companion stops behaving.

### Business & Commercial Layer

This skill maps to inspection drones, mapping platforms, infrastructure monitoring, research UAVs, and some defense-adjacent or industrial autonomy roles. Companies pay for reliable offboard behaviors when those behaviors enable mission flexibility without rewriting the flight stack. A companion-computer engineer who can integrate ROS 2, perception, and mission logic with PX4 safely helps shorten prototype cycles and de-risk field tests. That is commercially valuable because aerial testing is expensive and risky.

In India, this page is relevant to drone startups, mapping and inspection services, agri-tech UAVs, and autonomy work around domestic UAV platforms. In the US and Europe, it maps to enterprise drones, inspection, survey, infrastructure, and advanced autonomy roles. Remote work is more feasible here than pure hardware bring-up if the engineer works heavily in SITL, logging, and mission logic. Commercially, this topic sits at the point where aerial intelligence becomes a product rather than just a piloted platform.

### Hiring Signal

Job titles that hire for this topic:

- UAV Autonomy Engineer
- Robotics Software Engineer (Aerial Systems)
- Drone Companion Computer Engineer
- Flight Software Integration Engineer
- Offboard Control Engineer

Interview screens that reveal real aerial-systems depth:

- explain the control boundary between PX4 and a ROS 2 offboard node for a given mission scenario
- debug a SITL run where mode transitions or setpoint timing cause offboard failure
- identify where an ENU versus NED mismatch would surface in telemetry and motion
- design a conservative validation sequence before moving from SITL to real flight
- explain what logs or telemetry you would capture after a failed offboard mission

### Portfolio Projects

Beginner: `px4-offboard-starter`
Deliverables: SITL setup, one offboard setpoint node, frame note, mission video, log review.
Suggested repo structure:

```text
px4-offboard-starter/
├── src/
├── sitl/
├── logs/
├── docs/
└── README.md
```

Acceptance criteria:

- one simple offboard behavior runs repeatably in SITL
- frame conventions and mode assumptions are documented
- one failure case is captured and explained

Intermediate: `uav-mission-and-telemetry-lab`
Deliverables: waypoint or task mission, telemetry analysis, recovery behavior note, QGroundControl workflow.
Suggested repo structure:

```text
uav-mission-and-telemetry-lab/
├── mission_nodes/
├── telemetry/
├── qgc_notes/
├── logs/
└── docs/
```

Acceptance criteria:

- the mission behavior is tied to telemetry evidence, not only video
- one estimator or mode-handling assumption is made explicit
- stale-link or dropped-setpoint behavior is tested in SITL

Advanced: `px4-ros2-autonomy-sandbox`
Deliverables: reusable offboard architecture, perception or task trigger, test scenarios, safety contract document.
Suggested repo structure:

```text
px4-ros2-autonomy-sandbox/
├── autonomy/
├── interfaces/
├── scenarios/
├── safety_contract/
└── README.md
```

Acceptance criteria:

- the repo clearly separates flight-critical and autonomy responsibilities
- one safety fallback path is described and tested
- another engineer could review the architecture for flight-readiness questions

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: PX4 plus companion-computer autonomy remains a practical entry path for aerial robotics roles.
- `2030`: more aerial systems will combine classical autopilot logic with richer onboard perception and mission reasoning.
- `2035`: multi-vehicle coordination, semantic mission planning, and edge AI payloads will increase the value of disciplined offboard interfaces.
- `2045`: even with more autonomous aerial behavior, strong separation between certified or trusted flight functions and high-level intelligence will likely remain important.

### Interview Questions

1. Why should PX4 keep low-level stabilization instead of delegating it to ROS 2?
   Short answer: because flight-critical control and safety require tighter guarantees and better-bounded behavior than a general companion stack should own.
2. Why is NED versus ENU such a common source of bugs?
   Short answer: because the vehicle may interpret correct-looking numeric commands in the wrong coordinate convention and move dangerously.
3. What causes offboard mode to drop unexpectedly?
   Short answer: stale or missing setpoints, bad mode sequencing, interface issues, or underlying estimator problems.
4. Why is SITL mandatory before flight?
   Short answer: because it lets you validate the interface contract, timing, and failure handling without risking hardware or airspace incidents.
5. What is one sign an autonomy node is taking too much responsibility?
   Short answer: it tries to own stabilization or ignore autopilot state and fail-safe behavior instead of operating within them.

### Further Depth

- PX4 ROS 2 documentation
- PX4 user guide
- MAVLink documentation
- QGroundControl documentation
- Auterion public developer materials
