# Chapter 2.1 — Ubuntu Preparation

---

# Overview

Ubuntu is the operating system used throughout the Drone EGO Swarming
project.

Every piece of software used by this repository—including ROS 2, PX4,
Gazebo, EGO Planner, MAVROS, and Micro XRCE-DDS—runs on top of Ubuntu.

Choosing the correct version of Ubuntu is the most important start to 
the process as a whole, we recommend using the suggested tested version.

---

# Why Ubuntu?

Robotics software is traditionally developed for Linux operating systems.

Although some components may support Windows or macOS, the complete Drone
EGO Swarming software stack was designed and tested using Linux.

Ubuntu provides:

- Long-Term Support (LTS)
- Stable package repositories
- Excellent ROS compatibility
- PX4 development support
- Native Gazebo support
- Community documentation
- Driver support for NVIDIA GPUs

Because nearly every robotics research laboratory uses Ubuntu, choosing
Ubuntu also makes it significantly easier to receive community support.

---

# Why Ubuntu 22.04 LTS?

This project was developed using:

```text
Ubuntu 22.04 LTS
```

Ubuntu 22.04 was selected because it is the officially supported operating
system for:

- ROS 2 Humble
- Gazebo Harmonic
- PX4 Autopilot
- MAVROS
- Micro XRCE-DDS Agent

Using Ubuntu 24.04 or newer may require:

- different package names,
- newer ROS distributions,
- modified launch files,
- newer PX4 message definitions,
- or additional dependency fixes.

For the most reproducible installation, use Ubuntu 22.04 LTS.

If newer models are proven to be stable, please update.

---

# Tested Development Machine

The Drone EGO Swarming project was successfully tested using the
following hardware.

| Component | Tested Hardware |
|------------|-----------------|
| Operating System | Ubuntu 22.04.5 LTS |
| CPU | Intel Core i7-8750H |
| Memory | 16 GB RAM |
| Graphics | NVIDIA GeForce GTX 1060 |
| Secondary Graphics | Intel UHD Graphics 630 |
| Shell | Bash |

The complete software stack operated correctly on this hardware.

Performance, however, was only moderate while simultaneously running:

- Gazebo
- RViz
- PX4 SITL
- EGO Planner
- MAVROS
- QGroundControl
- Micro XRCE-DDS Agent
- Depth image processing
- Point cloud processing

Newer processors and GPUs will improve simulation performance,
particularly during future multi-drone development.

---

# Official Ubuntu Documentation

Ubuntu

https://ubuntu.com/

Ubuntu Downloads

https://ubuntu.com/download

Ubuntu Installation Guide

https://ubuntu.com/tutorials/install-ubuntu-desktop

---

# Installing Ubuntu

If Ubuntu 22.04 is not already installed:

1. Download Ubuntu 22.04 LTS from the official Ubuntu website.
2. Create a bootable USB installer.
3. Install Ubuntu.
4. Update the operating system before continuing.

The Drone EGO Swarming project assumes a clean Ubuntu installation.

---

# Update Ubuntu

Open a terminal.

Run:

```bash
sudo apt update
sudo apt upgrade -y
```

This updates all installed packages to the newest versions available for
Ubuntu 22.04.

Reboot if requested.

---

# Install Basic Development Tools

Many robotics packages require common Linux development utilities.

Install them now.

```bash
sudo apt install -y \
git \
curl \
wget \
build-essential \
cmake \
ninja-build \
python3 \
python3-pip \
python3-venv \
python3-colcon-common-extensions \
nano \
software-properties-common
```

These tools will be used throughout the remainder of the project.

---

# Verify Ubuntu Version

Run:

```bash
lsb_release -a
```

Expected output should contain:

```text
Distributor ID: Ubuntu

Release: 22.04
```

---

# Verify Kernel

Run:

```bash
uname -r
```

Expected:

A Linux kernel version is displayed.

Example:

```text
6.8.x
```

Kernel versions may differ depending on updates.

---

# Verify Available Memory

Run:

```bash
free -h
```

Verify that sufficient memory is available.

The tested system contained:

```text
16 GB RAM
```

---


# Common Issues

---

## Unsupported Ubuntu Version

If:

```bash
lsb_release -a
```

returns anything other than Ubuntu 22.04, the remainder of this guide
may not exactly match your system.

---

## `apt` cannot update

If:

```bash
sudo apt update
```

returns repository errors:

Verify:

- internet connectivity,
- Ubuntu mirrors,
- date and time settings.

---

## Terminal commands not found

If common Linux commands are unavailable, verify that Ubuntu installed
correctly and that the development tools were installed successfully.

---

# Completion Checklist

Before continuing to Chapter 2.2, verify:

- [ ] Ubuntu 22.04 is installed.
- [ ] Ubuntu packages have been updated.
- [ ] Development tools have been installed.
- [ ] Internet connectivity works.
- [ ] Disk space is sufficient.
- [ ] CPU information is available.
- [ ] RAM information is available.

---

# How Ubuntu Fits Into Drone EGO Swarming

Ubuntu forms the foundation of the complete software stack.

Every major component used throughout this project runs on top of Ubuntu.

```text
Ubuntu
│
├── ROS 2 Humble
│
├── Gazebo Harmonic
│
├── PX4 Autopilot
│
├── MAVROS
│
├── Micro XRCE-DDS Agent
│
├── RViz
│
├── QGroundControl
│
├── EGO Planner
│
└── Drone EGO Swarming
```

The remaining chapters progressively build upward through this software
stack.

The next chapter installs the communication framework that connects every
component together:

➡ **Chapter 2.2 — ROS 2 Humble**
