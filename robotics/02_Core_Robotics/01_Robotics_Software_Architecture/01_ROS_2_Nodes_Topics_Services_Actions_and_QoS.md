# ROS 2 Nodes Topics Services Actions and QoS

## Overview

This page focuses on the architecture choices inside a ROS 2 system. The concepts are simple in isolation, but most real robotics quality comes from using them correctly together. The goal is not just to know the terms. The goal is to choose the right communication pattern, define clean node boundaries, and avoid graphs that become impossible to debug.

## Why This Topic Matters

Many robotics bugs are architecture bugs disguised as algorithm bugs. Bad node boundaries, wrong communication choices, or sloppy QoS settings create latency, dropped data, startup problems, and brittle behavior.

## Core Concepts

### Nodes
- keep responsibilities narrow
- separate perception, planning, control, logging, and UI where useful

### Topics
- ideal for sensor streams, odometry, telemetry, and event distribution

### Services
- ideal for quick commands or state queries
- avoid for long-running behavior

### Actions
- ideal for navigation goals, manipulation tasks, and cancellation-aware workflows

### QoS
- sensor data often needs different behavior from reliable command channels
- history depth, reliability, and durability settings matter

## Decision Framework

```text
continuous data -> topic
short request/response -> service
long-running goal with feedback -> action
runtime structure + failure behavior -> QoS choice
```

## Hands-On Example / Mini Project

Refactor one messy robot demo into:

- a sensor publisher node
- a localization consumer node
- a goal action server
- a status service
- explicit QoS settings for each path

## Next Step

Continue to [Localization SLAM and Nav2](../02_Navigation_and_Mobile_Robotics/01_Localization_SLAM_and_Nav2.md).


<!-- FULL_TOPIC_EXPANSION_START -->
## Real-World Context / Industry Relevance

This is daily architecture work in most ROS 2 codebases.

## History / Evolution of the Topic

ROS 2 pushed communication design closer to distributed-system thinking because QoS and DDS behavior became explicit.

## Core Terminology

- `Reliability`: Whether delivery should favor guaranteed receipt or best effort.
- `Durability`: Whether late joiners should receive earlier published data.
- `History`: How much prior message data is buffered.
- `Lifecycle`: Managed state transitions for nodes that need controlled startup and shutdown.

## Mental Model / Big Picture

```text
good communication choices -> clearer graphs -> more reliable robot behavior
```

## Main Concepts / Core Concepts

This page already contains the primary concept material above. The appended sections below extend it into industry and implementation context.

## Subtopics Breakdown

- node boundaries
- messaging choice
- QoS choice
- lifecycle management

## Architecture / Components / Building Blocks

- publishers
- subscribers
- servers
- clients
- action interfaces

## Process Flow / Lifecycle

```text
define responsibilities -> choose interface -> configure QoS -> test failure cases
```

## Practical / Design / Operational Sections

Design the runtime graph before you optimize implementation details.

## Step-by-Step Implementation Guide

1. Draw the graph
1. Classify each edge as topic, service, or action
1. Test startup and restart behavior

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

An AMR stack uses actions for goals, topics for sensors, and services for resets, making the graph understandable.

### Case Study 2 / Real Scenario

A manipulation stack overloads services for long tasks, causing blocking behavior and poor cancellation handling.

## Best Practices

- keep interfaces explicit
- document QoS rationale
- separate command paths from telemetry paths

## Performance / Optimization Considerations

Incorrect QoS settings can silently waste bandwidth or drop data.

## Security / Reliability Considerations

Startup ordering and message compatibility affect operational reliability.

## Scalability Considerations

Large robots and multi-robot fleets need naming, namespacing, and graph discipline.

## Common Pitfalls

- one giant node
- default QoS everywhere
- no graph documentation

## Debugging / Troubleshooting Guide

- inspect topic compatibility
- verify action servers are available before sending goals
- compare expected and actual QoS

## Common Misconceptions

- services are simpler, so use them more
- actions are only for advanced systems
- QoS does not matter on localhost

## Tradeoffs / Decision Frameworks

The main trade-offs are simplicity versus operational correctness and flexibility versus graph clarity.

## Metrics / KPIs / What to Measure

- message loss
- action completion reliability
- graph readability
- restart behavior

## Tools Commonly Used Around This Topic

- `ros2 topic info`
- `ros2 action list`
- `rqt_graph`

## Ecosystem / Platforms / Vendors

- ROS 2
- DDS vendors

## Automation Opportunities

Graph smoke tests and launch-time interface validation are high-value automation points.

## AI Impact on This Topic

AI can propose interfaces quickly, but it often underestimates operational failure modes unless you verify them.

## Recommended Resources

Use ROS 2 concepts docs and tutorials, then validate with your own runtime graph.

