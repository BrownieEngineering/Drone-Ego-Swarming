# System Requirements

## Purpose

This document explains the hardware, operating system, software, versions, and directory layout required to reproduce the tested Drone EGO Swarming simulation.

This page describes **what must be available** before beginning installation and workspace setup.

Installation commands are provided separately in [Software Installation](02-installation.md).

## Tested configuration

The working single-drone simulation was tested using the following environment:

| Component | Tested configuration |
|---|---|
| Operating system | Ubuntu 22.04 |
| ROS distribution | ROS 2 Humble |
| Simulator | Gazebo Harmonic |
| PX4 commit | `25b7d627da` |
| PX4 description | `v1.18.0-alpha1-469-g25b7d627da` |
| Ground-control station | QGroundControl |
| ROS build system | colcon |
| Shell | Bash |
| Primary language | Python 3 and C++ |

Other software versions may work, but they may use different package names, message versions, ROS topics, launch behavior, or dependency combinations.

## Clean-machine assumption

The normal setup documentation assumes a clean Ubuntu 22.04 machine that does not already contain:

- older PX4 source trees,
- duplicate EGO Planner workspaces,
- stale colcon build directories,
- conflicting ROS overlays,
- or manually installed Gazebo versions that conflict with the ROS packages.

Machines with previous robotics workspaces may still work, but they may require additional cleanup. Those cases are documented in [Troubleshooting](08-troubleshooting.md).

## Recommended computer hardware

Running Gazebo, PX4 SITL, EGO Planner, RViz, MAVROS, QGroundControl, and ROS 2 at the same time can require substantial system resources.

Recommended minimums:

| Resource | Recommendation |
|---|---|
| Processor | Modern six-core CPU or better recommended |
| Memory | 16 GB minimum; 32 GB recommended for multi-drone development |
| Storage | At least 40 GB of free SSD space |
| Graphics | Dedicated NVIDIA GPU recommended |
| Tested GPU | GTX 1060; functional but moderately slow under the complete stack |
| Preferred GPU | Newer NVIDIA GPU with proprietary Linux driver |
| Display | 1080p or larger recommended |

## Required operating system

### Ubuntu 22.04

Ubuntu 22.04 is the tested operating system for this project.

It was selected because it is the supported Ubuntu release associated with ROS 2 Humble and is compatible with the software versions used during development.

The setup instructions assume:

```text
Ubuntu 22.04
64-bit x86 Linux
Bash shell
sudo access
```

Verify the Ubuntu version with:

```bash
lsb_release -a
```

Expected output should include:

```text
Release:        22.04
```

## Required middleware

### ROS 2 Humble

ROS 2 provides the communication layer used by the project.

It allows the following components to exchange messages:

- RViz,
- EGO Planner,
- the keyboard publisher,
- the EGO-to-PX4 bridge,
- MAVROS,
- PX4 through Micro XRCE-DDS,
- Gazebo sensor bridges,
- and ROS visualization and debugging tools.

The tested ROS distribution is:

```text
ROS 2 Humble
```

Verify the ROS distribution after installation with:

```bash
echo $ROS_DISTRO
```

Expected output:

```text
humble
```

Also verify the ROS command-line interface:

```bash
ros2 --help
```

## Required simulator

### Gazebo Harmonic

Gazebo simulates:

- the drone model,
- the environment,
- depth-camera data,
- point-cloud data,
- vehicle physics,
- and the EGO obstacle world.

This project uses the ROS-packaged Gazebo Harmonic integration because the ROS-Gazebo bridge is required for sensor communication.

The installation guide uses packages such as:

```text
ros-humble-ros-gzharmonic
ros-humble-ros-gz-bridge
```

Installing only the standalone `gz-harmonic` package may not provide the ROS bridge configuration expected by this project.

After installation, verify Gazebo with:

```bash
gz sim --version
```

## Required flight stack

### PX4 Autopilot

PX4 provides:

- vehicle-state estimation,
- arming logic,
- Offboard mode,
- flight-mode handling,
- trajectory-setpoint control,
- failsafes,
- and the simulated vehicle controller.

The tested source state is:

```text
Commit: 25b7d627da
Description: v1.18.0-alpha1-469-g25b7d627da
```

The project uses PX4 SITL rather than physical hardware during the current development phase.

After cloning PX4, verify the selected commit with:

```bash
cd ~/PX4-Autopilot
git rev-parse --short HEAD
```

Expected output:

```text
25b7d627da
```

Verify the descriptive version with:

```bash
git describe --tags
```

Expected output:

```text
v1.18.0-alpha1-469-g25b7d627da
```

The exact PX4 version matters because PX4 ROS message topics may use versioned names. During testing, the active vehicle-status topic was:

```text
/fmu/out/vehicle_status_v4
```

## Required PX4 ROS messages

### `px4_msgs`

The `px4_msgs` package provides the ROS 2 message definitions used to communicate with PX4.

Important messages used by this project include:

- `VehicleStatus`,
- `VehicleCommand`,
- `VehicleCommandAck`,
- `VehicleLocalPosition`,
- `OffboardControlMode`,
- and `TrajectorySetpoint`.

The message definitions must be compatible with the PX4 source version being used.

## Required PX4-to-ROS transport

### Micro XRCE-DDS Agent

Micro XRCE-DDS Agent connects PX4’s uXRCE-DDS client to the ROS 2 DDS network.

The tested runtime command is:

