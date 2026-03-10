# ZEUS

ZEUS is a custom-built hexacopter UAV developed by **Team ASRL** at SRM Institute of Science and Technology for the **Rotorcraft Nitte 2024** competition (Team No: ROTOR2407).

> **Team Members:** P. Tarun Kumar, Raghunath VM, Adarsh Jha, Manan Wadhwa, Rhythm Pareek, Muhammed Sahal M N, Vijay Solanki, Akshika Pathania

---

## Conceptual Design

<!-- ADD IMAGE HERE: Fig 1 - High Level View (actual photo of ZEUS on ground) -->

ZEUS is engineered for autonomous flight missions with precision payload delivery. Built on a lightweight carbon fiber hexacopter frame, it integrates an advanced avionics stack to perform fully autonomous waypoint navigation and controlled payload dropping.

---

## Detailed Design

### Weight Estimation

The take-off weight is calculated using:

```
Wto = Woe + Wpl + Wf
```

| Parameter | Value |
|---|---|
| Operational Weight (Woe) | 671g (Frame 250g + Electronics 421g) |
| Payload Weight (Wpl) | 900g |
| Battery / Fuel Weight (Wf) | 480g |
| **Total Take-off Weight** | **2051g** |

> Preliminary estimate was 2120g. Final estimate is 2051g — a difference of 69g after design refinement.

---

### Thrust Estimation

```
Thrust for take-off = Total Weight + 20% margin
                    = 2051g + 410.2g = 2461.2g

Thrust per motor = 2461.2 / 6 = 410.2g
```

---

### Propulsion System

<!-- ADD IMAGE HERE: Fig 2 - BLDC Motor (Emax ECO II 2306) -->
<!-- ADD IMAGE HERE: Fig 3 - 5-inch Tri-blade Propeller -->

An electrical propulsion system was selected for environment-friendly, low carbon footprint operations.

- **Motors:** Emax ECO II 2306, 1700KV BLDC — high torque, durable, low electrical noise
- **Propellers:** 5-inch tri-blade — optimum performance with maximum stability
- **Battery:** 2x 1300mAh 6S LiPo connected in parallel → 2600mAh, 25.2V nominal, 100C discharge rate

---

### UAV Configuration Selection

<!-- ADD IMAGE HERE: Fig 4, 5, 6 - X Quad / X Hexa / X Octo configuration diagrams (side by side) -->

| Configuration | Weight | Endurance | Stability | Thrust |
|---|---|---|---|---|
| Quadcopter | Low | High | Low | Low |
| **Hexacopter** | **Medium** | **Medium** | **High** | **High** |
| Octacopter | High | Low | High | High |

A **Hexacopter** was selected — two extra motors over a quadcopter increase thrust by 50%, reduce per-motor load and current draw, and provide greater stability for smooth flight. An Octocopter adds unnecessary weight for this mission.

---

### Wheelbase & Sizing

<!-- ADD IMAGE HERE: Fig 7 - Wheelbase diagram with dimensions -->
<!-- ADD IMAGE HERE: Fig 8 - Top View drawing -->
<!-- ADD IMAGE HERE: Fig 9 - Side View drawing -->
<!-- ADD IMAGE HERE: Fig 10 - Front View drawing -->

- Horizontal wheelbase from centre motor mount: **168mm**
- Diagonal wheelbase: **335mm**
- Propeller clearance: **40mm** (to prevent collisions)
- All electronics placed on the top plate for optimal CG and easy access
- Two battery slots positioned front and back symmetrically for CG balance

**Overall Dimensions:** L = 335.5mm, W = 290.5mm, H = 237.6mm
**Landing gear height:** 100mm ground clearance — sufficient for payload bay attachment without ground collision

---

### UAV Performance

#### Power Estimation

```
Hover current per motor : 4A
Voltage                 : 25.2V
Power per motor         : 100.8W
Power (6 motors)        : 604.8W
Electronics overhead    : ~20W
Total power consumption : 625W
Energy for 5 min flight : 51.875 Wh
```

#### Power System

```
Battery energy = 2.6 Ah × 25.2V = 65.52 Wh  ✓ (exceeds 51.875 Wh required)
```

#### Endurance

```
Average Amp Drawn = (2.051 kg × 294.811 W/kg) / 25.2V = 23.99A

Flight time (80% discharge) = (2.6 × 0.8) / 23.99 = 5.201 min
```

---

### Design Iterations

<!-- ADD IMAGE HERE: Fig 11 - Iteration 1 (SolidWorks render) -->
<!-- ADD IMAGE HERE: Fig 12 - Iteration 2 (SolidWorks render, front and top view) -->
<!-- ADD IMAGE HERE: Fig 13 - Final Iteration (top view render) -->

