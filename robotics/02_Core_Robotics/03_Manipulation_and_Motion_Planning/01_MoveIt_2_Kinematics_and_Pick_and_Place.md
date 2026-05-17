# MoveIt 2 Kinematics and Pick and Place

## Overview

Manipulation is the robotics path where kinematics, collision checking, motion planning, and task execution come together most clearly. MoveIt 2 is the main ROS 2 ecosystem stack for industrial and research manipulation workflows. It gives you planning scenes, robot models, interactive tooling, and programmatic APIs for motion planning.

This topic matters because many employable robotics roles involve arms, tooling, fixturing, pick-and-place, and collision-aware planning rather than only mobile navigation.

## Prerequisites

- ROS 2 basics
- URDF and tf2
- simulation workflow

## Core Concepts

### Kinematics
- forward kinematics
- inverse kinematics
- joint limits
- end-effector frames

### Planning Scene
- collision objects
- attached objects
- environment representation

### Motion Planning
- path generation under constraints
- joint-space and Cartesian workflows

### Pick and Place
- grasp pose
- approach and retreat
- object attachment and release

## Mental Model / Big Picture

```text
robot model + planning scene + IK + planner + execution interface -> manipulation workflow
```

## Step-by-Step Implementation Guide

1. Load a manipulator model into MoveIt 2.
1. Verify groups, joints, and end-effector frames.
1. Add obstacles to the planning scene.
1. Run interactive plans in RViz.
1. Move to programmatic planning in C++ or Python.
1. Build a simple pick-and-place sequence.

## Hands-On Example / Mini Project

Build a simulated `6-DOF` arm demo with:

- one planning scene
- one object pickup
- one placement target
- one C++ node that triggers the sequence

## Recommended Resources

