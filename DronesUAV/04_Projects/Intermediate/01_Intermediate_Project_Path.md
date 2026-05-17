# Intermediate Project Path

## Overview

These projects are for learners who already have basic simulation and tooling fluency and want more job-relevant UAV systems work.

## Projects

### Project 1: MAVLink Ground Tool
- arm or disarm
- mode change
- mission upload
- live telemetry dashboard

### Project 2: PX4 or ArduPilot Behavior Change
- run SITL
- modify one behavior
- capture before and after logs

### Project 3: ROS 2 Offboard Demo
- one companion node
- trajectory or waypoint control
- documented safety assumptions

### Project 4: Estimation Benchmark
- synthetic IMU and GPS data
- EKF or UKF toy implementation
- plots and metrics

## Completion Standard

Finish `1-2` with strong documentation, metrics, and reproducible setup.

## Next Step

Move to [Advanced Project Path](../Advanced/01_Advanced_Project_Path.md) when you can explain failure cases, not just success cases.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Intermediate UAV projects are where engineering judgment first becomes visible. At the beginner level, the task is using the stack correctly; at the intermediate level, the task is integrating multiple components and making defensible choices about how they connect. The integration seams — where MAVSDK hands off to ROS 2, where an EKF filter consumes synthetic IMU data, where a behavior change in PX4 must be validated against before-and-after logs — are where engineering competence shows.

Each intermediate project in this path maps to a real engineering task type. The MAVLink Ground Tool mirrors what operations teams at Wing and Zipline use for manual mission management and fleet testing. The PX4 Behavior Change project mirrors what embedded engineers do when validating a controller parameter or failsafe logic change. The ROS 2 Offboard Demo mirrors what autonomy engineers do when testing a new trajectory generation module. The Estimation Benchmark mirrors the educational work that GNC engineers do to understand EKF tuning before modifying production parameters.

The quality bar at the intermediate level is: before-and-after evidence, not just before. An intermediate project without a comparison log, a parameter baseline, or a metric that shows the modification actually changed something in a measurable way is unfinished.

### Industry Tool Stack

- **MAVSDK Python** — for the MAVLink Ground Tool project: `Action` (arm/disarm/mode change), `Mission` (upload/start/monitor), `Telemetry` (live streaming); async Python with `asyncio`
- **pymavlink MAVLink connection** — for lower-level ground tool implementations where MAVSDK's abstraction is too opaque; `master.mav.command_long_send()` for MAV_CMD commands
- **PX4 parameter system** — `QGC > Parameters` for interactive parameter editing; `mavlink param set` for scripted parameter changes; parameter comparison between before/after flight logs via `ulog_info`
- **pyulog** — for before/after log comparison in Project 2; `ulog2csv` for both logs; pandas for aligned comparison on timestamp
- **px4_ros_com + Micro-XRCE-DDS** — for Project 3 (ROS 2 Offboard Demo): sets up the bridge from PX4 SITL to ROS 2; publishes uORB topics as ROS 2 topics
- **rclpy** — ROS 2 Python client library; `Node`, `Publisher`, `Subscription`, `Timer` classes; async spin with `rclpy.spin_once()`
- **NumPy + SciPy** — for Project 4 (Estimation Benchmark): matrix operations for EKF predict/update equations; `scipy.linalg.cholesky` for covariance factorization; `scipy.stats.norm` for synthetic noise generation
- **matplotlib** — for all intermediate project plots: position estimate vs truth, EKF covariance bounds, telemetry time series, before/after controller comparison
- **FlightGear** (optional) — for JSBSim visual validation if running PX4 JSBSim SITL; provides 3D aircraft view during fixed-wing intermediate projects

### Step-by-Step Applied Workflow

1. **Project 1 (MAVLink Ground Tool): Build arm → mode → mission → monitor** — start with the MAVSDK Python mission example; add: (a) a `--vehicle-address` CLI argument to specify the vehicle's UDP port; (b) a pre-flight checks function that verifies GPS fix and battery level before arming; (c) a live telemetry monitor that prints latitude, longitude, altitude, groundspeed, and battery every 2 seconds during the mission; (d) a post-mission summary that prints distance traveled, max altitude, and mission duration.

