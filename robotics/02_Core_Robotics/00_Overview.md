# Core Robotics

## Overview

Core Robotics is the structural center of the curriculum. This section explains how robot software behaves when planning, sensing, control, and physical constraints become real. If Foundation teaches you how to set up a robotics workspace, Core Robotics teaches you how to assemble a working robotics stack.

These subjects are tightly connected. ROS 2 architecture affects debugging and deployment. Simulation feeds navigation and control. Perception informs planning. Control abstractions determine how software reaches hardware. Algorithmic robotics provides the classical reasoning behind many practical stacks.

## What This Section Covers

### 1. Robotics Software Architecture
ROS 2 graph design, communication patterns, and system decomposition.

### 2. Navigation and Mobile Robotics
Localization, mapping, costmaps, planners, controllers, and Nav2.

### 3. Manipulation and Motion Planning
MoveIt 2, kinematics, collision checking, planning scenes, and pick-and-place.

### 4. Control and Hardware Interfaces
ros2_control, hardware abstractions, controllers, and actuator integration.

### 5. Perception and Robot Vision
Calibration, features, camera geometry, fiducials, and practical perception loops.

### 6. Robotics Algorithms
Planning, localization, SLAM, tracking, and control through PythonRobotics and notebook-first learning.

## Study Advice

- do not study these as isolated silos
- keep using simulation while reading
- tie every topic to one small system you can launch and inspect

## Exit Criteria

You are ready for Advanced when you can:

- explain how a mobile or manipulation stack is structured
- integrate ROS 2, simulation, control, and one planning or perception subsystem
- debug frame, controller, or message-flow failures methodically

## Next Step

Start with [ROS 2 Nodes Topics Services Actions and QoS](01_Robotics_Software_Architecture/01_ROS_2_Nodes_Topics_Services_Actions_and_QoS.md).


<!-- FULL_TOPIC_EXPANSION_START -->
## Why This Topic Matters

This is the layer where robotics becomes an engineering system instead of a set of disconnected demos.

## Real-World Context / Industry Relevance

Core Robotics maps directly to daily work on AMRs, manipulation stacks, autonomy pipelines, and robot platform integration.

## History / Evolution of the Topic

The open-source robotics ecosystem matured enough that navigation, manipulation, control, and perception now have reusable production-grade building blocks.

## Core Terminology

- `Stack`: A group of coordinated software components solving a robotics problem.
- `Planner`: A component that decides paths or trajectories.
- `Controller`: A component that drives behavior toward a desired target.
- `Estimator`: A component that infers state from noisy measurements.

## Mental Model / Big Picture

```text
architecture + control + perception + planning -> working robot behavior
```

## Main Concepts / Core Concepts

This page already contains the primary concept material above. The appended sections below extend it into industry and implementation context.

## Subtopics Breakdown

- architecture
- navigation
- manipulation
- control
- perception
- algorithms

## Architecture / Components / Building Blocks

- middleware
- simulator
- planners
- controllers
- sensors

## Process Flow / Lifecycle

```text
model system -> integrate subsystem -> test -> observe -> tune
```

## Practical / Design / Operational Sections

Treat Core Robotics as the layer where system decomposition and interface quality become visible.

## Step-by-Step Implementation Guide

1. Choose one robot class
1. Build one subsystem at a time
1. Keep launch, config, and verification commands documented

## Hands-On Example / Mini Project

Build a mobile robot stack that combines simulation, localization, navigation, and logging.

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

A robotics team succeeds because middleware, controllers, and planners are modular and inspectable.

### Case Study 2 / Real Scenario

A robotics team struggles because architecture drift makes it impossible to isolate failures between perception, planning, and control.

## Best Practices

- keep subsystem boundaries explicit
- tune with data, not guesses
- document runtime assumptions

## Performance / Optimization Considerations

Latency, controller frequency, sensor rates, and compute budgets all start to matter strongly here.

## Security / Reliability Considerations

Incorrect assumptions about state, timing, or interfaces create reliability failures that look like “random robot behavior.”

## Scalability Considerations

The same principles become more important as robots, maps, environments, and team size grow.

## Common Pitfalls

- tuning without logging
- no architecture diagram
- weak controller and frame understanding

## Debugging / Troubleshooting Guide

- isolate the failing layer first
- verify inputs before touching algorithms
- compare expected state with observed state

## Common Misconceptions

- the planner is the whole system
- perception quality alone solves autonomy
- control abstractions are optional

## Tradeoffs / Decision Frameworks

The main trade-offs are modularity versus complexity, fidelity versus speed, and flexibility versus maintainability.

## Metrics / KPIs / What to Measure

- task success rate
- localization accuracy
- controller stability
- debugging time

## Tools Commonly Used Around This Topic

- `Nav2`
- `MoveIt 2`
- `ros2_control`
- `OpenCV`
- `PythonRobotics`

