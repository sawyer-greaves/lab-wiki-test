[Home](../Home)
# Universal Robots UR5e 6-DOF Robot Arm

**Contents**

[TOC]

---
## Introduction

The Universal Robots UR5e 6-DOF Robot Arm is our silver and blue robot arm. The robot consists of the 6-DOF manipulator arm itself, the e-Series control box responsible for driving the robot, and the teach pendant device providing the primary touch-screen user interface for the robot. Among other things, the teach pendant enables manual jogging of the robot joints and writing and executing programs for robot motion. The robot can also be remotely software controlled using a computer communicating with the e-Series control box over Ethernet. Several communication protocols are supported with varying paradigms for telling the robot what to do. These techniques are all detailed in the documentation and using them requires additional software development. As an alternative, Universal Robots develops and maintains a ROS 2 driver (see details in the *Software Control from a Host Computer Using ROS 2* section below). The ROS 2 driver is the method we use in the lab for controlling this robot.

The **5** in **UR5e** refers to the payload the robot can support in kilograms (the UR3e can support 3 kg, the UR5e can support 5 kg, etc.), the **e** indicates that it is an e-Series robot.

> :warning: **You must read and be familiar with the UR5e User Manual (found at the documentation link below) before attempting to interact with the UR5e robot or use the teach pendant!**

> :warning: **The joints are back-drivable when drive power is off, but considerable manual force/torque is required. Back-driving the joints in this way is only intended for emergency purposes.**

- [Universal Robots UR5e Documentation][docs]

   Contains:

   - Documentation from the manufacturer
   - Solidworks and other CAD models of the UR5e manipulator
   - Information related to maintenance (receipts, etc.)

### Terminology & Acronyms

- **PolyScope**: The user interface (GUI) running on the teach pendant
- **CB**: Usually refers to Control Box (e.g. CB3, CB 5.2, etc.)
- **URControl**: The low-level robot controller running on the Mini-ITX PC inside the control box
- **URScript**: A scripting/programming language interpretable by URControl used to command the robot (no need to learn this if you are using the ROS 2 driver).
- **URCap**: A software bundle meant to be installed onto the teach pendant and runs as a child process of PolyScope. URCaps contribute additional functionality to PolyScope.


---
## Software Control from a Host Computer Using ROS 2

### ROS 2 Driver Setup and Usage

The [ROS 2](../necessary_skills/ROS.md) driver for UR robots consists of several ROS 2 packages. The source code for these packages is hosted on GitHub in repositories managed by the [Universal Robots GitHub Organization][ur-github]. These repositories have branches corresponding to releases of the driver for each ROS 2 distribution. Most of the packages are found in the [Universal_Robots_ROS2_Driver][ros2driver-repo] repository, however, some of the packages exist in other standalone repositories. Here is a summary of the packages and their contents:

- `ur` - meta-package that provides a single point of installation for the released packages. **Introduced in the release for ROS Humble.**
- `ur_bringup` - launch file and run-time configurations, e.g. controllers. **In the release for ROS Galactic, launch files in this package were moved to the other driver packages (below) and this package was deprecated. This package will be removed in the release for ROS Iron.**
- `ur_calibration` - tool for extracting calibration information from a real robot.
- `ur_controllers` - implementations of controllers specific for UR robots.
- `ur_dashboard_msgs` - package defining messages used by dashboard node.
- `ur_description` - description files for the UR robots: meshes, URDF/XACRO files, etc. **Moved to a standalone repository in ROS Galactic.**
- `ur_moveit_config` - example MoveIt configuration for UR robots.
- `ur_robot_driver` - driver / hardware interface for communication with UR robots.


The documentation explaining setup and usage of the ROS 2 driver is a little disorganized because it was written and improved gradually over the course of several ROS releases (ROS Foxy through ROS Humble). However, as they improved the documentation, Universal Robots didn't really retroactively update it in branches for prior ROS releases (e.g. the release for ROS Foxy). In earlier releases (ROS Foxy) the documentation was basically all in the README file for the [Universal_Robots_ROS2_Driver][ros2driver-repo] repository. By the time of the release for ROS Humble, the repository README is still the starting place for the documentation, but the majority of the official driver documentation is found on docs.ros.org:

- [Driver Documentation][driver-docs]

Subtle things have changed with each release making it hard to recommend 

This wiki page attempts to unify this information such that it can be used as the main starting point and refers to the driver repository README for any information not described here.

Since ROS Foxy, the driver packages have been released on the ROS 2 APT repository and therefore can be easily installed on Linux using the APT package manager:

```
sudo apt install ros-${ROS_DISTRO}-ur-robot-driver
```

The above command will install the `ur_robot_driver` package and all the other driver packages as a result of the package dependency tree.



### Specific ROS 2 Driver Usage Tips

### Dealing With Non-Smooth Motion

If you experience non-smooth motion on the robot, it may be necessary to switch to using a real-time kernel. Universal Robots provides instructions on how to do this in the `doc/` directory of the   `ur_robot_driver` ROS package. For ROS 2 Foxy these instructions are located [here](https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver/blob/foxy/ur_robot_driver/doc/real_time.md). For other distributions, the structure of the `doc/` directory is different.

[docs]: https://bitbucket.org/utahtelerobotics/docs-ur5e-6dof-arm/src/master/
[ur-github]: https://github.com/UniversalRobots
[ros2driver-repo]: https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver
[driver-docs]: https://docs.ros.org/en/ros2_packages/rolling/api/ur_robot_driver/index.html