2. **Project 2 (PX4 Behavior Change): Choose a parameter, hypothesize, test, measure** — pick one of: `MPC_XY_P` (position controller proportional gain), `COM_RC_LOSS_T` (RC loss timeout), or `EKF2_GPS_P_NOISE` (GPS noise assumption). Before testing: write a one-sentence hypothesis ("increasing MPC_XY_P from 0.95 to 1.5 will reduce position tracking error but increase oscillation frequency"). Capture a baseline log. Change the parameter. Capture a second log. Compare using pyulog: extract `vehicle_local_position` from both logs, compute RMS position error and oscillation frequency. Was your hypothesis correct?

3. **Project 3 (ROS 2 Offboard): Connect, control, monitor** — set up PX4 SITL + Micro-XRCE-DDS + rclpy; write a node that subscribes to `/fmu/out/vehicle_local_position` and publishes setpoints to `/fmu/in/trajectory_setpoint`; implement a 4-point square trajectory (10m sides at 5m AGL); monitor the offboard setpoint timeout by deliberately stopping the node and observing the failsafe; document both the successful trajectory and the failsafe behavior.

4. **Project 4 (Estimation Benchmark): Implement EKF for 1D position** — synthetic data: position truth (sine wave at 0.1 Hz), IMU acceleration (numerical derivative of truth + Gaussian noise σ=0.5 m/s²), GPS position (truth sampled at 1 Hz + Gaussian noise σ=2 m). Implement: EKF predict (integrate acceleration), EKF update (fuse GPS when available), covariance propagation. Plot: truth vs estimate vs GPS measurements; covariance bounds as dashed lines around the estimate. Compute RMSE. Change the Q and R matrices and observe how RMSE changes.

5. **Generate comparative plots for Project 2** — the before/after comparison is the evidence. Plot both logs' `vehicle_local_position.x` and `vehicle_local_position.y` vs their respective setpoints on the same axes with different colors; compute and display RMS position error for each in the plot title. This is what "before-and-after evidence" means at the intermediate level.

6. **Write documented safety assumptions for Project 3** — list: maximum setpoint velocity (verify against `MPC_XY_VEL_MAX`), offboard timeout behavior (what failsafe fires when the node crashes), wind conditions (SITL default), GPS availability assumptions, and what would happen if the node published setpoints outside the aircraft's velocity limits.

### AI Integration

At the intermediate level, AI tools have the most value for the implementation scaffolding that is time-consuming but not intellectually core. The EKF implementation in Project 4 requires mathematical understanding (predict/update equations, covariance propagation) that cannot be delegated to an LLM — but the NumPy matrix code that implements those equations can be drafted by an LLM and verified by the engineer. The MAVSDK async Python patterns for Project 1 are verbose but repetitive; LLM generation of the boilerplate is reasonable, but the pre-flight check logic (what constitutes acceptable GPS quality) must come from the engineer.

Specific use case: use an LLM to explain the `MISSION_ITEM_INT` MAVLink message field structure before implementing Project 1's mission upload. The LLM can correctly describe the `frame`, `command`, `lat`, `lon`, `alt`, and `autocontinue` fields from the MAVLink specification — saving 20 minutes of specification reading. Verify one field against the actual spec to calibrate confidence before trusting the rest.

### Case Studies

**Zipline's Simulation-Validated Parameter Tuning Process**: Zipline's GNC team validates every controller parameter change against SITL logs before any hardware flight — a professionally executed version of Project 2. Their tuning workflow: define the metric (delivery accuracy in meters), establish a baseline, change one parameter, run 100 SITL trials, compare metric distributions. This is exactly what Project 2 teaches, scaled to a production team's rigor standard. Their public engineering talks have described this process as the foundational discipline of their flight software team.

