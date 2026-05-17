# ROS 2 Offboard Control and Companion Architecture

## Overview

This page explains how higher-level UAV software should interact with the autopilot. The core design problem is deciding what belongs in firmware versus what belongs on a companion computer.

## Why This Topic Matters

Weak boundaries between the autopilot and companion software create brittle systems. Strong boundaries create maintainable autonomy stacks.

## Core Concepts

### Autopilot Responsibilities
- stabilization
- estimation and control loops
- failsafes
- actuator output

### Companion Responsibilities
- planning
- perception
- mission logic
- cloud or payload integration

### ROS 2 Responsibilities
- modularity
- data flow between onboard applications
- reusable nodes for autonomy and tooling

## Mental Model / Big Picture

```text
mission logic / perception / planning (ROS 2)
                 |
            offboard commands
                 |
             autopilot
                 |
          hard realtime control
```

## Architecture / Components / Building Blocks

- ROS 2 nodes
- bridges or interfaces to the autopilot
- estimator and control topics
- telemetry and logs
- safety states and mode transitions

## Step-by-Step Implementation Guide

1. Define what the autopilot owns.
2. Define what companion software owns.
3. Build one ROS 2 node that publishes or reacts to flight-state data.
4. Test offboard behavior in simulation before field use.

## Hands-On Example / Mini Project

Create a ROS 2 node that commands a simple trajectory in simulation while logging state transitions and safety assumptions.

## Best Practices

- keep offboard interfaces narrow
- document mode assumptions
- test degraded link behavior
- treat safety state transitions as first-class

## Common Pitfalls

- pushing too much fast-loop behavior into ROS 2
- ignoring startup and reconnect behavior
- designing around the happy path only

## Interview Questions

- What belongs in the autopilot versus the companion computer?
- Why is ROS 2 useful in a UAV stack if the autopilot already exists?

## Portfolio / Resume Application

A clean ROS 2 offboard demo with logs and safety notes is directly job-relevant.

## Next Step

