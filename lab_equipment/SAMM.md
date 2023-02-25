[Home](../Home)
# SAMM - Spherical-Actuator-Magnet Manipulator

**Contents**

[TOC]

>:exclamation: **Serious risk of bodily injury or harm to sensitive electronics!** The SAMM contains a **strong permanent magnet**. Always maintain caution when working near the SAMM and avoid bringing magnetically permeable (e.g. ferrous) objects or sensitive electronics into close proximity.

---
## Introduction

The Spherical-Actuator-Magnet Manipulator (SAMM) is a custom end-effector designed to act as a singularity-free 3-DOF spherical-wrist manipulator controlling the orientation of a strong permanent magnet. It consists of a spherical permanent magnet surrounded by three mutually-orthogonal omni wheels and is capable of controlling the magnet dipole direction or continuously rotating the magnet dipole about arbitrary axes.

The SAMM was designed by Sam Wright (yes, he named it after himself) and its theoretical design is presented in the associated IEEE Transactions on Robotics journal publication titled [*The Spherical-Actuator-Magnet Manipulator: A Permanent-Magnet Robotic End-Effector*][tro-paper]. This wiki page contains hardware specifications and implementation details of the SAMM meant to enable its use by members of the lab. The software implementation for controlling the SAMM from a host computer has been implemented in the [Robotics Framework][rob] (see details in the *Software Control from a Host Computer Using the Robotics Framework* section below).


---
## Hardware Specifications and Implementation Details

The implementation of the SAMM in our lab contains a 50.8-mm-diameter (2-inch-diameter), Grade-N42, spherical permanent magnet with a dipole strength of 66.03 A m<sup>2</sup>. Each omni wheel has a diameter of 57.8 mm and the motors are Maxon RE-max 29 motors each with a gear box with a 24:1 gear ratio. The SAMM can rotate its internal magnet with a maximum angular speed of 3 Hz.

The SAMM base coordinate frame and the number assignments of the wheel-motor combinations are shown in the image below. The base frame origin is located at the center of the internal magnet.

> :information_source: The motor and wheel number assignments here in this implementation do not match those used in the TRO paper. In that paper, motor/wheel 1 is assigned the number 3 and motor/wheel 3 is assigned 1. However, the SAMM base coordinate frame is the same as that used in the TRO paper.

![](images/SAMM_frame_diagram.png)

The center of the mounting-hole pattern at the top of the SAMM is located 148 mm from the SAMM base frame in the +z direction (i.e. the center of the pattern expressed in the SAMM base frame is [0, 0, 148 mm]). This mounting-hole pattern is designed for mounting the SAMM directly on the [Yaskawa Motoman MH5 6-DOF Robot Arm](Yaskawa_Motoman_MH5_Robot_arm.md) tool flange, however, the pattern is standard and the SAMM may fit on other commercially available robot arms. When using the software implementation supplied by the [Robotics Framework][rob], the SAMM must be mounted to the MH5 robot as indicated in the *Software Control from a Host Computer Using the Robotics Framework* section below.

The three motors of the SAMM are each driven by an [ESCON 36/2 DC servo controller][maxon-doc] from Maxon. These servo controllers are configured to perform closed-loop speed control of the motors and receive speed commands via digital and analog signals from a host computer with a DAQ. The ESCON controllers are configured through their USB interface using a Windows-only application called ESCON Studio which can be installed through a software bundle called ESCON Setup available on the [Maxon website][escon-web] (the bundle includes firmware for the controller and documentation). The configuration of the controllers is provided in the following table.

| Servo Controller Parameter          | Value/Function                              | Details |
|-                                    |-                                            |-        |
| Motor Speed Constant                | 201.0 rpm/V                                 |         |
| Motor Thermal Time Constant Winding | 15.9 sec                                    |         |
| Max. Permissible Speed              | 3840.0 rpm                                  |         |
| Nominal Current                     | 0.57 A                                      |         | 
| Max. Output Current Limit           | 3.24 A                                      |         |
| Type of Speed Sensor                | Digital Incremental Encoder                 |         |
| Encoder Resolution                  | 512 counts/turn                             |         |
| Encoder Direction                   | Inverted                                    | When rotating clockwise, the rising edge of Ch A leads the rising edge of Ch B by 90 degrees. |
| Mode of operation                   | Speed Controller (Closed Loop)              | Uses Inner Current Control Loop |
| Controller Gain                     | Motor 1 = 210, Motor 2 = 399, Motor 3 = 180 |         |
| Digital Input 1                     | Enable, Active Low                          |         |
| Digital Input 2                     | Direction, Active Low                       | An active direction input results in counter-clockwise rotation of the motor. |
| Analog Input 1                      | Speed Input Reference                       | 0.0 V maps to 0.0 rpm, 10.0 V maps to 3840.0 rpm |
| Analog Output 1                     | Actual Current Averaged                     | 0.0 A produces 0.0 V, 1.0 A produces 4.0 V, -1.0 A produces -4.0 V. **Mappings have not been confirmed.**        |
| Analog Output 2                     | Actual Speed Averaged                       | 0.0 rpm produces 0.0 V, 3840.0 rpm produces 4.0 V, -3840.0 rpm produces -4.0 V. **Mappings have not been confirmed.**        |

