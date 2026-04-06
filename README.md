# ZEUS — Autonomous Payload-Delivery Hexacopter

![ArduPilot](https://img.shields.io/badge/ArduPilot-Mission%20Planner-blue)
![Pixhawk](https://img.shields.io/badge/Pixhawk-Cube%20Orange-red)
![Frame](https://img.shields.io/badge/Frame-Carbon%20Fiber-333)
![CAD](https://img.shields.io/badge/CAD-SolidWorks-CC0000)
![License](https://img.shields.io/badge/License-MIT-yellow)

A custom-built hexacopter for autonomous waypoint missions with a 900 g servo-actuated payload drop. Designed and flown by **Team ASRL** at SRM Institute of Science and Technology for **Rotorcraft Nitte 2024** (Team No. ROTOR2407).

## Overview

ZEUS is a 2 kg-class hexacopter built around a Pixhawk Cube Orange flight controller and a topology-optimised 3K carbon-fiber frame. The mission profile is autonomous take-off → GPS waypoint navigation → target loiter → payload release → return to home, planned and uploaded via Mission Planner over a 433 MHz MAVLink telemetry link.

The hexacopter configuration was chosen over a quadcopter for the 50% thrust margin and motor-failure tolerance, and over an octocopter to keep weight and current draw low enough to fit a 5+ minute flight envelope on a single 6S battery pack.

## System Architecture

<p align="center">
  <img src="architecture.png" width="100%" alt="ZEUS System Architecture"/>
</p>

## Specifications

| Parameter | Value |
|---|---|
| Configuration | X-Hexacopter |
| Take-off weight | 2051 g |
| Payload capacity | 900 g |
| Diagonal wheelbase | 335 mm |
| Overall (L × W × H) | 335.5 × 290.5 × 237.6 mm |
| Endurance (80% discharge) | ~5.2 min |
| Hover power | 625 W |
| Cruise current | ~24 A |
| Battery | 2× 1300 mAh 6S LiPo (parallel, 25.2 V, 100C) |

## Hardware

| Subsystem | Component | Notes |
|---|---|---|
| Flight controller | Pixhawk Cube Orange | 3× redundant IMUs, EKF, temperature stabilised |
| GPS / INS | Here3 | RTK + gyro/accel/mag/baro over CAN |
| Telemetry | Holybro SiK | MAVLink, 433 MHz, 500 mW |
| RC link | TBS Tango 2 Pro + Crossfire Rx | 915 MHz, 4 km range, 8 channels |
| Motors | 6× Emax ECO II 2306, 1700 KV | BLDC, 5" tri-blade props |
| ESCs | 2× 4-in-1, 50 A | 3S–6S, 1000 µF spike caps |
| Payload servo | Single-rod double-door release | Torque-balanced drop |
| Frame | 3K roll-wrapped CF tubes + CF plates | Topology-optimised |
| Landing gear | Skid type, 100 mm clearance | PLA+ FDM print |

## Design Process

**Weight estimation.** `Wto = Woe + Wpl + Wf` → 671 g operational + 900 g payload + 480 g battery = 2051 g final, down 69 g from the 2120 g preliminary estimate after frame iteration.

**Thrust budget.** 20% margin above hover gives 2461 g total static thrust → 410 g per motor. The Emax ECO II 2306 / 5" tri-blade combination clears this comfortably at ~4 A per motor.

**Power & endurance.** 6 × 100.8 W motor draw + 20 W avionics = 625 W total. With a 65.52 Wh pack and 80% safe discharge, the endurance works out to ~5.2 min — sufficient for the competition mission profile.

**Frame iterations.**
1. *Iteration 1* — built for strength, 15 mm CF round tube arms, dual motor mount attachments. Too heavy, too many fasteners.
2. *Iteration 2* — pultruded CF square tube arms, motor mount bolts cut from 9 to 2. Significant weight reduction.
3. *Final* — 8 mm 3K roll-wrapped CF tube arms (lighter and stronger than pultruded), reduced top-to-base plate spacing for stiffness.

**Topology optimisation.** Two FEA load cases applied to the base plate — fixtures at arm mounts with center load, and the inverse — final geometry combines both results to remove material where neither case carries stress.

**Static structural analysis.** Whole-frame FEA validated against the worst-case combined thrust of all six motors (~120 N) to ensure plate integrity under maximum flight load.

## Autonomous Mission

Mission planning is done in **Mission Planner (ArduPilot)**. The pilot defines the home position, take-off altitude (5 m), waypoint sequence, and return-to-home behaviour; the full plan is uploaded to the Pixhawk over MAVLink before flight.

```
Arm + Take-off  →  Waypoint nav  →  Target loiter  →  Payload drop  →  Return to home
```

The payload bay sits below the frame on a double-door mechanism actuated by a single servo driving a sliding lock rod. The double-door geometry cancels reaction torque at release so the drop does not perturb attitude.

## Bill of Materials

| Component | Qty | Total (₹) |
|---|---|---|
| Pixhawk Cube Orange | 1 | 32,999 |
| TBS Tango 2 + Crossfire Rx | 1 | 26,378 |
| Here3 GPS | 1 | 18,093 |
| BLDC motors (Emax ECO II 2306) | 6 | 8,790 |
| 4-in-1 ESC (50 A) | 2 | 8,098 |
| Holybro Telemetry | 1 | 7,563 |
| 6S 1300 mAh LiPo | 2 | 4,998 |
| CF plate (2.5 mm) | 1 | 4,308 |
| CF tube (8 mm) | 3 | 1,947 |
| PLA+ filament | 1 | 999 |
| Propellers, servo | — | 455 |
| **Total** | | **₹1,14,628** |

## Repository Layout

```
zeus/
├── cad/              # SolidWorks parts, assemblies, and rendering setups
├── architecture.svg  # System architecture diagram (vector)
├── architecture.png  # Rendered architecture diagram
└── README.md
```

## Stack

`ArduPilot` · `Mission Planner` · `Pixhawk Cube Orange` · `Here3 RTK GPS` · `MAVLink` · `Crossfire` · `SolidWorks` · `FEA` · `Carbon Fiber` · `PLA+`

## Team

**Team ASRL — SRM Institute of Science and Technology**
P. Tarun Kumar · Raghunath VM · Adarsh Jha · Manan Wadhwa · Rhythm Pareek · Muhammed Sahal M N · Vijay Solanki · Akshika Pathania

## License

This project is licensed under the [MIT License](LICENSE).
