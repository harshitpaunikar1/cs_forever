# Drones and UAV Premium Course Module

Level Assumption: `Beginner -> Intermediate -> Advanced`

This module was created from the new `DronesUAV` folder and expanded into a single industry-ready course document. It keeps the roadmap focused on free and open written resources, with emphasis on PX4 or ArduPilot, ROS 2, Gazebo or JSBSim, MAVLink, QGroundControl, OpenCV, embedded systems, and safety-minded testing.

Verification note:

- Official documentation was checked on `2026-04-17` for ROS 2, PX4, ArduPilot, Gazebo, MAVLink, QGroundControl, JSBSim, OpenCV, and NuttX resource availability.
- As of `2026-04-17`, ROS 2 `Kilted Kaiju` is the latest stable release and `Jazzy Jalisco` remains the supported LTS release.
- As of `2026-04-17`, Gazebo `Jetty` is listed as LTS through `September 2030`, while `Harmonic` remains LTS through `September 2028`. For ROS 2 `Jazzy`, official Gazebo guidance still recommends `Harmonic`.

## 1. Topic Overview

Drones and UAV software sits at the intersection of robotics, embedded systems, control, simulation, telemetry, and operational reliability.

- Definition:
  UAV engineering combines autopilot firmware, companion software, communication protocols, simulation, estimation, control, and field operations into a safety-critical flying system.
- Why it exists:
  Companies need autonomous and remotely operated aircraft for inspection, mapping, logistics, defense, agriculture, survey, public safety, and industrial data collection.
- Why companies use it:
  UAV systems create reach, speed, and data collection capability in places that are expensive, dangerous, or slow for people.
- Why it matters in `2026+`:
  The strongest hiring path is still centered on the open-source stack teams actually build on: `PX4` or `ArduPilot`, `ROS 2`, `Gazebo` or `JSBSim`, `MAVLink`, `QGroundControl`, plus strong `C++`, `Python`, Linux, controls, and embedded fundamentals.
- Where it is used in industry:
  ISR platforms, inspection drones, mapping pipelines, warehouse inventory drones, agricultural UAVs, VTOL logistics systems, defense R&D, and autonomy startups.

Text roadmap:

```text
Linux + Git + C++/Python
    -> aerodynamics + electronics + control basics
    -> PX4 or ArduPilot + MAVLink + QGroundControl
    -> Gazebo/JSBSim + SITL
    -> ROS 2 companion compute + offboard control
    -> estimation + perception + logs + testing
    -> embedded/NuttX + fixed-wing/VTOL depth
    -> multi-vehicle systems + portfolio + upstream contribution
```

## 2. Highest-ROI Resource Stack

1. PX4 User and Developer Guide
2. ArduPilot Documentation and Dev Wiki
3. ROS 2 Jazzy Documentation
4. Gazebo Documentation
5. MAVLink Developer Guide
6. QGroundControl Developer Guide
7. MIT Underactuated Robotics
8. OpenCV Official Documentation
9. JSBSim Reference Manual
10. Apache NuttX Documentation

## 3. Best Picks By Career Direction

### Drone Software Engineer

- PX4 or ArduPilot docs
- MAVLink
- QGroundControl
- ROS 2
- Gazebo or JSBSim
- Linux, C++, Python

### UAV Autonomy Engineer

- ROS 2
- PX4 ROS 2 guide
- Underactuated Robotics
- OpenCV docs
- Gazebo or JSBSim
- estimation and control material

### Embedded Flight Software Engineer

- PX4 developer guide
- NuttX docs
- ArduPilot dev docs
- C and C++
- drivers, buses, and RTOS workflows

### GCS / Mission Tooling Engineer

- MAVLink guide
- QGroundControl dev guide
- PX4 and ArduPilot message flows
- Python tooling
- telemetry and log analysis

## 4. Recommended 12-Month Sequence

### Months 1-3

- Linux as daily driver
- Git, CMake, Python packaging, debugging
- C++ refresh
- basic aerodynamics and electronics
- ROS 2 basics
- first simulator loops

### Months 4-6

- MAVLink and QGroundControl
- PX4 or ArduPilot SITL
- autopilot architecture
- one small autopilot modification
- one ROS 2 or telemetry integration

