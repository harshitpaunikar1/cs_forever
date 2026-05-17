# Advanced Project Path

## Overview

These projects are intended to produce portfolio pieces that look like real UAV engineering work rather than expanded tutorials.

## Projects

### Project 1: Flight-Stack Integration Capstone
- SITL autopilot
- ROS 2 autonomy node
- mission upload
- telemetry monitoring
- logs and metrics

### Project 2: Vision-Guided Landing
- OpenCV perception node
- pose estimation
- simulation loop
- landing or approach logic

### Project 3: Multi-Vehicle Coordination Demo
- two-drone simulation
- deconfliction or leader-follower behavior
- architecture diagram
- failure analysis

### Project 4: Embedded or Driver Exploration
- NuttX or driver path deep dive
- one board or sensor data-path writeup
- reproducible build or analysis steps

### Project 5: JSBSim Fixed-Wing or VTOL Study
- aircraft model
- scenario experiments
- plots
- interpretation notes

## Completion Standard

Complete at least `1` flagship project and make it recruiter-runnable.

## Next Step

Return to the [Portfolio Checklist](../../05_Resources/Cheatsheets/Portfolio_Checklist.md) before declaring a project finished.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Advanced UAV projects are distinguished from intermediate ones by a single criterion: the engineer had to make non-obvious system-level design decisions and can defend them under examination. The five project options in this path each require integrating multiple subsystems from previous sections into a cohesive, validated whole — and each has a direct analog in professional UAV engineering work.

The Flight-Stack Integration Capstone (Project 1) mirrors what a new engineer at an autonomy company delivers in their first 3 months: a working SITL environment with their team's software stack (ROS 2, MAVSDK, or both), flying a representative mission with logs showing healthy EKF and mission completion. The Vision-Guided Landing (Project 2) is the canonical UAV perception project — it appears in every autonomy company's engineering challenge and in almost every senior autonomy engineer's portfolio. Multi-Vehicle Coordination (Project 3) is the Advanced-tier flagship project that opens Senior and Swarm Systems Engineer roles. Embedded/Driver Exploration (Project 4) is the entry point to firmware engineering roles. JSBSim FDM Study (Project 5) is the entry point to GNC and simulation engineering roles at eVTOL companies.

Each project should take 3–6 weeks of focused weekends and evenings to complete to the standard expected at this level. The completion standard — "recruiter-runnable" — means a senior engineer from the target company can clone the repo, follow the README, and have a working demo within 30 minutes, on their own machine, without asking the project author any questions.

### Industry Tool Stack

- **PX4 SITL + Gazebo Classic or Ignition** — for Projects 1, 2, 3; pin the specific version; document Gazebo vs Ignition choice in the README (Ignition is the forward-looking choice but Gazebo Classic has more SITL model support as of 2025)
- **ROS 2 Humble/Jazzy** — for Projects 1, 2, 3; use lifecycle nodes for production-grade node management; namespace all nodes from the launch file
- **MAVSDK C++ or Python** — for Projects 1, 3; async mission management and telemetry; C++ for performance-sensitive applications, Python for rapid prototyping
- **OpenCV 4.9+** — for Project 2; `cv2.aruco.ArucoDetector`, `cv2.solvePnP`, `cv2.calibrateCamera`; ensure `cv2.aruco` is available (requires `opencv-contrib-python`)
- **px4_ros_com + Micro-XRCE-DDS** — for Projects 1, 2, 3; the bridge from PX4 SITL to ROS 2 via uORB-over-DDS
- **pyulog + pandas + matplotlib** — for all projects' log analysis and metric generation; required for the metrics report artifact
- **PX4 NuttX source** — for Project 4; reading the driver source in `src/drivers/imu/invensense/icm42688p/` and the uORB listener; no build required for the reading note variant
- **JSBSim Python API** — for Project 5; `jsbsim.FGFDMExec` and Python scripting for batch simulation runs and trim analysis
- **GitHub Actions** — for CI on all projects; at minimum: a build check; for Projects 1–3: a SITL smoke test that flies a 30-second mission and checks the log for GPS lock
- **Docker** — strongly recommended for Projects 1–3; packaging the entire environment (ROS 2, PX4 SITL, Gazebo, MAVSDK) into a Docker container makes "recruiter-runnable" achievable across operating systems

### Step-by-Step Applied Workflow

1. **Project 1 (Integration Capstone): Define the stack before building it** — write a one-page architecture document: which component handles mission planning (MAVSDK or QGC), which component handles offboard control (ROS 2 node or MAVSDK), how does ROS 2 connect to PX4 (XRCE-DDS agent), where is the log captured (onboard ULog), and what is the mission profile (4-waypoint survey or inspection loop). Having this document prevents architecture drift during implementation.

