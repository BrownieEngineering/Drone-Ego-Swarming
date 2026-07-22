# Chapter 2.9 — Installation Verification

**Estimated Time:** 10–20 minutes

---

# Overview

At this point, every major software dependency required by the Drone EGO
Swarming project should be installed.

Before creating the ROS workspace or modifying any source code, verify
that every required component has been installed correctly.

Completing this verification now greatly reduces debugging time later in
the project.

If any step below fails, resolve the issue before continuing to
Chapter 3.

---

# Purpose

This chapter verifies that the following components are available and
functioning correctly:

- Ubuntu
- ROS 2 Humble
- Gazebo Harmonic
- PX4
- px4_msgs
- Micro XRCE-DDS Agent
- MAVROS
- QGroundControl

The goal is to confirm that the software environment is ready before
building the Drone EGO Swarming workspace.

---

# Verify Ubuntu

Run:

```bash
lsb_release -a
```

Expected:

```text
Distributor ID: Ubuntu
Release: 22.04
```

---

# Verify ROS 2

Run:

```bash
ros2 --help
```

Expected:

The ROS command line help menu appears.

Verify the ROS distribution:

```bash
echo $ROS_DISTRO
```

Expected:

```text
humble
```

---

# Verify Gazebo

Run:

```bash
gz sim --version
```

Expected:

A Gazebo Harmonic version number.

Verify the ROS bridge:

```bash
ros2 pkg prefix ros_gz_bridge
```

Expected:

A valid package path.

---

# Verify PX4

Navigate to the PX4 directory.

```bash
cd ~/PX4-Autopilot
```

Verify the repository version.

```bash
git rev-parse --short HEAD
```

Expected:

```text
25b7d627da
```

Verify the descriptive version.

```bash
git describe --tags
```

Expected:

```text
v1.18.0-alpha1-469-g25b7d627da
```

Verify the PX4 binary.

```bash
ls build/px4_sitl_default/bin/
```

Expected:

```text
px4
```

---

# Verify px4_msgs

Run:

```bash
ros2 pkg prefix px4_msgs
```

Expected:

```text
/home/<username>/ego_ws/install/px4_msgs
```

Verify the message definitions.

```bash
ros2 interface show px4_msgs/msg/TrajectorySetpoint
```

Expected:

The complete message definition is displayed.

---

# Verify Micro XRCE-DDS Agent

Verify the executable.

```bash
which MicroXRCEAgent
```

Expected:

A valid executable path.

Example:

```text
/usr/local/bin/MicroXRCEAgent
```

Verify the command launches.

```bash
MicroXRCEAgent --help
```

Expected:

The help information is displayed.

---

# Verify MAVROS

Run:

```bash
ros2 pkg prefix mavros
```

Expected:

A valid installation path.

Verify GeographicLib.

```bash
ls /usr/share/GeographicLib
```

Expected:

The directory exists.

---

# Verify QGroundControl

Launch:

```bash
~/Applications/QGroundControl.AppImage
```

Verify:

- Application opens.
- User interface loads.
- No critical startup errors appear.

Close QGroundControl before continuing.

---

# Verify Development Tools

Run:

```bash
git --version
python3 --version
colcon version-check
```

Expected:

Each command returns version information.

If `colcon version-check` is unavailable on your installation, verify
instead that:

```bash
colcon --help
```

returns the command help successfully.

---

# Verify Expected Directories

The following directories should exist:

```text
~/Drone-Ego-Swarming
~/PX4-Autopilot
~/ego-planner-ros2-sim
~/ego_ws
~/ego_ws/src
```

Verify:

```bash
ls ~
```

---

# Verify Shell Configuration

Open a **new terminal**.

Run:

```bash
echo $ROS_DISTRO
```

Expected:

```text
humble
```

If the variable is empty, verify that:

```bash
source /opt/ros/humble/setup.bash
```

has been added to:

```text
~/.bashrc
```

---

# Common Issues

---

## One verification failed

Do **not** continue.

Resolve the failed installation before beginning the workspace setup.

---

## Commands disappear in a new terminal

Verify:

```bash
cat ~/.bashrc
```

Confirm that the ROS setup command has been added.

---

## Package not found

If any package returns:

```text
Package not found
```

verify:

- installation completed,
- workspace built successfully,
- workspace sourced correctly.

---

## Wrong PX4 version

Verify:

```bash
git rev-parse --short HEAD
```

If the commit differs from the tested version, switch to the correct
commit before continuing.

---

# Installation Checklist

Use this checklist before moving on.

| Component | Verified |
|-----------|----------|
| Ubuntu 22.04 | ☐ |
| ROS 2 Humble | ☐ |
| Gazebo Harmonic | ☐ |
| PX4 | ☐ |
| px4_msgs | ☐ |
| Micro XRCE-DDS Agent | ☐ |
| MAVROS | ☐ |
| QGroundControl | ☐ |
| Development Tools | ☐ |
| Directory Structure | ☐ |
| Shell Configuration | ☐ |

---

# Completion

Congratulations.

At this point the complete software environment required by the Drone
EGO Swarming project has been installed and verified.

No project-specific code has been modified yet.

The next chapter begins constructing the Drone EGO Swarming workspace.

➡ Continue to **Chapter 3 — Workspace Setup**
