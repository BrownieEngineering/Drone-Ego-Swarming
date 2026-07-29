# Chapter 5.4 — Executing an Autonomous Mission

**Estimated Time:** 10–15 minutes

---

# Overview

With the Drone EGO Swarming system fully initialized and operating in
Offboard mode, the vehicle is now ready to execute an autonomous
mission.

This chapter explains how to issue a navigation goal using RViz,
interpret the system response, and verify that the EGO Planner, PX4
Bridge, and PX4 flight controller are working together to execute the
planned trajectory.

---

# Before Sending a Navigation Goal

Confirm that:

- The drone has successfully taken off.
- The vehicle is hovering in Position mode.
- Offboard mode has been enabled.
  
# Note:
the publisher may be displaying that 
it is switching from both offboard and position
mode after pressing " o ", you are in offboard mode

- Gazebo is running normally.
- RViz is open.
- The EGO Planner is active.
- The PX4 Bridge is running.
- No communication errors are present.

The drone should be hovering steadily while waiting for a goal.

---

# Step 1 — Select the Goal Tool

Within RViz, locate the toolbar.

Select:

```text
2D Goal Pose
```

The cursor will change, indicating that RViz is ready to receive a
navigation goal.

---

# Step 2 — Define the Goal

Click and drag within the map to specify:

- the destination position,
- and the desired heading.

Release the mouse button to publish the navigation goal.

RViz immediately publishes the goal to the EGO Planner.

---

# Expected Planner Response

After the goal is received, observe the EGO Planner terminal.

Typical output includes:

- successful trajectory generation,
- trajectory optimization,
- planner state transitions,
- trajectory publication.

These messages indicate that a valid path has been generated.

---

# Expected Bridge Response

The PX4 Bridge begins converting the planner trajectory into PX4
trajectory setpoints.

Verify that the bridge continues running without errors.

---

# Expected PX4 Response

PX4 should begin accepting trajectory setpoints while remaining in
Offboard mode.

---

# Expected Gazebo Behavior

After a short delay, the drone should:

- begin moving smoothly,
- follow the generated trajectory,
- avoid obstacles,
- continue toward the selected goal,
- stabilize after reaching the destination.

Movement should appear continuous without abrupt direction changes.

---

# Hopeful RViz Behavior

RViz should display:

- the selected goal,
- the planned trajectory,
- updated vehicle position,
- planner visualization data.

The displayed trajectory should closely match the vehicle's motion in
Gazebo.
 
# Note
The current sim has these issues and will more than likely collide 
into an obstacle and begin flying throughout the environment while being mapped on Rviz

---

# Monitoring the Mission

During flight, monitor:

- the planner terminal,
- the bridge terminal,
- Gazebo,
- RViz.

The system should continue publishing trajectory updates while the
vehicle is moving.

---

# Successful Mission

A successful autonomous mission is characterized by:

- successful trajectory generation,
- continuous trajectory publication,
- stable Offboard flight,
- smooth obstacle avoidance,
- arrival at the selected goal,
- stable hover after reaching the destination.

---

# Common Issues

---

## No trajectory appears

Verify that:

- Offboard mode has been enabled,
- the planner is running,
- a goal was successfully published from RViz.

---

## Drone does not move

Verify that:

- trajectory setpoints are being published,
- the PX4 Bridge is active,
- PX4 remains in Offboard mode.

---

## Planner reports repeated failures

Verify that:

- valid odometry is available,
- the map initialized correctly,
- the selected goal is reachable.

---

## Drone collides with an obstacle

Possible causes include:

- incomplete map information,
- insufficient sensing range,
- planner configuration,
- dynamic obstacles outside the current planning horizon.

Review planner parameters before attempting another mission.

---

# Completion Checklist

Before continuing, verify:

- [ ] Navigation goal published successfully.
- [ ] Planner generated a trajectory.
- [ ] PX4 Bridge remained active.
- [ ] PX4 accepted trajectory setpoints.
- [ ] Drone followed the planned path.
- [ ] Drone reached the destination.
- [ ] Vehicle stabilized after completing the mission.

---

# Transition

The Drone EGO Swarming system has successfully completed an autonomous
mission.

The final chapter describes the recommended shutdown procedure for
ending a simulation session safely.

➡ Continue to **Chapter 5.5 — System Shutdown**
