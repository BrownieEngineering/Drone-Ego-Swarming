# Drone-Ego-Swarming
Using ROS2 Humble, PX4, QGroundControl, Gazebo, Micro XRCE Agent, Mavros2, and Ubuntu 22.04 to create a swarming repo for Search and Rescue. Conditions at time of test:

    Tested operating system: Ubuntu 22.04 
    ROS distribution: ROS 2 Humble 
    PX4 source commit: 25b7d627da 
    PX4 description at time of testing: v1.18.0-alpha1-469-g25b7d627da	 

# Swarming Prep
Your machine must have / be able to run
- Ubuntu22.04 

- ROS2 Humble 

- PX4 Firmware (>= 1.14.0,) and px4_msgs  

- QGroundControl 

- Gazebo Harmonic (Tips: use sudo apt-get install ros-humble-ros-gzharmonic. The command sudo apt-get install gz-harmonic may lead to problems of gz_bridge at following steps). Ensure you have the ego world donwloaded and ready to be activated. 

- Micro XRCE Agent 

- Mavros2 