### Months 7-9

- dynamics, control, and state estimation
- OpenCV perception for drones
- multi-vehicle simulation basics
- failure analysis and log reading

### Months 10-12

- one flight-stack integration project
- one perception or simulation project
- one embedded or systems project
- one upstream contribution
- portfolio hardening and interview preparation

## 5. Programming Language Priority

1. `C++`
2. `Python`
3. `Embedded C`
4. `Rust` as a strategic add-on
5. `MATLAB` only when a specific team or control workflow needs it

## 6. Portfolio That Actually Helps Hiring

Build proof that you can:

- run SITL
- modify autopilot behavior
- use MAVLink
- operate and extend QGroundControl or mission tooling
- write ROS 2 integration code
- debug telemetry and logs
- produce reproducible simulation tests

## 7. Core Resource Links

- PX4: <https://docs.px4.io/main/en/>
- PX4 ROS 2 guide: <https://docs.px4.io/main/en/ros2/user_guide>
- ArduPilot docs: <https://ardupilot.org/ardupilot/index.html>
- ArduPilot dev docs: <https://ardupilot.org/dev/index.html>
- ROS 2 Jazzy docs: <https://docs.ros.org/en/jazzy/>
- Gazebo docs: <https://gazebosim.org/docs>
- Gazebo releases: <https://gazebosim.org/docs/all/releases>
- MAVLink guide: <https://mavlink.io/en/index.html>
- QGroundControl guide: <https://docs.qgroundcontrol.com/master/en/qgc-user-guide/>
- QGroundControl dev guide: <https://docs.qgroundcontrol.com/v4.4.3/en/qgc-dev-guide/>
- Underactuated Robotics: <https://underactuated.mit.edu/>
- OpenCV docs: <https://docs.opencv.org/4.x/>
- JSBSim manual: <https://jsbsim-team.github.io/jsbsim-reference-manual/>
- NuttX docs: <https://nuttx.apache.org/docs/latest/index.html>

---
## 🔧 Industry Enrichment (Appended)
---

## 8. Industry Career Lane Mapping

UAV software engineering has five distinct career lanes, each with a different technical emphasis and hiring profile. Choose the lane that matches your background and target company type.

### Lane 1: Autopilot Firmware Engineer (PX4/ArduPilot)
**Technical focus**: NuttX RTOS, STM32H7 hardware, uORB pub/sub, sensor driver authoring, board bring-up, embedded C++  
**Target companies**: Auterion, Holybro, Cube Pilot, mRo Technology, ideaForge (hardware teams), Emlid  
**Key portfolio signal**: A driver reading note tracing a real PX4 sensor driver from `init()` to `orb_publish()`, or a NuttX module built and verified in SITL  
**Interview signature question**: "Walk me through how the ICM-42688-P driver initializes, reads data, and publishes to uORB in PX4."

### Lane 2: UAV Autonomy / Companion Software Engineer
**Technical focus**: ROS 2 (Humble/Jazzy), px4_ros_com, Micro-XRCE-DDS, offboard control, VIO (ORB-SLAM3, OpenVINS), onboard perception  
**Target companies**: Skydio, Wing, Zipline (autonomy team), Shield AI, most autonomy research labs  
**Key portfolio signal**: A ROS 2 offboard project with documented safety assumptions, coordinate frame documentation, and failure injection test results  
**Interview signature question**: "You are writing an offboard controller. The node crashes mid-flight. Walk me through what the autopilot does and how you would design the node to recover."

### Lane 3: Mission Software / GCS Engineer
**Technical focus**: MAVLink protocol (pymavlink, MAVSDK), QGroundControl, mission planning, fleet monitoring, ground station software  
**Target companies**: Wing (ground software team), Zipline (operations software), Garuda Aerospace, government UAV operators  
**Key portfolio signal**: A MAVSDK mission tool with pre-flight checks, live telemetry monitoring, and post-mission log analysis  
**Interview signature question**: "Walk me through the exact MAVLink message sequence when a GCS operator uploads a 5-waypoint mission to a PX4 vehicle."

