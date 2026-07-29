# Chapter 5.3 — Keyboard Publisher Operation

**Estimated Time:** 10–15 minutes

---

# Overview

The keyboard publisher provides the operator interface for transitioning
the vehicle from an idle simulation into autonomous flight.

Rather than directly controlling the drone, the keyboard publisher sends
high-level commands to the PX4 bridge, allowing the flight controller
and EGO Planner to coordinate vehicle operation.

Throughout normal operation, only a few commands are required for a navigation goal
and when you no other goals to input.

---

# Operator Controls

The Drone EGO Swarming project uses the following key assignments.

| Key | Function |
|-----|----------|
| `t` | Takeoff |
| `p` | Position Mode |
| `o` | Offboard Mode |
| `l` | Land Mode |
| `d` | Disarm Mode |

Commands should be entered from the terminal running the keyboard
publisher.

---

# Before Sending Commands

Before issuing any commands, verify that:

- Gazebo is running.
- PX4 is running.
- MAVROS is connected.
- The PX4 Bridge is active.
- The EGO Planner is running.
- RViz is open.
- No terminal has reported a fatal error.

The vehicle should remain stationary inside Gazebo.

---

# Step 1 — Takeoff

Operator Action

Press:

```text
t
```

Expected System Response

- The vehicle arms.
- PX4 acknowledges the command.
- The drone ascends vertically.
- The drone stabilizes at the configured takeoff altitude.

Expected Planner Behavior

The planner remains active and continues monitoring vehicle state.

Expected Gazebo Behavior

The drone should lift smoothly from the ground without excessive
oscillation.

---

# Step 2 — Position Mode

Operator Action

Press:

```text
p
```

Expected System Response

- PX4 transitions into Position mode.
- The vehicle maintains a stable hover.
- Vehicle state continues updating.

Expected Planner Behavior

The planner remains active and ready to generate trajectories.

Expected Gazebo Behavior

The drone continues hovering without noticeable drift.

---

# Step 3 — Offboard Mode

Operator Action

Press:

```text
o
```

Expected System Response

- PX4 transitions into Offboard mode.
- The PX4 Bridge begins supplying trajectory commands.
- The vehicle remains stable while awaiting a navigation goal.

Expected Planner Behavior

The planner waits for a valid goal from RViz.

Expected Gazebo Behavior

The drone should continue hovering until a navigation goal is selected.

---

# Steps for when complete
--- 
# step 1 — Landing Mode

Operator Action

Press:

```text
l
```

Expected System Response

- PX4 transitions into Landing mode.
- The drone begins lowering towards the ground 
- The vehicle remains stable while completing this action

Expected Gazebo Behavior

The drone should continue rotating its propellers until a the
disarming mode is activated or the takeoff mode is initiated.

---

# step 2 — Disarming Mode

Operator Action

Press:

```text
d
```

Expected System Response

- PX4 transitions into Disarming mode.
- The drone propellor stops rotating  
- The vehicle remains stable while completing this action

Expected Gazebo Behavior

The drone's propellors will stop moving, Gazebo will be 
operational still while the publisher keeps you updated
on the status of the vehicle. The drone is still operational
and goals can be completed again once the launch process is done.

---

# Correct Operating Sequence

Always perform the commands in the following order.

```text


Takeoff

↓

Position Mode

↓

Offboard Mode

↓

Navigation Goal
```

Changing the order may prevent PX4 from accepting Offboard control.

---

# Expected Terminal Messages

During successful operation, the keyboard publisher should acknowledge
each command.

Typical messages include:

```text
Arm

Takeoff

Position Mode

Offboard Mode
```

The exact wording may vary depending on software version.

---

# Common Issues

---

## Nothing happens after pressing a key

Verify that the keyboard publisher terminal has keyboard focus.

---

## Takeoff command is ignored

Verify that:

- PX4 is running.
- The bridge node is active.
- Communication has been verified.

---

## Position mode does not engage

Verify that the vehicle has completed takeoff before attempting to switch
flight modes.

---

## Offboard mode is rejected

Possible causes include:

- No trajectory setpoints are being published.
- The PX4 Bridge is not running.
- Communication between PX4 and ROS 2 has not been established.

Return to Chapter 5.2 and verify the communication pipeline before
continuing.

---

# Completion Checklist

Before continuing, verify:

- [ ] Takeoff command functions correctly.
- [ ] Vehicle reaches a stable hover.
- [ ] Position mode is accepted.
- [ ] Offboard mode is accepted.
- [ ] The vehicle remains stable while awaiting a navigation goal.

---

# Continuing

The vehicle is now ready to receive an autonomous navigation command.

The next section explains how to send a navigation goal and execute an
autonomous mission using the EGO Planner.

➡ Continue to **Chapter 5.4 — Executing an Autonomous Mission**
