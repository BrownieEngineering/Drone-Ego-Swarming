# Chapter 4.6 — Project Modification Verification

**Estimated Time:** 10–15 minutes

---

# Overview

At this stage, every required project modification should be complete.

Before attempting autonomous flight, perform a final verification of the
project configuration to ensure that every major software component,
launch file, bridge, and communication interface has been configured
correctly.

Completing this verification significantly reduces the likelihood of
runtime failures during system operation.

---

# Verify the Workspace

Confirm that the ROS workspace has been built successfully.

```bash
cd ~/ego_ws

colcon build --symlink-install
```

The build should complete without errors.

---

# Verify the PX4 Bridge

Confirm that the bridge package is available.

```bash
ros2 pkg prefix px4_ego_py
```

Verify that ROS recognizes the package.

---

# Verify the Launch Configuration

Confirm that the customized launch file exists.

```bash
ls ~/PX4-Autopilot/launch
```

Verify that:

```text
px4_sitl_ros2.launch.py
```

is present.

---

# Verify the Communication Pipeline

Launch the simulation.

```bash
ros2 launch ~/PX4-Autopilot/launch/px4_sitl_ros2.launch.py
```

Open another terminal.

Verify that PX4 publishes vehicle state.

```bash
ros2 topic echo /fmu/out/vehicle_status_v4
```

Verify that trajectory setpoints are received.

```bash
ros2 topic echo /fmu/in/trajectory_setpoint
```

Both topics should begin publishing when the system is operating
normally.

---

# Verify the Keyboard Publisher

Launch the keyboard publisher.

Confirm that the following commands operate correctly.

| Key | Expected Behavior |
|-----|-------------------|
| `t` | Vehicle arms and initiates takeoff |
| `p` | Vehicle enters Position mode |
| `o` | Vehicle enters Offboard mode |

Each command should be acknowledged by PX4.

---

# Verify Autonomous Navigation

Open RViz.

Select a navigation goal using the **2D Goal Pose** tool.

Confirm that:

- the EGO Planner generates a trajectory,
- trajectory setpoints are published,
- the drone follows the planned path,
- vehicle state updates continuously throughout the flight.

If all checks succeed, the project has been configured correctly.

---

# Final Project Checklist

Before continuing to system operation, verify that:

- [ ] ROS workspace builds successfully.
- [ ] PX4 Bridge package is installed.
- [ ] Customized PX4 launch file is present.
- [ ] Gazebo launches successfully.
- [ ] PX4 starts successfully.
- [ ] Micro XRCE-DDS Agent is running.
- [ ] MAVROS is connected.
- [ ] Vehicle state topics are publishing.
- [ ] Trajectory setpoints are publishing.
- [ ] Keyboard commands function correctly.
- [ ] RViz goals generate trajectories.
- [ ] The drone successfully completes an autonomous flight.

---

# Transition

The Drone EGO Swarming project has now been fully configured and
verified.

The next chapter introduces the standard operating procedure for
launching the complete system, preparing the vehicle for flight, and
executing an autonomous mission.

➡ Continue to **Chapter 5 — Running the System**
