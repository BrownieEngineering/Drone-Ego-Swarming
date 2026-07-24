# Chapter 4.2 — Integrating the PX4 Bridge

**Estimated Time:** 15–20 minutes

---

# Overview

The Drone EGO Swarming project uses a custom bridge package to establish
communication between the EGO Planner and the PX4 flight controller.

The EGO Planner generates smooth, collision-free trajectories based on
user-defined goals and environmental information. While these
trajectories describe where the vehicle should travel, PX4 requires
commands formatted using its own message definitions and communication
interfaces.

The PX4 bridge is responsible for translating planner output into
commands that the flight controller can execute while continuously
monitoring vehicle state throughout the mission.

Without this bridge, the EGO Planner and PX4 operate as independent
systems and autonomous flight cannot be achieved.

---

# Purpose of the PX4 Bridge

The bridge serves as the communication layer between the planning
software and the flight controller.

Its primary responsibilities include:

- Receiving trajectory information from the EGO Planner.
- Converting planner output into PX4-compatible messages.
- Publishing trajectory setpoints to PX4.
- Monitoring vehicle state information.
- Maintaining communication required for Offboard flight.

By separating these responsibilities into a dedicated package, the
planner remains independent of the flight controller while allowing each
system to operate using its native interfaces.

---

# Bridge Package Location

Within the ROS workspace, the bridge package is located at:

```text
~/ego_ws/src/px4_ego
```

This package contains the ROS 2 nodes responsible for communication with
PX4.

After building the workspace, the package becomes available through the
standard ROS 2 environment.

---

# How the Bridge Fits Into the System

The bridge connects the planner with the PX4 flight controller as shown
below.

```text
RViz

↓

EGO Planner

↓

PX4 Bridge

↓

PX4 Offboard Controller

↓

Gazebo Simulation
```

Once the vehicle begins moving, state information is returned through
the communication pipeline, allowing the planner to continuously update
future trajectories.

---

# Building the Bridge Package

Whenever modifications are made to the bridge source code, rebuild the
package before launching the system.

Navigate to the ROS workspace.

```bash
cd ~/ego_ws
```

Load the ROS environment.

```bash
source /opt/ros/humble/setup.bash
```

Build the bridge package.

```bash
colcon build --packages-select px4_ego_py --symlink-install
```

Reload the workspace.

```bash
source install/setup.bash
```

---

# Verifying the Bridge

Confirm that ROS recognizes the bridge package.

```bash
ros2 pkg prefix px4_ego_py
```

A valid installation path should be returned.

Next, verify that the package provides executable nodes.

```bash
ros2 pkg executables px4_ego_py
```

One or more bridge executables should be listed.

---

# Development Notes

During development, the bridge package was rebuilt frequently while
testing communication between the EGO Planner and PX4.

Rather than rebuilding the entire workspace after every change, only the
bridge package was rebuilt using:

```bash
colcon build --packages-select px4_ego_py --symlink-install
```

This significantly reduced iteration time while debugging the project.

---

# Common Issues

---

## Package cannot be found

Cause

The workspace has not been built or sourced.

Solution

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

Rebuild the package if necessary.

---

## Source code changes do not appear

Cause

The modified package has not been rebuilt.

Solution

```bash
colcon build --packages-select px4_ego_py --symlink-install
```

Restart any running bridge nodes before testing again.

---

## Bridge starts but the vehicle does not respond

Cause

The bridge is operating correctly, but communication with PX4 has not
been established.

Possible causes include:

- Micro XRCE-DDS Agent is not running.
- PX4 is not in Offboard mode.
- Required ROS topics are unavailable.
- Launch sequence was not followed.

These communication checks are covered later in this chapter.

---

# Completion Checklist

Before continuing, verify:

- [ ] The `px4_ego` package exists in the workspace.
- [ ] The bridge package builds successfully.
- [ ] ROS recognizes the bridge package.
- [ ] Bridge executables are available.
- [ ] The workspace has been sourced after building.

---

# Transition

With the PX4 bridge integrated into the workspace, the next section
documents the launch file modifications required to start the Drone EGO
Swarming system and establish communication between all major
components.

➡ Continue to **Chapter 4.3 — Modifying PX4 Launch Files**
