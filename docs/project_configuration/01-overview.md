# Chapter 4.1 — Overview of Project Modifications

**Estimated Time:** 10–15 minutes

---

# Overview

The previous chapters prepared the development environment by installing
the required software, creating the ROS workspace, and building the
project packages.

This chapter begins configuring the Drone EGO Swarming project.

Unlike the installation steps, the modifications described here are
specific to this project and are not part of the standard PX4 or ROS 2
installation procedures.

Each modification has been tested with the software versions documented
earlier in this manual.

---

# Why Are Modifications Required?

The Drone EGO Swarming project combines software from several independent
projects.

These projects were not originally designed to operate together without
additional configuration.

Several files must therefore be modified to:

- establish communication between PX4 and ROS 2,
- launch the correct simulation environment,
- configure project-specific nodes,
- support autonomous trajectory execution,
- and provide a consistent runtime environment.

Each modification described in this chapter has a specific purpose and
should be applied exactly as documented.

---

# Modification Categories

The project modifications fall into five categories.

| Category | Purpose |
|----------|---------|
| ROS Packages | Add project-specific ROS nodes |
| PX4 Configuration | Configure the flight controller for simulation |
| Launch Files | Start the correct collection of processes |
| Communication Bridges | Connect PX4, ROS 2, and Gazebo |
| Input Nodes | Provide commands to the autonomous system |

Each category is covered in the following sections.

---

# Before Making Changes

Before modifying any project files, verify:

- the workspace builds successfully,
- PX4 is on the documented commit,
- all required repositories are present,
- and the ROS environment has been sourced.

If any of these checks fail, return to the previous chapters before
continuing.

---

# Keeping Track of Modifications

Throughout this manual, every modified file will include:

- its location,
- the reason for the modification,
- the required changes,
- and how to verify the modification.

This approach makes it easier to compare future project updates with the
documented configuration.

---

# Common Issues

---

## Editing the wrong file

Some projects contain files with similar names.

Always verify the complete file path before making changes.

---

## Applying changes to a different software version

The modifications in this manual were developed using the software
versions documented in Chapter 2.

Applying them to newer versions may require additional adjustments.

---

## Skipping verification

Each modification should be verified before moving to the next section.

Small configuration mistakes are often easier to correct immediately than
after several additional changes have been made.

---

# Completion Checklist

Before continuing, verify:

- [ ] Development environment completed.
- [ ] Workspace builds successfully.
- [ ] ROS environment sourced.
- [ ] PX4 checked out to the documented commit.
- [ ] Ready to begin project-specific modifications.

---

# Transition

The next section begins integrating the PX4 bridge package into the
system and preparing communication between PX4 and ROS 2.

➡ Continue to **Chapter 4.2 — Integrating the PX4 Bridge**