**Iteration 1** — Designed for maximum strength. Base plate topology-optimized with 10% material removal. 15mm CF tubes used in arms. Motor mounts with dual arm attachments. Drawback: excessive weight and fastener count.

**Iteration 2** — Focus on weight reduction. Maximum topology optimization. 15mm CF tubes replaced with pultruded CF square tubes. Motor mount bolts reduced from 9 to 2 per motor.

**Final Iteration** — Minimized distance between base and top plate for maximum stability. Pultruded CF tubes replaced with 8mm circular 3K roll-wrapped CF tubes — lighter per arm and significantly stronger.

---

### Material Selection

<!-- ADD IMAGE HERE: Fig 14 - CF Tube 3K Roll -->

**Carbon Fiber Plate (Frame)**
High strength-to-weight ratio — withstands flight stresses while keeping weight minimal. Rigid under high loads, maintaining structural integrity and preventing flex that could affect stability.

**Carbon Fiber Tube (Arms)**
3K roll-wrapped CF tubes selected for drone arms — excellent strength-to-weight ratio, essential for efficient flight.

**PLA+ (3D Printed Attachments)**
Complex attachment parts manufactured via 3D printing using PLA+ — higher strength and toughness than standard PLA, with better layer-to-layer adhesion preventing delamination.

---

### Subsystem Selection

#### Telemetry

<!-- ADD IMAGE HERE: Fig 15 - Holybro Telemetry SiK Module -->

**Holybro Telemetry SiK Module** — MAVLink-compatible, integrates with Mission Planner. Output: 500mW, Frequency: 433MHz.

#### Radio Transmission

<!-- ADD IMAGE HERE: Fig 16 - TBS Tango 2 Pro Transmitter & Crossfire Receiver -->

**TBS Tango 2 Pro** — Crossfire protocol, 915MHz, range up to 4km. 8 channels: 4 for UAV movement control, remainder for flight modes.

#### Flight Controller & GPS

<!-- ADD IMAGE HERE: Fig 17 - Pixhawk Cube Orange -->
<!-- ADD IMAGE HERE: Fig 18 - Here3 GPS -->

**Pixhawk Cube Orange**
- 3 sets of IMU sensors for redundancy
- 2 vibration-isolated IMUs for accurate state estimation
- Temperature-controlled IMUs via onboard heating resistors

**Here3 GPS** — Full inertial navigation (gyroscope, accelerometer, compass, barometer) + GNSS. RTK positioning data fused with Extended Kalman Filter (EKF) in ArduPilot/PX4 for optimized positioning.

#### Electronic Speed Controllers

<!-- ADD IMAGE HERE: Fig 19 - Speedybee 50A ESC -->
<!-- ADD IMAGE HERE: Fig 20 - HGLRC 50A ESC -->

Two **4-in-1 ESC modules** (vs. 6 individual ESCs) to reduce weight. Voltage range: 3S–6S. Max current: 50A per module. 1000μF capacitor per ESC to filter current spikes from PWM signal changes.

---

### Electronics Architecture

<!-- ADD IMAGE HERE: Electronics Architecture block diagram (from PDF page 13) -->

```
BLDC x6 → ESC x6 → Pixhawk Cube Orange Flight Controller
                         ↑               ↑
               Radio Telemetry     Transmitter TX
                         ↓
                  Power Module (PixHawk)
                         ↓
                      PDB + BEC
                         ↑
              LiPo Battery Pack → Battery Management System
```

---

### CG Estimation & Stability Analysis

<!-- ADD IMAGE HERE: Fig 21 - Center of Gravity (loaded and unloaded CG side-by-side renders) -->

Two battery slots placed symmetrically front and back of the frame. CG estimated to lie near the midpoint of the two battery slots, above the drone's geometric origin.

#### Topology Optimization

<!-- ADD IMAGE HERE: Fig 22 - Topology Optimization results (two heat maps side by side) -->

Goal: lightweight structure without compromising structural integrity. Two methods applied:
- **Method 1:** Fixtures at arm mountings, force at plate center
- **Method 2:** Center fixed, force applied at arm mountings

Final design incorporates both optimized results.

#### Static Structural Analysis

<!-- ADD IMAGE HERE: Fig 23 - Structural Analysis (SolidWorks FEA results) -->

Performed under maximum combined thrust of all 6 motors (**120N**) to validate plate integrity under worst-case flight loads.

#### Landing Gear

<!-- ADD IMAGE HERE: Fig 24 - Landing Gear FEA analysis render -->

