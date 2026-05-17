# Tooling Index

## Core Tooling

- `PX4`
- `ArduPilot`
- `MAVLink`
- `QGroundControl`
- `ROS 2`
- `Gazebo`
- `Git`
- `Docker`

## Simulation and Flight Dynamics

- `SITL`
- `Gazebo Harmonic`
- `Gazebo Jetty`
- `JSBSim`

## Companion and Autonomy

- `ROS 2`
- `colcon`
- `rviz2`
- `pymavlink`

## Perception

- `OpenCV`
- camera calibration tools
- fiducial or marker detectors

## Embedded

- `NuttX`
- cross-compilers
- `i2c-tools`
- `spidev`
- serial tools

## Testing and Operations

- log analyzers
- parameter diff tools
- CI pipelines
- mission rehearsal scripts

---
## 🔧 Industry Enrichment (Appended)
---

## Extended Tooling Reference by Use Case

### Flight Stack Setup and Build

| Tool | Command / Key Usage | Notes |
|------|--------------------|----|
| PX4 SITL Gazebo | `make px4_sitl_default gazebo-classic` | Multi-vehicle: set `NUMSITL=3` |
| PX4 SITL JSBSim | `make px4_sitl_default jsbsim_rascal` | Uses JSBSim FDM instead of Gazebo |
| ArduPilot SITL | `sim_vehicle.py -v ArduCopter --console` | `--count=3` for multi-vehicle |
| PX4 hardware flash | `make px4_fmu-v6x_default upload` | Requires USB, board in bootloader mode |
| colcon build (ROS 2) | `colcon build --symlink-install` | `--packages-select <pkg>` for single package |
| NuttX NSH console | USB serial 57600 baud, `screen /dev/ttyACM0 57600` | `Ctrl+C` to interrupt; `?` for command list |

### Sensor and Autopilot Diagnostics

| Tool | Command | What It Shows |
|------|---------|--------------|
| `uorb top` (NSH) | `uorb top -1` | One-shot topic list with publish rates |
| `listener` (NSH) | `listener sensor_accel -n 10` | 10 IMU samples in real time |
| `ps` (NSH) | `ps` | NuttX task list with stack watermarks |
| `perf` (NSH) | `perf` | Per-driver CPU time: mean, max, count |
| `free` (NSH) | `free` | Heap available and used |
| `i2cdetect` (NSH) | `i2cdetect 1` | Scan I2C bus 1 for responsive devices |
| `param show` (NSH) | `param show EKF2_*` | List all EKF2 parameters |
| QGC MAVLink Inspector | Analyze > MAVLink Inspector | Live MAVLink message rates and values |
| `ros2 topic hz` | `ros2 topic hz /fmu/out/vehicle_local_position` | Message rate from DDS bridge |
| `ros2 topic echo` | `ros2 topic echo /fmu/out/vehicle_status` | Live topic values in terminal |

### Log Analysis

| Tool | Install / Launch | Primary Use |
|------|-----------------|------------|
| Flight Review | review.px4.io or `python3 app.py` (self-hosted) | EKF health plots, vibration, flight path |
| pyulog `ulog_info` | `pip install pyulog && ulog_info flight.ulg` | Log metadata: topics, start time, duration |
| pyulog `ulog2csv` | `ulog2csv flight.ulg -o output_dir/` | Bulk CSV export for pandas analysis |
| PlotJuggler | apt/snap install + drag-and-drop ULog | Deep per-flight investigation with sync cursor |
| QGC Log Download | Analyze > Log Download | Retrieve onboard ULog via MAVLink |
| `mavlogdump.py` | `python mavlogdump.py --type ATT flight.tlog` | ArduPilot DataFlash log message dump |
| pandas + matplotlib | `import pandas as pd` | Fleet-level multi-log comparison and metrics |

### MAVLink and Mission Scripting

| Tool | Install | Key API / Usage |
|------|---------|-----------------|
| MAVSDK Python | `pip install mavsdk` | `System()`, `Mission`, `Action`, `Telemetry`, `Offboard` |
| pymavlink | `pip install pymavlink` | `mavutil.mavlink_connection()`, `recv_match()`, `command_long_send()` |
| MAVProxy | `pip install mavproxy` | `--out` for fan-out routing; `module load` for plugins |
| QGC Plan JSON | Save via QGC > Plan > File | Mission waypoints in GeoJSON-like format; loadable by MAVSDK |
| MAVLink shell | `./Tools/mavlink_shell.py` (PX4 source) | Direct NSH console access over MAVLink without USB serial |

### ROS 2 UAV Integration