2. **Project 2 (Vision Landing): Build the perception pipeline before the control pipeline** — validate that ArUco detection and `solvePnP` produces correct poses in static images before connecting to SITL; compute the coordinate frame chain (image → camera → body → NED) and verify each transform on paper before coding it; test the pose estimation with a known marker at a known distance and verify the estimated distance matches ground truth within 5%.

3. **Project 3 (Multi-Vehicle): Launch the simulation before writing coordination logic** — verify that both PX4 SITL instances are running (distinct UDP ports, distinct Gazebo models, distinct GCS connections) and can each fly an independent waypoint mission before adding any inter-vehicle communication; coordination logic on a broken multi-vehicle simulation produces bugs that are extremely difficult to diagnose.

4. **Project 4 (Embedded/Driver Exploration): Trace the code before writing about it** — open `src/drivers/imu/invensense/icm42688p/ICM42688P.cpp` in VSCode with PX4 source indexed; trace from `probe()` through `init()` through the interrupt handler through `RunImpl()` through `orb_publish()`; annotate each step in a text file as you go; only then write the structured document from your annotated notes.

5. **Project 5 (JSBSim Study): Run trim before running scenarios** — always verify the model trims at a reasonable state (pitch angle, throttle, elevator deflection) before running any scenario simulation; a model that does not trim correctly will produce nonsensical scenario results; document the trim state as the first result in your analysis.

6. **Write the architecture diagram for every project** — use Mermaid, draw.io, or a hand-drawn scan; show the major components (PX4, ROS 2 nodes, MAVSDK, Gazebo, ArUco detector) and the communication links between them (DDS, UDP, ros2 topics); embed in the README and keep it updated as the architecture evolves.

7. **Run the failure injection tests before claiming completion** — for each project, define 2 failure injection tests; run them; document the results; include a screenshot or log snippet showing the failure behavior. No project is complete until the failures have been exercised.

8. **Package in Docker and verify it runs on a fresh machine** — build the Docker image on your machine; push to Docker Hub; ask a friend (or use a GitHub Actions runner) to pull and run it; fix any environment-specific issues that arise. "It works on my machine" is not acceptable for an Advanced-tier portfolio project.

### AI Integration

At the Advanced level, AI tools are most productive for the architectural reasoning and documentation phases rather than for implementation. GitHub Copilot and Cursor accelerate C++ implementation of ROS 2 nodes and PX4 modules, but the generated code must be carefully reviewed — autopilot-adjacent code that has incorrect coordinate frame assumptions or unsafe pointer usage will not be caught by a unit test if the test itself was AI-generated from the same incorrect premise.

Specific high-value AI applications at the Advanced level: (1) generating Mermaid architecture diagram code from a text description of component connections; (2) drafting the GSN safety argument skeleton for the safety case document; (3) explaining specific PX4 driver patterns before writing Project 4's driver reading note; (4) generating LaTeX or markdown tables for metrics reports. The common thread: AI for formatting and scaffolding, engineer for technical accuracy.

One emerging use: generating test scenarios for multi-vehicle coordination. Describing the coordination scenario to an LLM and asking it to generate Python MAVSDK mission scripts for 2–3 vehicles is a reasonable starting point, provided the engineer verifies the mission geometry (no collision courses, correct altitude assignments) before running in SITL.

### Case Studies

**Skydio's Vision-Guided Navigation as an Advanced Project Template**: Skydio's obstacle avoidance and visual navigation stack — the technology that distinguishes Skydio from other commercial drone companies — is built on the same foundational components as Project 2: camera pose estimation (they use stereo cameras instead of single-camera ArUco), body-to-NED coordinate transforms, and offboard setpoint commands to the PX4 flight stack. Their autonomy engineers describe the core challenge as exactly what Project 2 teaches: the coordinate frame chain and the latency budget from camera frame to autopilot setpoint. Skydio's engineering blog has published technical details on their visual navigation architecture.

**Shield AI V-BAT Integration Capstone at Scale**: Shield AI's V-BAT fixed-wing VTOL UAS runs a Hivemind autonomy stack that is structurally analogous to Project 1 — a flight stack (PX4-adjacent firmware), an autonomy compute layer (the Hivemind ROS-compatible nodes), and a mission management layer — all integrated and validated in simulation before hardware flights. Their engineering team uses SITL for every software change validation. The integration capstone project at the Advanced level is the individual analog of what their team does collectively.

