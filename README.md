# Sensor-Based KUKA Pick-and-Place Automation System
![KUKA](https://img.shields.io/badge/KUKA-Robotics-orange?style=for-the-badge) ![ROS2](https://img.shields.io/badge/ROS2-Humble-blue?style=for-the-badge) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

## Overview
Industrial robotics simulation and path planning using KUKA Robot Language (KRL) and KUKA.Sim Pro. Implements Point-to-Point (PTP) and Linear (LIN) trajectory planning, Base/TCP coordinate calibration, and simulated conveyor sensor I/O triggers.

## System Architecture
```\n[Relational Database / Core API Architecture]\n```

## Features
- Trajectory programming (PTP and LIN path planning) in KUKA Robot Language (KRL).
- Base coordinate and Tool Center Point (TCP) calibration setup.
- Reachability analysis and sensor I/O integration within virtual workcells.

## Tech Stack
- KRL (KUKA Robot Language) trajectory scripts
- KUKA.Sim Pro for virtual workcell layout design
- ROS2 Humble and Ubuntu Docker containers

## Getting Started
To configure and run the project locally, clone the repository and execute the setup instructions:

```bash
git clone https://github.com/Raghuram-sekar/KUKA-Pick-and-Place-Automation.git
cd KUKA-Pick-and-Place-Automation

# Execute local setup commands:
# Run simulations inside KUKA.Sim Pro
# Or execute paths via KRL interpreters
```