## Ecosystem / Platforms / Vendors

- Open Robotics
- PickNik
- ROS-Industrial

## Automation Opportunities

Integration tests, simulation smoke tests, parameter sweeps, and bag replay regression testing are valuable here.

## AI Impact on This Topic

AI can assist with code and planning experiments, but system integration still determines whether the robot works.

## Recommended Resources

Use the official docs for each stack plus notebook-style algorithm references for deeper understanding.

## Practice Exercises

- sketch a full mobile robot stack
- compare classical planning and plugin-based Nav2 planning
- explain where controller tuning ends and architecture fixes begin
-->
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Core Robotics is where a robotics engineer stops building tutorial fragments and starts assembling systems that can survive integration pressure. In industry, this tier looks like the first time you own a real subsystem boundary. You are no longer only setting up a workspace or loading a simulator. You are deciding how localization feeds navigation, how controllers consume planned trajectories, how perception publishes target information, how a manipulator scene stays synchronized, and how logs, parameters, and launch files make the whole stack observable. This layer is the backbone of AMRs, industrial manipulators, inspection robots, and many service robots.

The page matters because most robotics hiring happens in this zone. Companies need people who can reason about message flow, latency, transforms, controller timing, map handling, collision checking, and sensor interpretation together. Core Robotics is also where subsystem errors start to look deceptively similar. A robot missing goals may have a planner issue, a localization issue, a controller issue, or a frame issue. An arm failing a pick may have a perception problem, a kinematics mismatch, a planning-scene problem, or a gripper interface problem. This tier teaches the habit of isolating layers, validating assumptions, and integrating with evidence instead of intuition. That is the step from “I know the tools” to “I can own behavior.”

### Industry Tool Stack

- `ROS 2`: used to structure the graph, transport messages, and compose subsystem packages.
- `Nav2`: used for mobile robot localization, planning, control, and recovery behaviors.
- `MoveIt 2`: used for kinematics, motion planning, planning scenes, and pick-and-place pipelines.
- `ros2_control`: used to present actuators and sensors through reusable controller interfaces.
- `OpenCV`: used for calibration, fiducials, detection pipelines, and pose-estimation support.
- `PythonRobotics`: used to understand classical planning, localization, and control algorithms at a smaller scale.
- `Gazebo` and `rviz2`: used to observe whole-system behavior while tuning or debugging.
- `rosbag2`: used to capture evidence when the system fails intermittently or under load.

### Step-by-Step Applied Workflow

1. Choose one robot problem, such as indoor AMR navigation or tabletop pick-and-place, and draw the full subsystem graph first.
2. Verify the shared prerequisites: robot description, frames, launch, simulator, and package boundaries must already be stable.
3. Bring up one core subsystem at a time, beginning with the one that produces the most trusted state, such as odometry or joint states.
4. Add the next dependent layer, such as localization over odometry or planning over current scene state, and inspect every interface in between.
5. Record logs and bags while the system is still small so later regressions have a baseline.
6. Introduce failure scenarios deliberately, such as stale transforms, blocked goals, sensor dropout, or obstacle inflation changes, and study the system response.
7. Document one architecture diagram and one runtime debugging checklist per subsystem, not just code.
8. Promote the stack toward Advanced only when you can explain the failure boundaries of each layer clearly.

### AI Integration

AI is useful in Core Robotics when it is attached to real system boundaries. It can summarize bag runs, propose parameter sweeps, classify repeated failure patterns, generate test scenarios, or speed up implementation of wrappers around classical stacks. Perception nodes may use learned detectors; task planners may use language models to produce high-level goals; anomaly detectors may watch navigation or controller metrics. But Core Robotics is still fundamentally about making those components behave inside a bounded, observable robot system.

That means AI does not replace the hard parts of this tier. It does not remove the need to understand controller frequencies, transform consistency, costmap semantics, collision objects, or hardware abstractions. In fact, the more learned components you add, the more important this tier becomes, because the system around the model has to expose timing, confidence, safe fallbacks, and recoverable failure states. A candidate who can integrate AI inside these classical boundaries is more valuable than one who can only produce an isolated demo.

### Case Studies

This tier aligns closely with how real robotics ecosystems are organized. Nav2 shows the mobile robotics side: localization, planners, controllers, behavior trees, and recoveries composed as a reusable stack. PickNik’s MoveIt tools show the manipulation side, where kinematics, collision scenes, and execution need strong interface discipline. ROS-Industrial training reflects the deployment side, where control abstractions, workcell integration, and reproducibility matter more than flashy demos. Together, they capture the system character of Core Robotics.

### Failure Modes & Safety

Core failures are multi-layer failures. A robot may oscillate near a goal because the controller is badly tuned, because localization jumps, because the local costmap is noisy, or because the transform chain is late. A manipulator may fail to reach because the target frame is wrong, because the planning scene is stale, because the end effector is mis-modeled, or because the controller cannot track the commanded trajectory. Another common risk is tuning by intuition: changing several parameters at once until the behavior “looks better” without knowing which assumption was corrected. That produces systems no one can maintain.

