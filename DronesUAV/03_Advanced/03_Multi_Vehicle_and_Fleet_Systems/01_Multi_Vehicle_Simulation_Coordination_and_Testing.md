# Multi-Vehicle Simulation Coordination and Testing

## Overview

This page covers the first serious step beyond single-vehicle autonomy: multi-vehicle simulation, coordination logic, and test discipline.

## Why This Topic Matters

Many people claim “swarm” interest before they can cleanly control one vehicle. Multi-vehicle work only becomes credible after single-vehicle fundamentals are strong.

## Core Concepts

- namespacing and multi-vehicle simulation
- coordination and deconfliction
- shared state or task allocation
- reproducible test scenarios

## Hands-On Example / Mini Project

Build a two-drone simulation with simple waypoint deconfliction or leader-follower behavior and document failure modes.

## Best Practices

- keep the coordination task simple and measurable
- use explicit namespaces and scenario configs
- analyze logs per vehicle and across vehicles

## Common Pitfalls

- adding too much intelligence at once
- no safety assumptions
- no repeatable scenario setup

## Next Step

Continue to [UAV Logs Safety Cases and Production Readiness](../04_Operations_Safety_and_Reliability/01_UAV_Logs_Safety_Cases_and_Production_Readiness.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Multi-vehicle UAV systems are commercially deployed in three distinct operational models: (1) **synchronized swarms** — many vehicles executing a coordinated display or survey pattern simultaneously (DroneShow companies like Ehang Intel Drone Light Shows, Verity Studios); (2) **independent fleet operations** — many vehicles operating concurrently in the same airspace with shared deconfliction rules but independent missions (Wing delivery network, Zipline corridor operations); (3) **cooperative task allocation** — vehicles sharing a mission objective with dynamic task redistribution based on vehicle state (agricultural spray fleets, defense ISR clusters). Each operational model has different engineering requirements for coordination, communication bandwidth, and failure handling.

In SITL, multi-vehicle work begins with namespace isolation. PX4's multi-vehicle SITL launch assigns each vehicle instance a unique `MAV_SYS_ID` (1, 2, 3…) and unique UDP ports (14540, 14541, 14542…), allowing a single GCS to manage multiple vehicles by routing MAVLink messages by system ID. ROS 2 multi-vehicle architectures use namespace prefixes (`/vehicle_1/`, `/vehicle_2/`) to prevent topic collisions between vehicle nodes.

Real deconfliction systems are not typically centralized — a central authority that computes all paths for all vehicles simultaneously becomes a single point of failure and a communication bottleneck. Production fleet systems use distributed deconfliction protocols: each vehicle maintains a conflict detection window (its planned path for the next N seconds), broadcasts planned position to neighbors, and resolves conflicts locally by applying priority rules or renegotiating waypoints. The Wing delivery network, for example, uses corridor-based deconfliction: vehicles are assigned to specific altitude layers and horizontal corridors, eliminating most conflict cases without requiring real-time inter-vehicle communication.

### Industry Tool Stack

- **PX4 multi-vehicle SITL** — `Tools/simulation/gazebo-classic/sitl_multiple_run.sh` or the newer `make px4_sitl gazebo-classic` with `NUMSITL=3`; each instance gets a unique system ID, UDP port, and Gazebo model; QGC connects to each via different port
- **MAVProxy multi-vehicle routing** — `--out` flag fans a single MAVLink stream to multiple consumers; SYSID-based filtering separates per-vehicle traffic; `--target-system` directs commands to a specific vehicle
- **ROS 2 multi-namespace launch** — `namespace` argument in Python launch files; remaps all topics and services under `/vehicle_N/` prefix; `ros2 topic list | grep vehicle_1` shows per-vehicle topics
- **MAVSDK multi-vehicle Python** — instantiate multiple `System()` objects each connected to a different UDP port; run concurrent async tasks per vehicle using `asyncio.gather()`
- **Gazebo multi-model spawning** — each SITL instance spawns a separate Gazebo model (quadrotor_x, quadrotor_x_1, etc.) with different initial pose; Gazebo handles physical collision between them (useful for testing proximity limits)
- **pyulog batch processing** — `ulog2csv` on multiple `.ulg` files; pandas for multi-vehicle DataFrame merging on timestamp; matplotlib for fleet-level position plots
- **ROS 2 `tf2` multi-vehicle transforms** — separate transform trees per vehicle namespace; `tf2_ros::Buffer` with namespace prefix resolves per-vehicle pose in a shared world frame
- **ArduPilot multi-vehicle SITL** — `sim_vehicle.py` with `--count=3` launches three ArduCopter instances; each instance gets its own MAVLink port and GCS connection

### Step-by-Step Applied Workflow

1. **Launch two PX4 SITL instances** — run `Tools/simulation/gazebo-classic/sitl_multiple_run.sh 2`; confirm two quadrotor models appear in Gazebo at offset positions; connect QGC to both via ports 14550 and 14551; verify both show as separate vehicles in QGC's vehicle list.

2. **Send independent waypoint missions to each vehicle** — use MAVSDK Python: create two `System()` objects, connect each to its UDP port (14540 and 14541); upload a 4-waypoint survey mission to vehicle 1 and a 4-waypoint coverage mission to vehicle 2; arm and start both missions concurrently using `asyncio.gather()`.

3. **Monitor position separation in real time** — write a Python script that subscribes to both vehicles' `VehicleLocalPosition` uORB topics via MAVSDK telemetry and computes the 3D Euclidean distance every 0.5 s; log any separation below 10 m as a conflict event.

4. **Implement simple altitude-layer deconfliction** — assign vehicle 1 to 30 m AGL and vehicle 2 to 50 m AGL in their respective missions; verify that the separation monitor never reports a conflict; then create a test case where both are at 30 m to confirm the monitor fires.

5. **Implement a leader-follower pair** — vehicle 1 executes a pre-planned route; vehicle 2 subscribes to vehicle 1's position telemetry and sends MAVSDK offboard position setpoints targeting vehicle 1's position with a 20 m lag; measure the lag distance over the course of the mission.

6. **Stress test with a vehicle failure scenario** — during the leader-follower mission, send a land command to vehicle 1 (simulating failure); observe whether vehicle 2 detects the leader's descent and halts, or continues to follow toward the ground; document the behavior and propose a safeguard.

7. **Analyze multi-vehicle logs** — after a 3-vehicle mission, use `pyulog` to extract position logs from all three `.ulg` files; merge into a single pandas DataFrame on timestamp; plot all three vehicle trajectories on a 2D top-down map; identify any timestamp where separation was below 10 m.

8. **Write a safety assumptions document** — list what conditions must be true for the two-vehicle simulation to behave as designed: nominal communication latency, GPS accuracy, absence of wind, correct SYSID assignment; list three failure modes (communication loss, GPS spoofing, SYSID collision) and describe how each would affect coordination.

### AI Integration

Multi-agent reinforcement learning (MARL) is the dominant AI research direction for multi-UAV coordination. In MARL, each vehicle agent learns a policy that maps its local observation (own position, velocity, planned path; neighbor positions and velocities received via communication) to a control action (next waypoint, speed command, altitude adjustment). The policy is trained in simulation using reward functions that penalize inter-vehicle conflict and reward mission completion. Groups at TU Delft, MIT CSAIL, and Carnegie Mellon have published MARL policies for task allocation, path deconfliction, and coverage optimization that outperform hand-coded heuristics in dense airspace scenarios.

For engineers not working in research, AI enters multi-vehicle coordination at the planning layer rather than the control layer. LLM-based mission planners can translate high-level operator intent ("survey this field with three drones in parallel strips") into per-vehicle waypoint lists respecting altitude-layer constraints and timing for simultaneous coverage. This is a practical near-term application: the AI handles mission decomposition, the conventional flight stack handles execution. Companies exploring this include Skydio (Skydio AI) and DroneBase.

Anomaly detection across a fleet is another maturing AI application: ML models trained on single-vehicle healthy logs learn normal position, vibration, and current draw profiles; deviations in any vehicle's telemetry trigger alerts. This is operationally deployed at Wing and Zipline to catch pre-failure behavior (motor bearing wear, EKF instability) before it causes an incident.

### Case Studies

**Shield AI Hivemind Multi-Vehicle Coordination**: Shield AI's Hivemind autonomy stack powers multi-vehicle operations on their V-BAT UAS and fixed-wing ISR platforms in GPS-denied and communication-degraded environments. Their coordination architecture is explicitly designed for decentralized operation: each vehicle runs a local Hivemind instance that maintains a shared situational awareness model and makes local decisions without requiring continuous communication to a central server. This addresses the central-controller failure mode and is documented in Shield AI's technical papers and engineering blog.

**Wing Delivery Network Corridor Deconfliction**: Wing's urban delivery network (operating in Christiansburg VA, Logan AU, and Helsinki FI) manages concurrent flight operations using airspace corridor reservation rather than real-time inter-vehicle communication. Each vehicle requests a corridor reservation for its planned route before departure; the UTM system grants or denies based on existing reservations; vehicles that share a corridor are assigned altitude separation. This makes the deconfliction problem tractable without requiring vehicle-to-vehicle communication — the complexity is in the UTM reservation system, not the vehicle stack.

**MAVLab TU Delft Crazyflie Swarm**: TU Delft's MAVLab has demonstrated synchronized swarms of up to 100 Crazyflie micro-drones using a combination of UWB-based relative positioning (no GPS) and an onboard consensus algorithm for position coordination. Their swarm coordination research (published in Science Robotics and ICRA) represents the academic frontier of multi-vehicle UAV coordination, and their open-source Crazyflie ecosystem provides a reproducible platform for swarm research that commercial engineers use as a validation environment.

### Failure Modes & Safety

**SYSID collision**: If two PX4 vehicles are launched with the same `MAV_SYS_ID`, a GCS connected to both sees a single vehicle with unpredictable telemetry (alternating between the two physical vehicles' actual states). QGC's vehicle list shows one vehicle; commands are broadcast to both. In a multi-vehicle SITL launch, SYSID assignment is automatic; in hardware deployments, manual SYSID assignment is required. The failure mode is silent — no error message, just wrong behavior.

**ROS 2 namespace topic collisions**: A multi-vehicle ROS 2 architecture without namespace isolation has all vehicles publishing to the same topic names (`/mavros/local_position/pose`, etc.). All subscribers receive the superposition of all vehicles' data — a position subscriber cannot distinguish which vehicle's position it is reading. The fix is namespace prefixing from the launch file, but this must be designed in from the start; retrofitting namespaces into an existing codebase is error-prone.

**Coordination logic that works for N=2 but breaks at N=3**: Many leader-follower and deconfliction algorithms are validated for two vehicles and assumed to generalize. At three vehicles, combinatorial interaction terms grow — a three-way proximity event (all three within 10 m simultaneously) requires resolution logic that was never implemented. Production multi-vehicle systems must be tested at the maximum intended vehicle count, not just the minimum.

**Communication latency causing stale neighbor models**: A deconfliction algorithm that assumes neighbor position is updated at 10 Hz but receives updates at 2 Hz (due to link degradation) may resolve a conflict based on the neighbor's position 0.5 s ago. At 10 m/s airspeed, 0.5 s of stale data represents 5 m of position error — which may be larger than the conflict detection threshold. The fix is to bound the maximum acceptable staleness and have the algorithm degrade gracefully (increase safety margins) when stale data is detected.

**Ignoring wind in multi-vehicle separation calculations**: Two vehicles executing parallel survey rows at 10 m horizontal separation in zero-wind simulation may close to 3 m separation in a 5 m/s crosswind because each vehicle's position controller responds to wind differently (different PID tuning, different mass, different drag coefficient). Multi-vehicle tests must include wind disturbance to validate that separation margins hold in realistic conditions.

### Business & Commercial Layer

Multi-vehicle coordination is the enabling technology for scalable commercial UAV operations, which is why it commands a disproportionate share of engineering investment in the industry. A fleet of 10 delivery drones that can operate concurrently scales linearly with vehicle count but multiplies revenue 10×; the coordination technology that enables concurrent operation is therefore the highest-leverage engineering capability in the commercial fleet model.

Defense UAV programs are the other major demand driver. Multi-vehicle ISR (intelligence, surveillance, reconnaissance) using collaborative sensor fusion across a swarm of vehicles provides coverage and persistence that no single platform can match. Defense prime contractors (L3Harris, Northrop Grumman, General Atomics) are investing heavily in swarm coordination; their advanced engineering teams need both the systems-level coordination background and the embedded flight stack depth to implement it reliably.

In India, agricultural fleet operations — where 5–10 spray drones work a field simultaneously — represent the first commercial multi-vehicle UAV deployment at scale. Companies like TartanSense, General Aeronautics, and Kisan Drone are building this infrastructure domestically, creating demand for multi-vehicle coordination engineers who understand both the ROS 2/MAVSDK coordination layer and the regulatory constraints for fleet operations under DGCA's BVLOS framework.

### Hiring Signal

**Job titles requiring multi-vehicle UAV coordination competence:**
- **Swarm Systems Engineer** — at Shield AI, AeroVironment, Joby; requires multi-agent coordination algorithms, distributed state management, and communication-degraded operation design
- **Fleet Software Engineer** — at Wing, Zipline, Dronamics; requires UTM integration, fleet telemetry aggregation, concurrent mission management, and anomaly detection across vehicles
- **Multi-Vehicle Simulation Engineer** — at eVTOL and delivery drone companies; requires PX4/ROS 2 multi-vehicle SITL, scenario-driven testing frameworks, and log analysis across vehicle fleets
- **Autonomous Systems Engineer (Multi-Agent)** — at defense UAV companies and research labs; requires MARL familiarity, decentralized coordination protocols, and safety-critical multi-agent behavior validation
- **UAV Software Architect (Fleet Scale)** — at enterprise fleet operators; requires system design for N-vehicle concurrent operations, deconfliction algorithm design, and failure mode analysis at fleet scale

**Specific interview screens for multi-vehicle UAV roles:**
1. "Design a deconfliction algorithm for three UAVs executing parallel survey rows over the same 500m × 500m field. What minimum information does each vehicle need about its neighbors, at what update rate, and how does the algorithm handle a communication dropout affecting one vehicle?"
2. "Walk me through setting up a PX4 multi-vehicle SITL with three instances in Gazebo. How do you assign unique MAV_SYS_IDs? How do you connect QGC to all three simultaneously?"
3. "In a leader-follower formation where vehicle 2 tracks vehicle 1's position with a 20m lag, vehicle 1 initiates an emergency landing. Describe what vehicle 2 should do, and write pseudocode for the detection-and-response logic."
4. "You are merging per-vehicle pyulog files from a 3-drone survey mission to compute the minimum inter-vehicle separation throughout the flight. Walk me through the data pipeline from .ulg files to a separation plot."
5. "A production fleet of 8 delivery drones uses a centralized path planner. The planner server becomes unreachable mid-operation. What should each vehicle do, and how would you design the system to handle this failure gracefully?"

### Portfolio Projects

**Beginner: `two-vehicle-sitl-mission`**
- Deliverables: A working two-vehicle PX4 SITL setup with a Python script (MAVSDK) that sends independent waypoint missions to both vehicles, monitors inter-vehicle separation every 0.5s, and logs any separation below 10m to a CSV file; one Gazebo screenshot showing both vehicles in flight
- Suggested repo tree: `README.md`, `scripts/launch_two_sitl.sh`, `scripts/dual_mission.py`, `scripts/separation_monitor.py`, `results/separation_log.csv`, `results/gazebo_screenshot.png`
- Acceptance criteria: (1) both missions complete successfully with both vehicles landing at their respective home positions; (2) the separation log captures at least 60 seconds of data with 2 Hz resolution; (3) the README documents how to reproduce the entire setup including PX4 version and Gazebo version used

**Intermediate: `leader-follower-formation`**
- Deliverables: A two-vehicle formation flight demo where vehicle 2 maintains a 20m lag behind vehicle 1 using MAVSDK offboard position commands; includes a failure injection test (vehicle 1 commanded to land) and documented behavior of vehicle 2 in response; pyulog analysis showing actual separation distance over time vs commanded separation
- Suggested repo tree: `README.md`, `scripts/formation_flight.py`, `scripts/failure_injection_test.py`, `logs/normal_mission.ulg`, `logs/failure_test.ulg`, `analysis/separation_analysis.ipynb`, `docs/safety_assumptions.md`
- Acceptance criteria: (1) the leader-follower maintains separation within ±5m of the 20m target during steady flight; (2) the failure injection test demonstrates a defined behavior (stop, hover, land) when the leader initiates landing; (3) the safety assumptions document lists at least 4 conditions required for the formation to behave as designed

**Advanced: `three-vehicle-deconfliction-system`**
- Deliverables: A three-vehicle SITL coordination system with altitude-layer deconfliction (each vehicle assigned to a different altitude band), a centralized conflict monitor that detects any 3D separation below 15m and logs it, a failure injection test where one vehicle's altitude controller is bypassed to simulate a level-hold failure, and a safety case document for the deconfliction architecture
- Acceptance criteria: (1) zero conflicts detected during the nominal 3-vehicle mission; (2) the failure injection test produces a logged conflict event and a defined system response; (3) the safety case document follows GSN (Goal Structuring Notation) format with at least 3 sub-goals, each with evidence

### Future Trends

- **2026**: Commercial UTM (Unmanned Traffic Management) systems mature; flight stack integration with UTM APIs (FAA LAANC, EASA U-space) becomes a standard skill for fleet engineers rather than a specialized capability
- **2030**: Multi-agent RL coordination policies trained in simulation are validated for limited operational domains (fixed corridors, constrained airspace); begin appearing in commercial fleet products alongside rule-based deconfliction
- **2035**: Urban air mobility at city scale requires coordinating hundreds of simultaneous VTOL vehicles; the engineering discipline of multi-vehicle coordination moves from aerospace specialty to infrastructure engineering, with dedicated UTM cloud services handling much of the complexity
- **2045**: Fully autonomous swarm coordination (no per-vehicle operator, no pre-planned missions, emergent goal completion from collective behavior) exits research and enters commercial deployment in controlled domains; engineers who built the foundation in the 2025–2030 window lead these programs

### Interview Questions

1. **What is the minimum information a vehicle needs about its neighbors to perform geometric deconfliction?**
   *Answer*: At minimum: neighbor position (3D), neighbor velocity vector, and a timestamp for both. With position and velocity, you can project the neighbor's future position forward by N seconds (linear prediction) and check whether your own projected position intersects within the conflict radius. In practice, production systems also use intent (planned trajectory, not just current velocity) because velocity alone produces false conflicts for vehicles turning into a crossing trajectory. Intent-based deconfliction (sharing planned waypoint sequences) significantly reduces unnecessary maneuvers.

2. **Explain how MAVLink's system ID (SYSID) enables multi-vehicle operation from a single GCS.**
   *Answer*: Every MAVLink message contains an 8-bit system ID in the header. A QGC connected to multiple vehicles via different UDP ports (or a MAVProxy fanout) receives messages from all vehicles but can filter by SYSID to display per-vehicle state. Commands sent to a specific vehicle use the target system ID field — a `MISSION_START` command with `target_system=2` is ignored by vehicle 1. SYSID collisions (two vehicles with the same ID) produce ambiguous telemetry and broadcast commands to both vehicles simultaneously — a dangerous failure mode in hardware deployments.

3. **Why is centralized path planning a single point of failure for a multi-vehicle fleet, and what is the alternative?**
   *Answer*: If the central planner is unavailable (server failure, communication loss, software crash), no vehicle can resolve conflicts — they may stop, fly unsafe trajectories, or exhibit undefined behavior depending on their fallback logic. The alternative is distributed deconfliction: each vehicle applies local conflict resolution rules using received neighbor state, without requiring a central authority. Corridor-based separation (Wing's model) is one form — conflicts are eliminated by design (spatial separation rules), not by real-time computation. Distributed priority rules (lower SYSID yields to higher SYSID) are another — simple to implement, no communication overhead for the decision itself.

4. **How do you merge pyulog files from three vehicles to produce a fleet-level minimum separation plot?**
   *Answer*: Parse each `.ulg` file with `pyulog.ULog` to extract `vehicle_local_position` (x, y, z, timestamp). Resample each vehicle's position to a common 10 Hz timestamp grid using pandas `resample()` and linear interpolation. Merge all three DataFrames on timestamp. For each timestamp, compute pairwise 3D Euclidean distances (3 pairs for 3 vehicles). Take the minimum across all pairs at each timestamp. Plot minimum separation vs time; annotate any point below the safety threshold. This pipeline is straightforward in pandas with 5–10 lines per step.

5. **What happens to a leader-follower formation if the follower's offboard setpoint timeout fires because of a communication failure?**
   *Answer*: PX4's offboard timeout parameter (`COM_OF_LOSS_T`) defines how long the vehicle waits for a new setpoint before exiting offboard mode. If the leader's position publisher (the follower's setpoint source) goes silent, the follower exits offboard mode after `COM_OF_LOSS_T` seconds (default 1 s) and triggers the offboard failsafe action (`COM_OBL_ACT` — typically hold position or loiter). The follower does not continue tracking the leader's last known position indefinitely — it stops. This is the safe failure behavior; the engineering challenge is making it detectable and recovery-able in the system design.

### Further Depth

- **PX4 multi-vehicle simulation documentation** (docs.px4.io/main/en/simulation/multi_vehicle_simulation.html) — official setup guide for multi-vehicle Gazebo SITL
- **MAVSDK Python multi-vehicle examples** (github.com/mavlink/MAVSDK-Python/tree/main/examples) — async Python patterns for concurrent multi-vehicle control
- **MAVProxy documentation — multi-vehicle routing** (ardupilot.org/mavproxy/) — `--out` flag, SYSID filtering, and multi-vehicle GCS patterns
- **"Multi-Robot Systems" — Dudek and Jenkin** — foundational academic text for multi-robot coordination algorithms; covers task allocation, formation control, and consensus protocols
- **TU Delft MAVLab publications** (mavlab.tudelft.nl) — open-access swarm research papers; Crazyflie swarm coordination and UWB-based relative positioning
- **Shield AI engineering blog** (shield.ai/research) — published perspective on decentralized autonomy and multi-vehicle coordination in adversarial environments
- **ROS 2 multi-robot documentation** (docs.ros.org) — namespacing patterns, tf2 multi-robot transform trees, and launch file composition for multi-vehicle systems
