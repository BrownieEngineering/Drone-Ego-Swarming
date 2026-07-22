# Chapter 2.3 — Gazebo Harmonic

**Estimated Time:** 15–30 minutes

---

# Overview

Gazebo Harmonic is the robotics simulator used throughout the Drone EGO
Swarming project.

Rather than testing flight software on a physical drone, Gazebo provides
a realistic virtual environment that simulates:

- vehicle physics,
- gravity,
- collisions,
- cameras,
- lidar,
- point clouds,
- depth images,
- and environmental obstacles.

Throughout this project, Gazebo is responsible for generating the world
that PX4 and EGO Planner interact with.

---

# What is Gazebo?

Gazebo is an open-source robotics simulator used by researchers,
universities, and robotics companies around the world.

Instead of writing software directly on physical hardware, Gazebo allows
developers to safely test algorithms inside a simulated environment.

For this project Gazebo simulates:

- the X500 quadrotor,
- the EGO obstacle world,
- camera sensors,
- depth images,
- lidar data,
- and the complete flight environment.

This allows autonomous navigation to be developed without risking
physical hardware.

---

# Why Gazebo Harmonic?

The Drone EGO Swarming project was tested using:

```text
Gazebo Harmonic
```

Gazebo Harmonic was selected because it is compatible with:

- Ubuntu 22.04
- ROS 2 Humble
- PX4 Autopilot
- ros_gz_bridge

Earlier Gazebo versions use different package names and may require
additional modifications to launch files or bridge configurations.

For the most reproducible installation, use Gazebo Harmonic.

---

# How Gazebo Fits Into Drone EGO Swarming

Gazebo provides the virtual world that the remainder of the software
stack operates within.

```text
Gazebo World

        │

        ├── Drone Model

        ├── Camera

        ├── Depth Image

        ├── Point Cloud

        └── Physics

                │

                ▼

PX4 SITL

        │

        ▼

ROS 2

        │

        ▼

EGO Planner

        │

        ▼

RViz
```

Without Gazebo, PX4 would have no simulated aircraft and EGO Planner
would receive no environmental information.

---

# Official Documentation

Gazebo

https://gazebosim.org/

ROS Gazebo Packages

https://gazebosim.org/docs

ROS-Gazebo Bridge

https://github.com/gazebosim/ros_gz

---

# Installing Gazebo Harmonic

The Drone EGO Swarming project uses the ROS-distributed Gazebo packages.

Install Gazebo Harmonic using:

```bash
sudo apt update

sudo apt install -y \
ros-humble-ros-gzharmonic \
ros-humble-ros-gz-bridge
```

Do **not** install only:

```bash
sudo apt install gz-harmonic
```

The standalone Gazebo package does not install the ROS bridge packages
required by this project.

---

# Required ROS Bridge Packages

The project relies on:

```text
ros_gz_bridge
```

This package translates messages between:

```text
Gazebo

↓

ROS 2
```

Examples include:

- depth images
- point clouds
- camera data
- sensor information

Without this bridge, ROS 2 cannot receive Gazebo sensor data.

---

# Verify Gazebo

Run:

```bash
gz sim --version
```

Expected:

A Gazebo Harmonic version number.

---

Verify the ROS bridge package:

```bash
ros2 pkg prefix ros_gz_bridge
```

Expected:

A valid package path is returned.

---

Verify Gazebo launches:

```bash
gz sim
```

The Gazebo simulator should open successfully.

Close Gazebo before continuing.

---

# Common Issues

---

## `gz: command not found`

Cause

Gazebo was not installed successfully.

Solution

Verify that the Gazebo packages were installed correctly.

---

## `ros_gz_bridge` package missing

Cause

Only the standalone Gazebo package was installed.

Solution

Install:

```bash
sudo apt install \
ros-humble-ros-gzharmonic \
ros-humble-ros-gz-bridge
```

---

## Gazebo opens but displays a black screen

Possible causes include:

- unsupported graphics drivers,
- integrated graphics,
- missing OpenGL support.

Verify the NVIDIA driver is functioning correctly.

---

## Gazebo runs slowly

Simulation performance depends heavily on:

- CPU performance,
- GPU performance,
- available memory,
- sensor update rates.

The tested GTX 1060 successfully ran the project but provided only
moderate performance under the complete simulation stack.

Newer NVIDIA GPUs will improve simulation performance.

---

# Completion Checklist

Before continuing, verify:

- [ ] Gazebo Harmonic is installed.
- [ ] `gz sim --version` executes successfully.
- [ ] `ros_gz_bridge` is installed.
- [ ] Gazebo launches successfully.
- [ ] Gazebo closes without errors.

---

# Transition

The simulation environment has now been installed.

The next chapter installs the flight controller responsible for
controlling the simulated drone.

➡ **Chapter 2.4 — PX4 Autopilot**