Safety at this tier is about bounded integration. Each layer should fail in a way another layer can detect. Controllers should expose limits. Navigation stacks should have recovery behavior instead of deadlock. Manipulation stacks should keep collision objects truthful. Perception inputs should carry timestamps and frames that the rest of the system can validate. When those rules are weak, robots act unpredictably and debugging becomes too slow for safe field work.

### Business & Commercial Layer

Core Robotics is where companies convert open-source ingredients into product behavior. A warehouse AMR vendor monetizes navigation, safety behavior, fleet coordination, and uptime; this tier underpins those features. A manipulation integrator monetizes cycle time, reliable picks, and safe cell behavior; this tier is where motion planning, control, and vision actually meet. A robotics services firm monetizes integration and deployment speed; again, this tier determines how quickly a system can be adapted, debugged, and stabilized.

For India, this tier maps strongly to industrial automation, warehouse robotics, inspection systems, and integration-heavy roles where cross-subsystem fluency is scarce. In the US and Europe, it maps to product companies in AMRs, manipulation, autonomy infrastructure, and logistics robotics. For remote roles, this tier is still viable if your work is well documented: bag captures, launch files, architecture notes, videos tied to logs, and parameter reviews. Commercially, this is the layer where the robot starts to earn or lose money.

### Hiring Signal

Job titles that hire strongly on this tier:

- Robotics Software Engineer
- Navigation Engineer
- Manipulation Engineer
- Robotics Integration Engineer
- Autonomy Systems Engineer

Interview screens that map to this page:

- decompose a robot failure into perception, state estimation, planning, control, and hardware interface hypotheses
- review a subsystem diagram and identify the weakest interface contract
- explain how you would capture evidence before tuning a controller or planner
- compare the structure of a mobile robot stack versus a pick-and-place stack and identify shared patterns
- read a rosbag-based incident summary and propose the next debugging step

### Portfolio Projects

Beginner: `core-robotics-stack-map`
Deliverables: system diagram, one runnable subsystem demo, one failure-analysis note, one tool matrix.
Suggested repo structure:

```text
core-robotics-stack-map/
├── docs/
├── demos/
├── diagrams/
└── README.md
```

Acceptance criteria:

- the repo explains the relationship between at least four core subsystems
- one runnable demo is tied to a documented graph or diagram
- one failure case is analyzed with evidence rather than guesswork

Intermediate: `mobile-or-manipulation-core`
Deliverables: one integrated stack, bag captures, parameter files, subsystem ownership notes.
Suggested repo structure:

```text
mobile-or-manipulation-core/
├── src/
├── launch/
├── config/
├── bags/
└── docs/
```

Acceptance criteria:

- the stack includes at least three interacting core layers
- logs or bags are used to justify one tuning decision
- the docs explain where the current system is still fragile

Advanced: `core-robotics-integration-handbook`
Deliverables: reusable integration checklist, simulator scenarios, architecture reviews, and one near-production repo skeleton.
Suggested repo structure:

```text
core-robotics-integration-handbook/
├── stack/
├── scenarios/
├── checklists/
├── reviews/
└── README.md
```

Acceptance criteria:

- the handbook can be applied to more than one robot class
- the repo separates assumptions by subsystem rather than hiding them in one narrative
- a reviewer can tell what would be needed to promote the stack into deployment work

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: employers still need engineers who can integrate classical robotics subsystems cleanly; this remains more scarce than tutorial-level familiarity.
- `2030`: more systems will combine classical stacks with learned perception and planning components, increasing the need for strong subsystem contracts.
- `2035`: fleet-level observability, digital twins, and safety monitoring will pull Core Robotics closer to platform engineering and operations.
- `2045`: robots will likely use more learned behavior, but state estimation, control interfaces, and bounded execution layers will still anchor the system.

### Interview Questions

1. Why is Core Robotics the “structural center” of a curriculum?
   Short answer: because it is where sensing, planning, control, and software architecture first have to work together as one system.
2. What is a common mistake when tuning a robot stack?
   Short answer: changing multiple layers at once without isolating which assumption is wrong.
3. Why are bags and diagrams important at this tier?
   Short answer: because they turn integration problems into inspectable evidence rather than subjective impressions.
4. What shared pattern exists between navigation and manipulation stacks?
   Short answer: both depend on trustworthy state, clean interfaces, bounded planning, and executable control.
5. What does it mean to “own behavior” in robotics?
   Short answer: to explain the system path from inputs to motion and to diagnose failures methodically across layers.

### Further Depth

- Nav2 documentation
- MoveIt documentation
- ROS-Industrial training materials
- `Modern Robotics` by Kevin Lynch and Frank Park
- `Underactuated Robotics` by Russ Tedrake