Skid-type landing gear selected for maximum stability and ground surface contact. Designed in SolidWorks to maximize strength while minimizing weight. Complex geometry manufactured via 3D printing.

---

## Autonomous Operations & Payload Mechanism

### Autonomous Flight

<!-- ADD IMAGE HERE: Fig 25 - Mission Planner Take-off screenshot -->
<!-- ADD IMAGE HERE: Fig 26 - Mission Planner Waypoints screenshot -->

Mission programmed via **Mission Planner (ArduPilot)**. Full mission breakdown:

**Phase 1 — Take-off:** Altitude set to 5m in ground station software.

**Phase 2 — Waypoint Navigation:** Multiple GPS waypoints defined between home location and target area. Drone follows planned path autonomously.

**Phase 3 — Return to Home:** On mission completion, drone autonomously returns to home position.

### Payload Dropping Mechanism

<!-- ADD IMAGE HERE: Fig 27 - Payload Mechanism (double-door bay open and closed) -->

- **Double-door payload bay** mounted below the frame
- Servo-actuated locking mechanism using a single moving rod
- Double-door design prevents torque-induced disturbance during payload release
- Safe, controlled drop without affecting flight stability

---

## Weight Breakdown

### Electronics

| Component | Weight (g) | Qty | Total (g) |
|---|---|---|---|
| BLDC Motors | 30.4 | 6 | 182.4 |
| Battery | 230 | 2 | 460 |
| 4-in-1 ESC | 18 | 2 | 36 |
| Here3 GPS | 48.8 | 1 | 48.8 |
| Pixhawk Cube Orange | 73 | 1 | 73 |
| Holybro Telemetry | 15 | 1 | 15 |
| Crossfire Receiver | 2 | 1 | 2 |
| Power Module | 14 | 1 | 14 |
| Propeller | 6.8 | 6 | 40.8 |
| Servo Motor | 9 | 1 | 9 |
| **Total** | | | **881g** |

### Frame

| Component | Weight (g) | Qty | Total (g) |
|---|---|---|---|
| Base plate | 46.23 | 1 | 46.23 |
| Top plate | 28.48 | 1 | 28.48 |
| FC plate | 19.81 | 1 | 19.81 |
| Arm tube | 4.83 | 6 | 28.98 |
| Motor Mount plate | 1.08 | 6 | 6.48 |
| LG Vertical | 4.39 | 2 | 8.78 |
| LG Horizontal | 6.59 | 2 | 13.18 |
| M3 × 20mm bolt | 1.60 | 24 | 38.4 |
| M3 × 8mm bolt | 1.1 | 6 | 6.6 |
| LG to Base mount | 6.5 | 2 | 13 |
| LG Damper | 1 | 4 | 4 |
| Arm mount | 1.5 | 12 | 18 |
| MM attachment | 1 | 12 | 12 |
| T attachment | 2 | 2 | 4 |
| **Total** | | | **247.94g** |

---

## Bill of Materials

| Component | Unit Price (₹) | Qty | Total (₹) |
|---|---|---|---|
| BLDC Motor | 1465 | 6 | 8790 |
| Battery | 2499 | 2 | 4998 |
| 4-in-1 ESC | 4049 | 2 | 8098 |
| Here3 GPS | 18093 | 1 | 18093 |
| Pixhawk Cube Orange | 32999 | 1 | 32999 |
| Holybro Telemetry | 7563 | 1 | 7563 |
| Transmitter & Receiver | 26378 | 1 | 26378 |
| Propeller | 179 | 2 | 358 |
| Servo Motor | 97 | 1 | 97 |
| CF Plate (2.5mm) | 4308 | 1 | 4308 |
| CF Tube (8mm) | 649 | 3 | 1947 |
| PLA+ | 999 | 1 | 999 |
| **Total** | | | **₹1,14,628** |

---

## Engineering Drawing

<!-- ADD IMAGE HERE: Full engineering drawing sheet — front view, right view, top view, isometric view with all dimensions and summary data table -->

**Summary Data**

| Parameter | Value |
|---|---|
| Dimensions | L=335.5mm, W=290.5mm, H=237.6mm |
| Empty Weight | 1250g |
| Motor | Emax ECO II 2306, 1700KV |

| Station | Weight (g) | Datum Distance (mm) |
|---|---|---|
| Frame Weight | 350g | 148mm |
| Battery 1 | 520g | 89mm |
| Battery 2 | 520g | 199mm |
| Motors | 180g | 0mm, 145mm, 290mm |
| Electronics | 120g | 145mm |
| Others | 80g | 148mm |

---

*Developed by Team ASRL — SRM Institute of Science and Technology | Rotorcraft Nitte 2024*
