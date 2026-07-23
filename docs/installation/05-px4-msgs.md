# Chapter 2.5 — px4_msgs

**Estimated Time:** 10–20 minutes

---

# Overview

The `px4_msgs` package provides the ROS 2 message definitions used to
communicate with PX4.

While PX4 itself controls the aircraft, ROS 2 applications cannot
understand PX4 data unless they share the same message definitions.

The `px4_msgs` package serves as the common language between ROS 2 and
PX4.

Without `px4_msgs`, the Drone EGO Swarming project cannot exchange
trajectory commands, vehicle states, or flight-control messages with
PX4.

---

# What is px4_msgs?

`px4_msgs` is a ROS 2 message package automatically generated from PX4's
uORB message definitions.

These messages expose PX4 information to ROS 2.

Examples include:

- VehicleStatus
- VehicleCommand
- VehicleCommandAck
- VehicleLocalPosition
- OffboardControlMode
- TrajectorySetpoint
- VehicleOdometry
- Timesync

Every ROS node communicating directly with PX4 depends on these message
definitions.

---

# Why is px4_msgs Required?

Within the Drone EGO Swarming project, several components communicate
directly with PX4.

Examples include:

- the EGO-to-PX4 bridge,
- the keyboard publisher,
- trajectory publishers,
- debugging tools,
- and vehicle monitoring nodes.

Without `px4_msgs`, ROS 2 would not know how to interpret PX4 messages.

---

# Why This Version?

The version of `px4_msgs` **must** match the PX4 version used by the
project.

This repository was tested using:

```text
PX4 Commit:
25b7d627da
```

Using a different PX4 version together with mismatched message
definitions can result in:

- missing topics,
- incompatible message fields,
- build failures,
- or unexpected runtime behavior.

Whenever PX4 is updated, verify that the corresponding `px4_msgs`
package is also updated.

---

# How px4_msgs Fits Into Drone EGO Swarming

The message package sits directly between ROS 2 and PX4.

```text
ROS 2 Nodes

↓

px4_msgs

↓

Micro XRCE-DDS

↓

PX4
```

Examples of project communication:

```text
TrajectorySetpoint

↓

PX4

VehicleStatus

↓

ROS 2
```

Without `px4_msgs`, neither direction of communication would be possible.

---

# Official Documentation

PX4 ROS 2 User Guide

https://docs.px4.io/main/en/ros2/

PX4 Messages Repository

https://github.com/PX4/px4_msgs

---

# Installation

Clone the message repository inside your ROS workspace.

```bash
cd ~/ego_ws/src

git clone https://github.com/PX4/px4_msgs.git
```

Return to the workspace.

```bash
cd ~/ego_ws
```

Build the package.

```bash
source /opt/ros/humble/setup.bash

colcon build --packages-select px4_msgs
```

After the build completes, source the workspace.

```bash
source install/setup.bash
```

---

# Verify Installation

Verify that ROS recognizes the package.

```bash
ros2 pkg prefix px4_msgs
```

Expected:

A valid package installation path.

Example:

```text
/home/<username>/ego_ws/install/px4_msgs
```

---

Verify that message definitions exist.

```bash
ros2 interface list | grep px4_msgs
```

Expected:

A list of PX4 message definitions.

---

Verify one message definition.

```bash
ros2 interface show px4_msgs/msg/TrajectorySetpoint
```

Expected:

The complete ROS definition of the message is displayed.

---

# Common Issues

---

## Package not found

Cause

The package was not cloned into the workspace.

Solution

Verify:

```bash
ls ~/ego_ws/src
```

The `px4_msgs` directory should be present.

---

## Build failed

Cause

The workspace was not sourced correctly.

Solution

Run:

```bash
source /opt/ros/humble/setup.bash
```

Then rebuild:

```bash
colcon build --packages-select px4_msgs
```

---

## `ros2 pkg prefix px4_msgs` returns nothing

Cause

The workspace has not been sourced.

Solution

Run:

```bash
source ~/ego_ws/install/setup.bash
```

or open a new terminal if the workspace has already been added to
`.bashrc`.

---

## Message definitions do not match PX4

Cause

The PX4 source version and `px4_msgs` version differ.

Solution

Ensure that both repositories are using compatible versions.

If PX4 is updated, update `px4_msgs` accordingly.

---

# Completion Checklist

Before continuing, verify:

- [ ] `px4_msgs` cloned successfully.
- [ ] Package builds successfully.
- [ ] Workspace sourced.
- [ ] `ros2 pkg prefix px4_msgs` returns a valid path.
- [ ] Message definitions can be displayed.
- [ ] `TrajectorySetpoint` interface is available.

---

# Transition

PX4 and ROS 2 now share a common message definition package.

The next chapter installs the middleware responsible for transporting
those messages between PX4 and ROS 2.

➡ Continue to **Chapter 2.6 — Micro XRCE-DDS Agent**
