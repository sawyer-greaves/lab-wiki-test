[Home](../Home)
# Yaskawa Motoman MH5 6-DOF Robot Arm

**Contents**

[TOC]

---
## Introduction

The Yaskawa Motoman MH5 6-DOF Robot Arm is our blue industrial robot arm found inside an aluminum safety cage. Specifically, the MH5 refers to the robot manipulator arm itself. The DX100 is the large controller box found underneath the MH5 and is responsible for driving it. Connected to the DX100 is a handheld pendant device that is used to manually control the MH5. The MH5 can be software controlled using a computer communicating with the DX100 over Ethernet. A software implementation for controlling the MH5 from a host computer has been implemented in the [Robotics Framework][rob] (see details in the *Software Control from a Host Computer Using the Robotics Framework* section below).

- [MH5 and DX100 Documentation][docs]
    
    Contains:
    - Documentation from the manufacture
    - A Solidworks CAD model of the MH5 Manipulator
    - Information related to maintenance (receipts, etc.)


---
## The MH5 Robot Arm

The MH5 robot arm has 6 joints. Each joint is named with a letter from base to tool flange as follows: `S L U R B T`.

### Robot Coordinate Frame

From the point of view of the robot, the x-axis points forward away from the robot, the y-axis points to the left, and the z-axis points upward (the coordinate axes match the ROS standard outlined in [REP 103](https://www.ros.org/reps/rep-0103.html)). A diagram is attached to the peg board in the workspace for quick reference. The exact location of the frame origin is unknown but it is somewhere in the center of the robot base. 

### Encoder Battery

The encoders measuring joint positions are not absolute encoders. The absolute joint position is known because the encoders are never powered off. There is a battery in the base of the arm that keeps the encoders powered even when the main DX100 power switch is turned off. This battery lasts about **10 years** and a warning will appear on the pendant when the battery level gets low. When this happens, you must contact Yaskawa to purchase a new battery. There are two battery ports such that the new battery can be connected before the old battery is removed. In this way power to the encoders is never lost.

The encoder battery was last replaced in February 2019.

>:warning: **The encoder battery in the base of the MH5 robot arm must be replaced approximately every 10 years or the robot's zero angle calibration will be invalidated and the robot will need to be manually recalibrated!**


---
## Basic Operation

Some basic operation of the robot will be described here. Full details are outlined in the DX100 Operators Manual (accessible through the documentation link above).

### Powering On/Off

The robot is powered on and off using a large switch on the door panel of the DX100. Note that red indicates the power is on and green indicates the power is off. Once the power has been switched on, the DX100 takes some time to boot up. This process can be monitored from the DX100 pendant. The DX100 should be allowed to fully boot up before commanding the robot or powering it off.

### DX100 Programming Pendant

The DX100 Programming Pendant is used to control the robot manually. It is primarily designed to program robot motion in factory settings. In our lab, it is primarily used to manually jog the robot, manage DX100 Controller settings, and view/investigate error and warning messages. Below is a diagram of the pendant.

![](images/DX100_programming_pendant_diagram.png)

A user ID (or password) is required to change the security mode to a higher level which enables access to features and settings. The user IDs have not been changed from the factory presets and can be found in the DX100 Operators Manual. **Do not change the user IDs from the factory presets.** The manual also details each feature and menu allowed in each security mode.

### Manually Jogging the MH5

To jog the robot you must first make sure that the mode switch in the top left corner of the pendant is set to *TEACH*. Then power the joint servos by pressing and holding the enable switch (a black bar on the back of the pendant). Once the servos are powered, you can jog the robot using the axis keys. The axis keys will either jog individual joints or jog the tool flange in task space. The type of jogging is selected using the *COORD* button just under the display on the left. Pressing the *COORD* button changes an icon in the top right of the display. When that icon looks like a robot arm, the axis keys will jog the joints. When the icon looks like a cartesian coordinate frame, the axis keys will jog the tool flange in task space. When the DX100 is powered on, it defaults to jogging in joints space. The jogging speed is controlled using the manual speed keys and the current speed setting is indicated at the top of the display next to the coordinate icon. See the DX100 Operators Manual for more details.

### Errors and Warnings

Errors and warnings will appear in the bottom right of the pendant display. Some errors will prevent the robot from moving if they are not cleared. To clear an error or warning message, touch the message in the bottom right of the display and clear it. The message history can be found in the main menu.


---
## Software Control from a Host Computer Using the Robotics Framework

Need to have the mode switch on the pendant set to *REMOTE*.

Set the network interface card (NIC) that is plugged directly into the DX100 to a manual IPv4 address with the following settings:

```
IPv4: 192.168.255.2
Netmask: 255.255.255.0
```

All other settings can be left at default. The IPv4 address of the server running on the DX100 which the MH5Communicator class uses to communicate with the robot is: `192.168.255.1`. Since the MH5Robot class is hard-coded to give this IP to the MH5Communicator class, it should not matter what the Gateway and DNS settings are for the NIC since DNS is unnecessary (we already have an IP address), and the IP protocol will automatically recognize that the server IP is on the same subnet and will not attempt to send traffic to the Gateway. Also, make sure that any security is turned off in the security settings.

The Robots component of the [Robotics Framework][rob] also contains implementations of these interfaces for specific robots. Currently only the Yaskawa Motoman MH5 robot is implemented as part of the core framework because it is the only implementation that does not have additional library dependencies. This implementation is found in `Robots/Motoman` and the implementation is called MH5Robot.

Talk about the "digital twin" implementation of the MH5Robot class.

The DX100 will time out the server connection after 30 seconds of inactivity. The functions of the MH5Communicator class will automatically recognize this situation and reestablish the connection.

[rob]: https://bitbucket.org/utahtelerobotics/roboticsframework/src/master/
[docs]: https://bitbucket.org/utahtelerobotics/docs-yaskawa-motoman-6dof-arm/src/master/