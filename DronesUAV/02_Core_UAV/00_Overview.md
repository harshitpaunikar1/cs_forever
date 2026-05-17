# Core UAV

## Overview

The Core UAV section explains how real drone software systems behave under the hood. It covers the autopilot internals, communication patterns, companion-compute architecture, dynamics, estimation, control, and perception pathways that dominate real engineering work.

## What This Section Covers

### 1. Flight Stack Architecture
- PX4 or ArduPilot modules, messaging, parameters, and firmware workflows.

### 2. ROS 2 and Companion Computers
- offboard control, onboard autonomy, and clean boundaries between firmware and higher-level software.

### 3. GCS, Telemetry, and Missions
- MAVLink message flow, QGroundControl, telemetry tooling, and operator-facing debugging.

### 4. Dynamics, Control, and Estimation
- vehicle models, PID and LQR intuition, IMU and GNSS fusion, and trajectory reasoning.

### 5. Perception and Autonomy
- OpenCV workflows for calibration, markers, tracking, and precision landing style tasks.

## Suggested Study Order

1. PX4 or ArduPilot Modules, uORB, and Firmware Workflows
2. ROS 2 Offboard Control and Companion Architecture
3. MAVLink, QGroundControl, Missions, and Telemetry
4. UAV Dynamics, Control, and State Estimation
5. OpenCV Perception, Precision Landing, and Autonomy

## Milestones

You are ready to leave Core UAV when you can:

- run SITL with a clear mission and telemetry path
- explain the boundary between autopilot firmware and companion software
- implement or modify one control or estimation component
- produce one perception-assisted simulation demo

## Next Step

