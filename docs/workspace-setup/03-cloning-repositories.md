# Chapter 3.3 — Cloning the Required Repositories

**Estimated Time:** 15–30 minutes

---

# Overview

The Drone EGO Swarming project is built from several independent
repositories.

Each repository provides a different part of the complete software
stack.

This chapter downloads each required repository and places it in the
expected directory.

By the end of this chapter, every required source repository will exist
on the system.

---

# Required Repositories

The project currently uses five primary directories.

| Repository | Purpose |
|------------|---------|
| Drone-Ego-Swarming | Documentation, project files, scripts, and guides |
| PX4-Autopilot | Flight controller source code |
| ego-planner-ros2-sim | Original simulation support repository |
| ego-swarm-ros2 | EGO Planner ROS 2 packages |
| px4_msgs | PX4 ROS message definitions |

---

# Clone Drone EGO Swarming

If you have not already cloned this repository:

```bash
cd ~

git clone https://github.com/BrownieEngineering/Drone-Ego-Swarming.git
```

Verify:

```bash
ls ~/Drone-Ego-Swarming
```

The repository contents should be displayed.

---

# Clone PX4 Autopilot

Navigate to your home directory.

```bash
cd ~
```

Clone PX4.

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

Enter the repository.

```bash
cd ~/PX4-Autopilot
```

Checkout the tested commit.

```bash
git checkout 25b7d627da
```

Update submodules.

```bash
git submodule update --init --recursive
```

---

# Clone the Simulation Repository

Return to your home directory.

```bash
cd ~
```

Clone:

```bash
git clone https://github.com/DongnanHu6556/ego-planner-ros2-sim.git
```

Verify:

```bash
ls ~/ego-planner-ros2-sim
```

---

# Clone EGO Planner

Navigate into the workspace source directory.

```bash
cd ~/ego_ws/src
```

Clone:

```bash
git clone https://github.com/DongnanHu6556/ego-swarm-ros2.git
```

Verify:

```bash
ls ~/ego_ws/src
```

Expected:

```text
ego-swarm-ros2
```

---

# Clone px4_msgs

Remain inside:

```text
~/ego_ws/src
```

Clone:

```bash
git clone https://github.com/PX4/px4_msgs.git
```

Verify:

```bash
ls ~/ego_ws/src
```

Expected:

```text
px4_msgs
```

---

# Copy the PX4 Bridge Package

The Drone EGO Swarming project uses the `px4_ego` package supplied by
the simulation repository.

Copy the package into the workspace.

```bash
cp -r \
~/ego-planner-ros2-sim/px4_ego \
~/ego_ws/src/
```

Verify:

```bash
ls ~/ego_ws/src
```

Expected:

```text
ego-swarm-ros2
px4_ego
px4_msgs
```

---

# Repository Summary

After completing this chapter, the important directories should appear
as follows.

```text
~

├── Drone-Ego-Swarming

├── PX4-Autopilot

├── ego-planner-ros2-sim

├── ego_ws
│   └── src
│       ├── ego-swarm-ros2
│       ├── px4_ego
│       └── px4_msgs

└── ros_proj
```

---

# Verify Repository Locations

Verify each repository exists.

```bash
ls ~

ls ~/ego_ws/src
```

The output should contain every required repository.

---

# Common Issues

---

## Repository already exists

If Git reports:

```text
destination path already exists
```

the repository has already been cloned.

Verify that it contains the expected files before continuing.

---

## Wrong repository location

If a repository was cloned into another directory, either:

- move it into the expected location,

or

- update every future command accordingly.

The documentation assumes the standard layout.

---

## Copy command failed

Verify that:

```text
~/ego-planner-ros2-sim/px4_ego
```

exists before copying.

---

# Completion Checklist

Before continuing, verify:

- [ ] Drone-Ego-Swarming cloned.
- [ ] PX4-Autopilot cloned.
- [ ] PX4 commit switched to the tested version.
- [ ] ego-planner-ros2-sim cloned.
- [ ] ego-swarm-ros2 cloned.
- [ ] px4_msgs cloned.
- [ ] px4_ego copied into the workspace.
- [ ] All repositories are located in the expected directories.

---

# Transition

The complete source code for the Drone EGO Swarming project has now been
downloaded.

The next chapter builds every ROS package inside the workspace using
`colcon`.

➡ Continue to **Chapter 3.4 — Building the Workspace**
