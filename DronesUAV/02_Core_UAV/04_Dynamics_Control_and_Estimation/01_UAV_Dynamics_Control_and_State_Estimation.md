# UAV Dynamics Control and State Estimation

## Overview

This page covers the mathematical layer that sits under UAV autonomy: vehicle dynamics, feedback control, and state estimation. The point is not to become a theoretician before you ship code. The point is to make your code less naive.

## Why This Topic Matters

Drone autonomy work falls apart quickly if you cannot reason about stability, disturbance rejection, sensor noise, and state uncertainty.

## Real-World Context / Industry Relevance

Autonomy and GNC roles still value strong C++, simulation, and filtering or controls literacy because vehicles move in the real world, not in clean API diagrams.

## Prerequisites

- basic linear algebra
- basic calculus
- willingness to work with plots and simulation

## Core Terminology

- `PID`: proportional-integral-derivative controller
- `LQR`: linear quadratic regulator
- `EKF`: extended Kalman filter
- `UKF`: unscented Kalman filter
- `state`: the variables describing the vehicle condition

## Mental Model / Big Picture

```text
true vehicle state
    -> noisy sensors
    -> estimator
    -> controller
    -> actuators
    -> changed vehicle state
```

## Main Concepts / Core Concepts

- translational and rotational dynamics
- feedback control
- sensor fusion for IMU and GNSS
- trajectory tracking and disturbance handling

## Step-by-Step Implementation Guide

1. Build a toy dynamic model.
2. Compare a PID baseline with a more structured controller.
3. Fuse noisy sensor data with an estimator.
4. Evaluate stability and error over time.

## Hands-On Example / Mini Project

Implement a PID benchmark and one EKF or UKF toy estimator using simulated IMU and GPS data.

## Best Practices

- start with simple models
- validate with plots
- compare controllers against clear metrics
- separate estimator error from controller error

## Common Pitfalls

- tuning blindly
- believing one clean sim run proves robustness
- mixing modeling error with software error

## Metrics / KPIs / What to Measure

- tracking error
- settling time
- overshoot
- estimator drift
- control effort

## Recommended Resources

- MIT Underactuated Robotics
- PX4 and ArduPilot control docs
- simulator-based experiments

## Practice Exercises

- implement PID on a toy model
- compare LQR reasoning to PID tuning
- estimate pose from noisy synthetic data

## Interview Questions

- What is the difference between control error and state-estimation error?
- Why is a sim-only controller result not enough?

## Portfolio / Resume Application

A repo with controller benchmarks, estimator plots, and clear metrics is strong evidence of real autonomy thinking.

## Next Step