**ETH Zürich ASL ROS 2 Offboard Research Platform**: ETH's Autonomous Systems Lab uses a ROS 2 offboard control architecture (structurally identical to Project 3) for researching trajectory optimization and model-predictive control algorithms on Pixhawk-based platforms. Their open-source framework (`px4_ros2_interface_lib`) is a professional extension of what Project 3 teaches — starting with the same XRCE-DDS bridge and offboard setpoint topic pattern and adding sophisticated trajectory generation on top. Studying their repository architecture shows the intermediate project's natural scaling direction.

**mRo Technology Parameter Compliance Tool**: mRo Technology ships a parameter compliance checking tool with their flight controllers that compares loaded parameter files against a recommended baseline and flags deviations that could affect flight safety. This is a production-scale version of Project 2's parameter analysis capability — the same underlying skill (parse parameter files, compare against a baseline, flag significant deviations) deployed as a product-facing feature.

### Failure Modes & Safety

**Offboard setpoint timeout not tested**: Project 3's ROS 2 Offboard Demo is incomplete without testing what happens when the node crashes mid-flight. PX4's offboard timeout (`COM_OF_LOSS_T`) triggers a failsafe — but the failsafe action depends on `COM_OBL_ACT` (hold, return to launch, or land). If the engineer has not verified the failsafe behavior, they cannot claim the system is safe to demonstrate. The fix: deliberately kill the ROS 2 node during a SITL flight and observe the autopilot's response before declaring the demo done.

**EKF implementation with no sanity checks**: A Project 4 EKF implementation that runs without checking whether the covariance matrix remains positive definite can produce numerically unstable results that look plausible but are incorrect — the estimate tracks the truth but with wrong confidence bounds. Adding a `np.linalg.eigvalsh(P).min() > 0` assertion at each timestep catches numerical issues early.

**Before/after comparison with different initial conditions**: Running the baseline and post-change SITL flights with different GPS starting positions, different initial battery levels, or different wind (even zero wind vs the SITL default) confounds the comparison. The parameter change is not the only variable. Intermediate project logs must be collected under identical conditions for the comparison to be valid.

**Using MAVSDK's high-level API without understanding what it does**: `action.arm()` in MAVSDK sends a `MAV_CMD_COMPONENT_ARM_DISARM` command and waits for acknowledgment — but it also implicitly handles some pre-arm checks. An engineer who uses `action.arm()` without knowing this may be confused when it fails with `COMMAND_DENIED` and not know how to debug it (the answer is to check `Telemetry.pre_flight_checks_ok()` first). Understanding the underlying MAVLink protocol prevents black-box debugging.

### Business & Commercial Layer

Intermediate-level UAV project skills map directly to the associate/junior engineer roles that commercial UAV companies hire most frequently. Wing, Zipline, and similar companies scale through teams of mid-level engineers who can integrate components, validate changes against logs, and debug across the software stack — the skills demonstrated in the four intermediate projects.

In India, the intermediate project skill set is the hiring bar for UAV startups in the 10–50 employee range (Throttle Aerospace, TartanSense, AgriDrones India). These teams cannot afford engineers who can only follow tutorials — they need engineers who can modify PX4 behavior for their application, set up ROS 2 offboard control for their sensor suite, and diagnose issues using flight logs. The intermediate project path is calibrated to exactly this bar.

Salary positioning: engineers who can demonstrate intermediate project capabilities (before/after SITL log comparison, ROS 2 offboard control, MAVSDK mission scripting) are competitive for junior UAV software engineering roles at 6–15 LPA in India and $110–130k USD at US companies. The delta to advanced project capability corresponds to approximately 30–50% salary increase in this market.

### Hiring Signal

**Job titles for intermediate project portfolio holders:**
- **UAV Software Engineer (Junior)** — at Wing, Zipline, Joby; intermediate projects demonstrate integration competence and log-analysis discipline
- **Autopilot Integration Engineer** — at enterprise UAV integrators; Project 2 (behavior change with log evidence) is directly relevant
- **ROS 2 Developer (UAV)** — at research labs and autonomy-focused companies; Project 3 demonstrates the integration pattern
- **GNC Engineer (Associate)** — at eVTOL companies; Project 4 demonstrates understanding of state estimation principles

