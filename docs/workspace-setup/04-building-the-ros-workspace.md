# Chapter 3.4 — Building the ROS Workspace

**Estimated Time:** 15–30 minutes

---

# Overview

At this point, every required ROS package has been downloaded into the
workspace.

This chapter compiles those packages using the ROS 2 build system
**colcon**.

Building the workspace generates the executable programs, libraries,
message definitions, and environment setup files that will be used
throughout the remainder of the project.

Unlike PX4, which was built using `make`, every ROS package in the
workspace is built together using `colcon`.

---

# What is colcon?

`colcon` is the standard build system used by ROS 2.

It automatically:

- discovers ROS packages,
- determines package dependencies,
- builds packages in the correct order,
- generates installation files,
- and creates the workspace environment.

Every time source code changes, the affected packages should be rebuilt.

---

# Build the Workspace

Navigate to the workspace.

```bash
cd ~/ego_ws
```

Load the base ROS environment.

```bash
source /opt/ros/humble/setup.bash
```

Build every package.

```bash
colcon build --symlink-install
```

The first build may take several minutes depending on the hardware.

---

# Why Use --symlink-install?

Throughout this manual, builds are performed using:

```bash
colcon build --symlink-install
```

This option creates symbolic links instead of copying installed files.

Advantages include:

- faster rebuilds,
- easier debugging,
- immediate visibility of many source changes,
- reduced disk usage during development.

Because this repository is intended for active development, the
`--symlink-install` option is recommended.

---

# Build Output

After a successful build, the workspace should contain:

```text
ego_ws/

├── src
├── build
├── install
└── log
```

These directories are generated automatically by `colcon`.

---

# Build a Single Package

During development, rebuilding the entire workspace is often
unnecessary.

To rebuild one package:

```bash
colcon build \
--packages-select px4_ego_py \
--symlink-install
```

Replace:

```text
px4_ego_py
```

with any package name that requires rebuilding.

This command became extremely useful while debugging the
EGO-to-PX4 bridge.

---

# Verify the Build

Verify that the install directory exists.

```bash
ls ~/ego_ws/install
```

Expected:

A list of installed packages.

---

Verify that ROS recognizes EGO Planner.

```bash
ros2 pkg prefix ego_planner
```

Expected:

A valid installation path.

---

Verify the PX4 bridge package.

```bash
ros2 pkg prefix px4_ego_py
```

Expected:

A valid installation path.

---

Verify px4_msgs.

```bash
ros2 pkg prefix px4_msgs
```

Expected:

A valid installation path.

---

# Build Logs

If a build fails, the first place to inspect is:

```text
~/ego_ws/log
```

The build log usually contains the package responsible for the failure.

---

# Common Issues

---

## colcon: command not found

Cause

The ROS development tools were not installed.

Solution

Install:

```bash
sudo apt install \
python3-colcon-common-extensions
```

---

## Package not found

Cause

The package does not exist inside:

```text
~/ego_ws/src
```

Verify:

```bash
ls ~/ego_ws/src
```

---

## Build succeeds but ROS cannot find the package

Cause

The workspace has not been sourced.

This is one of the most common ROS mistakes.

Solution

Run:

```bash
source ~/ego_ws/install/setup.bash
```

---

## Old code still runs

Cause

The package was rebuilt, but the running ROS node was never restarted.

Solution

1. Stop the running node.
2. Rebuild the package.
3. Source the workspace.
4. Launch the node again.

---

# Completion Checklist

Before continuing, verify:

- [ ] Workspace built successfully.
- [ ] build directory created.
- [ ] install directory created.
- [ ] log directory created.
- [ ] ROS recognizes `ego_planner`.
- [ ] ROS recognizes `px4_ego_py`.
- [ ] ROS recognizes `px4_msgs`.

---

# Transition

The workspace has now been compiled.

However, ROS still does not automatically know where these packages are
located.

The next chapter explains how to configure the environment so every new
terminal can immediately use the Drone EGO Swarming packages.

➡ Continue to **Chapter 3.5 — Configuring the Environment**
