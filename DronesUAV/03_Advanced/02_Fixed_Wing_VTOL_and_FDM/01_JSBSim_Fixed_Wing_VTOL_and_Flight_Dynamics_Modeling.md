# JSBSim Fixed-Wing VTOL and Flight Dynamics Modeling

## Overview

This page moves deeper into aircraft modeling, especially for fixed-wing and VTOL systems where intuition from a simple multirotor no longer covers enough ground.

## Why This Topic Matters

Teams working on fixed-wing or VTOL systems need stronger flight-dynamics reasoning and more credible simulation than generic “drone sim” knowledge provides.

## Core Concepts

- flight dynamics models
- aircraft configuration files
- trim and stability concepts
- control-surface and propulsion interactions
- scenario-driven simulation

## Hands-On Example / Mini Project

Use JSBSim to analyze a simple fixed-wing or VTOL scenario and document how model assumptions affect behavior.

## Best Practices

- state the assumptions of the model
- compare results across scenarios
- keep simulation outputs tied to engineering questions

## Common Pitfalls

- trusting a model without understanding its assumptions
- confusing simulator convenience with flight-dynamics fidelity

## Next Step

Continue to [Multi-Vehicle Simulation Coordination and Testing](../03_Multi_Vehicle_and_Fleet_Systems/01_Multi_Vehicle_Simulation_Coordination_and_Testing.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

JSBSim is an open-source flight dynamics model (FDM) engine originally developed for flight training simulators and adopted by the aerospace community for UAV and eVTOL simulation. Unlike Gazebo's generic rigid-body physics, JSBSim models aerodynamic coefficients explicitly — lift, drag, pitching moment, and their derivatives with respect to angle of attack, sideslip, control surface deflection, and airspeed. This makes it accurate for fixed-wing aircraft across a wide flight envelope and indispensable for VTOL transition analysis, where both multirotor and fixed-wing aerodynamics interact.

In a real fixed-wing UAV program, the FDM workflow begins before any hardware is built: aerodynamicists generate coefficient tables (CLα, CDα, Cm curves) from CFD analysis or wind tunnel tests; these are encoded in JSBSim XML configuration files; simulation engineers run trim and stability analyses; GNC engineers use the trimmed model to tune control surfaces and autopilot gains; flight test engineers use JSBSim predictions to establish envelope expansion protocols that bound the risk of first flights.

PX4's SITL integrates with JSBSim as a flight dynamics backend (alongside Gazebo), making it possible to test the full autopilot stack — EKF2, fixed-wing position controller, TECS (Total Energy Control System), L1 guidance — against aerodynamically accurate aircraft models before committing to hardware. This is the simulation-first culture: every parameter that goes into TECS (pitch time constant, speed weight, altitude weight) is validated in JSBSim before a test flight.

VTOL transition modeling is where JSBSim earns its keep in advanced programs. A tilt-rotor or tailsitter undergoing transition from multirotor to fixed-wing mode passes through a flight envelope region where neither aerodynamic model alone is accurate — JSBSim allows blending of multirotor thrust tables and fixed-wing aerodynamic coefficients as a function of airspeed and rotor tilt angle, producing a model that captures the actual transition behavior.

### Industry Tool Stack

- **JSBSim** (open-source) — aerodynamic coefficient-based flight dynamics engine; Python API (`import jsbsim`) and C++ library; XML-based aircraft configuration; trim solver and stability analysis tools built in
- **PX4 JSBSim SITL backend** — `make px4_sitl_default jsbsim` launches PX4 SITL with JSBSim as the physics engine instead of Gazebo; communicates via the JSBSim FDM protocol over UDP
- **FlightGear** — open-source flight simulator that can use JSBSim as its FDM; provides 3D visualization of JSBSim simulation; useful for visual validation of flight behavior
- **OpenVSP** (NASA) — parametric aircraft geometry tool; can export aerodynamic geometry to vortex-lattice method (VLM) solvers that feed into JSBSim coefficient tables
- **XFLR5 / XFOIL** — 2D and 3D panel method aerodynamic analysis for airfoil and wing design; produces CLα and CDα data for JSBSim input
- **MATLAB/Simulink** (with Aerospace Toolbox) — used at aerospace primes for system identification, state-space linearization around trim points, and generating Bode plots for stability analysis; JSBSim outputs feed Simulink plant models
- **PX4 TECS** — Total Energy Control System; the fixed-wing speed-altitude controller in PX4; its parameters (TECS_TIME_CONST, TECS_THR_DAMP, TECS_SPDWEIGHT) are tuned against JSBSim simulation before flight
- **ArduPlane** — ArduPilot's fixed-wing autopilot; uses JSBSim via the `--model jsbsim` flag in `sim_vehicle.py`; TECS implementation parallels PX4's
- **Aerosonde, Rascal 110 XML models** — reference JSBSim aircraft models included in the JSBSim repository; used as starting points for custom UAV models
- **pyFDM / JSBSim Python API** — `jsbsim.FGFDMExec` Python class for scripted simulation runs; enables batch parameter sweeps and automated stability analysis

### Step-by-Step Applied Workflow

1. **Install JSBSim and run the reference Rascal 110 model** — `pip install jsbsim` or build from source; run `python -c "import jsbsim; fdm = jsbsim.FGFDMExec('.'); fdm.load_model('Rascal110-JSBSim'); fdm.run_ic()"` to confirm installation; observe the initial state output.

2. **Examine the Rascal 110 aircraft XML** — navigate to `JSBSim/aircraft/Rascal110-JSBSim/Rascal110-JSBSim.xml`; read the `<aerodynamics>` section and identify the lift coefficient table (CLα as a function of angle of attack) and drag polar; understand the `COEFF` naming convention.

3. **Run a trim calculation** — use the JSBSim Python API to trim the Rascal at cruise speed (25 m/s, 100 m AGL); record the trimmed pitch angle, throttle setting, and elevator deflection; verify these are physically reasonable (pitch ~2°, throttle ~50%, elevator ~−2°).

4. **Perturb one aerodynamic parameter and re-trim** — increase the wing area by 20% in the XML and re-run the trim; observe how cruise speed, pitch, and throttle change; document the relationship between wing loading and trim state.

5. **Connect JSBSim to PX4 SITL** — run `make px4_sitl_default jsbsim_rascal` (or equivalent for your PX4 version); connect QGC; send a waypoint mission; observe how TECS manages airspeed and altitude using the aerodynamically accurate model.

6. **Tune TECS parameters against the JSBSim model** — adjust `TECS_TIME_CONST` (pitch time constant) and `TECS_SPDWEIGHT` (speed vs altitude priority); run the same waypoint mission after each change; compare altitude tracking error using `flight_path_angle` and `airspeed` from PX4 logs.

7. **Model a VTOL transition scenario** — if using a tailsitter or tilt-rotor configuration, add thrust vector tables to the JSBSim model XML; simulate a transition by ramping airspeed from hover (0 m/s) to cruise (20 m/s) and observing the aerodynamic force transition; plot lift and thrust as a function of time.

8. **Document trim envelope** — run trim calculations across the flight envelope (15–35 m/s in 5 m/s steps, 50–300 m AGL); produce a table of trim states; identify the stall speed and the maximum level-flight speed; this document is the first artifact in a flight test safety envelope.

### AI Integration

AI is entering flight dynamics modeling from two directions. The first is ML-based aerodynamic coefficient generation: instead of running CFD simulations (which take hours per operating point) or wind tunnel tests (which are expensive and limited in sweep resolution), neural networks trained on CFD data can predict lift and drag coefficients across the full operating envelope from geometry parameters alone. Research groups at DLR and ETH Zürich have published surrogate aerodynamic models for UAV configurations that run orders of magnitude faster than CFD while achieving 5–10% accuracy relative to ground truth.

The second direction is system identification from flight data. Rather than building an aerodynamic model from first principles, neural networks and Gaussian process regression can be trained on actual flight data (IMU, airspeed, GPS, control surface deflections) to learn the aircraft's aerodynamic behavior empirically. This approach is used by advanced programs where the aircraft's geometry is complex or partially proprietary — you do not need the exact aerodynamic theory if you can observe input-output behavior across a sufficient range of conditions.

For engineers without access to ML infrastructure, AI tools have narrower but still useful applications: LLMs can help interpret JSBSim XML schemas and coefficient naming conventions (CLadot, Cmq, etc.); they can generate Python scripts for batch parameter sweeps; they can draft stability analysis reports from trim calculation data. These are productivity multipliers, not aerodynamic modeling replacements.

### Case Studies

**Zipline Fixed-Wing Delivery Drone Simulation Pipeline**: Zipline's Zip fixed-wing delivery drone (which operates at 100+ km/h over range-limited corridors in Rwanda, Ghana, and the US) validates new software releases against aerodynamically faithful JSBSim-based simulation before any hardware flight. Their engineering team maintains a custom JSBSim model of the Zip that is continuously updated from system identification runs on flight data. TECS parameters, L1 guidance gains, and landing approach profiles are all pre-validated in simulation. This is publicly documented in Zipline engineering blog posts and conference presentations.

**PX4 VTOL Fixed-Wing Transition Controller Development**: The PX4 community's fixed-wing VTOL transition controller (used on platforms like the WingtraOne surveying drone) was developed and validated using JSBSim. The transition logic — blending multirotor thrust with increasing airspeed, pitching forward progressively, and switching from multirotor attitude control to fixed-wing position control — was iterated in JSBSim simulation across hundreds of transition profiles before hardware testing. The PX4 VTOL controller PR history on GitHub documents this simulation-first development process.

**ETH Zürich Autonomous Systems Lab Fixed-Wing UAV Research**: ETH ASL's work on fixed-wing UAV aerobatics and aggressive maneuver planning uses JSBSim-derived aerodynamic models as the plant model for model predictive control (MPC). By accurately capturing the coupling between airspeed, angle of attack, and control surface effectiveness, their MPC can plan roll reversals and split-S maneuvers that would be impossible to program with a simplified kinematic model. Their publications use JSBSim coefficient tables validated against wind tunnel measurements.

### Failure Modes & Safety

**Trim calculation divergence**: JSBSim's built-in trim solver can fail to converge if the initial conditions are outside the aircraft's feasible trim envelope or if the aerodynamic model has discontinuities in the coefficient tables. The symptom is a trim solution with extreme control surface deflections (elevator at 25°, full throttle) that are physically implausible. The fix is to check the coefficient tables for monotonicity around the trim point and to verify that the trim airspeed is above stall speed with margin.

**Coefficient table extrapolation errors**: JSBSim interpolates aerodynamic coefficients from lookup tables and extrapolates linearly beyond the table boundaries. If a simulation explores an angle of attack beyond the table range (e.g., post-stall), JSBSim's linear extrapolation produces non-physical forces. This is a silent error — JSBSim does not warn that it is extrapolating. Engineers must explicitly bound the simulation operating envelope within the table boundaries.

**Conflating JSBSim fidelity with Gazebo fidelity**: Gazebo's default aircraft models use simplified aerodynamics (constant lift-curve slope, no stall model, no control surface coupling) that are adequate for multirotor hover simulation but produce optimistic results for fixed-wing simulation. Engineers who tune TECS parameters against Gazebo and then test against JSBSim (or hardware) often find that the controller is overtuned — the Gazebo plant was too easy to control. The fix is to use JSBSim for fixed-wing and VTOL parameter tuning from the start.

**Ignoring propwash effects on empennage**: Tractor-configuration fixed-wing UAVs have significant propeller slipstream effects on the horizontal and vertical stabilizer effectiveness — the elevator is more effective when the propeller is running than when it is stopped. JSBSim can model propwash effects (via `<propwash_to_ht>` configuration), but this requires correct propulsion model setup. Teams that ignore propwash in simulation find that their pitch controller behaves differently at high throttle vs low throttle settings in flight.

**Missing VTOL transition stall risk**: VTOL transitions that accelerate through stall speed while in multirotor mode (still pitching at high angle of attack) can produce a momentary stall of the fixed wing just as the controller switches to fixed-wing mode. JSBSim captures this if the transition model is correct; engineers who validate only the post-transition fixed-wing behavior miss the stall risk at the transition point itself.

### Business & Commercial Layer

Fixed-wing and VTOL UAV programs command higher market values than multirotor programs in both hardware and engineering services, driven by the longer range, higher speed, and broader payload capacity of these platforms. The commercial segments — cargo delivery (Zipline, Wing, Dronamics), agricultural fixed-wing (senseFly eBee, Trimble UX11), and BVLOS surveillance — all require engineers who understand flight dynamics beyond the multirotor model.

In India, BVLOS operations for agricultural mapping and infrastructure inspection are being scaled commercially — companies like ideaForge (fixed-wing mapping drones) and Throttle Aerospace (VTOL delivery) need GNC engineers with JSBSim and fixed-wing TECS experience. The DGCA's BVLOS Type Certification pathway specifically requires simulation evidence of safe behavior across the flight envelope, which means JSBSim-level fidelity in the simulation artifacts submitted for certification.

The eVTOL market (Joby, Archer, Beta, Lilium) is the highest-growth segment for flight dynamics engineers. Every eVTOL company employs flight dynamics engineers who maintain JSBSim or equivalent FDM models of their aircraft, use these for autopilot parameter development, and submit simulation evidence as part of FAA Special Airworthiness Certificates and eventual type certification. The scale of these programs (tens of engineers per company) represents a generational hiring wave in the 2025–2030 window.

### Hiring Signal

**Job titles requiring JSBSim/FDM/fixed-wing GNC competence:**
- **GNC Engineer (Fixed-Wing/VTOL)** — at eVTOL companies (Joby, Archer, Beta), delivery drone companies (Zipline, Wing, Dronamics); requires JSBSim modeling, TECS tuning, and flight envelope analysis
- **Flight Dynamics Engineer** — at aerospace primes (Boeing, Airbus, Textron) and defense UAV programs (General Atomics, AeroVironment); requires formal aerodynamic modeling, stability and control analysis, and flight test envelope expansion
- **Simulation Engineer (UAV/eVTOL)** — at Joby, Wisk, Volocopter; requires JSBSim or equivalent FDM, Python/MATLAB simulation scripting, and validation against flight test data
- **Autopilot Algorithm Engineer (Fixed-Wing)** — at Zipline, senseFly, Trimble; requires TECS and L1 guidance algorithm understanding, PX4 or ArduPlane integration, and simulation-first development discipline
- **VTOL Systems Engineer** — at WingtraOne, quantum-systems, Wingcopter; requires VTOL transition modeling, aerodynamic-multirotor coupling analysis, and safety envelope documentation

**Specific interview screens for FDM/fixed-wing UAV roles:**
1. "Walk me through a JSBSim trim calculation for a fixed-wing UAV at cruise. What inputs do you provide, what does the solver produce, and how do you verify the result is physically reasonable?"
2. "A fixed-wing UAV running PX4 TECS is oscillating in altitude by ±5 m on a level flight segment at constant airspeed. What TECS parameter is most likely misconfigured and why?"
3. "Explain the difference between CLα (lift curve slope) and CD0 (zero-lift drag coefficient) in a JSBSim aerodynamics model. How does each one affect the trim state at cruise?"
4. "Compare JSBSim's aerodynamic model with Gazebo's default fixed-wing physics plugin. In what scenario would the difference between the two matter for autopilot parameter tuning?"
5. "A tailsitter VTOL is performing a transition from hover to cruise. During transition at 12 m/s, the fixed-wing controller takes authority but immediately produces a 30° pitch-up. What is the most likely cause and how would you reproduce it in JSBSim?"

### Portfolio Projects

**Beginner: `jsbsim-trim-analysis`**
- Deliverables: A Python notebook that uses the JSBSim Python API to trim a reference aircraft (Rascal 110 or Cessna 172) across a speed range (15–35 m/s in 2 m/s steps), plots the trim elevator deflection and throttle as a function of airspeed, and identifies the stall speed and best-glide speed
- Suggested repo tree: `README.md`, `notebooks/trim_analysis.ipynb`, `results/trim_table.csv`, `results/trim_plots.png`
- Acceptance criteria: (1) the trim table is physically reasonable (stall speed below cruise speed, elevator goes more negative as speed increases); (2) the notebook runs end-to-end with a single `jupyter nbconvert --execute` command; (3) the README explains what the plots show and what the stall/best-glide speeds mean operationally

**Intermediate: `px4-jsbsim-tecs-tuning`**
- Deliverables: A PX4 SITL session using the JSBSim backend (not Gazebo) for a fixed-wing model, with documented TECS parameter tuning: before-tuning log, parameter change rationale, and after-tuning log showing improved altitude tracking; PX4 logs analyzed with pyulog
- Suggested repo tree: `README.md`, `params/before_tuning.params`, `params/after_tuning.params`, `logs/before_tuning.ulg`, `logs/after_tuning.ulg`, `analysis/tecs_comparison.ipynb`, `docs/tuning_rationale.md`
- Acceptance criteria: (1) the before/after comparison quantitatively shows improved altitude tracking (e.g., RMS altitude error reduced from X to Y meters); (2) the tuning rationale document explains why each parameter was changed, not just what was changed; (3) the JSBSim model (not Gazebo) is used and the README documents how to reproduce the SITL session

**Advanced: `vtol-transition-model`**
- Deliverables: A JSBSim aircraft model for a simplified VTOL (e.g., quadplane configuration) that models the transition between hover and cruise, with a Python script that simulates the transition, plots aerodynamic forces during transition (lift, thrust, drag vs time), and identifies the minimum safe transition airspeed; safety assumptions document covering the transition envelope
- Acceptance criteria: (1) the model produces physically plausible aerodynamic forces at hover (thrust > weight, zero aerodynamic lift) and at cruise (aerodynamic lift > weight, reduced thrust); (2) the transition simulation identifies a stall risk region and the minimum safe transition speed with quantitative evidence; (3) the safety assumptions document lists 5 failure modes specific to VTOL transition

### Future Trends

- **2026**: ML-based aerodynamic surrogate models (neural networks trained on CFD data) become standard pre-tools in professional UAV FDM workflows, reducing coefficient generation time from weeks to hours; JSBSim remains the simulation backbone but coefficient generation is increasingly ML-automated
- **2030**: Real-time system identification from flight data (continuous learning of aerodynamic model from in-flight measurements) enters production on long-endurance fixed-wing UAVs, enabling adaptive control laws that update as the aircraft ages or configurations change
- **2035**: Regulatory frameworks for eVTOL certification (FAA G-1 issue papers, EASA SC-VTOL) mature; simulation evidence from JSBSim-equivalent FDMs becomes a formal certification artifact, elevating flight dynamics modeling from engineering practice to regulatory requirement
- **2045**: Urban air mobility at scale requires real-time FDM-based conflict detection for hundreds of simultaneous VTOL vehicles in corridors; the FDM engineering discipline is embedded in UTM infrastructure, not just aircraft development

### Interview Questions

1. **What is TECS in PX4 and how does it differ from a simple altitude PID controller?**
   *Answer*: TECS (Total Energy Control System) controls airspeed and altitude simultaneously by managing total mechanical energy (kinetic + potential) rather than each independently. Throttle controls total energy rate (climbing or descending), while elevator controls energy distribution (airspeed vs altitude). A simple altitude PID uses only elevator for altitude, ignoring the coupling with airspeed — at low throttle, commanding up elevator reduces airspeed (energy transfer) rather than gaining altitude (energy addition). TECS avoids this coupling, producing more stable and efficient flight across throttle settings.

2. **What does "trim" mean for a fixed-wing aircraft and why is it necessary before testing a new autopilot configuration?**
   *Answer*: Trim is the state of equilibrium where all aerodynamic and propulsive forces and moments are balanced at a given airspeed and altitude — the aircraft maintains level flight with zero control surface rates. For an autopilot, the trim state defines the linearization point around which control laws are derived. A mismatched trim (e.g., the autopilot assumes the elevator trim deflection is −2° but the actual trim is +3°) means the controller starts with a steady-state error that it must continuously compensate, reducing stability margin. JSBSim's trim solver finds the exact elevator and throttle settings for a given flight condition before the control law is applied.

3. **Describe the JSBSim aerodynamics XML format: how is CLα encoded and how does JSBSim use it during simulation?**
   *Answer*: In JSBSim XML, lift coefficient tables are specified as `<function name="aero/coefficient/CLalpha">` containing a `<table>` with angle-of-attack (AoA) as the independent variable and CL as the dependent variable. During simulation, JSBSim interpolates this table at the current AoA every timestep and multiplies by the dynamic pressure and wing area to compute aerodynamic lift force. This is the coefficient-based model: CL = f(α) × q × S, where q is dynamic pressure and S is wing area. Additional terms (CLq for pitch rate effect, CLde for elevator effect) are superimposed additively.

4. **What is L1 guidance in PX4 and how is it different from pure pursuit?**
   *Answer*: L1 guidance is a nonlinear lateral guidance law that selects a reference point on the desired path at a fixed distance L1 ahead of the aircraft and commands lateral acceleration toward that point. Unlike pure pursuit (which steers directly toward the nearest path point), L1 selects a lookahead point, giving it trajectory-following stability properties — the aircraft cannot overshoot the path by more than a bounded amount regardless of initial offset. L1 period (PX4's `FW_L1_PERIOD`) controls the lookahead distance; shorter values give tighter tracking but more oscillation; longer values give smoother flight but slower convergence to the path.

5. **Why is VTOL transition modeling harder than fixed-wing cruise modeling in JSBSim?**
   *Answer*: Cruise modeling operates in a well-characterized aerodynamic regime where classical thin-airfoil theory applies and coefficient tables are accurate. VTOL transition crosses multiple regimes simultaneously: at low airspeed, the wing is ineffective and rotor thrust dominates; at transition speed, both are significant but interact (rotor downwash changes effective AoA on the wing; wing blankets rotor flow in some configurations); above transition speed, classical aerodynamics dominates. JSBSim must correctly model the time-varying blend of rotor thrust tables and aerodynamic lift tables, with the blend depending on airspeed. Errors in the transition model (wrong crossover airspeed, missing propwash effects) produce control law behavior in simulation that does not match hardware flight.

### Further Depth

- **JSBSim GitHub repository** (github.com/JSBSim-Team/jsbsim) — source code, reference aircraft models, and Python API documentation
- **JSBSim Reference Manual** (jsbsim.sourceforge.net/JSBSimReferenceManual.pdf) — coefficient model definitions, XML schema documentation, and trim/linearization documentation
- **PX4 JSBSim SITL documentation** (docs.px4.io/main/en/simulation/jsbsim.html) — setup guide for PX4 + JSBSim integration
- **"Small Unmanned Aircraft: Theory and Practice" — Beard and McLain** (BYU) — the standard academic reference for fixed-wing UAV GNC; covers trim, linearization, and PID/LQR design against fixed-wing plant models
- **"Flight Stability and Automatic Control" — Nelson** — classical text for stability and control concepts underlying TECS and L1 guidance
- **XFLR5 documentation** (xflr5.tech) — open-source aerodynamic analysis tool that produces CLα and CDα tables for JSBSim import from wing geometry
- **ArduPlane TECS documentation** (ardupilot.org/plane/docs/tecs-total-energy-control-system-for-speed-height-tuning-guide.html) — practical TECS tuning guide; parameters align with PX4 TECS with minor naming differences
- **ETH ASL UAV research publications** (asl.ethz.ch) — fixed-wing UAV aerobatics, aggressive maneuver planning, and JSBSim-validated MPC; open-access papers with simulation methodology details