**MAVLab TU Delft Multi-Vehicle Crazyflie Demo**: TU Delft's MAVLab group regularly produces multi-vehicle demos at research conferences that meet Advanced project quality: the demo is reproducible (they publish their code and environment), measured (they report separation statistics and mission completion metrics), and safety-aware (they use UWB-based relative positioning in a constrained indoor arena rather than claiming the system works in unstructured airspace). Their open-source Crazyflie swarm framework is the research-community version of Project 3.

### Failure Modes & Safety

**Coordinate frame error in Project 2 that only manifests at scale**: The most common Project 2 failure is a subtle sign error in the coordinate frame conversion between camera frame (Z forward, X right, Y down in OpenCV convention) and body frame (X forward, Y right, Z down in PX4/NED convention) or between body frame and NED. The error typically manifests as a landing approach that converges initially and then diverges as the vehicle descends to low altitude where the error becomes large relative to the target size. Verifying each transform with a known test case (marker at known position, verify estimated position is correct) before connecting to SITL saves hours of debugging.

**Multi-vehicle SYSID collision in Project 3**: If both PX4 SITL instances are launched with the same `MAV_SYS_ID` (which can happen with certain launch scripts that do not correctly pass the SYSID argument), the coordination logic receives interleaved telemetry from both vehicles on the same topic — position updates may alternate between vehicle 1 and vehicle 2's actual positions. The coordination algorithm will behave erratically and produce difficult-to-diagnose failure modes. Always verify SYSID assignment with `ros2 topic echo /fmu/out/vehicle_status` for each vehicle namespace.

**Integration Capstone that adds too many components simultaneously**: Adding MAVSDK, ROS 2, XRCE-DDS, and a custom autonomy node all at once before verifying any of them work is a recipe for a debugging nightmare where the root cause could be any of the four components. The correct approach is incremental integration: PX4 SITL alone (verify flight), then XRCE-DDS (verify ROS 2 topics appear), then MAVSDK (verify mission upload), then custom node (verify autonomy behavior). Each step is verified before the next is added.

**JSBSim trim divergence treated as a solver bug**: When the JSBSim trim solver fails to converge, the error message can be cryptic — the output is an extreme control surface deflection or infinite iteration. Engineers who treat this as a JSBSim bug rather than an aircraft model problem waste time on the wrong root cause. The correct interpretation is: the model has a physical inconsistency (stall speed above cruise speed, negative drag at some condition, missing propulsion model) that makes the trim infeasible. Debugging requires examining the aerodynamic coefficient tables for the problematic condition.

**Driver reading note that is just code comments restated**: Project 4's driver exploration deliverable is often written as a direct paraphrase of the code comments — "the `init()` function initializes the sensor" — which adds no analytical value. The correct form of an Advanced driver reading note explains the engineering reasoning behind the code: why the SPI clock rate was chosen at this value (it is the maximum rate that allows the DMA to complete within the interrupt period without DMA priority issues), why the ODR register is configured before the interrupt is enabled (to avoid spurious interrupts during initialization), and what would happen if the order were reversed. This is the level of understanding that differentiates an Advanced-tier driver reading note from a paraphrase.

### Business & Commercial Layer

Advanced-tier portfolio projects are the gate to mid-level and senior engineering roles at commercial UAV companies, where the starting salary premium for demonstrated Advanced capability is 30–60% above junior-level roles. The specific project that matters depends on the target company's primary engineering domain: Vision-Guided Landing for autonomy companies (Skydio, Zipline, Wing), Multi-Vehicle Coordination for fleet and defense companies (Shield AI, AeroVironment), Embedded/Driver Exploration for hardware-oriented companies (Auterion, Holybro, ideaForge), and JSBSim FDM Study for eVTOL and fixed-wing companies (Joby, Archer, senseFly).

The return on investment for completing one Advanced project to recruiter-runnable quality — 40–80 hours of focused work — is significant. A senior engineer at Wing who reviews your Vision-Guided Landing project and sees clean ArUco detection, a correct coordinate frame chain, measured landing error across 50 SITL trials with documented failure modes and safety assumptions, and a passing CI badge, will recommend you for a technical screen. This is a hiring pathway that does not require a referral, a specific degree, or prior industry experience.

In India, Advanced-tier project quality is currently above the market norm — most UAV software engineer portfolio projects in the Indian market are at the beginner-to-intermediate level. An Advanced-tier portfolio project positions a candidate in the top 5% of applicants for roles at ideaForge, Garuda Aerospace, TSAW Drones, and the DRDO/HAL affiliated UAV programs that require software engineers with demonstrated depth.

### Hiring Signal