### Lane 4: GNC / Flight Dynamics Engineer
**Technical focus**: JSBSim aerodynamic modeling, TECS and L1 guidance, EKF state estimation, fixed-wing and VTOL transition dynamics  
**Target companies**: Joby, Archer, Beta Technologies, Wisk, Zipline (GNC team), senseFly  
**Key portfolio signal**: A JSBSim trim analysis study or a TECS parameter tuning experiment with before/after SITL log comparison  
**Interview signature question**: "Explain the EKF2 sensor fusion pipeline in PX4. Name three sensor types it fuses and describe how it detects a faulty sensor."

### Lane 5: UAV Reliability / Safety Engineer
**Technical focus**: Flight log analysis at scale, EKF health monitoring, safety case methodology (GSN), production reliability engineering, FMEA  
**Target companies**: Wing, Zipline, Joby (safety team), BVLOS operators, regulated commercial fleet operators  
**Key portfolio signal**: A demo safety case package with GSN argument, auto-generated metrics report, failure injection test results, and honest limitations  
**Interview signature question**: "Write a GSN safety argument for a new autonomous landing feature. What evidence would you need for each sub-goal?"

## 9. Hiring Screens by Experience Level

### Intern / New Grad Screens
1. "Show me your PX4 SITL setup. Run a 4-waypoint mission and open the log in Flight Review. Tell me what you see."
2. "Write a pymavlink script that monitors battery voltage and prints a warning when it drops below 20%."
3. "What is uORB? How does a PX4 module subscribe to a sensor topic?"
4. "What is the difference between Gazebo Classic and Gazebo Harmonic? Why would you choose one over the other?"
5. "Your ROS 2 node crashes mid-flight. What does PX4 do?"

### Junior / Associate Engineer Screens
1. "A PX4 vehicle arms correctly in QGC but fails to switch to OFFBOARD mode. Walk me through your diagnostic process."
2. "Explain the MAVLink mission upload handshake: MISSION_COUNT → MISSION_REQUEST → MISSION_ITEM_INT → MISSION_ACK. What does each message do?"
3. "Given a ULog from a SITL flight, identify whether the EKF was healthy throughout. What plots and metrics do you look at?"
4. "Write a Python function that loads two PX4 parameter files and returns a list of changed parameters with their before/after values."
5. "A precision landing system using ArUco detection is accurate in SITL but drifts in real flights. Name three possible root causes."

### Mid-Level / Senior Engineer Screens
1. "Describe the PX4 cascaded position controller for multirotors. Name the four loops, their bandwidths, and the uORB topics they read and publish."
2. "A flight log shows `estimator_status.solution_status_flags` transitioning to GPS-denied at t=47s. Walk me through what the EKF is doing at this moment and what the autopilot does in response."
3. "Design a deconfliction algorithm for a 10-vehicle delivery fleet operating in a shared 2km × 2km airspace. What information does each vehicle share, at what rate, and how does the algorithm handle a communication dropout affecting one vehicle?"
4. "You are authoring a PX4 sensor driver for a new barometer. Walk me through the `init()` function implementation, the uORB advertisement, and how you would verify correct operation from the NSH console."
5. "Write the top-level safety goal and two sub-goals for a safety case arguing that a new GPS-denied navigation feature using optical flow is safe to operate below 30m AGL."

## 10. Case Studies — Real-World Engineering Practices

### ideaForge Q-Series: Domestic BVLOS Engineering
ideaForge's Q-series VTOL platform represents the complete UAV engineering stack in a single product: PX4 firmware customized for fuel cell power management, DGCA-compliant remote ID implementation, a BVLOS telemetry link with link budget-managed handoffs, and a safety case package submitted for type certification. Their engineering team spans all five career lanes and demonstrates what the Advanced tier of this curriculum looks like when deployed commercially. Their trajectory — from PX4 SITL demos to DGCA type-certified BVLOS operations — maps exactly to the Foundation → Core → Advanced → Projects progression in this guide.

### Wing Delivery Network: Fleet-Scale Reliability
Wing's delivery network (operating in multiple countries simultaneously with hundreds of flights per day) demonstrates the production end of this curriculum's Operations and Safety section. Their post-flight log processing pipeline, anomaly detection system, and safety reporting infrastructure are the commercial-scale versions of pyulog + pandas + GSN safety case work covered in Core and Advanced. Engineers who have done the log analysis and safety case work in this curriculum are prepared to contribute to these systems from their first week.

