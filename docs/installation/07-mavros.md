# Chapter 2.7 — MAVROS

**Estimated Time:** 10–20 minutes

---

# Overview

MAVROS is a ROS package that provides communication between PX4 and ROS
using the MAVLink communication protocol.

Within the Drone EGO Swarming project, MAVROS is primarily used to
provide vehicle state information such as odometry and position.

Although the project communicates with PX4 primarily through
Micro XRCE-DDS, MAVROS is still required because EGO Planner expects
certain information through MAVROS topics.

---

# What is MAVROS?

MAVROS (MAVLink extendable communication node for ROS) is an interface
between ROS and MAVLink-compatible flight controllers.

It converts MAVLink messages into ROS topics and services.

Examples include:

- vehicle position
- vehicle orientation
- GPS information
- IMU data
- vehicle state
- odometry

MAVROS has become the standard ROS interface for PX4 and ArduPilot.

---

# Why is MAVROS Required?

Although PX4 communicates with ROS 2 using Micro XRCE-DDS, the current
EGO Planner implementation also expects vehicle information through
MAVROS.

During testing, the planner subscribed to:

```text
/mavros/local_position/odom
```

This odometry information allows the planner to know the current vehicle
position while generating trajectories.

Without MAVROS, the planner will not receive the odometry information
expected by the current implementation.

---

# How MAVROS Fits Into Drone EGO Swarming

```text
PX4

↓

MAVLink

↓

**MAVROS**

↓

ROS 2

↓

EGO Planner
```

MAVROS supplies odometry information while the Micro XRCE-DDS Agent
provides PX4 message communication.

Both communication paths are used throughout this project.

---

# Official Documentation

MAVROS

https://docs.ros.org/en/humble/p/mavros/

GitHub Repository

https://github.com/mavlink/mavros

---

# Installation

Install MAVROS and the additional plugins.

```bash
sudo apt update

sudo apt install -y \
ros-humble-mavros \
ros-humble-mavros-extras
```

---

# Install GeographicLib Datasets

MAVROS requires GeographicLib datasets for geographic coordinate
transformations.

Install them using:

```bash
sudo /opt/ros/humble/lib/mavros/install_geographiclib_datasets.sh
```

This only needs to be completed once.

---

# Verify Installation

Verify the package exists.

```bash
ros2 pkg prefix mavros
```

Expected:

A valid installation path.

---

Verify the package list.

```bash
ros2 pkg executables mavros
```

Expected:

A list of available MAVROS executables.

---

Verify GeographicLib installation.

```bash
ls /usr/share/GeographicLib
```

Expected:

The GeographicLib directory should exist.

---

# Common Issues

---

## `Package 'mavros' not found`

Cause

MAVROS was not installed successfully.

Solution

Install:

```bash
sudo apt install \
ros-humble-mavros \
ros-humble-mavros-extras
```

---

## GeographicLib missing

Symptoms include:

- geographic conversion errors
- startup warnings
- missing datasets

Solution

Run:

```bash
sudo /opt/ros/humble/lib/mavros/install_geographiclib_datasets.sh
```

---

## No odometry topics

Verify MAVROS has connected to PX4.

Later in the manual, this project launches MAVROS using:

```text
udp://:14540@127.0.0.1:14555
```

Once connected, verify:

```bash
ros2 topic list | grep mavros
```

---

# Completion Checklist

Before continuing, check:

- [ ] MAVROS installed successfully.
- [ ] GeographicLib installed.
- [ ] `ros2 pkg prefix mavros` returns a valid path.
- [ ] MAVROS executables are available.

---

# Transition

The Drone EGO Swarming project now has both communication paths required
by the software stack:

- Micro XRCE-DDS for PX4 message communication.
- MAVROS for MAVLink-based odometry and vehicle information.

The next chapter installs the ground control station used throughout
development.

➡ Continue to **Chapter 2.8 — QGroundControl**
