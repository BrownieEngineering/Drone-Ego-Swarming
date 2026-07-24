# Chapter 4.3 — Modifying PX4 Launch Files

**Estimated Time:** 20–30 minutes

---

# Overview

The Drone EGO Swarming project uses a customized PX4 launch file to
initialize the complete simulation environment.

While the original launch file supplied with the EGO Planner simulation
provides a starting point, additional modifications were required to
ensure reliable communication between PX4, Gazebo, ROS 2, MAVROS, and
the PX4 bridge.

This chapter documents the launch file used by the project, the changes
that were made, why they were necessary, and how to verify that the
system starts correctly.

---

# Modified Launch File

The primary launch file used by this project is:

```text
~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

This file originated from the simulation repository:

```text
~/ego-planner-ros2-sim/px4_sitl_ros2.launch.py
```

During project setup, the file was copied into the PX4 launch directory
and modified to support the Drone EGO Swarming system.

---

# Opening the Launch File

Navigate to the launch directory.

```bash
cd ~/PX4-Autopilot/launch
```

Open the launch file.

```bash
nano px4_sitl_ros2.launch.py
```

---

# Purpose

This launch file is responsible for starting the primary simulation
environment.

Its responsibilities include:

- launching the Gazebo simulator,
- starting the PX4 SITL instance,
- initializing the Micro XRCE-DDS Agent,
- launching MAVROS,
- starting the depth image bridge,
- publishing depth images using the Best Effort QoS profile.

Together, these components establish the communication framework
required by the Drone EGO Swarming project.

---

# Modification

Locate the `LaunchDescription` returned near the end of the file.

Replace the launch sequence with the following configuration.

```python
return LaunchDescription([
    gazebo_simulation_cmd,
    px4_instance0,
    # px4_instance1,
    micro_xrce_start_cmd,
    mavros_start_cmd,
    # lidar_point_bridge_node,
    depth_bridge_node,
    best_effort_depth_img_pub,
    # best_effort_lidar_points_pub,
])
```

---

# Why Was This Changed?

During development, communication failures were traced to the startup
order of several independent processes.

Some ROS nodes attempted to communicate with PX4 before the required
services had been initialized.

Reordering the launch sequence ensures that:

- Gazebo initializes before PX4.
- PX4 establishes its simulation environment.
- The Micro XRCE-DDS Agent is available before ROS 2 communication begins.
- MAVROS connects after PX4 is available.
- The depth image bridge begins forwarding sensor data once the
  simulation is active.

This sequence produced the most reliable startup configuration during
development and testing.

---

# Launching the System

Source the required environments.

```bash
source /opt/ros/humble/setup.bash

source ~/ego_ws/install/setup.bash
```

Launch the simulation.

```bash
ros2 launch ~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

The launch file automatically starts the required simulation and
communication services.

---

# Additional Launch Files

Once the simulation environment has started successfully, launch the
remaining project components.

Launch the EGO Planner.

```bash
ros2 launch ego_planner single_uav_gazebo.launch.py
```

Launch RViz.

```bash
ros2 launch ego_planner rviz.launch.py
```

These launch files are used without modification and remain part of the
original EGO Planner project.

---

# Verification

After launching the simulation, verify that:

- Gazebo opens successfully.
- PX4 starts without initialization errors.
- The Micro XRCE-DDS Agent starts.
- MAVROS establishes a connection with PX4.
- The depth image bridge starts successfully.
- No launch exceptions are reported in the terminal.

If all components initialize successfully, the launch configuration has
been applied correctly.

---

# Common Issues

---

## Launch file cannot be found

Verify that the launch file exists at:

```text
~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

---

## Gazebo starts but PX4 does not

Verify that PX4 has been built successfully and that the correct launch
file is being executed.

---

## MAVROS does not connect

Confirm that:

- PX4 has started successfully.
- The Micro XRCE-DDS Agent is running.
- The launch sequence has not been modified.

---

## Depth bridge fails to start

Verify that the required helper scripts were copied into the project
during the installation process.

---

# Completion Checklist

Before continuing, verify:

- [ ] The customized launch file exists.
- [ ] The launch sequence has been updated.
- [ ] Gazebo launches successfully.
- [ ] PX4 initializes successfully.
- [ ] The Micro XRCE-DDS Agent starts.
- [ ] MAVROS connects.
- [ ] The depth image bridge initializes correctly.

---

# Transition

The launch system is now configured and capable of starting the Drone
EGO Swarming simulation environment.

The next section documents the keyboard publisher used to control flight
modes and initiate autonomous operation.

➡ Continue to **Chapter 4.4 — Keyboard Publisher Configuration**
