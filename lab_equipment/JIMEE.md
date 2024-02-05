[Home](../Home)
# JIMEE - Junk Immobilizing Magnetic End Effector

**Contents**

[TOC]

>:exclamation: **Serious risk of bodily injury or harm to sensitive electronics!** The JIMEE contains a **strong permanent magnet**. Always maintain caution when working near the JIMEE and avoid bringing magnetically permeable (e.g. ferrous) objects or sensitive electronics into close proximity.

---
## Introduction

The Junk Immobilizing Magnetic End Effector (JIMEE) is a custom robot end-effector designed to spin a strong diametrically magnetized cylindrical permanent magnet at high speeds. It was designed for applying a magnetic wrench to non-magnetic conductive materials with applications in detumbling debris in orbit around the earth, but could certainly be used in other applications.

This wiki page contains hardware specifications and implementation details of the JIMEE to inform lab members who intend to use it.

---
## Software Control from a Host Computer

A software driver for controlling the JIMEE from a host computer has been implemented as a ROS 2 C++ node. The node (and ROS 2 package) is found in the [jimee_ros2_driver][driver_repo] repository.

---
## Hardware Specifications and Implementation Details

This section includes some important information about the parts in a JIMEE, but is not an exhaustive description of how to construct a JIMEE. Such a description is listed below this section.

### Magnet

The implementation of the JIMEE in our lab contains a 2-inch-diameter (50.8-mm-diameter), 2-inch-thick, Grade-N42, cylindrical permanent magnet with a 1/4-inch-diameter hole. (K&J Magnetics product [RY04Y0DIA][perm_mag]). The dipole strength is currently unknown. The magnet is diametrically magnetized such that when it is rotated within the JIMEE, the dipole moment is always orthogonal to the magnet rotation axis.

### Drive Motor

The drive motor is a Portescap 35GLT2R82-234E.1 brushed DC motor, with a Portescap E9 Encoder that has 500 lines per revolution. It is a 48 Volt motor with a no-load speed of 7490 rpm, a stall torque of 1300 mNm, and a torque constant of 61 mNm/A. The power supply (see below) is set to supply 43 Volts to the motor.

### Servo Drive
The motor on the JIMEE is driven by an Advanced Motion Controls (AMC) dpralte-020b080 servo drive. The servo drive is configured to perform P (proportional only) velocity control. To do this, the servo drive receives feedback from the encoder of the JIMEE's motor. The ribbon cable that connects the motor encoder to the servo drive has the following configuration:

|Encoder Pin | Wire Color (Encoder Side) | Signal | AMC Servo Drive Feedback Port Breakout Pin |
|-   |-       |-        |-   |
| 1  | Black  | GND     | 12 |
| 2  | White  | PWR     | 13 |
| 4  | Purple | Standby | 13 |
| 6  | Green  | Ch A    | 6  | 
| 8  | Orange | Ch B    | 4  |

The drive accepts reference command signals from a host PC by connecting digital and analog I/O pins from a DAQ card installed in the PC to the I/O port on the servo drive. If you are using the [JIMEE ROS 2 driver][driver_repo], then this DAQ card will be a Sensoray 826 (s826) card. The following table shows the connections necessary in the context of using an s826 card:

| AMC Servo Drive I/O Signal | AMC Servo Drive I/O Port Pin | Wire Color | s826 Port, Pin | Notes |
|-                              |-      |-   |-       |-  |
|GND                            | 2  | Black  | J3, 48 |  |
|Analog Output (180 rpm/V)      | 7   | TBD  | TBD    | This signal is currently not used, but could be used to obtain true velocity of the JIMEE's magnet as measured by the servo drive. |
|Analog Input + (Vref)          | 4   | Red  | J1, 42 | Used to specify the desired velocity. Desired velocity is interpreted using 540 rpm/Volt. Input range is +/- 10 Volts. Pin for the s826 is configurable by the JIMEE ROS 2 driver. |
|Analog Input - (GND)           | 5 | Black  | J1, 40 |  |
|Digital Input (Low to disable) | 11   | Red | J3, 47 | Used to enable the velocity controller and cause the magnet to spin. Pin for the s826 is configurable by the JIMEE ROS 2 driver. |

