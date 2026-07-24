# Chapter 4.4 — Keyboard Publisher Configuration

**Estimated Time:** 15–20 minutes

---

# Overview

The Drone EGO Swarming project uses a keyboard publisher to send control
commands to the autonomous flight system.

Rather than manually flying the vehicle, the keyboard publisher allows
the operator to arm the system, command takeoff, switch flight modes,
and enable Offboard operation before autonomous navigation begins.

Throughout development, this node was modified to support the control
scheme used by the Drone EGO Swarming project.

---

# Purpose

The keyboard publisher provides a simple interface between the operator
and the autonomous flight system.

Its responsibilities include:

- Arming the vehicle.
- Initiating takeoff.
- Switching the vehicle into Position mode.
- Enabling Offboard mode.
- Publishing flight commands to the PX4 bridge.

The node allows the operator to safely transition from manual startup
into autonomous flight.

---

# Package Location

The keyboard publisher is located within the project source code.

```text
~/ego_ws/src/px4_ego
```

*(Update this path if the keyboard publisher resides elsewhere in your final project.)*

---

# Control Mapping

The Drone EGO Swarming project uses the following keyboard commands.

| Key | Function |
|-----|----------|
| `t` | Takeoff |
| `p` | Position Mode |
| `o` | Offboard Mode |
| `l` | Landing Mode |
| `d` | Disarm |

These mappings were standardized during development and are used
throughout the remainder of this manual.

---

# Configuration

If modifications are required, navigate to the keyboard publisher source
file.

```bash
cd ~/ego_ws/src/px4_ego
```

Locate the keyboard publisher implementation.

```bash
find . -name "*.py"
```

or

```bash
find . -name "*.cpp"
```

depending on the implementation.

Open the file.

```bash
nano <keyboard_publisher_file>
```

Document any project-specific modifications before rebuilding the
workspace.

---

# Rebuilding the Package

After making changes, rebuild the affected package.

```bash
cd ~/ego_ws

source /opt/ros/humble/setup.bash

colcon build --packages-select px4_ego_py --symlink-install

source install/setup.bash
```

---

# Verification

Launch the project.

Run the keyboard publisher.

Press:

```text
t
```

The terminal should indicate that a takeoff command has been sent.

Press:

```text
p
```

The vehicle should transition into Position mode.

Press:

```text
o
```
The vehicle should transition into landing mode.

Press:

```text
l
```
The vehicle should disarm.

Press:

```text
d
```

The vehicle should transition into Offboard mode.

If all commands are accepted, the keyboard publisher has been configured
correctly.

---

# Common Issues

---

## Keyboard input is ignored

Verify that the keyboard publisher node is running and has terminal
focus.

---

## Flight mode does not change

Verify that:

- PX4 is connected.
- The bridge is running.
- The communication pipeline is operational.

---

## Offboard mode is rejected

Verify that:

- trajectory setpoints are being published,
- the PX4 bridge is running,
- the Micro XRCE-DDS Agent is connected.

---

# Completion Checklist

Before continuing, verify:

- [ ] Keyboard publisher launches successfully.
- [ ] `t` initiates takeoff.
- [ ] `p` switches to Position mode.
- [ ] `o` switches to Offboard mode.
- [ ] `l` switches to landing mode.
- [ ] `d` disarms the drone 
- [ ] Commands are accepted by PX4.

---

# Transition

The keyboard publisher is now configured and capable of commanding the
vehicle.

The next chapter verifies that communication between every major system
component is functioning correctly before autonomous flight testing
begins.

➡ Continue to **Chapter 4.5 — Communication Pipeline Verification**
