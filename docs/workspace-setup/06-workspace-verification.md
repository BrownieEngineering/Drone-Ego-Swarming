# Chapter 3.6 — Workspace Verification

**Estimated Time:** 10–15 minutes

---

# Overview

Before launching the Drone EGO Swarming system, verify that the ROS
workspace has been built successfully and that the required packages are
available.

This chapter performs several simple checks to confirm that the
development environment is ready for the remaining chapters.

If any verification step fails, resolve the issue before proceeding.

---

# Verify the Workspace Structure

Navigate to the workspace.

```bash
cd ~/ego_ws
```

Verify that the expected directories exist.

```bash
ls
```

Expected output:

```text
build
install
log
src
```

---

# Verify the Source Packages

List the packages stored in the workspace.

```bash
ls ~/ego_ws/src
```

Expected output should include:

```text
ego-swarm-ros2
px4_ego
px4_msgs
```

---

# Verify the ROS Environment

Open a new terminal.

Confirm that the ROS environment has been loaded.

```bash
echo $ROS_DISTRO
```

Expected output:

```text
humble
```

If no output is returned, source the environment.

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

---

# Verify Installed Packages

Confirm that ROS can locate the project packages.

```bash
ros2 pkg prefix ego_planner
```

```bash
ros2 pkg prefix px4_ego_py
```

```bash
ros2 pkg prefix px4_msgs
```

Each command should return a valid installation path.

---

# Verify Package Discovery

List all packages containing the word "ego".

```bash
ros2 pkg list | grep ego
```

Expected output should include the project packages.

---

# Verify the Build Tools

Confirm that the required development tools are available.

```bash
colcon --version
```

```bash
git --version
```

```bash
python3 --version
```

Each command should complete without errors.

---

# Verify the PX4 Repository

Navigate to the PX4 repository.

```bash
cd ~/PX4-Autopilot
```

Verify the checked-out commit.

```bash
git rev-parse --short HEAD
```

Expected output:

```text
25b7d627da
```

---

# Verify the Workspace Can Be Rebuilt

Return to the workspace.

```bash
cd ~/ego_ws
```

Run another build.

```bash
colcon build --symlink-install
```

The build should complete successfully without introducing new errors.

---

# Common Issues

---

## Package cannot be located

Cause

The workspace has not been sourced or the package failed to build.

Solution

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

If the problem persists, rebuild the workspace.

---

## ROS_DISTRO is empty

Cause

The ROS environment has not been loaded.

Solution

Source the ROS installation and workspace.

---

## Build reports errors

Cause

One or more packages failed to compile.

Solution

Review the terminal output and the build logs located in:

```text
~/ego_ws/log
```

Correct the reported issue before continuing.

---

# Completion Checklist

Before continuing, verify:

- [ ] Workspace structure is correct.
- [ ] Source packages are present.
- [ ] ROS 2 environment is loaded.
- [ ] `ego_planner` is recognized.
- [ ] `px4_ego_py` is recognized.
- [ ] `px4_msgs` is recognized.
- [ ] Development tools are available.
- [ ] PX4 is on the documented commit.
- [ ] The workspace builds successfully.

---

# Transition

The Drone EGO Swarming development environment is now fully prepared.

The next chapter begins the project-specific configuration by modifying
the files required for communication between PX4, ROS 2, Gazebo, and
the EGO Planner.

➡ Continue to **Chapter 4 — Code Modifications**