Continue to [OpenCV Perception Precision Landing and Autonomy](../05_Perception_and_Autonomy/01_OpenCV_Perception_Precision_Landing_and_Autonomy.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

UAV dynamics, control, and state estimation are the mathematical backbone of every flight that does not crash. Attitude stabilization, position hold, trajectory tracking, wind disturbance rejection, sensor fusion — all of these depend on a correct understanding of how the vehicle moves and how the estimator maintains confidence in the vehicle's state.

In practice, controls and estimation show up in three distinct engineering contexts. First, **autopilot tuning**: when a multirotor oscillates, undershoots, or fails to hold position in wind, the engineer must understand PID gain relationships, integrator windup, derivative filtering, and the cascade structure (rate → attitude → velocity → position) to fix it systematically rather than guessing. Second, **EKF diagnostics**: when the EKF rejects GPS or the position estimate drifts, the engineer must read `estimator_innovations` and `estimator_status` topics in the log, understand what the innovation threshold means physically, and identify whether the root cause is sensor noise, incorrect noise parameters, or a hardware issue. Third, **custom controller development**: when a vehicle class or autonomy behavior requires a controller that the autopilot does not provide out of the box, the engineer must implement it — typically as a companion-side offboard controller or a PX4 module.

The key shift at this page is from "configure it and it works" to "I understand why it works and can fix it when it does not."

### Industry Tool Stack

- **PX4 EKF2** — the onboard Extended Kalman Filter fusing IMU, GPS, barometer, magnetometer, and external vision; parameters in `EKF2_*` namespace; health monitored via `estimator_status` and `estimator_innovations` uORB topics
- **ArduPilot EKF3** — ArduPilot's equivalent; configured via `EK3_*` parameters; inspected via DataFlash `XKQ` and `XKF` log messages
- **pyulog + pandas + matplotlib** — log analysis for EKF and controller behavior; extract topics, compute derived quantities, plot controller error vs. response
- **scipy.signal** — Python library for control system analysis; use `bode()`, `step_response()`, and `lti()` to analyze PID transfer functions analytically before testing in SITL
- **Gazebo + PX4 SITL** — the simulation environment for controller validation; supports wind injection via `world` files and sensor noise configuration
- **JSBSim** — flight-dynamics model for fixed-wing and VTOL analysis; more accurate aerodynamic models than Gazebo's default physics for non-multirotor vehicles
- **MATLAB / GNU Octave** — optional; useful for Simulink-based controller design if available; Octave is free and covers most control system analysis use cases

### Step-by-Step Applied Workflow

1. **Model a simplified multirotor in Python**: write a Python class representing a quadrotor with 6-DOF dynamics (3 translation, 3 rotation). Implement thrust and torque from four motors. Simulate a step response in position Z to understand settling time and overshoot.
2. **Implement a cascaded PID controller**: outer loop (position → velocity setpoint), inner loop (velocity → attitude setpoint), innermost loop (attitude → rate setpoint). Each loop produces a setpoint for the next. Tune each loop separately in simulation.
3. **Add simulated sensor noise**: add Gaussian noise to the position and velocity outputs of the simulated vehicle. Observe how the PID controller responds to noisy feedback.
4. **Implement a 1D Kalman filter**: fuse a noisy position measurement with IMU-integrated velocity using a simple linear Kalman filter. Compare the filtered state estimate to the noisy measurement and to the true state.
5. **Read EKF2 logs in PX4**: load a SITL flight log in pyulog, extract `estimator_innovations`, and plot the GPS horizontal velocity innovation vs. the innovation gate threshold. Identify any periods where the gate is exceeded.
6. **Tune PX4 attitude gains in SITL**: lower `MC_ROLLRATE_P` to induce sluggish response, then raise it to induce oscillation. Document both behaviors in plots. Find the critically damped setting.
7. **Implement an LQR for the simplified model**: compute the LQR gain matrix using scipy (or by hand), apply it to the toy quadrotor model, and compare the step response to the PID controller. Note the differences in transient behavior.

### AI Integration

AI and machine learning are entering UAV control and estimation at three specific points:

**Learning-based flight control**: reinforcement learning (RL) policies trained in simulation can learn to control a quadrotor directly from IMU and GPS states to motor commands. Systems like Crazyflie's learned controllers (from ETH Zürich's Robotics Systems Lab) and NVIDIA's IsaacGym-based aerial RL work demonstrate that RL can outperform hand-tuned PIDs in specific scenarios (fast aggressive maneuvers, robustness to wind gusts). These are not mainstream in production yet, but are approaching it for non-certified vehicles.

**Neural network-based state estimation**: replacing or augmenting the EKF with neural network estimators (e.g., LSTM-based velocity estimation from IMU alone, or deep VIO replacing the visual odometry frontend). These are used in research and some commercial GPS-denied navigation systems.

**Log-based controller health monitoring**: ML models trained on flight logs can detect patterns preceding controller instability — increasing attitude error variance, changing motor output distribution — before a crash occurs. This is used in fleet safety monitoring at scale.

### Case Studies

**ETH Zürich Robotics Systems Lab (Flying Machine Arena)**: ETH's FMA operates Crazyflie micro-UAVs with custom model predictive control (MPC) and RL-based controllers. Their publications demonstrate aggressive trajectory tracking (flips, fast turns, recovery from large disturbances) that standard PIDs cannot achieve. The underlying engineering — correct dynamics models, rigorous state estimation, and principled control design — is the same discipline described on this page at a more advanced level.

**PX4 EKF2 Development History**: the PX4 EKF2 was developed by Paul Riseborough and the PX4 community over several years, replacing the earlier complementary filter-based attitude estimator with a full 24-state EKF supporting GPS, optical flow, visual odometry, and beacon-based positioning. Reading the EKF2 parameter documentation and the original design notes in the PX4 dev guide is one of the best ways to understand how a production-grade state estimator is structured.

