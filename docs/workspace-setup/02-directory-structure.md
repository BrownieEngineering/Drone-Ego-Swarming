# Chapter 3.2 — Directory Structure

**Estimated Time:** 10–15 minutes

---

# Overview

Before cloning repositories or building software, it is important to
create and understand the directory structure used throughout this
project.

Using the same directory layout as this manual ensures that every
command, launch file, script, and configuration works exactly as
documented.

Although the directory names can be changed, doing so requires updating
launch files, scripts, and documentation.

For the most reproducible setup, use the structure shown below.

---

# Home Directory Layout

The Drone EGO Swarming project assumes the following layout inside your
home directory.

```text
~

├── Drone-Ego-Swarming
│
├── PX4-Autopilot
│
├── ego-planner-ros2-sim
│
├── ego_ws
│   ├── src
│   ├── build
│   ├── install
│   └── log
│
├── ros_proj
│   └── gazebo_start
│
└── .simulation-gazebo
    └── worlds
```

Every directory shown above will either be created manually or generated
during later chapters.

---

# Drone-Ego-Swarming

```text
~/Drone-Ego-Swarming
```

This repository contains:

- documentation,
- project history,
- modified project files,
- launch files,
- helper scripts,
- Gazebo worlds,
- and future Search and Rescue development.

This repository is **not** a ROS workspace.

It serves as the central reference for the entire project.

---

# PX4-Autopilot

```text
~/PX4-Autopilot
```

This directory contains the PX4 flight controller source code.

Examples include:

- PX4 firmware
- simulator launch files
- flight controller source
- PX4 build output

Later chapters will modify one launch file inside this repository.

---

# ego-planner-ros2-sim

```text
~/ego-planner-ros2-sim
```

This repository contains the original simulation support package used by
this project.

Examples include:

- keyboard publisher
- Gazebo helper scripts
- example launch files
- EGO simulation resources

Several files from this repository will later be copied into the ROS
workspace or referenced while configuring the project.

---

# ego_ws

```text
~/ego_ws
```

This is the primary ROS 2 workspace used throughout development.

Every ROS package that belongs to the Drone EGO Swarming project will be
built inside this workspace.

The important directory is:

```text
~/ego_ws/src
```

where the source code for all ROS packages will be placed.

After building, additional directories will appear automatically:

```text
build/

install/

log/
```

---

# ros_proj

```text
~/ros_proj
```

This directory stores helper scripts that are not part of the ROS
workspace itself.

For this project it contains:

```text
gazebo_start/
```

which stores:

- simulation startup script
- depth image bridge
- additional Gazebo helper scripts

Keeping these scripts separate helps avoid cluttering the ROS workspace.

---

# .simulation-gazebo

```text
~/.simulation-gazebo
```

This hidden directory is created by the Gazebo simulation tools.

It stores:

- downloaded models,
- downloaded worlds,
- simulation resources,
- user configuration.

The Drone EGO Swarming project copies the EGO world into:

```text
~/.simulation-gazebo/worlds
```

during setup.

---

# Create the Workspace Directory

Create the ROS workspace.

```bash
mkdir -p ~/ego_ws/src
```

Verify:

```bash
tree -L 2 ~/ego_ws
```

Expected:

```text
ego_ws
└── src
```

If the `tree` command is not installed:

```bash
sudo apt install tree
```

or verify using:

```bash
ls -R ~/ego_ws
```

---

# Create the Gazebo Helper Directory

```bash
mkdir -p ~/ros_proj/gazebo_start
```

Verify:

```bash
ls ~/ros_proj
```

Expected:

```text
gazebo_start
```

---

# Verify the Home Directory

Run:

```bash
ls ~
```

By the end of this manual the following directories should exist:

```text
Drone-Ego-Swarming

PX4-Autopilot

ego-planner-ros2-sim

ego_ws

ros_proj
```

Some of these may not exist yet depending on how far you have progressed
through the manual.

---

# Common Issues

---

## Repository cloned into the wrong directory

Cause

A repository was cloned somewhere other than the home directory.

Solution

Move the repository into the expected location or update all later
commands to match your chosen directory structure.

---

## `tree` command not found

Install:

```bash
sudo apt install tree
```

or use:

```bash
ls -R
```

instead.

---

## Missing directories

Create them manually using:

```bash
mkdir -p
```

The command is safe to run even if the directory already exists.

---

# Completion Checklist

Before continuing, verify:

- [ ] `~/Drone-Ego-Swarming` exists.
- [ ] `~/PX4-Autopilot` exists.
- [ ] `~/ego-planner-ros2-sim` exists.
- [ ] `~/ego_ws/src` exists.
- [ ] `~/ros_proj/gazebo_start` exists.
- [ ] You get the purpose of each directory.

---

# Transition

The required directory structure is now in place.

The next chapter downloads the repositories required by the Drone EGO
Swarming project and places them into the workspace.

➡ Continue to **Chapter 3.3 — Cloning the Required Repositories**
