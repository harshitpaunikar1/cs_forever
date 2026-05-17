# Course Index

## Highest-ROI UAV Resources

1. [PX4 User Guide](https://docs.px4.io/main/en/)
1. [PX4 ROS 2 User Guide](https://docs.px4.io/main/en/ros2/user_guide)
1. [ArduPilot Documentation](https://ardupilot.org/ardupilot/index.html)
1. [ArduPilot Dev Wiki](https://ardupilot.org/dev/index.html)
1. [ROS 2 Jazzy Documentation](https://docs.ros.org/en/jazzy/)
1. [Gazebo Docs](https://gazebosim.org/docs)
1. [Gazebo Releases](https://gazebosim.org/docs/all/releases)
1. [MAVLink Developer Guide](https://mavlink.io/en/index.html)
1. [QGroundControl Guide](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/)
1. [QGroundControl Dev Guide](https://docs.qgroundcontrol.com/v4.4.3/en/qgc-dev-guide/)
1. [MIT Underactuated Robotics](https://underactuated.mit.edu/)
1. [OpenCV Docs](https://docs.opencv.org/4.x/)
1. [JSBSim Reference Manual](https://jsbsim-team.github.io/jsbsim-reference-manual/)
1. [Apache NuttX Documentation](https://nuttx.apache.org/docs/latest/index.html)

## 2026 Status Note

Official docs checked on `2026-04-17` show:

- ROS 2 `Kilted Kaiju` is the latest stable release.
- ROS 2 `Jazzy Jalisco` is the current supported LTS release.
- Gazebo `Jetty` is listed as an LTS release through `September 2030`.
- Gazebo `Harmonic` remains LTS through `September 2028` and is still the recommended Gazebo pairing for ROS 2 `Jazzy`.

---
## 🔧 Industry Enrichment (Appended)
---

## Extended Resource Index by Topic

### PX4 Autopilot
- [PX4 Developer Guide](https://docs.px4.io/main/en/) — primary reference for all PX4 development; SITL setup, parameter reference, module authoring, uORB documentation
- [PX4 GitHub](https://github.com/PX4/PX4-Autopilot) — source code; issue tracker for `good first issue` upstream contributions; PR history shows recent changes
- [PX4 discuss forum](https://discuss.px4.io) — community Q&A; search before posting; `dev` tag for engineering questions
- [Flight Review](https://review.px4.io) — web-based ULog analysis; upload `.ulg` files for EKF health, vibration, and flight path plots
- [PX4 Flight Log Analysis Guide](https://docs.px4.io/main/en/log/flight_log_analysis.html) — official log analysis methodology; covers pyulog, Flight Review, and PlotJuggler
- [pyulog](https://github.com/PX4/pyulog) — Python ULog parser; `ulog2csv`, `ulog_info`, and the `ULog` class for programmatic log analysis

### ArduPilot
- [ArduPilot Developer Wiki](https://ardupilot.org/dev/) — development guide for ArduCopter, ArduPlane, ArduRover; driver architecture, module system, `sim_vehicle.py`
- [ArduPilot GitHub](https://github.com/ArduPilot/ardupilot) — source; AP_Scheduler, AP_HAL, DataFlash log format
- [Mission Planner](https://ardupilot.org/planner/) — ArduPilot GCS; log analysis tab reads DataFlash binary logs; parameter tree
- [mavlogdump.py](https://github.com/ArduPilot/pymavlink/blob/master/tools/mavlogdump.py) — DataFlash log parser from pymavlink; equivalent of pyulog for ArduPilot logs

### MAVLink and SDKs
- [MAVLink Developer Guide](https://mavlink.io/en/) — message definitions, protocol specification, serialization; `common.xml` message set
- [MAVLink message reference](https://mavlink.io/en/messages/common.html) — all common message fields and types
- [MAVSDK GitHub](https://github.com/mavlink/MAVSDK) — C++ SDK; Python bindings at github.com/mavlink/MAVSDK-Python; API docs at mavsdk.mavlink.io
- [pymavlink](https://github.com/ArduPilot/pymavlink) — low-level Python MAVLink library; `mavutil.mavlink_connection()`, `recv_match()`, `mav.command_long_send()`
- [MAVSDK Python examples](https://github.com/mavlink/MAVSDK-Python/tree/main/examples) — reference implementations for mission, offboard, telemetry, multi-vehicle

### ROS 2 and Companion Compute
- [ROS 2 Jazzy documentation](https://docs.ros.org/en/jazzy/) — current LTS reference; node, topic, service, action, lifecycle node APIs
- [px4_ros_com](https://github.com/PX4/px4_ros_com) — PX4 ROS 2 package with auto-generated message types from uORB; example subscriber/publisher nodes
- [Micro-XRCE-DDS Agent](https://github.com/eProsima/Micro-XRCE-DDS-Agent) — DDS bridge from PX4 SITL or hardware to ROS 2; setup required before any PX4+ROS 2 work
- [mavros](https://github.com/mavlink/mavros) — MAVLink-to-ROS 2 bridge; used for ArduPilot+ROS 2 and some PX4 configurations; being superseded by px4_ros_com for PX4

### Simulation
- [Gazebo Harmonic docs](https://gazebosim.org/docs/harmonic/) — current LTS Gazebo; sensor models, plugin API, world file format
- [JSBSim reference manual](https://jsbsim-team.github.io/jsbsim-reference-manual/) — aerodynamic coefficient model, aircraft XML format, trim solver, Python API
- [JSBSim GitHub](https://github.com/JSBSim-Team/jsbsim) — source; reference aircraft models (Rascal 110, Cessna 172); Python API documentation
- [PX4 JSBSim SITL](https://docs.px4.io/main/en/simulation/jsbsim.html) — setup guide for running PX4 SITL with JSBSim as the flight dynamics backend
- [AirSim](https://github.com/microsoft/AirSim) — photorealistic Unreal Engine-based simulation; useful for vision-based projects where Gazebo visual fidelity is insufficient

### Perception and Computer Vision
- [OpenCV documentation](https://docs.opencv.org/4.x/) — complete API reference; ArUco detection at `d5/dae/tutorial_aruco_detection.html`
- [OpenCV camera calibration tutorial](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html) — checkerboard calibration workflow; `calibrateCamera`, reprojection error, distortion coefficients
- [ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB-SLAM3) — monocular/stereo/RGB-D SLAM; GPS-denied navigation; works with ROS 2 wrappers

### Embedded and RTOS
- [Apache NuttX documentation](https://nuttx.apache.org/docs/latest/) — official RTOS reference; POSIX subset API, task scheduling, file system, UART/SPI/I2C drivers
- [PX4 NuttX driver guide](https://docs.px4.io/main/en/hardware/porting_guide_nuttx.html) — how to port PX4 to a new NuttX board; BSP structure and requirements
- [OpenOCD documentation](https://openocd.org/doc/html/) — JTAG/SWD debug interface; STM32 target configuration; GDB server for live hardware debugging

### Safety and Regulation
- [EASA SORA](https://www.easa.europa.eu/en/domains/drones/sora) — European BVLOS risk assessment framework; structured safety argument methodology for regulatory submission
- [FAA BVLOS ARC Report](https://www.faa.gov/uas/advanced_operations/beyond_visual_line_of_sight) — US BVLOS safety evidence requirements; waiver application guidance
- [DGCA Digital Sky](https://digitalsky.dgca.gov.in) — India drone registration and operational approval; BVLOS notification filing
- [GSN Community Standard v3](https://scsc.uk/r141C) — Goal Structuring Notation specification; free PDF; the reference for safety case argument structure

### Academic and Textbook References
- [Beard and McLain — Small Unmanned Aircraft](https://uavbook.byu.edu) — BYU textbook covering fixed-wing UAV GNC; free online; covers trim, linearization, PID/LQR design
- [MIT Underactuated Robotics](https://underactuated.mit.edu) — Russ Tedrake's course; covers trajectory optimization, LQR, model-predictive control; applicable to advanced UAV GNC
- [Probabilistic Robotics — Thrun, Burgard, Fox](http://www.probabilistic-robotics.org) — Kalman filter, EKF, particle filter derivations; foundational reference for state estimation understanding
- [ETH ASL publications](https://asl.ethz.ch/research/research-interests.html) — fixed-wing, VTOL, and swarm UAV research; open-access papers with simulation methodology

## How to Use This Index

- **Setting up for the first time**: PX4 User Guide → Gazebo docs → MAVSDK Python examples
- **Debugging a SITL flight**: Flight Review upload → pyulog extraction → PX4 discuss search
- **Writing a ROS 2 node**: ROS 2 Jazzy docs → px4_ros_com examples → Micro-XRCE-DDS setup
- **Starting an upstream contribution**: PX4 GitHub issues (filter: `good first issue`) → PX4 discuss (confirm approach) → PX4 Contribution Guide
- **Preparing a safety case**: GSN Community Standard → EASA SORA (for structure reference) → pyulog (for evidence collection)
- **Fixed-wing or VTOL project**: JSBSim reference manual → Beard and McLain (GNC theory) → PX4 JSBSim SITL guide