**Zipline Fixed-Wing Autonomy**: Zipline's fixed-wing delivery aircraft use a combination of GPS/IMU fusion, barometric altitude, and wind estimation to navigate reliably in complex terrain (Rwanda's mountainous landscape). Their custom estimator and controller work — not public but described in their engineering blog — reflects the same principles covered here applied to a fixed-wing vehicle with different dynamics and different failure modes than a multirotor.

### Failure Modes & Safety

**EKF divergence from sensor misconfiguration**: the most common EKF failure is not a software bug — it is incorrect noise parameters. If `EKF2_GPS_V_NOISE` (GPS velocity noise) is set too low, the EKF weights GPS too heavily and rejects valid IMU measurements. If set too high, GPS corrections arrive too slowly and the position estimate drifts. Setting these parameters correctly requires understanding the noise characteristics of the specific GPS hardware in use.

**Integrator windup**: a PID controller's integral term accumulates when the vehicle is at its physical limits (maximum motor speed, physical obstruction, strong wind). When the limit is removed, the integrator dumps a large correction that causes the vehicle to overshoot violently. Anti-windup schemes (clamping the integrator when at saturation) are implemented in both PX4 and ArduPilot but require explicit configuration of saturation limits.

**Derivative kick**: when the position setpoint changes suddenly (e.g., a new waypoint is loaded), the derivative term of the position controller produces a large spike because the error changes instantaneously. This causes a sudden attitude command that the vehicle cannot physically execute. The fix is derivative filtering — PX4 implements a low-pass filter on the derivative term (`MC_ROLLRATE_D_*` filter frequency); ArduPilot implements similar filtering in its rate controllers.

**Cascaded controller instability**: in a cascaded PID (position → velocity → attitude → rate), if the inner loop is not faster than the outer loop, the control system can become unstable. The bandwidth hierarchy must be maintained: rate loop bandwidth > attitude loop bandwidth > velocity loop bandwidth > position loop bandwidth. Violating this (e.g., tuning position gains too aggressively before the rate loop is stable) produces oscillations that are difficult to diagnose.

**Magnetic declination misconfiguration**: the EKF uses the magnetometer for heading estimation, which in turn requires correct magnetic declination for the operating location. An incorrect declination produces a systematic heading error that cascades into position errors (the vehicle thinks North is a different direction than it actually is). PX4 auto-configures declination from GPS position; ArduPilot requires manual verification.

### Business & Commercial Layer

Controls and estimation expertise commands a significant premium in the UAV industry because it is rare. Most UAV software engineers can operate an autopilot; few can diagnose an EKF divergence or implement a custom controller. This scarcity makes it a high-value specialization.

**eVTOL industry** (Joby, Archer, Supernal, Lilium-successor programs): eVTOL certification requires rigorous flight dynamics analysis, controller robustness testing, and state estimation reliability under degraded sensor conditions. Controls engineers with UAV backgrounds are among the most sought-after hires in the eVTOL space.

**Defense GNC** (General Dynamics, L3, ideaForge advanced programs): guidance, navigation, and control engineers for defense UAVs need both classical control theory and embedded implementation capability. ArduPilot and PX4's controller architectures are often the starting point for customization.

**Agricultural UAV optimization** (Indian market): agricultural spraying drones need precise position holding and wind disturbance rejection for uniform spray coverage. Garuda Aerospace and similar companies need engineers who can tune estimators and controllers for their specific airframes and operating environments.

### Hiring Signal

**Job titles requiring controls and estimation depth:**
- **Flight Controls Engineer** — at eVTOL companies (Joby, Archer), aerospace primes (Boeing, Airbus UAV programs), and advanced UAV OEMs; requires classical control theory, GNC design, and autopilot implementation experience
- **UAV Autonomy Engineer** — at Skydio, Shield AI; requires EKF understanding, controller architecture, and the ability to diagnose estimation failures from logs
- **Autopilot Firmware Engineer (PX4)** — uORB-level access to EKF2 and controller modules; requires controls and estimation understanding to make meaningful changes
- **Systems Test Engineer (GNC)** — at OEMs and test organizations; designs test cases specifically for controller and estimator robustness, disturbance rejection, and sensor failure response