The drive is configured such that the analog input uses 540 rpm/Volt to interpret the signal as a commanded velocity. The +/-10 Volt range means that the maximum commandable speed of the JIMEE motor is 5400 rpm. The JIMEE has a gear ratio from magnet output to motor input of 1.5 (meaning the motor spins 1.5 times faster than the magnet) resulting in a maximum magnet speed of 3600 rpm (60 Hz).

### Power Supply and Emergency-Stop-Activated Relay

The JIMEE's motor gets power from a MEAN WELL USA UHP-1000-36 36V power supply set to supply 43 Volts to the motor. More information about the power supply can be found [here](https://www.digikey.com/en/products/detail/mean-well-usa-inc/UHP-1000-36/10056330).

Interrupting the flow of current between the power supply and the servo drive is a relay that is activated by the emergency stop on the [UR5e Robot Arm](UR5e.md). As such, **the UR5e must be turned on in order for power to be delivered from the power supply to the servo drive.** Once the UR5e is turned on, the relay will close the contacts and allow power to be delivered to the servo drive. If the emergency stop on the UR5e's teach pendant is pressed, the relay will lose power and the contacts will open, disconnecting power from the servo drive.

The following table indicates the configuration of the relay:

|Terminal Pair   | Configuration   | Use                             |
|-               |-                |-                                |
| (A1, A2)       | Actuator        | Activates/Deactivates the relay |
| (43/41, 44/42) | Normally Closed | UR5e Red LED Status Light Power |
| (33/31, 34/32) | Normally Closed | Unused                          |
| (23, 24)       | Normally Open   | Servo Drive GND                 |
| (13, 14)       | Normally Open   | Servo Drive Power               |

The terminal pair (A1, A2) is connected to the configurable output pair (0V, CO0) inside the UR5e e-Series control box.

### UR5e Status Light

A status light is attached to the structure to which the UR5e is affixed. It consists of 3 colors whose semantic meanings are as follows:

| Status Light Color | Meaning                                |
|-                   |-                                       |
| Solid Green        | Robot power is on                      |
| Flashing Amber     | Robot is running a program and may move. **Use caution when standing or walking near the robot.** |
| Solid Red          | System emergency stop has been pressed |

When the emergency stop has been pressed, everything on the robot is disabled, including the JIMEE. Thus, if the red or green light is on, it is safe to be around the robot.

[driver_repo]: https://bitbucket.org/mmrobotics/jimee_ros2_driver/src/master/
[perm_mag]: https://www.kjmagnetics.com/proddetail.asp?prod=RY04Y0DIA

## JIMEE Construction Procedure

This document explains all details concerning the construction of a JIMEE end effector. You will need access to the `production_JIMEE` directory on box. Ask Travis Allen for help with this. 

## What's in a JIMEE
"Part Number" in the first column refers to the part numbers in [production_JIMEE_exploded_view.pdf](images/production_JIMEE_exploded_view.pdf). Note that **the following list does not contain all of the parts in a JIMEE!** There are two subassemblies listed below that allowed for better organization and clearer assembly instructions than if they were included in this list and in production_JIMEE_exploded_view.pdf or production_JIMEE.sldasm. Additionally, note that this construction guide does NOT include instructions for constructing the JIMEE's hall effect sensor array. 

