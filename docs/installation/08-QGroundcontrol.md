# Chapter 2.8 — QGroundControl

**Estimated Time:** 5–10 minutes

---

# Overview

QGroundControl (QGC) is the Ground Control Station (GCS) used throughout
the Drone EGO Swarming project.

It provides a graphical interface for monitoring and interacting with PX4.

Unlike RViz, which is responsible for autonomous goal selection and
trajectory planning, QGroundControl is primarily used to monitor the
vehicle and verify that PX4 is functioning correctly.

Throughout this project, QGroundControl is **not** responsible for
planning trajectories.

Instead, it is used to:

- verify PX4 connection,
- monitor vehicle state,
- observe flight modes,
- monitor battery and health information,
- and inspect PX4 messages during testing.

---

# What is QGroundControl?

QGroundControl is the official ground station application developed for
PX4.

It communicates with PX4 using the MAVLink protocol.

QGroundControl allows users to:

- monitor vehicle telemetry,
- configure PX4 parameters,
- inspect sensors,
- upload missions,
- monitor GPS,
- calibrate hardware,
- and perform firmware updates.

Although many of these capabilities are intended for physical aircraft,
they are still useful while working in simulation.

---

# Why is QGroundControl Required?

During development, QGroundControl was used to verify:

- PX4 successfully started,
- PX4 connected correctly,
- Offboard mode requests,
- vehicle arming state,
- flight mode transitions,
- vehicle health.

When debugging communication between ROS 2 and PX4, QGroundControl
provides immediate confirmation that PX4 is operating correctly.

---

# Why Doesn't This Project Fly Through QGroundControl?

Many PX4 projects use QGroundControl to create autonomous missions.

The Drone EGO Swarming project does **not**.

Instead, the autonomous navigation pipeline is:

```text
RViz

↓

Goal Pose

↓

EGO Planner

↓

PX4 Bridge

↓

PX4

↓

Gazebo
```

QGroundControl simply monitors PX4 while this process occurs.

Think of it as the vehicle dashboard rather than the navigation system.

---

# How QGroundControl Fits Into Drone EGO Swarming

```text
QGroundControl

↓

MAVLink

↓

PX4

↓

Micro XRCE DDS

↓

ROS2

↓

EGO Planner
```

Notice that QGroundControl and ROS 2 both communicate with PX4, but
they perform different jobs.

ROS 2 controls the mission.

QGroundControl monitors the vehicle.

---

# Official Documentation

QGroundControl

https://qgroundcontrol.com/

GitHub Repository

https://github.com/mavlink/qgroundcontrol

---

# Installation

Download the latest stable Linux AppImage from the official
QGroundControl website.

Move the AppImage into a permanent location.

Example:

```bash
mkdir -p ~/Applications

mv ~/Downloads/QGroundControl*.AppImage \
~/Applications/QGroundControl.AppImage
```

Make the file executable.

```bash
chmod +x \
~/Applications/QGroundControl.AppImage
```

---

# Launching QGroundControl

Run:

```bash
~/Applications/QGroundControl.AppImage
```

The application should open.

---

# Verify Installation

After launching:

Verify that:

- the application opens,
- no startup errors appear,
- the user interface loads correctly.

Later, after PX4 is running, verify:

- vehicle connected,
- vehicle icon appears,
- flight mode displayed,
- heartbeat received.

---

# Expected Warnings

While running inside simulation, several warnings may appear.

Examples include:

- terrain server unavailable,
- Bing map unavailable,
- SSL warnings,
- geolocation warnings.

These warnings generally do **not** prevent simulation from functioning.

The important verification is that PX4 connects successfully.

---

# Common Issues

---

## AppImage will not start

Verify executable permissions.

```bash
chmod +x \
~/Applications/QGroundControl.AppImage
```

---

## Vehicle does not connect

Verify:

- PX4 running
- MAVROS running
- PX4 launch completed successfully

Vehicle connection is verified later in this manual.

---

## Terrain or map warnings

These warnings usually indicate online map services are unavailable.

They do not prevent Drone EGO Swarming from operating in simulation.

---

# Completion Checklist

Before continuing, check:

- [ ] QGroundControl downloaded.
- [ ] AppImage executable.
- [ ] Application launches.
- [ ] User interface loads.
- [ ] Ready to connect to PX4.

---

# Transition

Every major software dependency has now been installed.

The next chapter verifies that the complete software environment has
been installed correctly before building the Drone EGO Swarming
workspace.

➡ Continue to **Chapter 2.9 — Installation Verification**