Start with [PX4 ArduPilot Modules uORB and Firmware Workflows](01_Flight_Stack_Architecture/01_PX4_ArduPilot_Modules_uORB_and_Firmware_Workflows.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Core UAV is where the stack becomes an engineering system. Foundation taught you that the components exist and how to operate them; Core UAV teaches you how they behave internally — what the autopilot modules do, how uORB or the ArduPilot scheduler moves data between them, how the EKF integrates sensor measurements into a state estimate, how ROS 2 offboard control crosses the companion-autopilot boundary, and how perception integrates with flight state to enable autonomy.

This is the tier where most UAV engineering jobs actually live. "Flight Software Engineer" roles at Wing, Zipline, and Joby require all five topics in this section. "UAV Autonomy Engineer" roles at Skydio and Shield AI require the companion compute, perception, and control topics specifically. "Mission Software Engineer" roles require the GCS/telemetry and mission execution topics. The five subsections here are not academic completeness — they map to five real engineering responsibilities that employers screen for.

The critical shift at Core tier is diagnostic confidence: after working through this section, you should be able to open a flight log from an anomalous flight and correctly identify which layer — firmware, estimator, controller, companion, perception — produced the anomaly and why. This is a skill that takes deliberate practice. Every SITL run should be treated as a diagnostic opportunity, not just a demo.

### Industry Tool Stack

- **PX4 uORB message bus** — typed publish/subscribe system for inter-module communication; tools: `uorb top`, `listener sensor_combined`, `uorb status` in the PX4 console
- **ArduPilot GCS_Mavlink and AP_Scheduler** — the equivalent messaging and scheduling architecture in ArduPilot; inspected via MAVProxy and DataFlash logs
- **ROS 2 Humble / Jazzy** — companion-compute middleware; used for node graphs, sensor fusion, and offboard control pipelines; integrates with PX4 via `px4_ros_com` / Micro-XRCE-DDS
- **MAVSDK Python** — high-level SDK for offboard control, mission scripting, and telemetry; the cleanest entry point for companion-compute work before dropping to raw MAVLink
- **OpenCV (4.x / 5.x)** — camera calibration, fiducial detection (ArUco, AprilTag), optical flow, and basic perception pipelines on the companion
- **Extended Kalman Filter (EKF2 in PX4, EKF3 in ArduPilot)** — the state estimator fusing IMU, GPS, barometer, magnetometer, and optionally optical flow or visual odometry
- **pyulog + pandas + matplotlib** — log analysis stack for Core UAV; extract estimator states, controller outputs, and mode transitions

### Step-by-Step Applied Workflow

1. **Map the firmware layer first**: in PX4, use `uorb top` in the NuttX console to list active topics and publication rates. Identify which modules publish `vehicle_attitude`, `vehicle_local_position`, `actuator_outputs`, and `vehicle_status`. In ArduPilot, trace the equivalent through the AP_Scheduler documentation.
2. **Identify the companion-autopilot boundary**: determine which commands will cross the boundary (offboard setpoints via `OFFBOARD` mode, mission items via `AUTO` mode, parameter changes via MAVLink) and which will not (internal controller states, EKF intermediate outputs).
3. **Implement one offboard control node**: use MAVSDK Python or `px4_ros_com` to send position setpoints to the vehicle in SITL. Verify that the vehicle follows them. Capture the log and check the `vehicle_local_position_setpoint` vs. `vehicle_local_position` trace.
4. **Inspect the EKF state in a flight log**: load a `.ulg` log in pyulog, extract `estimator_innovations` and `estimator_status`, and plot GPS innovation magnitudes and EKF consistency flags against time. Identify any period where the EKF flagged a sensor as inconsistent.
5. **Run a perception-assisted task in SITL**: implement a marker detection node (ArUco or QR) in ROS 2 that publishes a detected marker pose. Subscribe to it in an offboard controller that commands the vehicle to hover above the detected marker.
6. **Compare control performance with and without estimation correction**: run the same mission with and without magnetometer fusion (`EKF2_MAG_TYPE` in PX4) and compare the heading estimate drift in the log.
7. **Document every system boundary explicitly**: write a one-page architecture diagram for your Core UAV integration showing what each layer owns, what messages cross each boundary, and what the failsafe behavior is if each layer fails.

### AI Integration

AI enters Core UAV most naturally in two places: perception and EKF-adjacent estimation.

**Perception at Core UAV**: the OpenCV-based perception pipeline on this page's topic 5 is the classical approach — calibration, feature detection, pose estimation. The modern extension replaces some of those steps with lightweight neural networks: YOLO-family or MobileNet-family detectors for object detection, depth estimation networks for obstacle avoidance, and VIO (Visual Inertial Odometry) networks replacing some EKF fusion components. On embedded compute like Jetson Orin Nano, these run at 15–30 fps in INT8 quantized form with TensorRT.

**Log-based anomaly detection**: after accumulating flight logs from Core UAV experiments, AI-assisted log analysis tools can cluster flights by behavior, flag outliers, and suggest probable failure modes. The PX4 Flight Review platform does this at a heuristic level; ML-based extensions (used by fleet operators like Wing and Zipline) do it at scale across thousands of flights.

**LLM-assisted code generation for ROS 2**: companion-compute ROS 2 code (node structure, launch files, parameter files) benefits more from LLM assistance than firmware code, because the safety criticality is lower and the boilerplate is higher. This is a legitimate productivity tool at Core UAV tier.

### Case Studies

**Skydio's Onboard Autonomy Architecture**: Skydio's autonomous obstacle avoidance and subject tracking uses a custom compute platform running visual odometry, obstacle detection, and path planning — all on a Snapdragon compute module. The architecture mirrors the Core UAV tier: firmware layer (flight controller owning attitude and rate control), companion layer (Linux compute running perception and planning), and a MAVLink-adjacent boundary between them. Skydio's engineering blog posts and ICRA papers describe this architecture in enough detail to use as a reference.

**Auterion Skynode — PX4 + Companion Integration**: Auterion's Skynode module integrates PX4 (running on NuttX) with a companion Linux environment (running Ubuntu and ROS 2) on the same hardware board. Their architecture uses uXRCE-DDS as the PX4-to-companion bridge rather than legacy MAVLink, which is the current direction for PX4 development. This is the reference implementation of the firmware-companion boundary described in Core UAV topic 2.

**ideaForge SWITCH — ArduPilot Field Operations**: ideaForge's SWITCH UAV platform uses ArduPilot with a payload and GCS integration layer custom-developed by their engineering team. Their field operations in DGCA-regulated Indian airspace demonstrate what the GCS/telemetry and mission topics of Core UAV look like in a real deployment context: automated pre-flight checks, parameter management, mission file validation, and post-flight log review are all non-optional parts of the engineering workflow.

### Failure Modes & Safety

**The boundary ambiguity failure**: the most dangerous Core UAV failure is an unclear or unacknowledged boundary between what the autopilot controls and what the companion controls. The autopilot's safety protections — arming checks, failsafes, mode restrictions — exist to prevent unsafe states. When companion code bypasses or ignores these protections (e.g., by sending setpoints that drive the vehicle into the ground, or by commanding arm when prearm conditions are not met), the safety architecture breaks. Every companion-compute developer must know exactly where their code's authority ends and the autopilot's begins.

**EKF divergence misdiagnosis**: EKF divergence (rapidly growing position or velocity error) is a common field failure mode. The most frequent cause is not a software bug — it is a configuration mismatch: wrong IMU noise parameters, incorrect GPS accuracy setting, or magnetometer interference creating inconsistent measurements the EKF cannot reconcile. Diagnosing this requires reading `estimator_innovations` and `estimator_status` in the log, not just looking at the vehicle's flight path.

**Offboard mode safety gaps**: `OFFBOARD` mode in PX4 (and equivalent modes in ArduPilot) allows the companion computer to send arbitrary setpoints. If the companion sends a setpoint to fly to altitude 0 (ground level), the autopilot will comply. The safety mitigation is to (1) always have a hardware RC override configured, (2) test every offboard behavior with a safety pilot present, and (3) implement companion-side safety limits before deploying outdoors.

**Perception-in-the-loop without estimation alignment**: adding a perception component that publishes vehicle-relative positions of targets before verifying that the companion's coordinate frame matches the autopilot's coordinate frame. This is a source of silent, hard-to-diagnose errors where the vehicle executes a "correct" command in the wrong direction.

### Business & Commercial Layer

Core UAV skills map directly to the highest-hiring categories in the commercial UAV industry:

**Autonomy product companies** (Skydio, Shield AI, Joby, Aurora): need engineers who can build and debug the full firmware-to-perception stack. Average engineering team salary for UAV Autonomy Engineers in the US is $140–200k+ in 2026.

**Enterprise UAV platforms** (Auterion, DJI Enterprise, senseFly): need engineers who can extend and integrate flight stack APIs, companion software, and telemetry systems. This is Mission Software + GCS tooling at Core UAV scale.

**Defense contractors** (L3 Technologies, Joby Defense, ideaForge India): need engineers who can work with constrained, auditable flight stacks and integrate payloads. Core UAV firmware and mission software skills are entry requirements.

**India-specific market**: the Indian defense drone PLI scheme and DGCA Type Certification process are creating significant demand for engineers who can build, test, and document UAV software at Core tier. Teams at ideaForge, Garuda Aerospace, NewSpace Research, and Indian startups backed by DRDO are hiring for exactly these skills in Bengaluru, Pune, and Delhi NCR.

### Hiring Signal

**Job titles that require Core UAV proficiency:**
- **Flight Software Engineer** — at Wing, Zipline, Joby, Shield AI; requires uORB/ArduPilot internals, EKF literacy, and companion-compute boundary understanding
- **UAV Autonomy Engineer** — at Skydio, Shield AI, Aurora; requires ROS 2 offboard control, perception-to-command pipelines, and state estimation
- **Autopilot Firmware Engineer (PX4)** — at Auterion, Dronecode-affiliated startups; requires uORB pub/sub model, module authoring, and SITL debugging at the firmware level
- **Perception Engineer (UAV)** — at Skydio, emerging Indian autonomy startups; requires OpenCV calibration pipelines, ArUco/AprilTag integration, and VIO fundamentals
- **Systems Test Engineer (UAV)** — at OEMs and test organizations; requires the full Core UAV stack in order to write meaningful test cases for each layer

**Specific interview screens for Core UAV entry:**
1. "Explain the uORB publish/subscribe model in PX4. Name three topics that are published by the sensor layer and three that are consumed by the flight controller. What happens if a subscriber is too slow to consume a publication?"
2. "Given a PX4 log where the EKF switched from GPS-fusion to GPS-denied at timestamp 45s, what are the three most likely causes and what do you look at in the log to distinguish them?"
3. "You are building a companion-compute offboard controller that commands position setpoints via MAVSDK. What safety conditions do you verify before arming, and what watchdog behavior do you implement in case your control loop crashes?"
4. "Describe the complete message flow from an ArUco marker detection on the companion camera to a corrective position setpoint sent to the autopilot via MAVLink."
5. "What is the difference between PX4's `OFFBOARD` mode and `POSITION` mode, and what are the safety implications of each for an autonomous mission that uses companion-computer control?"

### Portfolio Projects

**Beginner: `core-stack-boundary-map`**
- Deliverables: working SITL setup with an offboard MAVSDK Python controller that takes off, holds a position for 30 seconds, and lands; architecture diagram showing exactly which messages cross the companion-autopilot boundary; annotated log trace identifying EKF health, mode transitions, and setpoint tracking
- Suggested repo tree: `README.md`, `scripts/offboard_controller.py`, `docs/architecture.svg`, `logs/run_001.ulg`, `analysis/boundary_trace.md`
- Acceptance criteria: (1) controller runs headlessly in SITL without manual intervention; (2) architecture diagram correctly identifies all message types at the boundary; (3) log annotation identifies at minimum 3 EKF health indicators

**Intermediate: `aruco-precision-hover`**
- Deliverables: ROS 2 node that detects an ArUco marker from a simulated camera stream, computes marker pose in vehicle frame, and publishes position setpoints to hold hover above the marker; runs in Gazebo SITL with a Gazebo camera plugin; logged and plotted
- Suggested repo tree: `README.md`, `src/aruco_hover_node.py`, `launch/`, `config/`, `logs/`, `analysis/hover_accuracy.md`
- Acceptance criteria: (1) node detects marker and maintains hover within 0.5 m laterally in sim; (2) log shows stable position error once marker is acquired; (3) analysis note quantifies hover accuracy statistically

**Advanced: `core-uav-integration-stack`**
- Deliverables: three-layer integration demo (PX4 SITL + ROS 2 offboard + perception) with safety watchdog, CI test, EKF health monitor, and architecture writeup; one deliberate failure mode tested and logged
- Suggested repo tree: `README.md`, `.github/workflows/`, `firmware_layer/`, `companion_layer/`, `perception_layer/`, `docs/architecture.md`, `docs/safety_analysis.md`, `logs/`
- Acceptance criteria: (1) all three layers run together in Gazebo SITL headlessly; (2) safety watchdog triggers correctly when companion control loop is intentionally killed; (3) architecture document explains every inter-layer interface and message type

### Future Trends

- **2026**: PX4's migration from MAVLink to uXRCE-DDS as the primary companion-compute bridge (fully supported in v1.14+) changes how Core UAV engineers write offboard code. DDS-native ROS 2 nodes replace many MAVSDK use cases.
- **2030**: Onboard neural inference (TensorRT-optimized perception models on Jetson Orin class hardware) becomes part of the standard Core UAV stack. Engineers who understand both the flight-stack and inference optimization bridge will be the highest-value hires.
- **2035**: Formal verification of companion-compute behavioral constraints (e.g., contract-based design for offboard controllers) becomes a requirement for BVLOS and urban operations certification. Core UAV engineers who learned safety-case thinking as a discipline will adapt naturally.
- **2045**: The firmware-companion boundary likely evolves — perhaps toward more distributed compute architectures — but the discipline of knowing what each layer owns and how failures propagate remains essential.

### Interview Questions

1. **Explain the EKF2 estimator in PX4: what sensor inputs does it fuse, what does it output, and when does it reject GPS measurements?**
   *Answer*: EKF2 fuses IMU (accelerometer + gyroscope), GPS (position and velocity), barometer (altitude), magnetometer (heading), and optionally optical flow, range finders, and visual odometry. It outputs `vehicle_local_position`, `vehicle_global_position`, `vehicle_attitude`, and `estimator_status`. GPS measurements are rejected when the horizontal velocity innovation or position innovation exceeds the configured gate threshold (controlled by `EKF2_GPS_V_GATE` and similar parameters) — this usually indicates GPS interference, multipath, or a sudden GPS fix jump.

2. **What is the uORB message bus and why does PX4 use it instead of ROS 2 directly in the firmware?**
   *Answer*: uORB is PX4's internal publish/subscribe system designed for the NuttX RTOS environment where ROS 2 cannot run directly. It uses a fixed-size, statically-typed message format published to named topics by ID. Subscribers poll or register callbacks on topics they need. It is extremely low latency (microseconds) and deterministic — appropriate for a 1 kHz attitude control loop. ROS 2 operates on the companion side via the Micro-XRCE-DDS bridge that translates between uORB topics and DDS topics.

3. **What is the safety model for PX4 OFFBOARD mode — who can override whom, and under what conditions?**
   *Answer*: In OFFBOARD mode, the companion sends setpoints (position, velocity, attitude, or thrust) that the autopilot tracks. The RC pilot can override at any time by switching modes via the RC transmitter — this always takes priority and exits OFFBOARD mode. The autopilot also exits OFFBOARD mode if setpoints stop arriving for longer than the configured timeout (typically 0.5 seconds), triggering the OFFBOARD failsafe (which defaults to Hold or RTL). The autopilot's hard limits — maximum tilt, maximum altitude, geofence — remain active in OFFBOARD mode and cannot be overridden by setpoints.

4. **Describe a realistic scenario where the firmware-companion boundary causes a safety-relevant failure.**
   *Answer*: A companion-compute node computing a landing position sends a target altitude of -0.5 m (0.5 m below the current home position) because of a coordinate frame error (NED vs. ENU confusion). In OFFBOARD position control mode, PX4 attempts to track the setpoint, commanding a descent. Without a minimum altitude safeguard on the companion side, the vehicle descends into the ground. The autopilot's ground proximity sensor may or may not catch this depending on configuration. The failure was caused by a coordinate frame mismatch at the companion-autopilot boundary — a classic Core UAV failure mode.

5. **How does perception data (e.g., an ArUco marker pose) get from the companion camera to an autopilot position correction, and what can go wrong at each step?**
   *Answer*: Steps: (1) Camera captures frame → latency (typically 30–100 ms processing). (2) OpenCV ArUco detector finds marker → risk: false detection or pose ambiguity with small markers. (3) Marker pose converted from camera frame to vehicle body frame → risk: incorrect extrinsic calibration or mounting angle. (4) Body frame pose converted to NED world frame using vehicle attitude from EKF → risk: EKF attitude error propagates into position error. (5) Position error sent as OFFBOARD position setpoint via MAVSDK → risk: setpoint rate too low (< 2 Hz risks OFFBOARD timeout). (6) Autopilot tracks setpoint → risk: controller cannot converge if the marker pose estimate is noisy or updates too infrequently.

### Further Depth

- **PX4 Architecture Documentation** (docs.px4.io/main/en/concept/architecture.html) — uORB, module system, and flight task architecture
- **PX4 EKF2 Documentation** (docs.px4.io/main/en/advanced_config/tuning_the_ecl_ekf.html) — EKF tuning and health monitoring; required reading for Core UAV estimation topic
- **ROS 2 + PX4 Integration Guide** (docs.px4.io/main/en/ros2/) — covers Micro-XRCE-DDS setup, px4_ros_com package, and offboard control examples
- **MAVSDK Python Documentation** (mavsdk.mavlink.io/main/en/python/) — mission scripting, offboard control, and telemetry subscription examples
- **OpenCV Camera Calibration Tutorial** (docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html) — the starting point for the perception pipeline on this page
- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain; chapters 8–11 cover state estimation, Kalman filters, and path planning directly relevant to Core UAV topics 4 and 5
