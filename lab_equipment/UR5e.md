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
## Electrical Signaling

> :exclamation: **If the proper settings are not configured in the Installation in the teach pendant, the emergency stop will not properly deactivate the end-effector power relay and/or the status LEDs will not indicate the correct status.**

The digital I/O signal ports inside the control box have been connected to the LED signal tower stack (the stoplight-like light) and the relay connecting power to the end-effector (currently the [JIMEE](JIMEE.md)) such that when the emergency stop button on the teach pendant is pressed, power to the end-effector is disconnected. Power to the end-effector is similarly disconnected when the UR5e is powered off. 

The status light and end-effector power relay are connected to the I/O ports inside the UR5e e-Series Control Box via an aviation plug and a 6-conductor wire with the following configuration:

|Aviation Plug Terminal  | Wire Color  | Signal      | UR5e Control Box Pin |
|-                       |-            |-            |-                     |
| 8                      | Black       | GND         | 0V                   |
| 1                      | Brown       | Amber Light | DO1                  |
| 2                      | Blue        | Green Light | DO0                  |
| 3                      | Red         | Red Light   | Power 24V            |
| 4                      | White       | Relay A1    | CO0                  |
| 5                      | Green       | Relay A2    | 0V                   |

The following table indicates the configuration of the relay. Note that to get an inverted signal for the red signal light, the red light power wire is connected through normally closed terminals in the relay:

|Terminal Pair   | Configuration   | Use                             |
|-               |-                |-                                |
| (A1, A2)       | Actuator        | Activates/Deactivates the relay |
| (13, 14)       | Normally Open   | End-Effector Power              |
| (23, 24)       | Normally Open   | End-Effector GND                |
| (33/31, 34/32) | Normally Closed | Unused                          |
| (43/41, 44/42) | Normally Closed | Red LED Status Light Power      |

The **Installation** settings on the teach pendant are set such that the digital outputs in the UR5e control box activate the LED signal tower stack to act as a status indicator with the following meaning:

| Status Light Color | Meaning                                |
|-                   |-                                       |
| Solid Green        | Robot power is on                      |
| Flashing Amber     | Robot is running a program and may move. **Use caution when standing or walking near the robot.** |
| Solid Red          | System emergency stop has been pressed |

The **Installation** settings are important to get the proper status signals and effects resulting from pressing the emergency stop button. If you use a new **Installation**, you will need to configure the I/O settings for that **Installation** appropriately. The **Installation** settings should be as follows:

**----------------ADD THE INSTALLATION SETTINGS USED HERE----------------------**

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

The documentation explaining setup and usage of the ROS 2 driver is a little disorganized because it was written and improved gradually over the course of several ROS releases (ROS Foxy through ROS Humble). However, as they improved the documentation, Universal Robots didn't really retroactively update it in branches for prior ROS releases (e.g. the release for ROS Foxy). In earlier releases (ROS Foxy) the documentation was basically all in the README file for the [Universal_Robots_ROS2_Driver][ros2driver-repo] repository. By the time of the release for ROS Humble, the repository README is still the starting place for the documentation, but the majority of the official driver documentation was moved to docs.ros.org:

- [Driver Documentation][driver-docs]

If you are using ROS Humble, simply start at the README for the [Universal_Robots_ROS2_Driver][ros2driver-repo] repository which will link to the driver documentation linked above. Unfortunately, if you are using an earlier ROS release, neither the README nor the documentation link above are perfect resources alone because the README is incomplete and makes you believe that you have to build the driver from source. On the other hand, the documentation on docs.ros.org (which is aimed at the release for ROS Humble) has subtle differences from earlier releases (e.g. the launch files are in different packages for ROS Humble and ROS Foxy). Probably the best course of action is to start at the README for any given release and then supplement with the docs.ros.org documentation. Honestly, the docs.ros.org documentation can be treated as the primary documentation, you just need to be familiar with the few differences if you are using earlier releases like ROS Foxy. These primary difference is the package where each particular launch file is found.

**Setup Necessary Only Once (e.g. setup already completed)**

The IP address of the UR5e has been configured to `192.168.1.102`. The UR5e already has the **External Control** URCap installed and configured to talk to a host PC with the IP address `192.168.1.101`. A program using the URCap has also already been made which is called `Control_with_ROS.urp`.

**Installing the Driver**

Since ROS Foxy, the driver packages have been released on the ROS 2 APT repository and therefore can be easily installed on Linux using the APT package manager:

```
sudo apt install ros-${ROS_DISTRO}-ur-robot-driver
```

The above command will install the `ur_robot_driver` package but will also result in installing the other driver packages due to the package dependency tree. It is recommended to install the driver in this way. The only package that may not automatically install is `ur_calibration`. If you need this package simply install it with

```
sudo apt install ros-${ROS_DISTRO}-ur-calibration
```

If you need to build the driver from source, follow the instructions on the README for each respective release.

### Overriding Driver Default Configuration and Robot Description (URDF, SRDF, etc.)