## Practice Exercises

- replace one service with an action and explain why
- tune QoS for a lidar topic
- draw a graph for a small AMR stack
-->
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

This page is where ROS 2 becomes architecture rather than terminology. In a real robot program, node boundaries determine who owns logic, how failures are isolated, and whether the graph remains understandable after six months of feature growth. A perception node may publish detections, a tracker may fuse them, a planner may consume the result, and a controller may execute a bounded command. If those responsibilities are collapsed into one giant process, debugging becomes slower and reuse gets harder. If they are split without discipline, the graph becomes chatty and fragile. Good architecture sits between those extremes.

Communication choice is equally operational. Topics are appropriate for continuous streams such as point clouds, odometry, and status. Services fit quick queries or resets. Actions fit goal-driven tasks such as navigation or pick-and-place where feedback, timeout, and cancellation matter. QoS is the runtime contract over these edges. Engineers choose best effort for high-rate sensors when stale data is worse than dropped packets, reliable delivery for commands or sparse state updates, and durability for configuration-like data that late joiners need. This page therefore maps directly to the day-to-day architecture reviews that decide whether a robot remains maintainable under scale, network noise, and team growth.

### Industry Tool Stack

- `rclcpp` and `rclpy`: used to implement well-bounded nodes and communication endpoints.
- `ros2 topic info --verbose`: used to inspect topic types, publishers, subscribers, and QoS compatibility.
- `rqt_graph` and `ros2 node list`: used to inspect whether runtime decomposition matches the intended architecture.
- `launch_ros`: used to group nodes, parameters, namespaces, and remappings into reproducible application bring-up.
- `LifecycleNode`: used when startup order, configuration, and controlled activation matter.
- `Fast DDS` or `Cyclone DDS`: used as the underlying transport whose behavior informs QoS tuning.
- `rosbag2`: used to replay message flows and expose architecture issues under repeatable conditions.
- `SROS2`: used when communication security and certificate-based access control become relevant.

### Step-by-Step Applied Workflow

1. Start by drawing the robot graph on paper, listing each responsibility such as sensing, estimation, planning, control, diagnostics, and UI.
2. Decide which responsibilities should be separate nodes based on failure isolation, computational load, team ownership, and reuse potential.
3. For each connection, choose topic, service, or action based on data rate, interaction duration, feedback needs, and cancellation behavior.
4. Assign explicit QoS profiles instead of defaults where behavior matters, especially for sensors, command channels, and startup state.
5. Launch the graph in a minimal scenario and inspect the live architecture using CLI tools and graph visualization rather than trusting the code structure alone.
6. Test restart and late-join behavior to see whether nodes recover correctly, stale state is handled properly, and hidden assumptions emerge.
7. Record one bag and replay it while checking whether architecture choices still hold under repeated evaluation.
8. Document the graph, QoS rationale, and failure boundaries so future contributors do not silently mutate the design.

### AI Integration

AI can help architecture work by generating candidate node decompositions, reviewing whether an interaction pattern is appropriate, and summarizing repeated graph diagnostics from bag replays or logs. It is also increasingly part of the architecture itself. A learned detector, semantic mapper, or language-conditioned planner often enters the ROS graph as a node or service layer. That makes architectural clarity more important, not less, because learned components need explicit timing, failure handling, and output contracts.

The risk is that AI suggestions often optimize for apparent simplicity instead of operational correctness. A model may suggest putting too much logic behind a service because it looks clean in pseudocode, ignoring cancellation, latency, and backpressure. It may also ignore QoS interactions under lossy links or executor contention under load. So the right use of AI on this page is as a design assistant around options and diagnostics, while the engineer remains responsible for runtime truth: rates, latency, reliability, and maintainability under actual robot behavior.

### Case Studies

Open Robotics provides the conceptual and tooling base for these architecture choices through ROS 2 design and CLI introspection tools. Nav2 offers a concrete example of separating planning, control, behavior-tree orchestration, and recovery logic into bounded components rather than one opaque “navigation node.” MoveIt 2 provides a similar lesson on the manipulation side, where planning, scene updates, and execution are distinct responsibilities with explicit interfaces.

### Failure Modes & Safety

Architecture mistakes create stubborn failures. One oversized node can hide too many responsibilities behind internal state, making logs ambiguous and failures hard to isolate. The opposite mistake is over-fragmentation, where tiny nodes produce excessive serialization, coordination complexity, and configuration sprawl. Services are commonly misused for long-running tasks; when that happens, a caller blocks, timeout behavior is unclear, and cancellation becomes awkward. QoS mistakes are more subtle: a local test may work because timing is favorable, then fail in the field when Wi-Fi drops packets or when a late-joining subscriber misses critical state because durability was not set.

