# VEX Robotics Project – Autonomous Beacon-Seeking Robot

This repository contains the complete source code for a VEX Robotics autonomous robot project developed in **Fall 2024** using **VEXcode V5** and **RobotC** syntax. The robot was designed to identify and respond to red and green infrared (IR) beacons using a custom IR sensing circuit and programmed behavior logic.

---

## Project Overview

### Objective:
The robot autonomously:
- Searches for and navigates toward IR beacons.
- Uses photo-diode readings to estimate direction and proximity.
- Interacts with beacon objects using a continuous-rotation arm mechanism.
- Switches between red and green beacon detection phases.
- Responds to touch sensors and proximity to shift control states.

### Key Features:
- **Beacon detection** using analog IR intensity (custom Expose-and-Read function).
- **Sensor integration**: limit switches, analog photo-diodes, digital outputs.
- **Arm manipulation**: servo control to raise/lower mechanisms based on proximity.
- **State machine**: multiple phases to handle different beacon interactions.
- **Failsafe motion logic**: search-spin, forward/backward motion, reactive stopping.

---

## Hardware Configuration

The project uses **RobotC-style configuration directives**, including:

- **Motors:**
  - `leftMotor`, `rightMotor`: Drive system
  - `armMotor`: Continuous rotation arm
- **Sensors:**
  - `analog1`: Custom IR sensing circuit
  - `limitSwitch`, `btnSwitch`: Touch sensors
  - `digital10–12`: Custom digital outputs for shutter control, beacon frequency

For full configuration details, see the `#pragma config` section at the top of `main.c`.

---

## Behavior Logic

The robot is built around a state-based autonomous control system:
1. **Wait for Start**: Starts when the button switch is pressed.
2. **Red Beacon Phase**:
   - Seeks IR signal (1kHz), aligns, and stops on contact.
   - Performs interaction with arm.
3. **Green Beacon Phase**:
   - Switches frequency to 10kHz and repeats approach.
   - Executes final behavior (e.g., backing up or navigating a set route).

Key functions include:
- `Expose_and_read()`: Controls sensor shutter and returns intensity.
- `ReadPD()`: Collects 8 PD readings and computes IR signal strength.
- `Find_max()`: Determines strongest sensor for directional alignment.
- `Move()`: Calculates motor output based on signal strength and direction.

---

## Files

- `main.c`: Full autonomous behavior code for the VEX robot.
- `.vscode/`: (Optional for GitHub use) Placeholder if project is later adapted for VS Code or PROS.
- `README.md`: This file.

---

## How to Use

1. Open this project in **RobotC**.
2. Upload to a compatible VEX Cortex controller.
3. Ensure sensor and motor ports match `#pragma config` settings.
4. Power on the robot and press the button switch to start.

---

## Author Contributions

This project was developed as part of a VEX Robotics team effort. My primary responsibilities included:

- Writing and debugging autonomous behavior logic.
- Calibrating IR sensor exposure and gain.
- Designing state transitions and steering sensitivity logic.
- Implementing motor control functions with PWM limiting and steering control.

---