**Job titles for Advanced project portfolio holders:**
- **UAV Autonomy Engineer (Mid/Senior)** — at Skydio, Wing, Zipline; Vision-Guided Landing (Project 2) is the direct portfolio evidence
- **Swarm Systems Engineer** — at Shield AI, AeroVironment, defense UAV labs; Multi-Vehicle Coordination (Project 3) is the portfolio evidence
- **Autopilot Firmware Engineer** — at Auterion, Holybro, ideaForge; Embedded/Driver Exploration (Project 4) is the portfolio evidence
- **GNC/Simulation Engineer** — at Joby, Archer, Wisk; JSBSim FDM Study (Project 5) is the portfolio evidence
- **Senior UAV Software Engineer** — at any commercial UAV company; Integration Capstone (Project 1) plus one specialized project demonstrates the integration + depth combination required for senior roles

**Specific interview screens that directly reference Advanced project work:**
1. "You have a Vision-Guided Landing demo with 50 SITL trials showing 0.35m median error. A reviewer says 'how does this scale to real camera noise and lens distortion?' Walk me through your answer."
2. "Describe your multi-vehicle separation monitoring algorithm. What is the minimum information each vehicle needs to share, at what update rate, and what happens when update rate drops to 1 Hz?"
3. "I am cloning your Integration Capstone repo right now. What is the first thing likely to break on my Ubuntu 22.04 machine that your README does not mention?"
4. "Your NuttX driver reading note describes the ICM-42688-P initialization sequence. What would happen if you swapped steps 2 and 3 in the sequence you described?"
5. "In your JSBSim study, you found that increasing wing area by 20% reduced cruise speed. Can you derive that result from the trim equations without running the simulation?"

### Portfolio Projects

**Project 1 hardened: `flight-stack-integration-capstone`**
- Deliverables: A complete integration of PX4 SITL + Micro-XRCE-DDS + ROS 2 autonomy node + MAVSDK mission manager; architecture diagram showing all components and communication links; a 4-waypoint survey mission flown autonomously; pyulog metrics report (mission completion time, max altitude error, EKF innovation RMS, GPS health throughout); Docker image that runs the demo from a single `docker run` command; CI badge from GitHub Actions running a 30-second SITL smoke test
- Acceptance criteria: (1) the Docker image builds and runs the demo on Ubuntu 22.04 without additional configuration; (2) the metrics report is auto-generated by a script from the log file; (3) the architecture diagram correctly shows the data flow from sensor to autopilot to ROS 2 to mission manager

**Project 2 hardened: `vision-guided-precision-landing`**
- Deliverables: ArUco marker detection → body-frame pose estimation → NED setpoint → PX4 offboard landing; 50 SITL trial log showing landing error distribution (median, 90th percentile); explicit documentation of the coordinate frame chain with verification test; failure injection test (marker out of frame at 5m AGL) with documented behavior; safety assumptions document
- Acceptance criteria: (1) landing error median < 0.5m across 50 trials with ≥4 m/s simulated wind; (2) the coordinate frame chain document includes a numerical verification step (expected vs actual pose at a known marker position); (3) the failure injection test demonstrates a defined safe behavior when the marker is lost at low altitude

**Project 3 hardened: `multi-vehicle-coordination-demo`**
- Deliverables: Two-vehicle PX4 SITL with altitude-layer deconfliction, real-time separation monitoring, a leader-follower scenario, and a failure injection test (leader landing during formation); fleet log analysis showing minimum separation over time; GSN safety case for the deconfliction architecture; architecture diagram
- Acceptance criteria: (1) zero separation violations below 10m in the nominal 15-minute mission; (2) the failure injection test produces a defined response (follower hovers, does not track leader to ground); (3) the GSN safety case has at least 3 nodes with evidence references to the actual log files

### Future Trends

- **2026**: Advanced project CI standards rise — GitHub Actions SITL tests become expected rather than optional; projects without CI are at a disadvantage in portfolio reviews
- **2030**: Photorealistic simulation (Unreal Engine + AirSim or Isaac Sim) enables visual navigation projects (Project 2) to be tested under much more realistic lighting conditions in SITL; the gap between SITL and real-world performance for vision projects narrows significantly
- **2035**: Advanced project work transitions from individual portfolio projects to collaborative open-source contributions at scale; multi-engineer open-source UAV projects (not just contributions to existing codebases) become the Advanced portfolio standard
- **2045**: The specific flight stacks and simulation tools are different; the Advanced project discipline — system design, integration across subsystems, failure analysis, safety documentation, recruiter-runnable packaging — remains the hiring gate for senior engineering roles

### Interview Questions

