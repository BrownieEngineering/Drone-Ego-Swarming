# Chapter 2.6 — Micro XRCE-DDS Agent

**Estimated Time:** 15–30 minutes

---

# Overview

The Micro XRCE-DDS Agent is responsible for transporting information
between PX4 Autopilot and ROS 2.

PX4 does not communicate directly with ROS 2.

Instead, PX4 publishes and subscribes to uORB topics internally.
The Micro XRCE-DDS Agent acts as a translator between PX4's internal
communication system and the ROS 2 DDS network.

Without this agent, ROS 2 cannot send commands to PX4 or receive
vehicle status information.

---

# What is Micro XRCE-DDS?

DDS stands for **Data Distribution Service**.

ROS 2 uses DDS as its communication middleware.

PX4, however, does not directly use ROS 2 DDS.

Instead, PX4 contains a lightweight DDS client known as the
**uXRCE-DDS Client**.

The Micro XRCE-DDS Agent connects this client to the ROS 2 network.

Think of it as a bridge:

```text
PX4

↓

uXRCE-DDS Client

↓

Micro XRCE-DDS Agent

↓

ROS 2 DDS

↓

ROS Nodes
```

Every PX4 message seen inside ROS 2 passes through this bridge.

---

# Why is it Required?

The Drone EGO Swarming project relies on ROS 2 to generate trajectories.

Those trajectories must eventually reach PX4.

Likewise, PX4 must continuously publish:

- vehicle status
- local position
- odometry
- acknowledgements
- timestamps

Without the XRCE Agent, these topics never appear inside ROS 2.

The bridge is therefore one of the most critical components of the
entire project.

---

# Why This Version?

The Micro XRCE-DDS Agent is developed by eProsima and is maintained
alongside the DDS ecosystem used by ROS 2 and PX4.

This project was tested using the version installed by the PX4
development environment.

Always verify compatibility with:

- Ubuntu 22.04
- ROS 2 Humble
- PX4 commit `25b7d627da`

---

# How Micro XRCE-DDS Fits Into Drone EGO Swarming

This component sits directly between ROS 2 and PX4.

```text
RViz

↓

EGO Planner

↓

PX4 Bridge

↓

ROS 2 DDS

↓

Micro XRCE-DDS Agent

↓

PX4

↓

Gazebo
```

Notice that every PX4 message travels through this component.

Examples include:

```text
TrajectorySetpoint

VehicleStatus

VehicleCommand

VehicleLocalPosition

VehicleOdometry

OffboardControlMode
```

---

# Official Documentation

Micro XRCE-DDS

https://micro-xrce-dds.docs.eprosima.com/

PX4 ROS 2 Documentation

https://docs.px4.io/main/en/ros2/

---

# Installation

The PX4 Ubuntu setup script installs the required dependencies for
the Micro XRCE-DDS Agent.

If the agent is not already available on your system, follow the
official PX4 documentation for installation.

After installation, verify that the executable exists.

```bash
which MicroXRCEAgent
```

Expected output:

```text
/usr/local/bin/MicroXRCEAgent
```

Your installation path may differ.

---

# Running the Agent

During the Drone EGO Swarming project, the agent is started using:

```bash
MicroXRCEAgent udp4 -p 8888
```

This command creates a UDP server on port:

```text
8888
```

PX4 connects to this server during startup.

---

# Verify Installation

Verify that the executable exists.

```bash
which MicroXRCEAgent
```

Expected:

```text
/usr/local/bin/MicroXRCEAgent
```

or another valid executable path.

---

Verify the version.

```bash
MicroXRCEAgent --help
```

Expected:

The Micro XRCE-DDS help information is displayed.

---

Verify communication.

After PX4 has been launched later in this manual, run:

```bash
ros2 topic list | grep /fmu
```

Expected:

Multiple PX4 topics such as:

```text
/fmu/in/trajectory_setpoint

/fmu/in/offboard_control_mode

/fmu/out/vehicle_status_v4

/fmu/out/vehicle_local_position_v1
```

These topics indicate that the DDS bridge is functioning correctly.

---

# Common Issues

---

## `MicroXRCEAgent: command not found`

Cause

The agent has not been installed.

Solution

Verify the PX4 development environment installation or install the
agent following the official documentation.

---

## No `/fmu` topics appear

Cause

The agent is not running.

Solution

Start the agent:

```bash
MicroXRCEAgent udp4 -p 8888
```

---

## PX4 launches but ROS receives no messages

Possible causes include:

- Agent not running
- Wrong UDP port
- PX4 started before the agent
- Firewall blocking communication

Verify that the agent is active before troubleshooting PX4.

---

## Connection repeatedly drops

Verify that only one Micro XRCE-DDS Agent is running.

Multiple agents attempting to use the same port may cause conflicts.

---

# Completion Checklist

Before continuing, verify:

- [ ] Micro XRCE-DDS Agent installed.
- [ ] `which MicroXRCEAgent` returns a valid executable.
- [ ] Agent launches successfully.
- [ ] UDP port 8888 starts without errors.
- [ ] `/fmu` topics appear after PX4 launches.

---

# Transition

ROS 2 can now communicate with PX4.

The next chapter installs MAVROS, which provides additional MAVLink-
based communication and odometry support used throughout the Drone
EGO Swarming project.

➡ Continue to **Chapter 2.7 — MAVROS**