**Specific interview screens:**
1. "A PX4 multirotor is oscillating in roll at about 15 Hz. The pilot says it started after a propeller change. Walk me through your diagnostic process from first log inspection to solution."
2. "Explain the cascade structure of PX4's multirotor position controller. What does each loop produce as output, and what does it receive as input? What are the bandwidth requirements between loops?"
3. "Given a PX4 log where `estimator_innovations.vel_pos_innov[1]` (East velocity innovation) spikes to 3.5 at timestamp 45s, what does this tell you and what would you investigate?"
4. "Implement a 1D position controller for a quadrotor in Python: given target altitude, current altitude, and current vertical velocity, output a thrust increment. Include an integrator with anti-windup."
5. "What is the difference between an EKF and a complementary filter for attitude estimation? When would you use one over the other, and what are the failure modes of each?"

### Portfolio Projects

**Beginner: `pid-controller-benchmark`**
- Deliverables: Python simulation of a 1D quadrotor altitude controller comparing P, PD, and PID with anti-windup; plots showing step response (settling time, overshoot, steady-state error) for each; matplotlib output with labeled axes
- Suggested repo tree: `README.md`, `src/quadrotor_1d.py`, `src/pid_controller.py`, `analysis/compare_controllers.py`, `outputs/`, `requirements.txt`
- Acceptance criteria: (1) simulation produces step responses for all three controller types; (2) plots clearly show the improvement from P to PD to PID; (3) anti-windup effect is demonstrated with a saturation case

**Intermediate: `ekf-sensor-fusion-demo`**
- Deliverables: Python simulation fusing noisy GPS position and IMU acceleration for 2D position estimation using a linear Kalman filter; comparison of filtered estimate vs. raw GPS vs. IMU-only integration; plots showing RMS error for each; configurable noise parameters
- Suggested repo tree: `README.md`, `src/kalman_filter.py`, `src/sensor_simulation.py`, `analysis/fusion_comparison.py`, `outputs/`, `config/noise_params.yaml`
- Acceptance criteria: (1) Kalman filter outperforms both raw GPS and IMU-only integration in RMS position error; (2) plots show all three traces with error bounds; (3) noise parameter changes produce the expected qualitative effects

**Advanced: `px4-ekf-diagnostics-tool`**
- Deliverables: Python CLI tool loading PX4 `.ulg` logs, extracting EKF2 innovation and status topics, computing a per-flight health score (fraction of time innovations are within gate), plotting innovations vs. gates, and flagging flights that fail the health threshold; batch-processable over a log directory
- Suggested repo tree: `README.md`, `src/ekf_diagnostics.py`, `data/sample_logs/`, `reports/`, `requirements.txt`
- Acceptance criteria: (1) tool runs on any well-formed PX4 SITL log; (2) health score is correctly computed and matches manual inspection; (3) batch mode processes all `.ulg` files in a directory and generates a summary CSV

### Future Trends

- **2026**: Adaptive control and online parameter identification (the ability of the autopilot to estimate and compensate for changing vehicle dynamics — battery depletion, propeller damage, payload change) become standard features in PX4 and ArduPilot. Engineers who understand control theory can contribute to and evaluate these features.
- **2030**: RL-based flight control for high-performance maneuvers reaches commercial deployment for non-safety-critical applications. Classical control remains dominant for certified BVLOS operations because RL policies are not yet certifiable under existing regulatory frameworks.
- **2035**: Uncertainty-aware control (tube-based MPC, robust LQR, probabilistic EKF extensions) becomes a standard expectation for vehicles operating in adversarial or uncertain environments. Engineers who understand the underlying mathematics adapt to these tools faster.
- **2045**: The fundamental physics of flight control — dynamics, stability, disturbance rejection — does not change. Engineers who built their understanding on correct physical intuition and principled mathematical tools remain relevant regardless of how the tooling evolves.

### Interview Questions

1. **Explain the cascade controller structure in PX4's multicopter position controller. What are the four loops, what does each produce, and what is the bandwidth requirement between them?**
   *Answer*: The four loops from outermost to innermost are: (1) Position loop — takes position setpoint and current position, outputs velocity setpoint; bandwidth ~1–2 Hz. (2) Velocity loop — takes velocity setpoint and current velocity (from EKF), outputs attitude setpoint (tilt angle); bandwidth ~3–5 Hz. (3) Attitude loop — takes attitude setpoint and current attitude (from EKF), outputs body rate setpoint; bandwidth ~10–15 Hz. (4) Rate loop — takes rate setpoint and current rate (from IMU gyro), outputs motor torque commands; bandwidth ~30–60 Hz. Each loop must have at least 3–5× higher bandwidth than the outer loop for stable cascade behavior.

