# Chapter 2.2 — ROS 2 Humble

**Estimated Time:** 20–40 minutes

---

# Overview

ROS 2 (Robot Operating System 2) is the communication framework used
throughout the Drone EGO Swarming project.

Unlike a traditional application where everything runs inside one
program, this project consists of many independent processes:

- PX4 Autopilot
- Gazebo
- RViz
- MAVROS
- Micro XRCE-DDS Agent
- EGO Planner
- Keyboard Publisher
- EGO-to-PX4 Bridge

ROS 2 allows all of these independent applications to exchange
information through topics, services, parameters, and actions.

Without ROS 2, none of these components would be able to communicate.

---

# What is ROS 2?

ROS 2 (Robot Operating System 2) is an open-source robotics middleware.

It is **not** an operating system.

Instead, it provides:

- message passing
- distributed communication
- package management
- launch systems
- visualization support
- logging
- debugging
- parameter management

Every software component in this repository communicates using ROS 2.

Examples include:

```text
RViz
        ↓
    /goal_pose

        ↓

EGO Planner

        ↓

/drone_0_planning/pos_cmd

        ↓

PX4 Bridge

        ↓

/fmu/in/trajectory_setpoint

        ↓

PX4
```

Without ROS 2, this message flow would not exist.

---

# Why ROS 2 Humble?

The Drone EGO Swarming project was developed and validated using:

```text
Ubuntu 22.04 LTS
ROS 2 Humble
```

ROS 2 Humble was selected because it is:

- the official ROS distribution for Ubuntu 22.04,
- stable,
- long-term supported,
- compatible with PX4,
- compatible with Gazebo Harmonic,
- compatible with MAVROS,
- compatible with EGO Planner.

Using another ROS distribution (Iron, Jazzy, Rolling, etc.) may require:

- newer dependencies,
- modified launch files,
- updated message definitions,
- different package names,
- or changes to this repository.

For the most reproducible setup, use ROS 2 Humble.

---

# ROS 2 in Drone EGO Swarming

Every major software component communicates through ROS 2.

```text
RViz
│
├── publishes goals
│
▼

EGO Planner
│
├── publishes trajectories
│
▼

PX4 Bridge
│
├── converts ENU → NED
│
▼

PX4

▲

Micro XRCE DDS

▲

ROS2
```

Notice that ROS 2 is the communication layer connecting the entire
software stack.

---

# DDS Communication

ROS 2 communicates using DDS (Data Distribution Service).

DDS allows software components to exchange information without needing
to know where every other component is running.

Instead of directly talking to one another, each node simply:

publishes

or

subscribes

to a topic.

Example:

```text
RViz

publishes

/goal_pose
```

while

```text
EGO Planner
```

subscribes to

```text
/goal_pose
```

The two programs never communicate directly.

ROS 2 handles everything in between.

---

# Official Documentation

ROS 2 Documentation

https://docs.ros.org/en/humble/

Official Ubuntu Installation Guide

https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html

Follow the official installation guide before returning to this manual.

---

# Installing ROS 2 Humble

Follow the official ROS 2 Humble installation guide.

Do **not** skip any dependency installation steps.

After installation, return here.

---

# Configure the ROS Environment

ROS 2 must be sourced before ROS commands become available.

Temporarily source ROS:

```bash
source /opt/ros/humble/setup.bash
```

Verify:

```bash
ros2 --help
```

If successful, make this permanent:

```bash
echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc
```

Reload Bash:

```bash
source ~/.bashrc
```

Every future terminal should automatically load ROS 2.

---

# Verify ROS Installation

## Verify ROS command line

Run:

```bash
ros2 --help
```

Expected:

```text
ROS 2 command help appears.
```

---

## Verify the installed ROS distribution

Run:

```bash
echo $ROS_DISTRO
```

Expected:

```text
humble
```

---

## Verify ROS version

Run:

```bash
printenv | grep ROS
```

Expected variables include:

```text
ROS_DISTRO=humble

ROS_VERSION=2
```

---

## Verify the setup script

Run:

```bash
ls /opt/ros/humble/
```

Expected folders include:

```text
bin
include
lib
share
setup.bash
```

---

## Verify Python packages

Run:

```bash
python3 -c "import rclpy; print('ROS2 Python OK')"
```

Expected:

```text
ROS2 Python OK
```

---

# Common ROS Commands

These commands will be used repeatedly throughout the Drone EGO
Swarming project.

```bash
ros2 topic list

ros2 topic echo

ros2 topic info

ros2 topic hz

ros2 node list

ros2 node info

ros2 pkg prefix

ros2 run

ros2 launch
```

Do not worry about understanding every command yet.

Each command will be introduced later.

---

# Common Issues

---

## `ros2: command not found`

Cause

ROS has not been sourced.

Solution

Run:

```bash
source /opt/ros/humble/setup.bash
```

Then verify:

```bash
ros2 --help
```

---

## `$ROS_DISTRO` is empty

Cause

The ROS environment has not been loaded.

Solution

Run:

```bash
source /opt/ros/humble/setup.bash
```

or

```bash
source ~/.bashrc
```

---

## `rclpy` import failed

Cause

ROS Python packages are not installed correctly.

Solution

Revisit the official ROS installation guide and verify that all desktop
packages were installed.

---

## ROS commands disappear after opening a new terminal

Cause

The ROS setup script was not added to `.bashrc`.

Solution

Add:

```bash
echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc
```

Reload:

```bash
source ~/.bashrc
```

---

# Completion Checklist

Before continuing, verify:

- [ ] `ros2 --help` executes successfully.
- [ ] `echo $ROS_DISTRO` returns `humble`.
- [ ] `/opt/ros/humble/setup.bash` exists.
- [ ] Python can import `rclpy`.
- [ ] New terminals automatically recognize the `ros2` command.

---

# How ROS 2 Fits Into Drone EGO Swarming

ROS 2 is the communication backbone of the project.

Every planner command, vehicle state, visualization message, sensor
measurement, and debugging command passes through ROS 2.

```text
Ubuntu

↓

ROS 2

↓

Gazebo
PX4
RViz
MAVROS
XRCE Agent
EGO Planner
Keyboard Publisher
PX4 Bridge
```

Without ROS 2, the Drone EGO Swarming system cannot function.

The next chapter installs the simulation environment that will provide
the virtual world, sensors, and vehicle physics used throughout the
remainder of this manual.

➡ **Chapter 2.3 — Gazebo Harmonic**
