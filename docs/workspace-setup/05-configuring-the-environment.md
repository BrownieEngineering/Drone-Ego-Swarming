# Chapter 3.5 — Configuring the Environment

**Estimated Time:** 5–10 minutes

---

# Overview

After building the ROS workspace, the environment must be configured so
that ROS can locate the newly built packages.

Without sourcing the workspace, ROS will only recognize the packages
installed with the base ROS 2 distribution.

This chapter explains how to load the Drone EGO Swarming workspace and
optionally configure it to load automatically in new terminal sessions.

---

# Source the ROS 2 Installation

Before sourcing the workspace, load the base ROS 2 environment.

```bash
source /opt/ros/humble/setup.bash
```

This command makes the standard ROS 2 packages available.

---

# Source the Workspace

Next, source the workspace that was built in the previous chapter.

```bash
source ~/ego_ws/install/setup.bash
```

This command adds the Drone EGO Swarming packages to the current terminal
session.

This step must be repeated whenever a new terminal is opened unless the
workspace is configured to load automatically.

---

# Verify the Environment

Confirm that ROS can locate the workspace packages.

```bash
ros2 pkg list | grep ego
```

Expected output should include the project packages.

For example:

```text
ego_planner
ego_msgs
px4_ego_py
```

You can also verify an individual package.

```bash
ros2 pkg prefix px4_ego_py
```

A valid installation path indicates that the workspace has been sourced
successfully.

---

# Automatically Source the Workspace

To avoid manually sourcing the workspace every time a new terminal is
opened, append the following commands to your shell configuration.

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
echo "source ~/ego_ws/install/setup.bash" >> ~/.bashrc
```

Reload the configuration.

```bash
source ~/.bashrc
```

New terminal sessions will now automatically load both the base ROS 2
installation and the Drone EGO Swarming workspace.

---

# Common Issues

---

## Package not found

Cause

The workspace has not been sourced.

Solution

Run:

```bash
source /opt/ros/humble/setup.bash
source ~/ego_ws/install/setup.bash
```

---

## Changes are not reflected

Cause

The workspace was rebuilt, but the current terminal is still using the
previous environment.

Solution

Source the workspace again.

```bash
source ~/ego_ws/install/setup.bash
```

---

## New terminal cannot find packages

Cause

The workspace has not been added to `~/.bashrc`.

Solution

Either source the workspace manually or configure automatic sourcing as
shown above.

---

# Completion Checklist

Before continuing, verify:

- [ ] ROS 2 installation sourced.
- [ ] Drone EGO Swarming workspace sourced.
- [ ] Project packages are visible with `ros2 pkg list`.
- [ ] `px4_ego_py` can be located by ROS.
- [ ] Automatic sourcing has been configured (optional).

---

# Transition

The ROS environment is now fully configured.

The next chapter verifies that the workspace, packages, and environment
are ready before launching the Drone EGO Swarming system.

➡ Continue to **Chapter 3.6 — Workspace Verification**
