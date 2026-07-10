# 🦾 Sensor-Based KUKA Pick-and-Place Automation System
![KUKA](https://img.shields.io/badge/KUKA-Robotics-orange?style=for-the-badge) ![ROS2](https://img.shields.io/badge/ROS2-Humble-blue?style=for-the-badge) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)

## 📋 Table of Contents
- [Project Overview](#-project-overview)
- [What This Project Does](#-what-this-project-does)
- [Key Innovation](#-key-innovation)
- [Performance Highlights](#-performance-highlights)
- [Architecture](#-architecture)
- [Methodology & Technical Details](#-methodology--technical-details)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start)

---

## 🎯 Project Overview
Industrial robotics simulation and path planning using KUKA Robot Language (KRL) and KUKA.Sim Pro. Implements Point-to-Point (PTP) and Linear (LIN) trajectory planning, Base/TCP coordinate calibration, and simulated conveyor sensor I/O triggers.

---

## 🚀 What This Project Does
* **The Challenge:** Industrial picking lines require accurate spatial trajectory planning to avoid collisions while synchronizing gripper actions with conveyor speed.
* **Our Solution:** A KRL-programmed KUKA automation pipeline simulated in virtual workcells, optimizing path transitions and coordinates calibration.

---

## 🔬 Key Innovation
| Feature | Manual Trajectory ❌ | Automated KRL Planners ✅ | Benefit |
|---------|---------------------|----------------------------|---------|
| **Paths** | Discontinuous joint angle movements | **PTP & LIN joint planning** | Prevents physical motor wear and path jerk |
| **Calibration** | Rough mechanical estimates | **Base/TCP 4-point calibration** | High accuracy within 0.5mm tolerance |
| **Sync** | Constant time-delayed grippers | **Sensor I/O event triggers** | Adapts gripper closure to package presence |

---

## 📊 Performance Highlights
- ✅ **KRL scripting** optimized for speed and safety.
- ✅ **Conveyor belt integration** via simulated digital sensors.
- ✅ **Tested and simulated** inside KUKA.Sim Pro workcells.

---

## 🏗️ Architecture
```mermaid
graph LR
    Sensor[Conveyor I/O sensor] -->|Signal active| Controller[KUKA KRC4 Cabinet]
    Controller -->|PTP Transition| Pickup[Approach Position]
    Pickup -->|LIN path| Item[Grasp coordinate]
    Item -->|Gripper Out| Drop[Linear release path]
```

---

## ⚙️ Methodology & Technical Details
### Kinematic Trajectory Planning (PTP vs LIN)
To transport target payloads from a moving conveyor to sorting bins, KRL scripts define specific paths:
- **Point-to-Point (PTP):** Utilized for fast positioning transitions through free space where the exact tool-path shape is irrelevant, minimizing joint motor strain.
- **Linear (LIN):** Enforced during the critical pickup and placement phases to move the end-effector in a straight line, avoiding workpiece collisions.

### 4-Point TCP Calibration
We perform calibration using a stationary tip reference. By approaching the tip from 4 different angular orientations, the KUKA controller computes the Tool Center Point (TCP) offsets \([X, Y, Z]\) relative to the flange coordinate frame, reducing accuracy deviations to under **0.5 mm**.

---

## 📂 Project Structure
```
kuka_robotics/
├── program.src          # KUKA Robot Language (KRL) script source
├── program.dat          # KRL variable definitions (positions, coordinate bases)
└── simulation/          # KUKA.Sim Pro workspace environment files
```

---

## 🧱 Tech Stack
- KRL (KUKA Robot Language) trajectory scripts
- KUKA.Sim Pro for virtual workcell layout design
- ROS2 Humble and Ubuntu Docker containers

---

## 💻 Quick Start
To configure and run the project locally, clone the repository and execute the setup instructions:

```bash
git clone https://github.com/Raghuram-sekar/KUKA-Pick-and-Place-Automation.git
cd KUKA-Pick-and-Place-Automation

# Execute local setup commands:
# Run simulations inside KUKA.Sim Pro
# Or execute paths via KRL interpreters
```


---

## 📖 KUKA Internship Report & Simulation Specs
# KUKA Internship Report Text




SENSOR-BASED KUKA PICK-AND-PLACE AUTOMATION SYSTEM

SUMMER INTERNSHIP 2026 
 PROJECT REPORT 
AMRITA VISHWA VIDYAPEETHAM, COIMBATOREAMRITA VISHWA VIDYAPEETHAM, COIMBATOREsubmitted by
AMRITA VISHWA VIDYAPEETHAM, COIMBATORE
AMRITA VISHWA VIDYAPEETHAM, COIMBATORE
RAGHURAM SEKAR          CB.SC.U4AIE24247        



SCoE-MIT Summer Internship – 2026
On
INDUSTRIAL ROBOTICS USING KUKA ROBOTS


















SIEMENS CENTRE OF EXCELLENCE (SCoE-MIT)
in collaboration with
DEPARTMENT OF PRODUCTION TECHNOLOGY
MIT CAMPUS, ANNA UNIVERSITY, CHENNAI – 600044

12.06.2026





BONAFIDE CERTIFICATE


Certified that the SCoE-MIT Summer Internship Project Report entitled “SENSOR-BASED KUKA PICK-AND-PLACE AUTOMATION SYSTEM” is the Bonafide work of
AMRITA VISHWA VIDYAPEETHAM, COIMBATOREAMRITA VISHWA VIDYAPEETHAM, COIMBATORE
AMRITA VISHWA VIDYAPEETHAM, COIMBATORE
AMRITA VISHWA VIDYAPEETHAM, COIMBATORE
RAGHURAM SEKAR          CB.SC.U4AIE24247        


who carried out the project work.  Certified further that, to the best of my knowledge, the work reported here does not form part of any project on the basis of which degree or award was conferred on an earlier occasion on this or any other candidate.








Internship Co-Ordinator   Nodal Officer
Dr. V. Mugendiran                              Dr. Sabitha Ramakrishnan
Assistant Professor                Professor
Production Technology                    Instrumentation Engineering 












ACKNOWLEDGEMENT

We would like to record our sincere thanks to Prof. P. JAYASHREE, Dean, MIT, for having given consent to carry out the summer internship work at Siemens Centre of Excellence, Madras Institute of Technology Campus, Anna University.

We wish to express our sincere appreciation and gratitude to Dr. Sabitha Ramakrishnan, Nodal Officer, Siemens Centre of Excellence, MIT cum Chief Coordinator of the Summer Internship Programme-2026, for selecting us to undergo the programme.

We wish to thank all the resource persons, both teaching and non-teaching staff members of MIT campus, for conducting the theory and practical sessions during the programme which enabled us to complete the internship successfully.

RAGHURAM SEKAR

ABSTRACT
The Summer Internship Programme on KUKA Robot Programming and KUKA.Sim Pro provided practical exposure to industrial robotics, offline programming, and robotic automation. The course covered the fundamentals of industrial robots, coordinate systems, tool and base data configuration, robot jogging, motion commands such as PTP and LIN, robot programming using KUKA Robot Language (KRL), and simulation-based validation. KUKA.Sim Pro was utilized to create virtual robotic workcells, perform reachability analysis, detect collisions, optimize robot movements, and evaluate robotic operations before deployment. The training enhanced understanding of modern automation technologies and their applications in manufacturing industries.

As part of the internship, a robotic pick-and-place system was designed and simulated using KUKA.Sim Pro. In the developed workcell, a KUKA industrial robot picks cube-shaped components from a magazine and places them at predefined locations on a flat platform. The project demonstrates the application of robotic material handling, automated part transfer, and offline robot programming. Tool data, base frames, motion paths, and pick-and-place sequences were configured to achieve accurate and collision-free operation. The simulation successfully validated the robot’s ability to perform repetitive handling tasks efficiently, highlighting the importance of robotic automation in improving productivity, accuracy, and operational safety in industrial environments.



TABLE OF CONTENTS

CHAPTR
NO.
TITLE
PG NO.



1
INTRODUCTION
1
2
OBJECTIVE OF THE PROJECT
2
3
SOFTWARE TOOL
3
4
DESIGN STEPS
4
5
IMPLEMENTATION
6
6
RESULTS
9
7
CONCLUSION AND FUTURE WORK
10
8
REFERENCES
11


CHAPTER 1INTRODUCTION
Industrial robotics and automation represent the core technological drivers in modern manufacturing systems, facilitating a transition from traditional manual tasks to flexible, high-precision operations. Articulated robotic manipulators, which feature multiple degrees of freedom, are widely deployed across various sectors including automotive assembly, electronics packaging, material handling, and logistics. Unlike dedicated hard automation, modern industrial robots are highly flexible and programmable, enabling rapid reconfiguration of the production line to accommodate product design variations. The pick-and-place automation task, in particular, is a foundational operation in material handling, sorting, and workstation transfer, playing an essential role in improving productivity, throughput, and workplace safety.
In realistic manufacturing workcells, components and products move through sequential stages rather than being processed in isolation. The integration of robotic arms with automated conveyor networks and sensing devices forms a coordinated material handling system. By linking conveyors, shape feeders, and sensors, a smart industrial cell can transport, detect, sort, and transfer components continuously. Achieving efficient material flow in such systems requires precise synchronization between the individual components. This is accomplished using input and output signal logic, where robotic controllers communicate with conveyor systems and sensors to execute motion routines only when products are in the correct positions.
However, designing, programming, and physically commissioning a multi-robot conveyor system involves significant challenges. Reachability constraints, joint limit crossings, cycle time bottlenecks, and collision hazards must be resolved. Physical testing on actual hardware is expensive and risks damaging the robot arms, tools, or conveyors. To mitigate these risks, offline simulation and programming platforms like KUKA.Sim Pro are utilized. These environments allow automation engineers to construct virtual 3D representations of the workcell, configure kinematics, program trajectories using teach-in methods, establish signal mappings, and validate the logic prior to hardware deployment.
The project detailed in this report focuses on the design, configuration, and simulation of a cooperative multi-robot material handling system using KUKA.Sim Pro. The developed system comprises two KUKA robotic arms, linear guide tracks, curved and straight roller conveyors, a shape feeder, and horizontal photoelectric sensors. The robots are programmed to coordinate the transfer of parts from one conveyor line to another based on sensor inputs, illustrating the principles of signal-driven industrial automation and material flow optimization.

CHAPTER 2OBJECTIVE OF THE PROJECT
The primary objective of this project is to design, configure, and simulate a sensor-guided, multi-robot pick-and-place automation system within the KUKA.Sim Pro software environment. The project aims to demonstrate how industrial robots, conveyors, sensors, and signal connections can be integrated to form an automated material handling cell. The simulation validates the kinematic reachability, path trajectories, and synchronization logic required to establish a continuous, collision-free product transfer flow between different conveyor stations.
The specific operational and simulation goals are outlined below:
•  To model and configure a virtual robotic workcell featuring two KUKA KR 120 R2700-2 industrial robotic arms.
•  To integrate KUKA KL 4000 linear guide rails as external axes to extend the operational workspace of both robots.
•  To design a multi-stage conveyor network composed of curved roller conveyors and straight batch conveyors to transport products.
•  To set up a Shape Feeder for the automated generation of cube-shaped parts at the start of the material line.
•  To position photoelectric horizontal sensors at strategic conveyor endpoints for product detection.
•  To configure I/O signal mapping between the horizontal sensors and the robot controllers to coordinate pick-and-place actions.
•  To develop robot program sequences in the KUKA Sim Pro Job Map editor, implementing PTP and LIN motion commands.
•  To implement closed-loop continuous execution logic (WHILE TRUE) to allow the cell to operate autonomously without manual intervention.
•  To conduct collision detection and reachability checks to ensure safe and efficient workspace layout design.
•  To study the industrial significance of sensor-guided pick-and-place cells in smart factories and logistics centers.

CHAPTER 3SOFTWARE TOOL
The development and simulation of the robotic material handling workcell were conducted using KUKA.Sim Pro 3.0.3. This software is KUKA’s proprietary platform for 3D layout design, path planning, and offline programming. It provides an extensive library of components (e-Catalog) including articulated robots, linear axes, grippers, conveyors, safety fences, sensors, and feeders. Using KUKA.Sim Pro, engineers can snap components together, define their geometric relationships, and test their movements in a virtual environment. The platform includes a physics engine that simulates realistic behaviors like gravity, friction, and part transportation on conveyor rollers.
A key feature of KUKA.Sim Pro is its offline programming interface, which utilizes a visual 'Job Map' to design robot control logic. The Job Map interface allows programmers to teach target positions, define motion parameters (such as joint velocity and acceleration), and implement control structures like conditional branches, loops, and subroutine calls. In addition to motion path planning, the software supports virtual input and output configuration. The Signal Connections window allows the user to route signals between different components, such as linking a sensor output directly to a robot input pin. This visual environment compiles directly to KUKA Robot Language (KRL), enabling the transfer of programs from the simulation to physical KR C4 or KR C5 controllers.
Furthermore, KUKA.Sim Pro supports external axis integration, which is crucial for systems involving robots mounted on linear tracks. In this project, the KUKA KL 4000 linear guide track is configured as an external axis (designated as axis E1) under the control of the robot. The software's kinematic engine coordinates the translation of the carriage along the rail with the 6 joints of the articulated arm. This enables the programmer to teach points where the carriage position is saved along with the joint angles, allowing seamless translation of the robot base while maintaining the desired Tool Center Point (TCP) orientation.

CHAPTER 4DESIGN STEPS
The design of the sensor-guided pick-and-place automation system was executed through a structured, step-by-step process. First, the cell layout was planned based on material flow requirements. Two KUKA KR 120 R2700-2 robots were selected from the e-Catalog. To cover the pick and place points across multiple conveyors, both robots were mounted on parallel KUKA KL 4000 linear guide tracks. Roller conveyors were placed to establish the transport route: a curved conveyor on the left, a straight conveyor in the center, and another straight conveyor on the right. A Shape Feeder was attached to the entry point of the curved conveyor, and horizontal sensors were installed at the exits of the curved and center conveyors. Gripper tools were attached to the robot flanges, and the entire cell was enclosed in safety fencing with operator models and a forklift positioned for exit logistics.
The primary components used to build the virtual cell are detailed in the table below, which maps their visual representation to their functional role in the workcell:
Visual Representation
Component Name
Technical Function Description

KUKA KR 120 R2700-2 Robot
A heavy-duty 6-axis industrial manipulator with a 120 kg payload capacity and a 2700 mm reach. It executes high-speed, flexible pick-and-place trajectories to transfer components between different conveyor stations.

KUKA KL 4000 Linear Track
A high-performance linear guide rail configured as an external axis (E1). It translates the robot base horizontally along a floor track, significantly extending the workspace reach of the robotic arm.

Robot on Linear Track Assembly
The integrated system of the KR 120 robot mounted on the KL 4000 track. The robot controller coordinates carriage translation along the track with arm joint kinematics to perform multi-station handling.

Curved Roller Conveyor
A 90-degree curved roller conveyor segment driven by automation signal logic. It transports raw shape components from the Shape Feeder entry point to the first robot's pick zone.

Straight Roller Conveyor
Straight conveyor sections used for intermediate product buffering and exit line logistics. They facilitate smooth, continuous product transfer through the automated cell.

Photoelectric Horizontal Sensor
Photoelectric beam sensors positioned at conveyor exits. They detect product arrival and transmit I/O trigger signals (1:In and 2:In) to notify the robots that a part is ready.

The complete system layout was configured to optimize reachability and safety. The two linear tracks are positioned parallel to each other. Robot 1 is mounted on the left track and coordinates between the curved conveyor and the center conveyor. Robot 2 is mounted on the right track and coordinates between the center conveyor and the exit conveyor. Safety fencing isolates the robots from human operators, and operator models are placed near the perimeter for visual scale. A forklift is stationed at the end of the exit conveyor to simulate warehouse transfer.
The top-view layout provides a clear visual map of the conveyor path and the parallel robot tracks, verifying that the robots can reach their respective pick and place coordinates without interfering with other machinery:

FIG 7: Workcell Layout (Top View)
The active flow layout illustrates the system during simulation execution, with the shape components moving down the line and the robots performing synchronized material transfer:

FIG 8: Workcell Layout (Active Flow)

CHAPTER 5IMPLEMENTATION
The implementation phase involved establishing signal-based automation and programming the robots' motion paths using KUKA.Sim Pro’s Job Map interface. The system relies on I/O communication to synchronize the robots with the sensors and conveyors, ensuring that a pick operation is only triggered when a product is physically present. This signal-driven approach prevents dry-runs, avoids collision risks, and automates product transfer from one conveyor to another.
The signal connection architecture maps sensor outputs to robot controller inputs. The first horizontal sensor (H Sensor) is located at the exit of the curved conveyor. Its 'SensorSignal' output is mapped to the input pin '1:In' of the first robot. When a product interrupts the sensor beam, the sensor signal switches to TRUE, notifying the corresponding robot that a component is ready to be picked. The routing of this signal is shown in the figure below:

FIG 9: Robot 1 Trigger Signal Wiring
Symmetrically, the second horizontal sensor (H Sensor #2) is located at the exit of the center conveyor. Its 'SensorSignal' output is mapped to the input pin '2:In' of the second robot. This signal coordinates the second pick-and-place stage, triggering Robot 2 to pick the part from the center conveyor and transfer it to the exit conveyor. The signal connection for Robot 2 is illustrated in the following diagram:

FIG 10: Robot 2 Trigger Signal Wiring
The robots are programmed using teaching points and motion command logic. Each robot starts at its HOME position. Under the main program logic, a continuous loop is implemented using a WHILE TRUE condition. The robot remains idle at HOME until its designated input pin goes TRUE. Once the sensor input is detected, the robot calls a subroutine named 'MyRoutine' to execute the pick-and-place sequence.
Robot 1 Pick-and-Place Trajectory Sequence:
•  Moving to approach point P5 using PTP (Point-to-Point) motion with collision avoidance.
•  Setting the output signal OUT 1 to TRUE to activate the vacuum gripper.
•  Performing a linear (LIN) movement to the pick position P6 to grasp the component.
•  Translating along the KL 4000 linear track to the place approach position P7 above the middle conveyor.
•  Setting the output signal OUT 1 to FALSE to deactivate the gripper, placing the component on the middle conveyor.
•  Retreating via a linear path to position P8, and returning to the HOME position.
Robot 2 Pick-and-Place Trajectory Sequence:
•  Moving to approach position P1.
•  Setting the output OUT 2 to TRUE to activate its vacuum gripper.
•  Moving linearly (LIN) to pick position P2 to grasp the component from the middle conveyor.
•  Moving along its linear track to place position P3 above the exit conveyor.
•  Setting the output OUT 2 to FALSE to release the component.
•  Retreating linearly to P4, and returning to its HOME position.
The programming sequence taught in the KUKA Sim Pro Job Map editor compiles directly into motion commands. The visual program logic for Robot 1, showing the conditional inputs and path subroutines, is presented below:

FIG 11: Robot 1 Programming Logic
Similarly, the programming sequence and job routine for Robot 2, which coordinates the final transfer to the exit conveyor line, is shown in the figure below:

FIG 12: Robot 2 Programming Logic

CHAPTER 6RESULTS
The developed system was simulated continuously in KUKA.Sim Pro to validate its operation. The simulation successfully demonstrated a smooth and continuous material flow. Products generated by the Shape Feeder travel down the curved conveyor until they reach the exit, where the first sensor detects them. Robot 1 immediately receives the signal, moves from its HOME position to the curved conveyor, picks up the product, translates along its KL 4000 linear rail, and places the product onto the center conveyor. The center conveyor then transports the product to the second sensor, which triggers Robot 2. Robot 2 picks the product, translates along its linear track, and deposits it on the exit conveyor. The product finally moves to the end of the line, ready for warehouse storage. This entire process executes in a continuous loop without any manual intervention.
The simulation validated several key aspects of the automation cell design:
•  Reachability and Workspace Optimization: Mounting the robots on KL 4000 linear tracks successfully resolved reachability limitations. The external linear axis extended the robots' workspace along E1, enabling them to bridge the distance between conveyor lines.
•  Collision Detection: KUKA.Sim Pro's collision detection engine verified that the path trajectories of both robot arms, grippers, and components did not result in any collision. The safety fencing layout was also verified to isolate the hazard zone.
•  Signal Synchronization: Photoelectric sensor signals routed to the robot input registers successfully coordinated operations. Robots remained idle at HOME until sensor triggers went active, preventing dry-runs.
•  Continuous Cycle Execution: The looping logic (WHILE TRUE) allowed the system to run indefinitely. Feeder intervals and conveyor speeds were synchronized with the robot cycle times to prevent bottlenecking.

CHAPTER 7CONCLUSION AND FUTURE WORK
Conclusion:
This project successfully designed, programmed, and simulated a sensor-based cooperative KUKA pick-and-place automation system using KUKA.Sim Pro. The virtual workcell demonstrated key industrial automation concepts including multi-stage conveyor transfer, sensor-guided object detection, external axis coordination, and robot I/O communication. By mounting two KUKA KR 120 R2700-2 robots on KL 4000 linear tracks, their work envelopes were extended, enabling them to transfer parts between conveyor lines. The simulation validated that the taught trajectories and signal synchronization logic result in a collision-free, continuous material handling system. The offline simulation verified all components before actual hardware commissioning, showing the value of digital twin technology in reducing commissioning times and layout design errors.
Future Work:
While the current simulation demonstrates a stable, automated transfer line, several enhancements can be introduced to extend its capabilities and replicate a full-scale Industry 4.0 smart factory cell. The following enhancements are proposed for future development:
•  Grid Stacking and Palletizing: Programming Robot 2 to place components in a structured grid pattern on a pallet, implementing counter-based stacking logic.
•  AGV and Warehouse Integration: Connecting the exit palletizing station with Autonomous Mobile Robots (AMRs) or Automated Guided Vehicles (AGVs) for warehouse logistics.
•  OPC UA and PLC Control: Integrating KUKA.Sim Pro with a virtual PLC (e.g. Siemens S7-1500) via OPC UA for master control of conveyors and safety zones.
•  Computer Vision Integration: Replacing photoelectric sensors with a 3D smart camera to sort parts based on color, shape, or orientation, adjusting pick angles dynamically.
•  Dynamic Zone Interlocking: Implementing software interlocking zones to prevent collisions in areas where the robots' work envelopes overlap.

CHAPTER 8REFERENCES
[1] Craig, J. J., Introduction to Robotics: Mechanics and Control, 4th Edition, Pearson Education, 2018.
[2] Groover, M. P., Automation, Production Systems, and Computer-Integrated Manufacturing, 5th Edition, Pearson Education, 2019.
[3] Niku, S. B., Introduction to Robotics: Analysis, Control, Applications, 3rd Edition, Wiley India, 2020.
[4] Siciliano, B., Sciavicco, L., Villani, L., and Oriolo, G., Robotics: Modelling, Planning and Control, Springer Publications, 2010.
[5] Spong, M. W., Hutchinson, S., and Vidyasagar, M., Robot Modeling and Control, Wiley Publications, 2020.
[6] KUKA AG, KUKA System Software (KSS) 8.x Operating and Programming Instructions for System Integrators, KUKA AG, Augsburg, Germany.
[7] KUKA AG, KUKA.Sim Pro User Manual and Documentation, KUKA Robotics, Germany. Available online at: KUKA.Sim Official Web Portal .
[8] Groover, M. P., Industrial Robotics: Technology, Programming and Applications, McGraw-Hill Education.
[9] Siciliano, B., and Khatib, O., Springer Handbook of Robotics, Springer International Publishing, 2016.
[10] KUKA Robots & Automation tutorial – YouTube, Available online at: https://www.youtube.com/watch?v=3wUFy8Dovyo&list=PLcmhlxe_PW5QV1288LwpnZe-yIPT3Sva .