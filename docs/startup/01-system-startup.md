# Chapter 5.1 — System Startup

**Estimated Time:** 10–20 minutes

---

# Overview

The Drone EGO Swarming system consists of several processes that must
remain active at the same time.

This chapter documents the standard terminal layout and startup sequence
used to bring the complete simulation environment online.

Each terminal has a specific responsibility. Keep every terminal open
until the shutdown procedure is completed.

---

# Required Terminals

The single-drone system uses four primary terminals.

| Terminal | Responsibility |
|----------|----------------|
| Terminal 1 | PX4, Gazebo, Micro XRCE-DDS, MAVROS, and sensor bridges |
| Terminal 2 | EGO Planner |
| Terminal 3 | RViz |
| Terminal 4 | PX4 bridge and keyboard control |

Optional verification terminals may be opened later to inspect ROS nodes,
topics, odometry, and trajectory commands.

---

# Before Starting

Confirm that the following directories exist:

```text
~/PX4-Autopilot

~/ego_ws

~/ego_ws/src/ego-swarm-ros2

~/ego_ws/src/px4_ego
```

Confirm that the workspace has already been built:

```bash
ls ~/ego_ws/install
```

Confirm that the customized PX4 launch file exists:

```bash
ls ~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

Do not continue until these checks succeed.

---

# Clean Previous Simulation Processes

Before launching a new simulation, stop any remaining processes from a
previous session.

```bash
pkill -f px4 || true
pkill -f mavros || true
pkill -f MicroXRCEAgent || true
pkill -f gz || true
```

Wait several seconds after running these commands.

This prevents old PX4, Gazebo, MAVROS, or XRCE processes from interfering
with the new session.

---

# Terminal 1 — Launch the Simulation Environment

Open the first terminal.

Source ROS 2 and the project workspace.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

Launch the customized PX4 simulation file.

```bash
ros2 launch ~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

This launch file starts the primary simulation components:

- Gazebo
- PX4 SITL
- Micro XRCE-DDS Agent
- MAVROS
- Depth image bridge
- Best Effort depth-image publisher

Keep this terminal open.

---

# Terminal 1 Startup Checks

Before opening the remaining terminals, confirm that:

- Gazebo opens.
- The drone model appears in the world.
- PX4 completes initialization.
- The Micro XRCE-DDS Agent starts on the configured UDP port.
- MAVROS begins connecting to PX4.
- The depth bridge starts without terminating.

Some warnings may appear during startup. Continue only if the major
processes remain running and no fatal launch exception is reported.

---

# Terminal 2 — Launch the EGO Planner

Open a second terminal.

Source the required environments.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

Launch the EGO Planner.

```bash
ros2 launch ego_planner single_uav_gazebo.launch.py
```

Keep this terminal open.

The planner terminal should begin displaying information about:

- odometry,
- map initialization,
- trajectory generation,
- planner state,
- and replanning activity.

The planner may wait for valid odometry, sensor data, or a navigation
goal before producing a trajectory.

---

# Terminal 3 — Launch RViz

Open a third terminal.

Source the required environments.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

Launch RViz.

```bash
ros2 launch ego_planner rviz.launch.py
```

Keep this terminal open.

RViz provides:

- vehicle visualization,
- map and point-cloud visualization,
- planned trajectory visualization,
- odometry visualization,
- and navigation-goal selection.

Do not send a navigation goal yet.

---

# Terminal 4 — Launch the PX4 Bridge and Keyboard Controller

Open a fourth terminal.

Source the required environments.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

Verify the available executable name before launching:

```bash
ros2 pkg executables px4_ego_py
```

Run the project bridge and keyboard-control executable identified by the
command above.

For the tested project configuration, this is expected to use the
`offboard_control_test` executable:

```bash
ros2 run px4_ego_py offboard_control_test
```

Keep this terminal selected whenever keyboard commands are entered.

---

# Standard Startup Order

The complete startup order is:

```text
Terminal 1
PX4 and Gazebo simulation environment

↓

Terminal 2
EGO Planner

↓

Terminal 3
RViz

↓

Terminal 4
PX4 bridge and keyboard controller
```

Allow each stage to initialize before starting the next one.

Starting every command simultaneously may cause components to search for
topics or services that are not yet available.

---

# Initial Visual Checks

After all four terminals are running, confirm that:

- Gazebo remains open.
- The simulated drone remains stable at its spawn position.
- RViz displays the expected world and vehicle information.
- The EGO Planner remains active.
- The bridge terminal accepts keyboard input.
- None of the primary terminals has exited.

At this stage, the vehicle should not yet be commanded to begin an
autonomous mission.

---

# Common Issues

## Gazebo opens but no drone appears

Confirm that PX4 started successfully and that the required simulation
world and model resources are available.

Restart the launch sequence if the model failed to spawn.

---

## PX4 terminates during startup

Verify that PX4 was built using the documented commit:

```bash
cd ~/PX4-Autopilot
git rev-parse --short HEAD
```

Expected:

```text
25b7d627da
```

---

## Micro XRCE-DDS Agent cannot bind to the port

A previous agent may still be running.

Stop it:

```bash
pkill -f MicroXRCEAgent
```

Then restart Terminal 1.

---

## MAVROS does not connect

Verify that PX4 remains active and that no older PX4 or MAVROS process is
using the required MAVLink ports.

Restart the complete simulation rather than restarting MAVROS alone.

---

## EGO Planner waits for odometry

Verify that MAVROS is publishing:

```bash
ros2 topic echo /mavros/local_position/odom --once
```

If no message is returned, resolve the MAVROS or PX4 connection before
continuing.

---

## Bridge executable cannot be found

Verify the package and executable names:

```bash
ros2 pkg prefix px4_ego_py
ros2 pkg executables px4_ego_py
```

If the package is missing, rebuild it:

```bash
cd ~/ego_ws

colcon build \
  --packages-select px4_ego_py \
  --symlink-install

source install/setup.bash
```

---

# Moving on

The complete Drone EGO Swarming software stack is now running.

Before commanding the vehicle, the next section verifies that odometry,
vehicle state, trajectory interfaces, sensor data, and communication
topics are operating correctly.

➡ Continue to **Chapter 5.2 — System Communication Verification**