| Component | Setup Command | Notes |
|-----------|--------------|-------|
| Micro-XRCE-DDS Agent | `MicroXRCEAgent udp4 -p 8888` | Required before PX4+ROS 2; bridges uORB to DDS |
| px4_ros_com | `git clone && colcon build` | Auto-generated message types; example nodes |
| ROS 2 namespace launch | `ros2 launch pkg node.launch.py namespace:=vehicle_1` | Multi-vehicle isolation |
| TF2 broadcaster | `tf2_ros.TransformBroadcaster` | Publish body→world transforms for rviz2 visualization |
| rviz2 | `ros2 run rviz2 rviz2` | 3D visualization; load config from package `rviz/` directory |
| `rqt_graph` | `ros2 run rqt_graph rqt_graph` | Node and topic connectivity visualization |

### Perception and Computer Vision

| Tool | Install | Key API |
|------|---------|---------|
| OpenCV (with contrib) | `pip install opencv-contrib-python` | Required for `cv2.aruco`; contrib version only |
| `cv2.aruco.ArucoDetector` | OpenCV 4.7+ | `detector.detectMarkers(gray)` → corners, ids |
| `cv2.solvePnP` | OpenCV built-in | Marker pose from 2D-3D point correspondences |
| `cv2.calibrateCamera` | OpenCV built-in | `ret, mtx, dist, rvecs, tvecs` from checkerboard images |
| camera_calibration (ROS 2) | `ros2 run camera_calibration cameracalibrator` | GUI checkerboard calibration; publishes `CameraInfo` |
| ORB-SLAM3 | Build from source | Monocular/stereo SLAM for GPS-denied VIO |
| OpenVINS | ROS 2 package | Visual-inertial odometry; lighter than ORB-SLAM3 |

### Embedded Development

| Tool | Install / Access | Purpose |
|------|-----------------|---------|
| OpenOCD | `sudo apt install openocd` | JTAG/SWD firmware flash and GDB server for STM32 |
| J-Link Commander | Segger download | Alternative to OpenOCD; faster for J-Link probes |
| STM32CubeMX | ST download | Pin-mux and clock tree configuration for new BSP work |
| arm-none-eabi-gdb | `sudo apt install gcc-arm-none-eabi` | Cross-GDB for NuttX thread-aware debugging |
| Saleae Logic 2 | saleae.com/downloads | SPI/I2C/UART waveform capture; verify driver timing |
| `i2c-tools` | `sudo apt install i2c-tools` | Linux-side I2C bus scanning for companion computer peripherals |
| `spidev` Python | `pip install spidev` | Python SPI device access on Linux (RPi / Jetson) |

### Simulation and FDM

| Tool | Install / Launch | Notes |
|------|-----------------|-------|
| JSBSim Python | `pip install jsbsim` | `jsbsim.FGFDMExec()` for scripted simulation |
| JSBSim trim solver | `fdm.do_trim(1)` (Python API) | Returns trimmed state; check for convergence |
| FlightGear + JSBSim | `fgfs --fdm=jsb --aircraft=Rascal110` | 3D visualization of JSBSim flight |
| XFLR5 | xflr5.tech | Wing aerodynamic analysis; exports CLα tables for JSBSim |
| AirSim | Unreal Engine plugin | Photorealistic simulation for vision-heavy projects |

### CI and Packaging

| Tool | Setup | Use |
|------|-------|-----|
| GitHub Actions | `.github/workflows/ci.yml` | Free CI for public repos; build smoke tests and SITL headless runs |
| Docker | `Dockerfile` in repo root | Reproducible environment across OS; required for recruiter-runnable Advanced projects |
| pytest | `pip install pytest && pytest tests/` | Unit and integration tests for Python tooling projects |
| colcon test | `colcon test && colcon test-result` | ROS 2 package test runner |
| pre-commit | `pip install pre-commit && pre-commit install` | Runs clang-format, flake8, trailing-whitespace on commit |

## Tooling Decision Guide

**New to UAV engineering?** Start with: PX4 SITL (Gazebo Classic) → QGC → MAVSDK Python

**Debugging a sensor issue on hardware?** Use: NSH console → `uorb top` → `listener` → `perf` → logic analyzer if timing is suspected

**Analyzing a flight log?** Use: Flight Review (quick overview) → pyulog + pandas (specific metric extraction) → PlotJuggler (deep time-series investigation)

**Building a ROS 2 autonomy node?** Use: Micro-XRCE-DDS agent → px4_ros_com → rclpy → rqt_graph to verify connectivity

**Contributing upstream to PX4?** Use: PX4 GitHub (issue tracker) → local PX4 build → NSH console or SITL to reproduce → `make tests` for CI → PR with clang-format checked

**Building a precision landing system?** Use: OpenCV (contrib) + ArUco → `cv2.solvePnP` → coordinate frame transform → MAVSDK Offboard API → PX4 SITL for integration test

**Fixed-wing or VTOL project?** Use: JSBSim Python API → PX4 JSBSim SITL → PX4 TECS parameter tuning → pyulog for log comparison