2. **A PX4 vehicle is drifting 2 m North during a position hold with no wind. What are the top three causes and how do you use the log to distinguish them?**
   *Answer*: (1) Magnetometer heading error — check `estimator_status.mag_innov` in the log; a systematic heading offset of even 2° translates to position drift when the velocity controller acts on the wrong direction. (2) GPS position offset — check `estimator_innovations.vel_pos_innov[2:4]` (North and East position innovations); large values indicate GPS position is inconsistent with the inertial estimate. (3) Wind compensation misconfiguration — check if EKF2 wind estimation is enabled (`EKF2_ARSP_THR`) and if the vehicle's airspeed sensor (if any) is calibrated. Plot `vehicle_local_position.x` (North) vs. time to confirm the drift rate.

3. **What is the difference between P, PD, and PID control, and when would you use each for UAV attitude control?**
   *Answer*: P (proportional) produces output proportional to error — simple, but causes steady-state error in the presence of disturbances and slow response to setpoint changes. PD adds a derivative term that damps oscillations and improves step response, but amplifies sensor noise in the derivative term. PID adds an integral term that eliminates steady-state error by accumulating the error over time. For UAV rate control, PD or PID with derivative filtering is standard — the derivative term helps with overshoot, the integral eliminates steady-state error from motor imbalance or gravity components. Integral windup protection is mandatory.

4. **What is IMU pre-integration and why does it matter for EKF performance at high rates?**
   *Answer*: IMU measurements arrive at 1000 Hz or higher, while the EKF update loop runs at 100–250 Hz. IMU pre-integration accumulates (integrates) the raw IMU samples between EKF updates into a single equivalent delta-velocity and delta-angle, which the EKF then uses as a single high-confidence prediction step. Without pre-integration, the EKF would need to run at IMU rate (too slow to implement in practice) or subsample IMU data (losing precision). PX4's EKF2 uses IMU pre-integration; it is a fundamental technique in all production-grade state estimators.

5. **A companion computer is sending position setpoints to PX4 via OFFBOARD mode. The vehicle tracks the setpoints but oscillates at ~2 Hz. The oscillation disappears when the setpoint is constant. What is likely causing this?**
   *Answer*: The most likely cause is setpoint jitter or quantization: if the companion publishes position setpoints that change slightly on every message (due to floating-point noise, coordinate frame rounding, or an upstream sensor measurement that is not filtered), the velocity controller sees a rapidly changing setpoint and responds with rapidly changing attitude commands. The solution is to add a low-pass filter on the companion-side setpoint before publishing, or to increase the position controller's setpoint filtering (`MPC_XY_VEL_MAX` is not the fix — the setpoint generation is the issue). Alternatively, switch to publishing velocity setpoints rather than position setpoints if the position source is noisy.

### Further Depth

- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain (Princeton University Press); chapters 5–11 cover rigid body dynamics, feedback control, state estimation, and path planning at exactly the right level for UAV software engineers
- **PX4 EKF2 Tuning Guide** (docs.px4.io/main/en/advanced_config/tuning_the_ecl_ekf.html) — the definitive guide to EKF2 configuration, health monitoring, and failure diagnosis
- **MIT Underactuated Robotics** (underactuated.mit.edu) — Russ Tedrake's open textbook and lectures; covers LQR, trajectory optimization, and nonlinear control at a level directly applicable to UAV controls
- **Stengel — Optimal Control and Estimation** (R. Stengel, Princeton University Press) — rigorous treatment of the Kalman filter theory underlying EKF2; dense but comprehensive
- **scipy.signal documentation** (docs.scipy.org/doc/scipy/reference/signal.html) — `bode()`, `lti()`, and `step()` for control system analysis in Python without MATLAB
- **PX4 Multicopter Control Architecture** (docs.px4.io/main/en/flight_stack/controller_diagrams.html) — block diagrams of the full cascade controller architecture
