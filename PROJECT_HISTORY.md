# Project History

This document records the major debugging milestones that led to the current working Drone EGO Swarming system.

The goal is to preserve technical knowledge that cannot easily be understood by looking at the final source code alone.

---

# Milestone 1

Keyboard control successfully connected to PX4 by completing calls and echos to determine where the information is going and if said information was being recieved. By creating a mnaul prige between PX4 and the publisher I was able to determine the launhc file had an improper ordering that woudl not correctly launch the Agent.

Commands:

- t
- p
- o
- l
- d
- m

worked as expected.

---

# Milestone 2

EGO Planner generated trajectories.

The drone did not follow them.

Investigation showed that the bridge was receiving planner commands but never forwarding them to PX4.

Issue was then solved in Milestone 3

---

# Milestone 3

The bridge originally subscribed to:

/fmu/out/vehicle_status

and

/fmu/out/vehicle_status_v1

The tested PX4 version actually published:

/fmu/out/vehicle_status_v4

Adding the v4 subscription allowed the bridge to recognize Offboard mode and publish EGO trajectories.

---

# Milestone 4

EGO Planner entered:

Depth Lost! EMERGENCY_STOP

The planner expected:

/depth_camera_bestef

/lidar_points

The simulation originally provided different topic names.

After correcting the sensor topics, EGO successfully generated trajectories.

---

# Milestone 5

RViz 2D Goal Pose successfully commanded the drone through:

RViz
↓

EGO Planner
↓

PX4 Bridge
↓

PX4

↓

Gazebo

Meaning the setup was completed.