- [MoveIt 2 Tutorials](https://moveit.picknik.ai/main/doc/tutorials/tutorials.html)
- [Modern Robotics](https://modernrobotics.northwestern.edu/)
- [MIT Robotic Manipulation](https://manipulation.csail.mit.edu/)

## Next Step

Continue to [ros2_control and Hardware Abstractions](../04_Control_and_Hardware_Interfaces/01_ros2_control_and_Hardware_Abstractions.md).


<!-- FULL_TOPIC_EXPANSION_START -->
## Why This Topic Matters

Manipulation work appears across industrial automation, warehousing, laboratories, service robotics, and embodied AI data collection.

## Real-World Context / Industry Relevance

MoveIt 2 is one of the main practical gateways into manipulation-focused robotics jobs.

## History / Evolution of the Topic

Manipulation stacks evolved from custom lab-specific pipelines toward more reusable scene-aware and ROS-integrated toolchains.

## Core Terminology

- `FK`: Forward kinematics, joint state to pose.
- `IK`: Inverse kinematics, desired pose to joint configuration.
- `Planning scene`: The scene representation used for collision-aware planning.
- `End effector`: The tool or gripper at the end of the arm.

## Mental Model / Big Picture

```text
know the arm geometry -> know the scene -> generate safe motion -> execute task
```

## Main Concepts / Core Concepts

This page already contains the primary concept material above. The appended sections below extend it into industry and implementation context.

## Subtopics Breakdown

- kinematics
- scene understanding
- planning
- task sequencing

## Architecture / Components / Building Blocks

- MoveIt config
- planning scene
- kinematics solver
- execution manager

## Process Flow / Lifecycle

```text
model arm -> configure MoveIt -> add scene -> plan -> execute -> refine
```

## Practical / Design / Operational Sections

Test manipulation in simulation before hardware, especially around collision objects and frame definitions.

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

An industrial cell succeeds because grasp frames, planning groups, and obstacles are modeled explicitly.

### Case Study 2 / Real Scenario

A demo fails because tool frames are inconsistent and collision geometry was never validated.

## Best Practices

- validate end-effector frames
- keep planning scenes explicit
- test approach and retreat paths separately

## Performance / Optimization Considerations

IK solver choice, planning time limits, and scene complexity affect responsiveness.

## Security / Reliability Considerations

Collision assumptions and execution timing matter strongly for safety.

## Scalability Considerations

Multiple tools, fixtures, and arms increase scene and orchestration complexity quickly.

## Common Pitfalls

- wrong tool frame
- planning with incomplete collision geometry
- no distinction between demo path and robust task flow

## Debugging / Troubleshooting Guide

- inspect planning groups
- visualize collision objects
- verify grasp pose and frame transforms

## Common Misconceptions

- MoveIt 2 solves manipulation automatically
- good IK alone means good task performance
- pick-and-place is only about motion planning

## Tradeoffs / Decision Frameworks

The main trade-offs are planner flexibility versus predictability and scene fidelity versus workflow simplicity.

## Metrics / KPIs / What to Measure

- plan success rate
- collision-free execution rate
- pick success rate
- cycle time

## Tools Commonly Used Around This Topic

- `MoveIt 2`
- `RViz`
- `ros2_control`

## Ecosystem / Platforms / Vendors

- PickNik
- ROS-Industrial
- Open Robotics

## Automation Opportunities

Planning scene regression tests and scripted pick-place sequences are high-value automation.

## AI Impact on This Topic

AI can help generate task-level ideas, but geometric and collision-aware correctness still dominate.

## Recommended Resources

Use MoveIt 2 tutorials as the direct path and Modern Robotics or MIT notes as the theory layer.

## Practice Exercises

- derive FK/IK for a simple arm
- add one obstacle and compare the resulting plan
- explain a failed pick in terms of geometry, not just code
-->
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Manipulation work becomes real when an arm must move through clutter, respect fixtures, align a gripper with an object, and execute repeatably on hardware that has backlash, latency, and payload limits. MoveIt 2 is valuable because it gives a structured way to connect a robot description, a planning scene, kinematics solvers, motion planners, and execution interfaces into one stack. In production, engineers use it to validate reachability, check collisions against tables and guards, generate approach and retreat motions, and reason about end-effector frames long before a cell is ready for continuous operation.

Pick-and-place rarely fails because “the arm cannot plan.” It fails because grasp poses are expressed in the wrong frame, collision objects are missing or stale, tool center points are modeled badly, IK solutions land near singularities, or execution timing on the real controller differs from the planning assumption. This page is therefore about system alignment between geometry, planning, and execution. A good manipulation engineer checks the planning scene, attached objects, joint limits, controller interface, and grasp semantics as one loop. That is what makes MoveIt 2 a job-relevant skill rather than just a demo tool.

### Industry Tool Stack

- `MoveIt 2`: used for motion planning, planning-scene management, and manipulation application structure.
- `move_group` and related APIs: used to request plans, set targets, and execute trajectories programmatically.
- `RViz Motion Planning plugin`: used to inspect planning groups, reachable targets, and collision objects interactively.
- `KDL` or `TRAC-IK`: used as kinematics solvers for forward and inverse kinematics depending on the robot and plugin setup.
- `ros2_control`: used to connect planned trajectories to simulated or real joint controllers.
- `Planning Scene Monitor`: used to keep collision geometry and attached objects synchronized with the runtime scene.
- `TF2`: used to keep target poses, tool frames, and sensor frames consistent during manipulation tasks.
- `Gazebo` or another simulator: used to test reachability, collisions, and sequencing before hardware execution.

### Step-by-Step Applied Workflow

1. Start with a correct robot description and MoveIt configuration package, including planning groups, end effector, joint limits, and controller mappings.
2. Validate forward and inverse kinematics on simple targets before attempting pick-and-place sequences.
3. Build the planning scene explicitly: add table geometry, bins, fixtures, and target objects instead of assuming open space.
4. Define grasp, pre-grasp, retreat, and placement poses in the correct frame and verify them visually in RViz.
5. Test planning interactively first, then move to code that sends targets and manages object attachment and release.
6. Inspect the generated trajectories for singularity proximity, unnecessary joint motion, and clearance around fixtures.
7. Run the sequence in simulation or a slow-speed hardware mode while comparing planned motion with actual controller execution.
8. Save the scene, parameters, and known-good sequence so future modifications can be compared against a baseline instead of guessed.

### AI Integration

AI is increasingly relevant to manipulation, but mostly around perception, grasp proposal, and high-level task selection rather than low-level geometric truth. Vision models can suggest candidate grasps or detect object pose classes. Language-conditioned systems can map instructions such as “pick the blue box from the left tray” into symbolic goals. Imitation-learning stacks can learn grasping or insertion policies in narrow domains. However, MoveIt 2 still plays the crucial role of ensuring collision-aware motion, respecting kinematic limits, and giving the robot a bounded execution layer.

For this page, the most practical AI adjacency is combining learned perception with classical manipulation planning. A model might estimate an object pose or propose a grasp region, then MoveIt consumes that pose, validates reachability, and generates a safe trajectory. The engineering skill is in the interface: confidence thresholds, coordinate transforms, fallback strategies, and how to recover when the learned component is wrong. AI is helpful here, but only when surrounded by explicit geometry, collision checking, and execution control.

### Case Studies

PickNik is the clearest named example because MoveIt 2 development and training are central to its work, showing how planning scenes, kinematics, and task pipelines become reusable industrial tooling. ROS-Industrial is another strong benchmark: industrial workcell training and integration patterns emphasize tool frames, collision models, and repeatable cell behavior rather than abstract planning alone. In factories, companies such as ABB and FANUC demonstrate the commercial importance of reliable motion planning and cell integration even when their internal planning stacks are not the same as MoveIt.

### Failure Modes & Safety

Manipulation failures often arise from modeling lies. If the TCP is wrong by a few millimeters, a grasp can miss or collide. If the planning scene omits a clamp, tray wall, or cable carrier, the path planner may approve a move that is unsafe in the real cell. If the collision mesh is oversized, the arm appears incapable; if undersized, it appears dangerous. Another failure mode is assuming that a valid plan implies a valid task. The path may be collision free, but the gripper approach angle may be poor, the object may slip during retreat, or the placement pose may violate fixture tolerances.

Controller integration is another safety boundary. A trajectory that is numerically valid may execute poorly if the hardware controller saturates, the timing changes, or the arm is close to a singularity. That is why slow-speed validation, guarded motion, and explicit scene truth matter so much in manipulation. Safe planning is not only about generating a path; it is about proving that the modeled scene, tool semantics, and execution layer match reality closely enough for the path to mean something.

### Business & Commercial Layer

Manipulation is commercially important because many robotics products are judged by cycle time, pick success, changeover effort, and cell safety. Warehousing, packaging, lab automation, machine tending, and electronics handling all depend on reliable pick-and-place behavior. Companies pay for shorter commissioning time, easier reconfiguration, and higher uptime. A manipulation engineer who can model scenes, debug grasp frames, and turn a prototype into a repeatable motion pipeline contributes directly to those outcomes.

In India, this skill maps to industrial automation, machine tending, packaging, electronics, and custom workcell integration. In the US and Europe, it appears strongly in industrial robotics, logistics manipulation, lab automation, and newer general-purpose manipulation startups. Remote work is possible when the engineer produces inspectable artifacts: MoveIt configs, planning-scene notes, sequence videos linked to logs, and frame diagrams. Commercially, this page sits close to revenue because it touches throughput, commissioning cost, and safety review.

### Hiring Signal

Job titles that hire for this page:

- Manipulation Software Engineer
- Motion Planning Engineer
- Robotics Application Engineer (Manipulators)
- Robotics Integration Engineer
- Industrial Robotics Software Engineer

Interview screens that test genuine manipulation skill:

- inspect a failed pick setup and identify whether the problem is grasp frame, planning scene, IK, or controller execution
- explain how an attached object changes the planning scene and why that matters during retreat
- compare joint-space and Cartesian planning for a constrained pick path
- review an end-effector frame definition and predict how it would affect grasp accuracy
- design a minimal validation plan before running a new trajectory on hardware

### Portfolio Projects

Beginner: `moveit-pick-place-starter`
Deliverables: arm model, MoveIt config, one pick sequence, one RViz scene capture, one failure note.
Suggested repo structure:

```text
moveit-pick-place-starter/
├── moveit_config/
├── src/
├── launch/
├── scenes/
└── docs/
```

Acceptance criteria:

- one object can be picked and placed in simulation
- the end-effector frame and object frames are documented
- one collision-related failure is reproduced and explained

Intermediate: `manipulation-scene-and-grasp-lab`
Deliverables: multiple objects, attached-object handling, sequence node, comparison of two grasp strategies.
Suggested repo structure:

```text
manipulation-scene-and-grasp-lab/
├── config/
├── src/
├── scenes/
├── bags/
└── docs/
```

Acceptance criteria:

- the planning scene changes during attach and release are visible and explained
- at least two grasp approaches are compared with evidence
- controller execution is validated against the planned trajectory

Advanced: `industrial-pick-cell-prototype`
Deliverables: near-production cell mockup, fixtures, safety assumptions, sequence orchestration, performance notes.
Suggested repo structure:

```text
industrial-pick-cell-prototype/
├── cell_description/
├── moveit/
├── controllers/
├── orchestration/
└── docs/
```

Acceptance criteria:

- the repo documents real scene assumptions and unsupported cases
- one pick metric such as success rate or cycle time is tracked
- another engineer could review the setup for hardware readiness

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: MoveIt 2 remains a strong entry point for manipulation roles because classical planning and scene reasoning are still required in production.
- `2030`: learned grasping and richer perception will increasingly feed classical planners rather than replacing them outright.
- `2035`: more manipulation systems will combine semantic task layers with collision-aware motion engines and stronger digital-twin workflows.
- `2045`: precise geometry, safe execution, and scene truth will still matter even as higher-level task reasoning becomes more learned and generalized.

### Interview Questions

1. Why can a successful motion plan still lead to a failed pick?
   Short answer: because planning validity does not guarantee the grasp frame, contact mechanics, or execution timing are correct for the task.
2. What does the planning scene do?
   Short answer: it represents obstacles, attached objects, and robot geometry so the planner can reason about collisions.
3. Why is the end-effector frame so important?
   Short answer: because grasp poses and tool motion are expressed relative to it, so small errors propagate directly into task accuracy.
4. When would Cartesian planning be preferable?
   Short answer: when the end effector needs a constrained path, such as a straight insertion or a controlled approach.
5. Why validate in slow-speed or simulation first?
   Short answer: because controller and scene mismatches can produce unsafe motion even when the plan looks correct in software.

### Further Depth

- MoveIt 2 tutorials
- MIT Robotic Manipulation materials
- `Modern Robotics` by Kevin Lynch and Frank Park
- ROS-Industrial training materials
- PickNik MoveIt documentation