```bash
MicroXRCEAgent udp4 -p 8888
```

It enables PX4 topics such as:

```text
/fmu/in/trajectory_setpoint
/fmu/in/offboard_control_mode
/fmu/in/vehicle_command
/fmu/out/vehicle_status_v4
/fmu/out/vehicle_local_position_v1
```

Verify the executable after installation with:

```bash
command -v MicroXRCEAgent
```

The command should return a valid executable path.

## Required MAVLink bridge

### MAVROS 2

MAVROS translates MAVLink communication between PX4 and ROS 2.

In the tested system, MAVROS was launched with:

```text
udp://:14540@127.0.0.1:14555
```

EGO Planner also used MAVROS odometry through:

```text
/mavros/local_position/odom
```

Verify MAVROS after installation with:

```bash
ros2 pkg prefix mavros
```

The command should return a valid package installation path.

## Required ground-control station

### QGroundControl

QGroundControl provides a visual interface for:

- PX4 connection status,
- vehicle arming state,
- flight mode,
- preflight checks,
- MAVLink communication,
- and general vehicle monitoring.

QGroundControl is not the primary trajectory planner in this project. RViz and EGO Planner provide the autonomous goal and path-planning path.

QGroundControl is used mainly to observe and verify PX4 behavior.

## Required planner

### EGO Planner ROS 2

EGO Planner generates collision-aware trajectories using:

- the current vehicle state,
- an RViz goal,
- depth-image data,
- point-cloud data,
- and an internal occupancy map.

The project references:

```text
https://github.com/DongnanHu6556/ego-swarm-ros2.git
```

The active planner node used during testing was:

```text
/drone_0_ego_planner_node
```

The main trajectory command topic was:

```text
/drone_0_planning/pos_cmd
```

## Required simulation-support repository

### `ego-planner-ros2-sim`

This project builds on files provided by:

```text
https://github.com/DongnanHu6556/ego-planner-ros2-sim.git
```

That repository provides or inspired:

- the PX4 SITL launch file,
- the keyboard publisher,
- the EGO-to-PX4 bridge,
- the Gazebo helper scripts,
- the EGO world,
- and supporting simulation configuration.

The BrownieEngineering repository stores and documents the known-working modifications required for the tested setup.

## Required visualization

### RViz 2

RViz is used to:

- visualize the map,
- view EGO trajectories,
- view the vehicle state,
- inspect planning behavior,
- and publish a 2D Goal Pose.

The working goal topic was:

```text
/goal_pose
```

The RViz fixed frame should be:

```text
map
```

Verify RViz after installation with:

```bash
ros2 pkg prefix rviz2
```

## Required ROS utility packages

The project also requires ROS packages or tools that provide:

- `ros_gz_bridge`,
- `topic_tools`,
- `tf2_ros`,
- message inspection,
- topic relays,
- and launch support.

Important debugging commands include:

```bash
ros2 topic list
ros2 topic info
ros2 topic echo
ros2 topic hz
ros2 node list
ros2 node info
ros2 pkg prefix
```

## Required development tools

The machine should also provide:

- Git,
- Python 3,
- pip,
- colcon,
- CMake,
- Ninja,
- GNU build tools,
- and a text editor.

The setup documentation uses `nano`, but any text editor may be used.

## Expected directory layout

The documentation assumes these paths:

```text
~/Drone-Ego-Swarming
~/PX4-Autopilot
~/ego-planner-ros2-sim
~/ego_ws
~/ego_ws/src
~/ros_proj/gazebo_start
~/.simulation-gazebo/worlds
```

Expected purpose of each directory:

| Directory | Purpose |
|---|---|
| `~/Drone-Ego-Swarming` | BrownieEngineering documentation and project files |
| `~/PX4-Autopilot` | PX4 source and SITL build |
| `~/ego-planner-ros2-sim` | Upstream simulation support repository |
| `~/ego_ws` | ROS 2 colcon workspace |
| `~/ego_ws/src` | EGO and PX4 bridge source packages |
| `~/ros_proj/gazebo_start` | Gazebo startup and depth bridge scripts |
| `~/.simulation-gazebo/worlds` | Gazebo world files |

Using different paths is possible, but launch files, copy commands, and helper scripts must be updated accordingly.

## Shell environment requirements

The project assumes Bash.

The base ROS 2 environment is loaded with:

```bash
source /opt/ros/humble/setup.bash
```

After the custom ROS workspace has been built, it is loaded with:

```bash
source ~/ego_ws/install/setup.bash
```

For a clean machine, `setup.bash` is the normal workspace entry point.

If a machine contains stale workspace underlays, the troubleshooting guide explains when `local_setup.bash` may be used temporarily.

## Simulation-only status

The current project has been tested in simulation.

It should not be transferred directly to a physical vehicle without validating:

- emergency-stop behavior,
- manual pilot takeover,
- coordinate conversion,
- sensor calibration,
- battery failsafes,
- communication-loss behavior,
- flight boundaries,
- geofencing,
- and physical safety procedures.

## Readiness checklist

Before continuing to installation and workspace setup, confirm that the target machine can support:

- Ubuntu 22.04,
- ROS 2 Humble,
- Gazebo Harmonic,
- PX4 SITL,
- Micro XRCE-DDS Agent,
- MAVROS,
- QGroundControl,
- RViz,
- EGO Planner,
- and the expected directory structure.

The next step is [Software Installation](02-installation.md).