The UR robot driver packages contain launch files that set up and launch the driver and, if desired, the `move_group` node from MoveIt 2 for motion planning with UR robots. There are many launch files, but the most important ones are: `ur_control.launch.py` and `ur_moveit.launch.py`. As mentioned above, the package in which these files are found is not the same in each ROS 2 release (e.g. in ROS Foxy they are found in the `ur_bringup` package). These launch files use `xacro` and many YAML configuration files to produce a URDF (and an SRDF in the case of `ur_moveit.launch.py`) of the robot at runtime and are designed to accept many arguments that allow for limited changes to the configuration and robot description (e.g. specifying the robot IP address, changing the UDRF/SRDF files used, etc). Although overriding the configuration and robot description used by these launch files is not strictly necessary, it must be done to achieve accurate robot motion or if the robot has a custom end effector. The following is a list of some reasons (not necessarily all of them) to override the default configuration:

1. It is important to use calibrated kinematic parameters specific to the robot in use. The driver launch files obtain this calibration from a `default_kinematics.yaml` file found in the `config/ur5e/` directory of the *description package* they are told to use. This package defaults to the `ur_description` package which contains a `default_kinematics.yaml` file with a default calibration. A calibration file with parameters for a specific robot can be obtained using the `ur_calibration` package. Overriding the default file makes forward and inverse kinematics accurate.
2. If an end-effector is attached to the robot (e.g. the [JIMEE][jimee]) you will need to modify the URDF of the robot. You will also likely want to modify the SRDF if motion planning with MoveIt is desired. Further, for some reason, adding collision obstacles to the MoveIt motion planning scene using the `PlanningSceneInterface` class has not worked as expected. As a workaround these obstacles can be added as links of the robot itself in the URDF.
3. When motion planning with MoveIt, we have found that the default joint limits produce conditions that make it impossible for MoveIt to compute plans. The driver launch files obtain joint limits from a `joint_limits.yaml` file found in the `config/ur5e/` directory of the *description package* they are told to use. This package defaults to the `ur_description` package. In order to successfully plan with MoveIt, the joint limits all need to be restricted to +/- 180 degrees by overriding the default `joint_limits.yaml` file.

It is recommended that a package using the UR robot driver should contain the configuration and robot description files meant to override the default ones. Then the driver launch files can be called with arguments that appropriately redirect them to use these new files. Since it is quite tedious to type these arguments every time a driver launch file is launched, the package with the overriding files can also contain simple launch files that launch the driver launch files with a specific set of arguments. Correctly overriding configuration and robot description in this way requires that the overriding files be located in specific relative paths within the overriding package and that these files be installed properly using the `install()` command in the `CMakeLists.txt` file. Please refer to the [`rogue_demo`][rogue_demo] package in the [ur-space-debris-experiments][ur-space-debris-experiments] repository for an example of how to correctly override the default driver configuration and robot descriptions and use MoveIt for motion planning.

The driver launch files do not allow for overriding every part of the configuration. These launch files use a number of configuration files that are hardcoded into the launch files and therefore can't be swapped for counterparts that could be stored in an overriding package. For example, it is not possible to override configuration files used to specify the motion planning settings of MoveIt. If modification of these files is necessary, it will be necessary to copy the driver launch files to the overriding package and modify them accordingly. Then these modified launch files are used instead of the ones in the driver. This will require taking time to understand the details of the driver configuration and launch structure because the driver launch files are more complex than typical launch files. The `README.md` files of the [Universal_Robots_ROS2_Description][ur_description] repository and the [`ur_calibration`][ur_calibration] package should be helpful in this regard. This also means that as the driver is updated by Universal Robots, it may be necessary to update the overriding package's modified copy of those launch files accordingly.

### Dealing With Non-Smooth Motion

If you experience non-smooth motion on the robot, it may be necessary to switch to using a real-time kernel. Universal Robots provides instructions on how to do this on [here on docs.ros.org][rt-kernel].

[docs]: https://bitbucket.org/mmrobotics/docs-ur5e-6dof-arm/src/master/
[ur-github]: https://github.com/UniversalRobots
[ros2driver-repo]: https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver
[driver-docs]: https://docs.ros.org/en/ros2_packages/rolling/api/ur_robot_driver/index.html
[rt-kernel]: https://docs.ros.org/en/ros2_packages/rolling/api/ur_robot_driver/installation/real_time.html
[jimee]: https://bitbucket.org/mmrobotics/lab-wiki/wiki/lab_equipment/JIMEE.md
[rogue_demo]: https://bitbucket.org/mmrobotics/ur-space-debris-experiments/src/master/rogue_demo/
[ur-space-debris-experiments]: https://bitbucket.org/mmrobotics/ur-space-debris-experiments/src/master/
[ur_description]: https://github.com/UniversalRobots/Universal_Robots_ROS2_Description
[ur_calibration]: https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver/tree/main/ur_calibration