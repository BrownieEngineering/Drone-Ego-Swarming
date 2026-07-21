# Drone EGO Swarming

A ROS 2 and PX4 simulation project for autonomous drone navigation and future multi-drone search-and-rescue development.

This repository documents and stores the modifications required to connect:

- ROS 2 Humble
- PX4 SITL
- Gazebo Harmonic
- EGO Planner
- Micro XRCE-DDS Agent
- MAVROS 2
- QGroundControl
- RViz 2

The current working system allows a user to select a goal in RViz, generate a collision-aware trajectory with EGO Planner, and send that trajectory to a PX4-controlled drone in Gazebo.

The project builds on work from:

- https://github.com/DongnanHu6556/ego-planner-ros2-sim.git

## Project status

The following single-drone simulation pipeline has been successfully tested:

```text
RViz 2D Goal Pose
        |
        v
EGO Planner
        |
        v
/drone_0_planning/pos_cmd
        |
        v
EGO-to-PX4 control bridge
        |
        v
/fmu/in/trajectory_setpoint
        |
        v
PX4 SITL
        |
        v
Gazebo vehicle
```

Current work is focused on turning this working single-drone system into a reusable search-and-rescue swarming framework.

## Tested configuration

| Component | Tested version |
|---|---|
| Operating system | Ubuntu 22.04 |
| ROS distribution | ROS 2 Humble |
| Simulator | Gazebo Harmonic |
| PX4 commit | `25b7d627da` |
| PX4 description | `v1.18.0-alpha1-469-g25b7d627da` |

Other versions may require different package names, topic versions, message definitions, or launch-file changes.

## Current capabilities

- Launch PX4 SITL with Gazebo Harmonic
- Connect PX4 to ROS 2 through Micro XRCE-DDS
- Connect QGroundControl through MAVLink
- Publish keyboard commands for takeoff, position hold, Offboard control, landing, and disarming
- Generate trajectories with EGO Planner
- Select destinations through RViz
- Convert EGO Planner commands from ROS ENU coordinates to PX4 NED coordinates
- Send trajectory setpoints to PX4
- Use simulated depth-image and point-cloud data for planning
- Stop and hover when EGO cannot generate a safe route

## Documentation

The project documentation is being organized into the following guides:

1. [System requirements](docs/01-system-requirements.md)
2. [Software installation](docs/02-installation.md)
3. [Workspace setup](docs/03-workspace-setup.md)
4. [Required code modifications](docs/04-code-modifications.md)
5. [Running the system](docs/05-running-the-system.md)
6. [First flight](docs/06-first-flight.md)
7. [System architecture](docs/07-system-architecture.md)
8. [Troubleshooting](docs/08-troubleshooting.md)
9. [Search-and-rescue roadmap](docs/09-search-and-rescue-roadmap.md)

## Planned repository contents

```text
Drone-Ego-Swarming/
├── README.md
├── CONTRIBUTING.md
├── PROJECT_HISTORY.md
├── .gitignore
├── docs/
├── config/
├── scripts/
├── launch/
├── project-files/
└── worlds/
```

## Quick-start sequence

After completing the installation and setup guides:

1. Install the required software.
2. Clone the required repositories.
3. Build PX4 and the ROS 2 workspace.
4. apply the required project modifications.
5. Launch PX4, Gazebo, MAVROS, and the sensor bridges.
6. Launch the keyboard publisher and EGO-to-PX4 bridge.
7. Launch EGO Planner.
8. Launch RViz.
9. Take off with `t`.
10. Enable Offboard trajectory control with the lowercase letter `o`.
11. Select a clear goal using RViz **2D Goal Pose**.

## Safety notice

This project is currently validated in simulation only.

Do not transfer the control workflow directly to a physical aircraft without validating:

- flight modes,
- emergency-stop behavior,
- geofencing,
- sensor calibration,
- coordinate-frame conversion,
- battery failsafes,
- communication-loss behavior,
- and manual pilot takeover.

## Contributing

Development should occur on a separate branch and be reviewed through a pull request before being merged into `main`.