The meaning of the LED on each servo controller is as follows:

| LED Signal            | Meaning |
|-                      |-        |
| Blinking Green        | Controller is disabled (i.e. Enable input is inactive) |
| Solid Green           | Controller is enabled (i.e. Enable input is active) |
| Solid or blinking red | An error has occurred |

A [Sensoray s626 DAQ card][s626] is used to produce the digital and analog signals necessary to drive the ESCON 36/2 servo controllers. The DAQ card is also used to sense the analog feedback signals generated by the servo controllers and the Hall-effect sensors of the SAMM. Note that any DAQ capable of the requisite analog and digital I/O can be used, but a new software implementation would need to be developed based on the one provided by the [Robotics Framework][rob]. The logical and physical pin connections are given in the table below. Note that the sense inputs (J1 pins 41, 43, 45, and 47) for the DAC pins (J1 pins 42, 44, 46, and 48) on the s626 have been disabled via jumpers inserted into J6 through J9 on the s626 PCI card itself. Thus these sense pins become alternate physical pins mapped to the same logical DAC pins (e.g. J1 pins 41 and 42 are both connected to logical DAC0).

| Logical s626 Pin (Physical Pin) | Logical Controller Pin (Physical Pin) or Hall-Effect Sensor |
|-                                |-                                                            |
| DIO0 (J2 Pin 47)                | Digital Input 2 (J5 Pin 2) for Motor 1                      |
| DIO1 (J2 Pin 45)                | Digital Input 1 (J5 Pin 1) for Motor 1                      |
| DIO2 (J2 Pin 43)                | Digital Input 2 (J5 Pin 2) for Motor 2                      |
| DIO3 (J2 Pin 41)                | Digital Input 1 (J5 Pin 1) for Motor 2                      |
| DIO4 (J2 Pin 39)                | Digital Input 2 (J5 Pin 2) for Motor 3                      |
| DIO5 (J2 Pin 37)                | Digital Input 1 (J5 Pin 1) for Motor 3                      |
| Ground (J2 Pin 2)               | GND (J5 Pin 5) for Motor 1                                  |
| Ground (J2 Pin 4)               | GND (J5 Pin 5) for Motor 2                                  |
| Ground (J2 Pin 6)               | GND (J5 Pin 5) for Motor 3                                  |
| Sense1/DAC0 (J1 Pin 41)         | Analog Input 1, positive signal (J6 Pin 1) for Motor 1      |
| Sense2/DAC1 (J1 Pin 43)         | Analog Input 1, positive signal (J6 Pin 1) for Motor 2      |
| Sense3/DAC2 (J1 Pin 45)         | Analog Input 1, positive signal (J6 Pin 1) for Motor 3      |
| +AD0 (J1 Pin 4)                 | Signal (Hall-effect sensor zA)                              |
| +AD1 (J1 Pin 6)                 | Signal (Hall-effect sensor ZB)                              |
| +AD2 (J1 Pin 8)                 | Signal (Hall-effect sensor xA)                              |
| +AD3 (J1 Pin 10)                | Signal (Hall-effect sensor xB)                              |
| +AD4 (J1 Pin 12)                | Signal (Hall-effect sensor yA)                              |
| +AD5 (J1 Pin 14)                | Signal (Hall-effect sensor yB)                              |
| +AD6 (J1 Pin 16)                | Analog Output 2 (J6 Pin 6) for Motor 1                      |
| +AD7 (J1 Pin 18)                | Analog Output 2 (J6 Pin 6) for Motor 2                      |
| +AD8 (J1 Pin 22)                | Analog Output 2 (J6 Pin 6) for Motor 3                      |
| +AD9 (J1 Pin 24)                | Analog Output 1 (J6 Pin 5) for Motor 1                      |
| +AD10 (J1 Pin 26)               | Analog Output 1 (J6 Pin 5) for Motor 2                      |
| +AD11 (J1 Pin 28)               | Analog Output 1 (J6 Pin 5) for Motor 3                      |
| -AD0 (J1 Pin 3)                 | GND (Hall-effect sensor zA)                                 |
| -AD1 (J1 Pin 5)                 | GND (Hall-effect sensor zB)                                 |
| -AD2 (J1 Pin 7)                 | GND (Hall-effect sensor xA)                                 |
| -AD3 (J1 Pin 9)                 | GND (Hall-effect sensor xB)                                 |
| -AD4 (J1 Pin 11)                | GND (Hall-effect sensor yA)                                 |
| -AD5 (J1 Pin 13)                | GND (Hall-effect sensor yB)                                 |
| -AD6 (J1 Pin 15)                | GND (J6 Pin 7) for Motor 1                                  |
| -AD7 (J1 Pin 17)                | GND (J6 Pin 7) for Motor 2                                  |
| -AD8 (J1 Pin 21)                | GND (J6 Pin 7) for Motor 3                                  |
| -AD9 (J1 Pin 23)                | GND (J6 Pin 7) for Motor 1                                  |
| -AD10 (J1 Pin 25)               | GND (J6 Pin 7) for Motor 2                                  |
| -AD11 (J1 Pin 27)               | GND (J6 Pin 7) for Motor 3                                  |

