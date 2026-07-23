# Chapter 4.2 — Launch System Configuration

**Estimated Time:** 15–30 minutes

---

# Overview

The Drone EGO Swarming project relies on several independent software
systems that must be started in the correct order.

Rather than launching a single application, the project consists of
multiple processes that work together to create the complete simulation
environment.

This chapter documents the launch configuration used by the project and
explains the purpose of each major component.

---

# Launch Sequence

The standard startup sequence is:

```text
1. PX4 SITL

↓

2. Gazebo Simulation

↓

3. Micro XRCE-DDS Agent

↓

4. MAVROS

↓

5. EGO Planner

↓

6. Keyboard Publisher

↓

7. RViz
```

Launching components in this order helps ensure that each process can
establish communication with the services it depends on.

---

# Major Launch Components

The launch system is composed of several independent applications.

| Component | Purpose |
|-----------|---------|
| PX4 SITL | Flight controller simulation |
| Gazebo | Physics simulation |
| Micro XRCE-DDS Agent | PX4 ↔ ROS 2 communication |
| MAVROS | Vehicle state interface |
| EGO Planner | Trajectory planning |
| Keyboard Publisher | Flight mode and mission commands |
| RViz | Visualization and waypoint selection |

Each component performs a specific role within the overall system.

---

# Launch Files

Several launch files are used throughout the project.

As the project evolves, these files may be updated to support additional
features such as multi-drone simulation.

Whenever a launch file is modified, document:

- its location,
- the reason for the change,
- the modification,
- and the verification procedure.

This ensures that future contributors can reproduce the working
configuration.

---

# Startup Verification

Before continuing, verify that:

- PX4 starts successfully.
- Gazebo opens without errors.
- The Micro XRCE-DDS Agent reports that it is running.
- MAVROS connects to PX4.
- RViz launches successfully.

Complete communication verification is covered in the following chapter.

---

# Common Issues

---

## Components started in the wrong order

Some services depend on others already running.

If a component fails to connect, stop the system and restart using the
recommended launch sequence.

---

## Launch file not found

Verify that the file path is correct and that the workspace has been
built successfully.

---

## Modified launch file ignored

Rebuild the workspace if the launch file belongs to a ROS package.

Restart all running processes before testing again.

---

# Completion Checklist

Before continuing, verify:

- [ ] Launch sequence is understood.
- [ ] All required launch files are present.
- [ ] PX4 starts successfully.
- [ ] Gazebo launches successfully.
- [ ] Micro XRCE-DDS Agent starts.
- [ ] MAVROS connects.
- [ ] RViz launches.

---

# Transition

The launch system is now configured.

The next chapter configures the keyboard publisher used to command the
vehicle and initiate autonomous flight.

➡ Continue to **Chapter 4.3 — Keyboard Publisher Configuration**