1. **What is the full coordinate frame chain for a vision-guided precision landing system using an onboard camera?**
   *Answer*: The chain has four frames: (1) Image frame (pixel coordinates, origin at top-left, y down); (2) Camera frame (OpenCV convention: Z forward/into scene, X right, Y down, origin at optical center); (3) Body frame (NED convention: X forward, Y right, Z down; or FRD); (4) NED world frame (North=X, East=Y, Down=Z). Transforms: image→camera via camera intrinsic matrix inverse (unprojection); camera→body via extrinsic calibration (rotation matrix from camera mounting, typically derived from `cv2.solvePnP` with known marker geometry); body→NED via the autopilot's attitude quaternion (available from EKF2 or `vehicle_attitude` uORB topic). The full transform: `P_NED = R_body_to_ned × R_cam_to_body × P_cam`.

2. **What does "recruiter-runnable" mean and why is it the Advanced project completion standard?**
   *Answer*: "Recruiter-runnable" means a senior engineer at the target company can clone the repository, follow the README, and have a working demo within 30 minutes, on their own machine, without asking the author any questions. This standard implies: (1) all dependencies are specified (requirements.txt, Docker image, ROS 2 package.xml); (2) the setup steps work from a fresh environment (not just the author's machine); (3) the README describes what to expect and what success looks like; (4) there is a CI badge confirming the build passes on a fresh environment. The alternative — "works on my machine" — means the project cannot be verified independently, which means the hiring manager cannot trust it.

3. **For Project 5 (JSBSim), how do you verify that a trim calculation is physically reasonable?**
   *Answer*: Check four properties: (1) Trim speed is above stall speed by a reasonable margin (typically 1.3× stall or more); (2) Elevator deflection is within the aircraft's physical limits (typically ±25° for a fixed-wing UAV); (3) Throttle is between 0 and 1 (not saturated); (4) Trim pitch angle is consistent with the wing angle of attack at the trim speed (for a conventional aircraft, positive pitch at low speed, near-zero at cruise). If any of these are violated, the aerodynamic model has a physical inconsistency. Common causes: missing propulsion model, incorrect wing area in the XML, or coefficient tables that do not include the trim operating point.

4. **Why does the Integration Capstone architecture document belong in the repo before the first line of code is written?**
   *Answer*: The architecture document forces explicit decisions before implementation: which component handles mission state (if both MAVSDK and a ROS 2 node send mission commands, there is a command conflict); how the coordinate frames are handled at each interface (MAVSDK uses NED, ROS 2 uses ENU by default — the transform must be explicit somewhere); where the safety logic lives (onboard PX4 failsafes, or in the ROS 2 node?). Decisions made implicitly during implementation tend to be inconsistent and create bugs that only appear at component integration points. Writing the document first forces consistency.

5. **What is the minimum acceptable evidence for claiming that a multi-vehicle separation monitoring system works?**
   *Answer*: Three types of evidence: (1) Nominal behavior: a log showing the minimum separation during a 15-minute mission, verified to be above the safety threshold throughout; (2) True positive test: a deliberately constructed scenario where two vehicles approach within the conflict zone, verified to trigger the monitor alert correctly; (3) True negative test: a scenario where two vehicles approach but remain above the safety threshold, verified to not trigger a false alert. Without the true positive test, you do not know if the monitor would detect a real conflict. Without the true negative test, you do not know if the monitor would alert excessively (leading to operators ignoring it). Both are required to claim the system works.

### Further Depth

- **PX4 SITL multi-vehicle documentation** (docs.px4.io/main/en/simulation/multi_vehicle_simulation.html) — Project 3 setup guide
- **px4_ros_com examples** (github.com/PX4/px4_ros_com) — Project 1 and 2 ROS 2 integration reference
- **OpenCV ArUco detection tutorial** (docs.opencv.org/4.x/d5/dae/tutorial_aruco_detection.html) — Project 2 perception pipeline reference
- **JSBSim Python API documentation** (jsbsim-team.github.io/jsbsim) — Project 5 simulation reference
- **PX4 NuttX ICM-42688-P driver source** (github.com/PX4/PX4-Autopilot/tree/main/src/drivers/imu/invensense/icm42688p) — Project 4 reading reference
- **Docker documentation** (docs.docker.com) — containerization for recruiter-runnable packaging; multi-stage builds for ROS 2 + PX4 environments
- **"A Philosophy of Software Design" — John Ousterhout** — architectural thinking applicable to Integration Capstone design; how to reduce complexity in multi-component systems
- **GitHub Actions documentation** (docs.github.com/en/actions) — CI setup; PX4 GitHub Actions workflows at github.com/PX4/PX4-Autopilot/.github/workflows are a reference for SITL CI patterns