**Specific interview screens for intermediate-level candidates:**
1. "You changed `MPC_XY_P` in your Project 2. Walk me through how you verified the change had the effect you expected. What metric did you use and how did you compute it from the log?"
2. "In your ROS 2 Offboard Demo, what happens if the node crashes 10 seconds into the flight? How did you test this?"
3. "Explain the EKF predict step in your Estimation Benchmark. What matrix is Q and what does it represent physically?"
4. "Your MAVSDK ground tool sends a `MISSION_START` command. What MAVLink message sequence actually happens between that call and the vehicle beginning to fly the mission?"

### Portfolio Projects

**Project 2 hardened: `px4-parameter-tuning-study`**
- Deliverables: A documented SITL parameter tuning experiment: hypothesis, baseline log, changed-parameter log, pyulog-generated comparison plots (before/after position tracking), computed RMSE table, and a one-page interpretation document explaining what the data shows about how the parameter affects behavior
- Suggested repo tree: `README.md`, `docs/hypothesis.md`, `params/baseline.params`, `params/tuned.params`, `logs/baseline.ulg`, `logs/tuned.ulg`, `analysis/comparison.ipynb`, `results/metrics_table.md`
- Acceptance criteria: (1) the comparison plots show aligned time series for both logs; (2) the RMSE table has one row per metric with baseline and tuned values; (3) the interpretation document explicitly states whether the hypothesis was confirmed or refuted and explains why

**Project 3 hardened: `ros2-offboard-square`**
- Deliverables: A ROS 2 node that flies a 10m × 10m square trajectory in PX4 SITL at 5m AGL; includes a deliberately-induced node crash test with documented failsafe behavior; pyulog analysis showing the actual trajectory vs the commanded trajectory; safety assumptions document
- Suggested repo tree: `src/square_offboard/square_offboard/square_node.py`, `launch/square_offboard.launch.py`, `logs/square_flight.ulg`, `analysis/trajectory_comparison.ipynb`, `docs/safety_assumptions.md`, `README.md`
- Acceptance criteria: (1) the trajectory analysis shows the actual path within ±0.5m of the commanded path during steady-state flight; (2) the node crash test demonstrates the defined failsafe behavior (loiter or RTL, as configured) with a log screenshot showing the mode transition; (3) the safety assumptions document includes the offboard timeout value and the failsafe action

**Project 4 hardened: `ekf-estimation-benchmark`**
- Deliverables: A Python notebook implementing a 2D position-velocity EKF with synthetic IMU and GPS inputs; plots of truth vs estimate vs measurements with covariance bounds; a parameter sweep showing how RMSE changes as Q and R matrices are varied; a brief written interpretation of what the sweep shows about EKF tuning
- Acceptance criteria: (1) the EKF implementation is mathematically correct (covariance is positive definite throughout, RMSE is computed against ground truth, not GPS measurements); (2) the parameter sweep produces a clear trade-off visualization (fast but noisy vs slow but smooth); (3) the notebook runs end-to-end with `jupyter nbconvert --execute`

### Future Trends

- **2026**: MAVSDK C++ becomes as approachable as the Python API; intermediate projects using C++ MAVSDK replace Python MAVSDK at companies that need stronger performance guarantees
- **2030**: ROS 2 Jazzy (LTS) and beyond integrate tighter with PX4 via native DDS bridging (eliminating the Micro-XRCE-DDS agent); Project 3's setup becomes simpler; the engineering skill shifts to lifecycle management and quality-of-service tuning
- **2035**: Simulation environments become photorealistic enough that SITL tests are accepted as FAA evidence for certain software changes (the current gap between simulation and flight test evidence narrows); intermediate SITL project discipline becomes formally recognized
- **2045**: The specific tools and APIs change; the intermediate project skill — integration, comparison, measurement — persists as the engineering baseline

### Interview Questions

