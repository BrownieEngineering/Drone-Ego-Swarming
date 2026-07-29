# Chapter 5.2 — System Communication Verification

**Estimated Time:** 10–15 minutes

---

# Overview

After launching the Drone EGO Swarming system, verify that every major
component is communicating correctly before attempting autonomous
flight.

A successful launch does not guarantee that PX4, Gazebo, ROS 2,
MAVROS, the PX4 Bridge, and the EGO Planner are exchanging data.

This chapter performs a series of communication checks to confirm that
the complete software stack is operating as expected.

---

# Verify Active ROS Nodes

Open a new terminal.

Source the ROS environment.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

List the active nodes.

```bash
ros2 node list
```

Verify that nodes corresponding to the following components are present:

- PX4 Bridge
- EGO Planner
- MAVROS
- RViz
- Supporting communication nodes

The exact node names may vary depending on software versions.

---

# Verify Available Topics

List all active topics.

```bash
ros2 topic list
```

Verify that topics related to PX4, MAVROS, and the planner are present.

Examples include:

```text
/fmu/in/trajectory_setpoint

/fmu/out/vehicle_status_v4

/mavros/local_position/odom
```

---

# Verify Vehicle Status

Confirm that PX4 is publishing vehicle state.

```bash
ros2 topic echo /fmu/out/vehicle_status_v4
```

Messages should begin appearing immediately.

Press **Ctrl+C** after confirming that data is being published.

---

# Verify Vehicle Odometry

Confirm that MAVROS is publishing odometry.

```bash
ros2 topic echo /mavros/local_position/odom
```

The vehicle position should update continuously while the simulation is
running.

Press **Ctrl+C** after verification.

---

# Verify Trajectory Setpoints

Open another terminal.

Monitor PX4 trajectory commands.

```bash
ros2 topic echo /fmu/in/trajectory_setpoint
```

Do not expect messages immediately.

Trajectory setpoints will begin publishing after a navigation goal is
selected in RViz.

Leave this terminal open for the next chapter.

---

# Verify Planner Activity

Return to the EGO Planner terminal.

The planner should report information similar to:

- successful planning,
- replanning,
- trajectory optimization,
- planner state transitions.

These messages indicate that the planner is operating normally.

---

# Verify the Bridge

Return to the PX4 Bridge terminal.

Confirm that:

- no exceptions are reported,
- keyboard input is accepted,
- the node continues running without errors.

The bridge should remain active throughout the simulation.

---

# Expected System State

Before continuing, the system should be in the following condition.

| Component | Status |
|-----------|--------|
| Gazebo | Running |
| PX4 | Running |
| Micro XRCE-DDS Agent | Running |
| MAVROS | Connected |
| EGO Planner | Active |
| PX4 Bridge | Active |
| RViz | Running |

No autonomous commands should have been issued yet.

---

# Common Issues

---

## No ROS nodes are listed

Verify that every launch command completed successfully before running:

```bash
ros2 node list
```

---

## No vehicle status messages

Verify that PX4 is running and that the Micro XRCE-DDS Agent has started.

---

## No odometry

Verify that MAVROS successfully connected to PX4.

Restart the simulation if necessary.

---

## No trajectory setpoints

No setpoints will be published until a navigation goal is selected in
RViz.

This is expected behavior.

---

## Planner reports no odometry

Verify that MAVROS is publishing:

```bash
/mavros/local_position/odom
```

before continuing.

---

# Completion Checklist

Before continuing, verify:

- [ ] ROS nodes are active.
- [ ] Required ROS topics are present.
- [ ] PX4 publishes vehicle status.
- [ ] MAVROS publishes odometry.
- [ ] Trajectory setpoints are ready to publish.
- [ ] The PX4 Bridge remains active.
- [ ] The EGO Planner is operating normally.

---

# Moving on

The communication pipeline has now been verified.

The next section explains how to operate the keyboard publisher and
transition the vehicle into autonomous flight.

➡ Continue to **Chapter 5.3 — Keyboard Publisher Operation**
