[Home](../Home)
# Universal Robots UR5e 6-DOF Robot Arm

**Contents**

[TOC]

---
## Safety Items
- The joints are back-drivable when drive power is off, but considerable manual force/torque is required. Back-driving the joints in this way is only intended for emergency purposes.

---
## Setup

This section is a guide for setting up the UR5e robot for use with the ROS 2 driver provided by Universal Robotics and for use in any particular robotics application.

The first set of steps below have been completed already and can be skipped. They are included here for completeness in documenting the setup process. They can be used when/if a new robot or computer needs to be set up or in case the configuration becomes messed up for whatever reason:

3. Install the External Control URCap onto the UR5e and create a program that runs it.
4. Configure a static IP address on the UR5e pendant
5. Configure a static IPv4 address on the host computer

Steps for a new user:

1. Install the ROS 2 distribution you plan to use
    - There are two common methods (see the [ROS page](../necessary_skills/ROS.md) for more info):
        1. System install using `apt` (system install only needs to happen once for each computer)
        2. Conda environment install using [RoboStack](https://robostack.github.io/)
2. Install colcon
   ```
   sudo apt install python3-colcon-common-extensions
   ```
3. Create a colcon workspace
   ```
   cd ~
   mkdir -p ros_ws/src
   ```
4. Follow the instructions in the [Universal_Robots_ROS2_Driver](https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver) GitHub repository README to clone the driver repository and any other relevant repositories, install dependencies, and compile. **Make sure to look at the instructions on the branch for the ROS distribution being used. The instructions are slightly different for each ROS distribution.**
5. Source the workspace as usual

## Using the ROS 2 Driver

## Dealing With Non-Smooth Motion

If you experience non-smooth motion on the robot, it may be necessary to switch to using a real-time kernel. Universal Robots provides instructions on how to do this in the `doc/` directory of the   `ur_robot_driver` ROS package. For ROS 2 Foxy these instructions are located [here](https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver/blob/foxy/ur_robot_driver/doc/real_time.md). For other distributions, the structure of the `doc/` directory is different.