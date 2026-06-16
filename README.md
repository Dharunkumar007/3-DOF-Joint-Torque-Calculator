# 🦾 3-DOF Robotic Arm Joint Torque Calculator

[![Live Demo](https://img.shields.io/badge/Live_Demo-Play_Now-success?style=for-the-badge)](https://3-dof-joint-torque-calculator.vercel.app/)

Building a robotic arm is incredibly fun right up until it tries to lift a payload and the shoulder motor burns out, turning your project into a very expensive, very heavy paperweight. 

This professional-grade, lightweight web tool takes the guesswork out of robotic mechanical design. It calculates the exact **Static (holding)** and **Dynamic (accelerating)** torques required for a 3-Degree-of-Freedom (3-DOF) articulated manipulator. 

---

## 🎯 Why This Tool is Critical for 3-DOF Manipulators

When designing a 3-DOF robotic arm (Shoulder, Elbow, and Wrist), you are primarily battling **gravity**. 

Unlike the base rotation joint (which only fights rotational inertia and friction), the vertical-plane joints carry heavily cantilevered loads. If you mount a 2.5kg motor and a 3.2kg gearbox at the elbow, that 5.7kg mass acts as a massive anchor dragging the shoulder down. 

This calculator uses an **O(N) Reverse Accumulation Algorithm** starting at the gripper and working mathematically backward to the shoulder to account for every gram of distal mass. It tells you exactly how much rotational force is required to:
1. Hover perfectly horizontal (Static Torque).
2. Snap upwards against gravity (Max Strain / Lifting).
3. Act as a brake during a controlled descent (Min Strain / Lowering).

*Note: This tool specifically calculates torques for the gravity-fighting joints (Shoulder, Elbow, Wrist) and excludes the base panning joint, which requires a completely different (and generally much lower) torque profile.*

---

## ⚙️ New: Dual-Mode Architecture

Not all robots are built the same. Version 2.0 introduces a **Mode Selector** to handle different manufacturing techniques:

* **Hollow Cylinder Mode:** Perfect for arms built using standard aluminum tubing or carbon fiber pipes. The math engine automatically calculates volume and mass based on your outer diameter (OD), inner diameter (ID), and material density.
* **Custom Shape Mode:** Essential if you are using complex geometries like topology-optimized 3D-printed links, custom Lost Foam Cast aluminum chassis, or irregular structural brackets. Just select this mode, bypass the dimensional math, and directly input the total mass of your custom link.

---

## 🛠️ How to Use This with Your CAD Design

You don't need to be a physics professor to use this. Just bridge the gap between your CAD software (SolidWorks, Fusion 360, etc.) and your motor supplier!

1. **Select Your Mode:** Choose either *Hollow Cylinder* or *Custom Shape* at the top of the dashboard. The UI will dynamically adjust to show only the inputs you need.
2. **Extract the Specs:** Pull the dimensions or mass properties from your design:
   * Link lengths (from joint center to joint center).
   * OD/ID and Density (if using standard tubes) **OR** Total Link Mass (if using custom geometries).
   * Estimated weights of the mechanical hardware (flanges, bearings, bolts).
3. **Pick a "Trial" Motor:** Look at a motor and gearbox catalog and note their physical weights.
4. **Plug it In:** Enter these numbers into the calculator, along with your target Angular Acceleration.
5. **Analyze & Buy:** The dashboard will immediately output the **Max Required Torque**. If your trial motor/gearbox combination can output that much torque (in Nm or kgf·cm), you are ready to buy! If not, pick a larger gearbox and run the numbers again.

---

## ✨ Key Features

* **Dynamic UI Engine:** The interface intelligently hides or reveals fields (like Gearbox Weight and Safety Margins) based on your selected link type to keep the workspace clean and relevant.
* **Real-Time Physics:** Instantly calculates Mass, Volume, Rotational Inertia ($I$), and Dynamic Lever Arms.
* **Granular Hardware Profiling:** Separates the weight of the raw links from the heavy point-masses of motors and gearboxes.
* **Safety Factor Multipliers:** Industrially standard inputs to guarantee your motors have sufficient overhead.
* **Zero Dependencies:** Written in vanilla JavaScript with Tailwind CSS. No Node modules, no build steps, no lag.
* **Context-Aware Excel Export:** One-click CSV generation that automatically adapts its columns based on whether you used Hollow or Custom geometries, allowing you to save design iterations and share them with your engineering team.

---

## 💻 Running It Locally on Your PC

Want to run this offline or tweak the code yourself? It couldn't be easier. Because it is a single-file application, you do not need to install any heavy web frameworks.

### Option 1: Direct Download (Easiest)
1. Go to the top of this GitHub repository.
2. Click the green **Code** button and select **Download ZIP**.
3. Extract the downloaded ZIP file to your desktop.
4. Double-click the `index.html` file to open it directly in Chrome, Edge, Firefox, or Safari.

### Option 2: Git Clone (Recommended)
Open your terminal or command prompt and run:

```bash
# 1. Clone the repository
git clone [https://github.com/your-username/robotics-torque-calculator.git](https://github.com/your-username/robotics-torque-calculator.git)

# 2. Navigate into the folder
cd robotics-torque-calculator

# 3. Open the file in your default web browser
# On Windows:
start index.html
# On macOS:
open index.html
# On Linux (Ubuntu):
xdg-open index.html