Continue to [MAVLink QGroundControl Missions and Telemetry](../03_GCS_Telemetry_and_Missions/01_MAVLink_QGroundControl_Missions_and_Telemetry.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

The companion computer is where most UAV autonomy lives: mission logic, perception pipelines, route planning, payload control, cloud communication, and fleet management. ROS 2 is the dominant middleware for organizing this software on Linux-based companion hardware (Jetson Orin, Raspberry Pi CM4, NXP i.MX, UP Board). The companion communicates with the autopilot via MAVLink (over serial UART, USB, or TCP/UDP) or, for PX4 v1.14+, directly via Micro-XRCE-DDS without a MAVLink bridge.

The core engineering challenge in companion-compute design is boundary definition: what the autopilot controls, what the companion controls, and how each layer behaves when the other fails. An autopilot running PX4 or ArduPilot provides deterministic, safety-critical attitude and rate control. Everything above that — position setpoints, velocity commands, mission waypoints, payload triggers — can be sourced from the companion. The design rule is: the autopilot should always be able to execute a safe fallback (RTL, LAND, Hold) without companion involvement. If the companion can prevent a failsafe from triggering, the architecture is wrong.

In a well-structured companion stack: ROS 2 nodes run as independent processes, each owning a narrow functional scope. A perception node publishes detected target poses. A mission node subscribes to target poses and publishes position setpoints. A health monitor node watches for missed heartbeats and triggers watchdog behavior. The autopilot interface node (MAVSDK or px4_ros_com) translates between ROS 2 topics and MAVLink/DDS.

### Industry Tool Stack

- **ROS 2 Humble LTS** — the primary ROS 2 release for companion-compute development in 2024–2025; Ubuntu 22.04 base; packages via `apt install ros-humble-*`
- **px4_ros_com** — PX4's ROS 2 package providing auto-generated message types and the Micro-XRCE-DDS bridge; enables direct uORB-to-DDS topic communication without MAVLink
- **Micro-XRCE-DDS agent** — the bridge process running on the companion; translates between PX4's embedded DDS client and the full ROS 2 DDS domain
- **MAVSDK Python / C++** — higher-level SDK wrapping MAVLink for mission scripting, offboard control, and telemetry; simpler API than raw pymavlink; good starting point before dropping to raw MAVLink
- **mavros** — ROS 1/2 bridge package providing ROS topics for ArduPilot and PX4 via MAVLink; still widely used in research but deprecated for PX4 in favor of px4_ros_com
- **Jetson Orin NX / Nano** — current reference companion hardware for onboard neural inference and ROS 2; runs Ubuntu 20.04 or 22.04 via JetPack; 10–40 TOPS for INT8 inference
- **tmux + systemd** — companion process management: `tmux` for interactive debugging sessions; `systemd` service units for production auto-start of ROS 2 nodes

### Step-by-Step Applied Workflow

1. **Set up PX4 SITL with the Micro-XRCE-DDS bridge**: install `MicroXRCEAgent`, start PX4 SITL, run `MicroXRCEAgent udp4 -p 8888`, and verify that PX4 uORB topics appear in the ROS 2 domain via `ros2 topic list`.
2. **Subscribe to a PX4 topic from ROS 2**: `ros2 topic echo /fmu/out/vehicle_local_position` — verify the vehicle position updates in real time from SITL.
3. **Implement a minimal offboard position controller**: write a ROS 2 node that publishes to `/fmu/in/trajectory_setpoint` at 10 Hz and switches the autopilot to OFFBOARD mode using a `VehicleCommand` publisher. Test in SITL.
4. **Add a watchdog**: if the trajectory setpoint publisher stops for more than 500 ms, the node should send a mode-switch command to Position Hold and log the watchdog trigger.
5. **Implement node lifecycle management**: use ROS 2 lifecycle nodes (`rclcpp_lifecycle`) so that the offboard controller can be activated and deactivated cleanly without killing and restarting the process.
6. **Build a launch file**: create a ROS 2 launch file that starts all companion nodes (XRCE agent, controller, health monitor) in the correct order with the correct parameters.
7. **Test failure modes**: kill the controller node mid-flight in SITL. Verify the watchdog triggers and the autopilot falls back to Hold or RTL as configured.

### AI Integration

ROS 2 companion compute is one of the most active areas for AI integration in UAV systems:

**Onboard neural inference**: perception nodes running YOLO, DepthPro, or custom object detection models via TensorRT on Jetson Orin. These run as ROS 2 nodes subscribing to `/camera/image_raw` and publishing to `/detections` or `/target_pose`. Inference latency on Jetson Orin Nano at INT8 is typically 15–50 ms depending on model size.

**Visual Inertial Odometry (VIO)**: tools like ORB-SLAM3, OpenVINS, or Kimera-VIO run as ROS 2 nodes and publish pose estimates to `/mavros/vision_pose/pose` (ArduPilot/mavros) or directly to the PX4 EKF2 as external vision measurements. This is how GPS-denied navigation works in practice.

**LLM-assisted mission planning**: experimental work at research groups (MIT, Stanford, TU Delft) is using LLMs as natural-language interfaces to generate waypoint missions or modify mission parameters via voice or text command. These run on the companion and translate to MAVSDK mission uploads.

### Case Studies

**Skydio's Companion Architecture**: Skydio's obstacle avoidance and subject tracking runs on a Snapdragon compute module — a custom companion hardware platform running their proprietary autonomy stack. The architecture follows the companion-compute pattern described here: vision (structured light + cameras) runs as a perception pipeline, obstacle detection runs as a separate processing stage, and motion planning sends position setpoints to their custom flight controller. The companion-autopilot boundary is clean: the flight controller handles attitude and rate, everything above is companion-owned.

**Auterion Skynode — ROS 2 Integration**: Auterion's Skynode integrates PX4 (NuttX) with Ubuntu (companion) on the same board via a high-speed UART bridge running Micro-XRCE-DDS. Their developer documentation shows exactly the px4_ros_com setup described in this page's workflow. Skynode is deployed in commercial inspection drones, surveying UAVs, and research platforms — it is the reference implementation of the PX4 + ROS 2 companion architecture.

**MAVLab TU Delft — Paparazzi + ROS 2 Research**: TU Delft's MAVLab uses ROS 2 as the research interface layer above their Paparazzi autopilot for experimental work with swarming, vision-based landing, and GPS-denied navigation. Their GitHub repositories (github.com/tudelft) show how academic UAV research groups structure the companion-compute stack for rapid iteration.

### Failure Modes & Safety

**Setpoint timeout failure**: the companion stops publishing setpoints (due to a crash, a slow computation, or a deadlock). If the OFFBOARD timeout is not configured or is too long, the vehicle continues on the last setpoint rather than executing a safe recovery. Always configure `COM_OF_LOSS_T` in PX4 to a short timeout (0.5–2 seconds) and test this failure mode explicitly.

**ROS 2 DDS discovery storm**: in some network configurations with multiple ROS 2 nodes, DDS discovery traffic creates a broadcast storm that consumes the companion's CPU and delays critical messages. Use domain ID isolation (`ROS_DOMAIN_ID`) and consider CycloneDDS or FastDDS QoS configuration to limit discovery traffic.

**Coordinate frame confusion**: the PX4 local position frame is NED (North-East-Down); ROS 2 convention is ENU (East-North-Up). The `px4_ros_com` package handles this conversion, but custom code that mixes frames without explicit conversion will silently send setpoints in the wrong direction. Always verify coordinate frames explicitly before any outdoor flight.

**Node startup sequencing**: companion nodes that start before the XRCE agent is ready, or before the autopilot has published its first position estimate, will operate on stale or zero data. Use ROS 2 lifecycle nodes and explicit readiness checks (wait for `/fmu/out/vehicle_local_position` to be non-zero) before commanding any motion.

**MAVLink link loss during OFFBOARD**: if the UDP/UART link between companion and autopilot drops while in OFFBOARD mode, the autopilot will trigger the OFFBOARD failsafe after the configured timeout. This is correct behavior — but the companion must handle the mode change event gracefully, stopping its setpoint publications and transitioning to a monitoring state, not looping on errors.

### Business & Commercial Layer

Companion-compute engineering is the fastest-growing segment of UAV software hiring because it is where AI integration meets the physical vehicle. The companion is where edge inference, fleet management, cloud integration, and operator interface all live — and all of those markets are expanding rapidly.

**Enterprise inspection** (Percepto, Skydio Enterprise, Flyability): companions run mission management, payload control, data upload, and report generation. Engineers who can build reliable ROS 2-based companion stacks are directly employable.

**Defense and ISR** (Shield AI, Joby Defense, Elbit adjacents): GPS-denied navigation using VIO and companion-compute is a key differentiator. Shield AI's Nova autonomy stack (for V-BAT and F-16 adjacent platforms) is a companion-first architecture.

**Delivery** (Zipline, Wing): companions manage flight planning, dynamic rerouting, weather avoidance, and cargo delivery sequencing — all on onboard compute without continuous cloud connectivity.

**India-specific market**: Garuda Aerospace, ideaForge, and Indian defense UAV integrators are beginning to add companion compute to their platforms for agricultural survey, parcel identification, and ISR payload management. Engineers with ROS 2 and companion-compute experience are among the most sought-after in the Indian UAV market in 2026.

### Hiring Signal

**Job titles requiring ROS 2 and companion-compute skills:**
- **UAV Autonomy Engineer** — at Skydio, Shield AI, Joby, Aurora; primary job function is building and maintaining the companion autonomy stack; requires ROS 2 node architecture, offboard control, and perception integration
- **Robotics / ROS 2 Engineer (Aerial)** — at research institutions and autonomy startups; requires ROS 2 fluency, DDS configuration, and hardware integration with autopilots
- **Flight Software Engineer** — at Wing, Zipline, and delivery companies; companion-compute flight software includes mission management and autonomous rerouting
- **Embedded Linux Engineer (UAV)** — at companies building custom companion hardware (Auterion, hardware startups); requires companion OS bring-up, system integration, and ROS 2 deployment

**Specific interview screens:**
1. "Walk me through setting up a PX4 SITL + Micro-XRCE-DDS + ROS 2 development environment from scratch. What are the version constraints and what is the first topic you would subscribe to to verify the bridge is working?"
2. "You are writing an offboard controller as a ROS 2 node that sends position setpoints to PX4. The node crashes mid-flight. What does the autopilot do, and what should your companion architecture do to handle this gracefully?"
3. "Explain the coordinate frame difference between PX4's NED local position frame and ROS 2's ENU convention. How does px4_ros_com handle the conversion, and what happens if you forget to account for it?"
4. "What is the difference between using MAVSDK and px4_ros_com for offboard control? When would you choose each?"
5. "Design a ROS 2 node graph for a precision landing system that uses a camera to detect a landing pad, estimates the pad position, and commands the vehicle to land on it. Name each node, its subscriptions, and its publications."

### Portfolio Projects

**Beginner: `ros2-px4-offboard-hover`**
- Deliverables: ROS 2 node using px4_ros_com that arms PX4 SITL, switches to OFFBOARD mode, commands a 5 m takeoff, holds for 30 seconds, and lands; includes a watchdog that logs and stops setpoints if the vehicle deviates more than 2 m from target; ROS 2 launch file included
- Suggested repo tree: `README.md`, `src/offboard_hover.py`, `launch/hover.launch.py`, `config/params.yaml`, `logs/`
- Acceptance criteria: (1) node runs headlessly in SITL without manual intervention; (2) watchdog is demonstrated by deliberately introducing a position error in SITL; (3) README documents the complete setup including XRCE agent version

**Intermediate: `companion-mission-executor`**
- Deliverables: companion-compute mission executor as a ROS 2 node that reads a YAML mission file, uploads waypoints via MAVSDK, monitors mission execution, and publishes mission status to a ROS 2 topic; supports pause/resume via ROS 2 service calls
- Suggested repo tree: `README.md`, `src/mission_executor.py`, `missions/sample_mission.yaml`, `srv/MissionControl.srv`, `test/`, `logs/`
- Acceptance criteria: (1) executor runs a 4-waypoint mission without user intervention; (2) pause/resume service works correctly in SITL; (3) mission status topic shows correct phase at each waypoint

**Advanced: `companion-full-stack`**
- Deliverables: three-node companion stack (perception node, mission logic node, health monitor) with a systemd service configuration for production auto-start; tested in Gazebo SITL with a simulated camera; failure mode documented and tested
- Suggested repo tree: `README.md`, `nodes/`, `launch/`, `config/`, `systemd/`, `test/`, `docs/architecture.md`, `docs/failure_modes.md`
- Acceptance criteria: (1) all three nodes start correctly via systemd on boot; (2) failure of any one node is detected by the health monitor and a safe recovery is logged; (3) architecture document identifies every inter-node message and every companion-autopilot message

### Future Trends

- **2026**: Micro-XRCE-DDS becomes the standard PX4-companion interface, replacing MAVLink for real-time topic streaming. Engineers who understand both the DDS protocol and the MAVLink fallback are positioned for the transition period.
- **2030**: ROS 2 Jazzy and subsequent releases add stronger lifecycle management, improved security, and better support for embedded deployment. The companion stack becomes more containerized (Docker, snap) and reproducibly deployable.
- **2035**: VIO-based GPS-denied navigation becomes a standard production feature rather than a research capability. Companions running ORB-SLAM3 or successor algorithms are deployed in certified BVLOS operations.
- **2045**: The companion-autopilot boundary may converge as compute becomes more integrated, but the software architecture discipline — clear interfaces, narrow contracts, fail-safe boundaries — remains the foundational design principle.

### Interview Questions

1. **What is the difference between MAVSDK and px4_ros_com for commanding a PX4 vehicle, and when do you use each?**
   *Answer*: MAVSDK is a high-level SDK (Python, C++, Swift) that wraps MAVLink commands into object-oriented APIs for mission management, offboard control, and telemetry. It works with any MAVLink-compliant autopilot (PX4, ArduPilot) via UDP or serial. px4_ros_com is a ROS 2 package that provides auto-generated PX4 message types and a Micro-XRCE-DDS bridge for direct uORB-to-DDS communication — faster and lower-latency than MAVLink, but PX4-specific and requires the XRCE agent. Use MAVSDK for mission scripting, multi-autopilot compatibility, and cross-platform apps. Use px4_ros_com for tight real-time companion integration on PX4-only platforms.

2. **Explain the offboard setpoint timeout mechanism in PX4 and why it is a safety feature.**
   *Answer*: In OFFBOARD mode, PX4 requires setpoints to be received at least once every `COM_OF_LOSS_T` seconds (configurable, typically 0.5 seconds). If setpoints stop arriving, PX4 exits OFFBOARD mode and executes the configured OFFBOARD failsafe (typically Hold or RTL). This prevents the vehicle from continuing the last commanded setpoint indefinitely when the companion crashes or loses connection — which could cause a controlled but unintended flight path. Engineers must ensure their companion publishes setpoints faster than this timeout, even if the setpoint does not change (re-publish the same value at a hold position).

3. **What is Visual Inertial Odometry (VIO) and how does it integrate with the PX4 EKF in GPS-denied environments?**
   *Answer*: VIO estimates vehicle position and velocity by fusing visual information (camera image sequences) with IMU measurements. The camera provides relative displacement estimates; the IMU provides high-rate rotation and linear acceleration. Algorithms like ORB-SLAM3 or OpenVINS run on the companion and output a 6-DOF pose estimate at 30–60 Hz. This is published to the PX4 EKF2 as an external vision measurement via the `vehicle_visual_odometry` uORB topic (through the XRCE bridge) or via the `VISION_POSITION_ESTIMATE` MAVLink message. The EKF fuses the VIO estimate with IMU, replacing GPS for navigation in GPS-denied environments.

4. **Describe the ROS 2 lifecycle node concept and why it is useful for UAV companion software.**
   *Answer*: ROS 2 lifecycle nodes have a defined state machine (Unconfigured → Inactive → Active → Finalized) with explicit transitions. The node only begins processing data when in the Active state. This allows controlled startup sequencing: configure all nodes first (allocate memory, open files), then activate them together when the vehicle is ready. For UAV software, this prevents nodes from sending commands before the vehicle is armed or before safety checks are complete, and allows graceful shutdown without abrupt setpoint stops.

5. **How does coordinate frame handling work in a PX4 + ROS 2 system, and what are the consequences of getting it wrong?**
   *Answer*: PX4 uses NED (North-East-Down) as its local position frame: X is North, Y is East, Z is down (positive Z means lower altitude). ROS 2 uses ENU (East-North-Up): X is East, Y is North, Z is up. The px4_ros_com package automatically converts between these when translating uORB messages to ROS 2 messages. However, custom code that reads raw PX4 position data and sends it back as a setpoint without conversion will have swapped X/Y axes and reversed Z — causing the vehicle to fly in the wrong direction or descend instead of ascending. Always verify coordinate frames explicitly using `ros2 topic echo` and comparing to QGC before any outdoor or high-altitude flight.

### Further Depth

- **PX4 ROS 2 User Guide** (docs.px4.io/main/en/ros2/) — the complete guide to px4_ros_com, Micro-XRCE-DDS setup, and offboard control with ROS 2
- **MAVSDK Python Documentation** (mavsdk.mavlink.io/main/en/python/) — mission scripting, offboard control, and telemetry subscription examples
- **ROS 2 Lifecycle Nodes** (design.ros2.org/articles/node_lifecycle.html) — the design document for the lifecycle node state machine; required reading for production companion software
- **ORB-SLAM3** (github.com/UZ-SLAMLab/ORB_SLAM3) — the leading open-source VIO system for GPS-denied navigation; integrates with ROS 2 via a wrapper
- **OpenVINS** (github.com/rpng/open_vins) — another popular VIO system; designed for ROS integration and real-world deployment
- **"A Gentle Introduction to ROS 2"** (available at ros2docs.com or equivalent) — covers nodes, topics, services, lifecycle, and launch files at the right depth for companion-compute work