1. **Explain the asyncio pattern used in MAVSDK Python mission scripts. Why is it async rather than synchronous?**
   *Answer*: MAVSDK Python uses `asyncio` because MAVLink communication involves waiting for responses — an `action.arm()` sends a command and waits for an acknowledgment; a `telemetry.position()` creates an async generator that yields values as they arrive. Synchronous code that blocks on each MAVLink roundtrip would be unable to interleave telemetry monitoring with command sending. The async pattern allows concurrent tasks: one task sends mission commands, another monitors telemetry, a third checks for failsafes — all running concurrently in the same thread via cooperative multitasking.

2. **What does the `COM_OF_LOSS_T` parameter control and what failsafe does it trigger?**
   *Answer*: `COM_OF_LOSS_T` is the offboard mode communication timeout — the number of seconds PX4 waits after the last received offboard setpoint before declaring offboard mode lost. The failsafe action is controlled by `COM_OBL_ACT`: 0 = hold position, 1 = return to launch, 2 = land immediately, 3 = terminate (extreme). Default timeout is 1 second. The typical safe setting for indoor demos (where immediate landing is preferred) is `COM_OBL_ACT=2` (land). For outdoor missions with a safety pilot, `COM_OBL_ACT=1` (RTL) is more appropriate.

3. **What is the difference between Q and R matrices in a Kalman filter?**
   *Answer*: Q is the process noise covariance — it represents uncertainty in the state prediction step (how much we trust the dynamic model). R is the measurement noise covariance — it represents uncertainty in the sensor measurements (how accurate we believe the GPS or IMU to be). A large Q relative to R means the filter trusts measurements more and responds quickly to corrections but is noisier. A small Q relative to R means the filter trusts the model more and is smoother but responds slowly to real changes. Tuning Q and R is the primary mechanism for trading responsiveness against smoothness in EKF behavior.

4. **In your PX4 behavior change project, you collected two logs. How do you align them in time for comparison?**
   *Answer*: PX4 ULog timestamps are microseconds since boot, not wall clock time. Two logs from different flights have different boot times and therefore different timestamp bases. To align them, use `vehicle_local_position.timestamp` relative to the first valid measurement in each log — subtract the first timestamp from all timestamps in each log so both start at t=0. Then resample both to a common time grid (e.g., 10 Hz) using pandas `resample().interpolate()`. Finally, compare by flight phase (take-off, cruise, landing) rather than by absolute time, since the two flights may have different total durations.

5. **Why is a before/after log comparison with two SITL flights more convincing than a single flight where you changed the parameter mid-flight?**
   *Answer*: Changing a parameter mid-flight in SITL introduces a transient disturbance (the parameter change itself affects the controller state temporarily). The log before and after the change contains this transient, making it hard to isolate steady-state behavior. Two separate flights with identical initial conditions (same mission, same GPS starting position, same SITL seed) provide clean before and after samples of steady-state behavior without transition effects. The comparison is cleaner and the evidence is more convincing. The cost is that starting conditions must be carefully controlled to be identical.

### Further Depth

- **MAVSDK Python API reference** (mavsdk.mavlink.io/main/en/) — complete API documentation for `Action`, `Mission`, `Offboard`, `Telemetry`; asyncio patterns and connection setup
- **px4_ros_com repository** (github.com/PX4/px4_ros_com) — auto-generated ROS 2 message types and example subscriber/publisher nodes; the starting point for Project 3
- **Micro-XRCE-DDS Agent** (github.com/eProsima/Micro-XRCE-DDS-Agent) — the DDS agent that bridges PX4 SITL to ROS 2; setup instructions in PX4 docs
- **"Probabilistic Robotics" — Thrun, Burgard, Fox** — the mathematical foundation for Project 4; Chapter 3 covers the Kalman filter derivation and implementation
- **pyulog** (github.com/PX4/pyulog) — essential for Project 2 log comparison; `ULog` class API and available message names
- **NumPy documentation** (numpy.org/doc) — for EKF matrix operations in Project 4; `np.linalg`, `np.random.multivariate_normal`, and array broadcasting
- **PX4 parameter reference** (docs.px4.io/main/en/advanced_config/parameter_reference.html) — complete parameter descriptions; essential for choosing and understanding the parameter changed in Project 2