In addition to the connections in the table above, all of the different grounds are connected to each other. The encoder for each motor is connected to J4 of its respective servo controller. The motor leads for each motor are connected properly to J2A of their respective servo controller. Motor power for each controller is supplied by a power supply set to 22 V with 0.5 A current limit connected to J1. Power for the Hall-effect sensors is supplied by the same power supply using its fixed 5 V channel.


---
## Software Control from a Host Computer Using the Robotics Framework

The [Robotics Framework][rob] contains an optional component providing a software implementation that enables control of the SAMM from a host computer. This implementation allows control over the dipole direction or the dipole angular velocity (where the dipole rotates such that it is always perpendicular to the angular velocity). The implementation is optional because it has library dependencies for using the [s626 DAQ][s626]. The implementation is a C++ class called `SAMM` and is found under the `Robots/SAMM` directory of the framework. Another class called `MH5SAMMDipoleRobot` is meant to enable control of the SAMM and MH5 robot arm through a single interface that abstracts away the robots to control the permanent magnet position and orientation directly. Documentation on the `SAMM` and `MH5SAMMDipoleRobot` classes can be obtained by building the framework documentation. Please see the [Robotics Framework][rob] repository for details on its usage, enabling optional components, and building its documentation. Also see the [s626-daq][s626] repository for details on setting up and using the s626 DAQ card.

The `MH5SAMMDipoleRobot` implementation expects the SAMM to be mounted to the MH5 robot arm as depicted in the zero-angle diagram below.

![](images/MH5_zero_angle_with_SAMM.png)

The `SAMM` and `MH5SAMMDipoleRobot` classes are integrated rather thoroughly with the rest of the Robotics Framework. Therefore, it is not recommended to attempt to use these classes separately from the framework (e.g. to copy the source files and use them directly in your own project). Please use the framework as it was intended if you wish to use the `SAMM` and/or `MH5SAMMDipoleRobot` classes.

A repository called `SAMM-interface` also exists containing older versions of this implementation. **This repository is DEPRECATED and should not be used!** It is only maintained on our lab Git workspace for historical reference should the need arise.

**Class Implementation Notes**

The implementation of the `SAMM` class follows the algorithms outlined in the TRO paper. Specifically, an extended Kalman filter is implemented to estimate the state of the permanent magnet and the control algorithm outputs desired velocities of the motors (which are realized with the ESCON servo controllers).


[tro-paper]: https://mmrobotics.mech.utah.edu/wp-content/uploads/2023/01/Wright_TRO17.pdf
[rob]: https://bitbucket.org/mmrobotics/roboticsframework/src/master/
[maxon-doc]: https://bitbucket.org/mmrobotics/docs-motors-and-inductive-loads/src/master/
[escon-web]: https://www.maxongroup.com/maxon/view/content/escon-detailsite
[s626]: https://bitbucket.org/mmrobotics/s626-daq/src/master/