### MAVLab TU Delft: Research-to-Open-Source Pipeline
TU Delft's MAVLab demonstrates the research → open-source → community contribution trajectory. Their contributions to PX4 (EKF improvements, VTOL transition controllers), ArduPilot (fixed-wing GNC), and Crazyflie (swarm coordination) are all public on GitHub and are directly used by commercial teams worldwide. The engineering discipline shown in their publications — reproducible simulation methodology, quantitative performance measurement, honest failure analysis — is exactly the portfolio standard described in this curriculum. Studying their open-source repositories provides concrete examples of production-quality UAV engineering work.

## 11. Failure Modes at the Curriculum Level

**Treating each section as independent**: The sections are interdependent. EKF2 behavior (Core/04) is the context for reading a NuttX sensor driver output (Advanced/01). MAVLink mission upload sequence (Core/03) is the foundation for building a multi-vehicle coordinator (Advanced/03). Skipping sections to reach "interesting" Advanced topics leaves gaps that appear in technical interviews.

**Portfolio that demonstrates tools, not judgment**: A portfolio of 10 SITL screenshots without failure analysis, without metrics, and without safety assumptions demonstrates tool usage, not engineering judgment. The question "what did you learn from this?" cannot be answered from a screenshot. Engineering judgment requires having encountered a failure, diagnosed its root cause, and made a design decision based on that diagnosis.

**Optimizing for impression over understanding**: Choosing the most impressive-sounding project (swarm coordination, neural flight controller) before being able to reliably explain the underlying subsystems (EKF2, coordinate frames, MAVLink protocol) produces knowledge that collapses under examination. A senior interviewer at Skydio or Wing can detect this in 10 minutes. The curriculum's section ordering is deliberate — do not skip.

## 12. Compensation Reference (2026)

These ranges reflect market data for UAV software engineering roles at commercial companies.

| Role | US (USD / year) | India (INR LPA) |
|------|----------------|----------------|
| Intern / New Grad | $90k–$120k | 8–18 LPA |
| Junior (1–2 years) | $120k–$145k | 14–25 LPA |
| Mid-Level (3–5 years) | $145k–$185k | 25–45 LPA |
| Senior (5+ years) | $185k–$250k+ | 40–80 LPA |
| Embedded Specialist (NuttX/RTOS) | $170k–$230k | 35–70 LPA |
| eVTOL GNC Engineer | $160k–$220k | 30–65 LPA |
| Safety Case Author (regulated) | $150k–$200k | 28–55 LPA |

Notes: US ranges reflect California/NYC tech market; defense/aerospace may differ. India ranges reflect startup (lower end) to established OEM/defense prime (upper end). The embedded specialist and eVTOL ranges reflect scarcity premiums for skills this curriculum's Advanced section specifically develops.

## 13. Recommended Supplementary Reading

The following books are worth owning alongside this curriculum's online resources:

- **"Small Unmanned Aircraft: Theory and Practice" — Beard and McLain** (BYU, free online): fixed-wing UAV GNC from first principles; covers trim, linearization, Kalman filter, and guidance laws; the academic foundation for Lane 4
- **"Probabilistic Robotics" — Thrun, Burgard, Fox**: EKF, particle filter, and SLAM derivations; the mathematical foundation for the state estimation sections in Core and Advanced
- **"Real-Time Concepts for Embedded Systems" — Qing Li**: RTOS fundamentals (priority, preemption, mutex, semaphore, message queue) before reading NuttX source; essential for Lane 1
- **"Making Embedded Systems" — Elecia White (O'Reilly)**: practical embedded development for hardware-software co-design; covers register-level debugging, driver patterns, and hardware bring-up workflow
- **"A Philosophy of Software Design" — John Ousterhout**: system architecture principles applicable to UAV integration capstone projects; reducing complexity in multi-component systems
- **"The Pragmatic Programmer" — Thomas and Hunt**: engineering discipline reference; "tracer bullets" concept maps directly to simulation-first UAV development
- **"System Safety Engineering and Risk Assessment" — Stephans**: safety engineering methodology applicable to UAV safety cases and BVLOS certification preparation
