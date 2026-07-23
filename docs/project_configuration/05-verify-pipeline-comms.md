# Chapter 4.5 — Communication Pipeline Verification

**Estimated Time:** 20–30 minutes

---

# Overview

The Drone EGO Swarming project relies on continuous communication
between multiple independent software systems.

Although each component may launch successfully, autonomous flight
cannot occur unless every part of the communication pipeline is
operating correctly.

This chapter verifies that communication has been successfully
established between PX4, Gazebo, ROS 2, MAVROS, the PX4 Bridge, and the
EGO Planner before flight testing begins.

---

# Communication Pipeline

The complete communication pipeline is shown below.

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

Micro XRCE-DDS

↓

ROS 2

↓

MAVROS

↓

EGO Planner
```

Every component in this loop must operate correctly before autonomous
navigation can begin.

---

# Verify Running Nodes

Open a new terminal.

List all active ROS nodes.

```bash
ros2 node list
```

Verify that the expected project nodes are present.

Depending on your current launch configuration, the output should include
nodes associated with:

- EGO Planner
- PX4 Bridge
- MAVROS
- Micro XRCE-DDS communication
- RViz (if running)

---

# Verify ROS Topics

List the available ROS topics.

```bash
ros2 topic list
```

Confirm that PX4, MAVROS, and planner topics are present.

Typical examples include:

```text
/fmu/in/trajectory_setpoint

/fmu/out/vehicle_status_v4

/mavros/local_position/odom
```

The available topics may differ slightly depending on software versions.

---

# Verify Vehicle State

Confirm that PX4 is publishing vehicle status.

```bash
ros2 topic echo /fmu/out/vehicle_status_v4
```

Vehicle state messages should begin appearing immediately.

---

# Verify Trajectory Commands

Command a navigation goal in RViz.

Open another terminal.

Monitor trajectory setpoints.

```bash
ros2 topic echo /fmu/in/trajectory_setpoint
```

When a goal is selected in RViz, trajectory messages should begin
appearing.

This confirms that:

- the EGO Planner generated a trajectory,
- the PX4 Bridge translated the command,
- PX4 received the resulting trajectory setpoints.

---

# Verify MAVROS

Confirm that MAVROS is publishing odometry.

```bash
ros2 topic echo /mavros/local_position/odom
```

Vehicle position updates should be displayed continuously while the
simulation is running.

---

# Verify Flight Commands

Run the keyboard publisher.

Verify the following sequence.

Press:

```text
t
```

The vehicle should arm and initiate takeoff.

Press:

```text
p
```

The vehicle should enter Position mode.

Press:

```text
o
```

The vehicle should transition into Offboard mode.

Each command should be acknowledged by PX4.

---

# Expected System Behavior

When the communication pipeline is functioning correctly:

- Gazebo remains synchronized with PX4.
- Vehicle state messages update continuously.
- MAVROS publishes odometry.
- EGO Planner produces trajectories.
- PX4 receives trajectory setpoints.
- The keyboard publisher changes vehicle modes successfully.
- RViz goals produce autonomous motion.

---

# Common Issues

---

## No nodes are listed

Cause

The project has not been launched successfully.

Solution

Restart the launch sequence and verify each terminal for errors.

---

## No trajectory setpoints

Cause

The EGO Planner is not publishing trajectories or the PX4 Bridge is not
running.

Solution

Verify that both nodes are active and that a navigation goal has been
selected in RViz.

---

## No vehicle status messages

Cause

PX4 is not communicating with ROS 2.

Solution

Verify that:

- PX4 is running.
- The Micro XRCE-DDS Agent has started.
- The bridge package is active.

---

## No odometry

Cause

MAVROS failed to connect.

Solution

Verify that PX4 started successfully before MAVROS initialized.

---

## Vehicle ignores keyboard commands

Cause

The communication pipeline has not been established or PX4 is not
accepting Offboard commands.

Solution

Verify every communication step above before attempting autonomous
flight.

---

# Completion Checklist

Before continuing, verify:

- [ ] ROS nodes are running.
- [ ] ROS topics are publishing.
- [ ] PX4 publishes vehicle state.
- [ ] MAVROS publishes odometry.
- [ ] Trajectory setpoints are published.
- [ ] Keyboard commands are accepted.
- [ ] RViz goals generate trajectories.
- [ ] The drone responds to autonomous commands.

---

# Next up

The Drone EGO Swarming communication pipeline has now been verified.

The next chapter performs a final verification of every project
modification before autonomous flight operations begin.

➡ Continue to **Chapter 4.6 — Project Modification Verification**
