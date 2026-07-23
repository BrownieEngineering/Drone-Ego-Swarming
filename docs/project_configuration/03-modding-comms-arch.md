# Chapter 4.3 — Communication Architecture

**Estimated Time:** 10–15 minutes

---

# Overview

The Drone EGO Swarming project is composed of several independent
software systems that communicate through ROS 2 topics, DDS, and
MAVLink.

Understanding how information flows between these components makes it
easier to debug communication issues and verify that the system is
operating correctly.

This chapter introduces the communication pipeline used throughout the
project.

---

# System Communication Flow

The overall communication path is shown below.

```text
RViz Goal

↓

EGO Planner

↓

PX4 Bridge

↓

PX4 Offboard Controller

↓

Gazebo Simulation

↓

Vehicle State

↓

MAVROS

↓

EGO Planner
```

This continuous feedback loop allows the planner to generate trajectories
while continuously receiving updated vehicle state information.

---

# Major Communication Components

| Component | Primary Role |
|-----------|--------------|
| RViz | User-defined navigation goals |
| EGO Planner | Trajectory generation |
| PX4 Bridge | Converts planner output into PX4-compatible commands |
| PX4 | Flight control and vehicle state |
| Gazebo | Vehicle simulation |
| MAVROS | Publishes odometry and vehicle state |
| Micro XRCE-DDS Agent | DDS communication between PX4 and ROS 2 |

---

# Verification Goals

Before moving on to system operation, confirm that:

- ROS nodes are running.
- Required topics are being published.
- PX4 reports a connected DDS client.
- MAVROS is publishing odometry.
- EGO Planner is publishing trajectories.

The next chapter performs these verification steps.

---

# Common Issues

## Missing ROS topics

Usually indicates that a required node failed to start.

---

## No PX4 communication

Verify that the Micro XRCE-DDS Agent is running before launching PX4.

---

## No odometry

Verify that MAVROS is connected and publishing the expected odometry topic.

---

# Completion Checklist

- [ ] Communication pipeline understood.
- [ ] Major system components identified.
- [ ] Ready to verify runtime communication.

---

# Transition

The final chapter of this section verifies that every component is
communicating correctly before autonomous flight testing begins.

➡ Continue to **Chapter 4.4 — System Verification**