| Part Number | Name | Supplier| Supplier Part Number | Quantity | CAD File Name| Related Information |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | JIMEE Base | Custom | None | 1 | base.sldprt | Machined from 3/4" Delrin |
| 2 | 0.125" Brass Dowel Pin | McMaster | 97325A135 | 10 | 97325A135.sldprt | None | 
| 3 | Drive-Side Side Plate| Custom | None | 1 | side_plate_DS.sldprt | Laser cut from 1/4" acrylic | 
| 4 | Non-Drive-Side Side Plate | Custom | None | 1 | side_plate_NDS.sldprt | Laser cut from 1/4" acrylic |
| 5 | Front | Custom | None | 1 | front.sldprt | Machined from 1/2" Delrin |
| 6 | Motor Mount | Custom | None | 1 | motor_mount.sldprt | Machined from 1/2" Delrin |
| 7 | Motor Shaft Bearing | McMaster | 60355K283 | 2 | 60355K283.sldprt | None | 
| 8 | Magnet Shaft Bearing | McMaster | 60355K291 | 2 | 60355K601.sldprt | Note part number and filename are different |
| 9 | Motor Shaft Coupler | McMaster | 8011N126 | 1 | 8011N126.sldprt | None |
| 10 | Drive-Side Magnet Shaft | Custom | None | 1 | shaft_DS.sldprt | Machined from 6061 aluminum |
| 11 | Non-Drive-Side Magnet Shaft | Custom | None | 1 | shaft_NDS.sldprt | Machined from 6061 aluminum |
| 12 | Magnet | K & J Magnetics | RY04Y0DIA | 1 | RY04Y0DIA.sldprt | None |
| 13 | Motor Bracket | Custom | None | 1 | motor_bracket.sldprt | Machined from aluminum angle |
| 14 | Motor | Portescap | 35GLT2R82-234E.1 | 1 | 35GLT2R82-234E.sldprt | With Portescap E9 encoder |
| 15 | Motor Shaft | Custom | None | 1 | motor_shaft.sldprt | Machined from 6061 aluminum |
| 16 | Magnet Cover | Custom | None | 1 | magnet_cover.sldprt | FDM 3D printed from PETG |
| 17 | 1/4"-20 x 1" Brass BHCS | McMaster | 97715A267 | 12 | 97715A267.sldprt | None |
| 18 | One Bolt Belt Support Spacer | Custom | None | 1 | belt_support_spacer_one_bolt.sldprt | FDM 3D printed from PETG |
| 19 | Two Bolt Belt Support Spacer | Custom | None | 1 | belt_support_spacer_two_bolt.sldprt | FDM 3D printed from PETG |
| 20 | 1/4"-20 x 1.5" Bronze Carriage Bolt | McMaster | 94050A210 | 1 | 94050A210.sldprt | None |
| 21 | 24t Timing Belt Pulley | McMaster | 1277N764 | 1 | 1277N764.sldprt | None |
| 22 | 16t Timing Belt Pulley | McMaster | 1277N747 | 1 | 1277N747.sldprt | None |
| 23 | 16" Kevlar Timing Belt | McMaster | 1679K29 | 1 | 1679K29.sldprt | None |
| 24 | Belt Bearing Support | Custom | None | 1 | belt_bearing_support.sldprt | None |
| 25 | 1/4"-20 x 1 3/4" Brass BHCS | McMaster | 97715A527 | 2 | 97715A527.sldprt | None |
| 26 | Belt Cover | Custom | None | 1 | belt_cover.sldprt | None |
| 27 | 1/4"-20 Thin Bronze Hex Nut | McMaster | 91952A110 | 3 | 91952A110.sldprt | None |
| 28 | 10-24 x 1" Stainless Carriage Bolt | McMaster | 93180A120 | 2 | 93180A120.sldprt | None |
| 29 | #10 Brass Washer | McMaster | 92916A345 | 4 | 92916A345.sldprt | None |
| 30 | 10-24 Brass Nylok Hex Nut | McMaster | 92092A025 | 4 | 92092A025.sldprt | None |
| 31 | 10-24 Brass Threaded Rod | McMaster | 98812A011 | 1 | 98812A011.sldprt | Cut to length |
| 32 | M3x0.5mm x 6mm SHCS | McMaster | 91290A111 | 4 | 91290A111.sldprt | None |