Safety implications follow from visibility and bounded behavior. If command channels are not separated from telemetry, operators may struggle to tell what the robot is actually executing. If lifecycle and startup assumptions are implicit, a partial restart can leave the robot in an undefined state. If the graph is too opaque, a bad output from a learned module may flow downstream without proper gating. Safe robotics architecture is therefore architecture that other engineers can inspect, reason about, and recover under fault conditions.

### Business & Commercial Layer

Architecture quality affects velocity and support burden. A robotics startup with clean node boundaries can split work across teams, reuse subsystems across robot variants, and debug customer issues with lower effort. An integrator can isolate site-specific customization in parameters and launch files instead of forking the whole stack. A larger product company can support fleets longer because message contracts, node ownership, and QoS policies are explicit enough for new engineers to inherit. This is a real commercial lever, not an academic preference.

For India, this page maps well to robotics software, industrial automation, middleware integration, and autonomy teams that need system clarity more than novel algorithms. In the US and Europe, it is common across AMR vendors, manipulation platforms, and autonomy infrastructure companies. Remote roles value this skill because good architecture is inspectable through diagrams, launch files, interfaces, and debug notes. Commercially, a clean graph reduces rework, accelerates onboarding, and lowers field-debugging cost.

### Hiring Signal

Job titles that test this skill explicitly:

- ROS 2 Middleware Engineer
- Robotics Software Architect
- Robotics Integration Engineer
- Navigation Software Engineer
- Manipulation Software Engineer

Interview screens that expose weak architecture thinking:

- classify a set of robot interactions into topics, services, or actions and justify each choice
- diagnose a QoS incompatibility from a small graph description and expected runtime symptom
- refactor a monolithic node design into bounded components with named interfaces
- explain how lifecycle nodes improve startup and recovery for a subsystem that should not activate too early
- review a multi-robot naming scheme and identify where namespaces or remappings will break

### Portfolio Projects

Beginner: `ros2-architecture-lab`
Deliverables: graph diagram, small node set, one service, one action, one QoS note, launch file.
Suggested repo structure:

```text
ros2-architecture-lab/
├── src/
├── launch/
├── docs/
├── config/
└── README.md
```

Acceptance criteria:

- each interface choice is justified in writing
- the graph can be inspected with CLI tools and matches the diagram
- one QoS experiment is captured with observed behavior

Intermediate: `graph-refactor-demo`
Deliverables: refactor of a messy robot demo into bounded nodes, namespace-safe launch, bag replay evidence.
Suggested repo structure:

```text
graph-refactor-demo/
├── src/
├── launch/
├── bags/
├── docs/
└── tests/
```

Acceptance criteria:

- the refactor makes one failure easier to isolate than before
- restart behavior is tested and documented
- the repo demonstrates one command path and one telemetry path with different QoS assumptions

Advanced: `ros2-architecture-template`
Deliverables: reusable graph skeleton with lifecycle nodes, diagnostics, QoS profiles, and architecture review notes.
Suggested repo structure:

```text
ros2-architecture-template/
├── bringup/
├── interfaces/
├── src/
├── diagnostics/
└── docs/
```

Acceptance criteria:

- the template supports at least two subsystem classes without architecture collapse
- the docs include failure boundaries and startup assumptions
- another engineer can extend the graph without guessing naming and QoS conventions

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: ROS 2 architecture depth remains a strong hiring signal because many candidates know APIs but not runtime design.
- `2030`: mixed classical and learned robotics stacks will make graph-level observability and bounded interfaces even more important.
- `2035`: architecture work will increasingly include fleet-level telemetry, remote diagnostics, and stronger security around message transport.
- `2045`: regardless of middleware evolution, robots will still need explicit component boundaries, typed interfaces, and recoverable task execution.

### Interview Questions

1. When is a topic a bad choice?
   Short answer: when the interaction needs explicit completion, feedback, or cancellation rather than fire-and-forget streaming.
2. Why can default QoS be risky?
   Short answer: because the defaults may not match the timing and reliability needs of sensors, commands, or late-joining subscribers.
3. What is one sign a node boundary is wrong?
   Short answer: the node owns unrelated responsibilities and failures inside it are hard to isolate or test.
4. Why are lifecycle nodes useful?
   Short answer: they provide controlled configuration and activation so dependent systems do not start in an unsafe or undefined order.
5. What architecture problem often appears only after scale?
   Short answer: naming, remapping, and QoS assumptions that looked harmless in one robot break in multi-instance or lossy-network setups.

### Further Depth

- ROS 2 concepts documentation
- ROS 2 QoS documentation
- Nav2 architecture documentation
- MoveIt documentation
- `Designing Data-Intensive Applications` by Martin Kleppmann for distributed-systems intuition
