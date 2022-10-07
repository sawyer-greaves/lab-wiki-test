[Home](../Home)
# JIMEE - Junk Immobilizing Magnetic End Effector

**Contents**

[TOC]

---
## Safety Items

>:exclamation: **Serious risk of bodily injury or harm to senstive electronics!** The JIMEE contains a **strong permanent magnet**. Always maintain caution when working near the JIMEE and avoid bringing magnetically permeable (e.g. ferrous) objects or sensitive electronics into close proximity.

---
## Setup

---
## Electronics

The JIMEE is part of a larger robotic system that contains many electronic parts. Below is some useful information about the electronic ecosystem in which JIMEE lives. 

### Servo Drive
JIMEE has an Advanced Motion Controls `dpralte-020b080` servo drive. The servo drive performs PI velocity control for the motor that spins the magnet. 

To perform velocity control, the servo drive accepts a signal from the motor encoder. The ribbon cable that connects the motor encoder to the servo drive has the following configuration:

|Encoder Pin | Wire Color | Signal | AMC Feedback Port Breakout Pin |
|-   |-       |-        |-   |
| 1  | Black  | GND     | 12 |
| 2  | White  | PWR     | 13 |
| 4  | Purple | Standby | 13 |
| 6  | Green  | Ch A    | 6  | 
| 8  | Orange | Ch B    | 4  |
| 10 | Brown  | Ch Z    | 8  |

To accept a reference command from the D/A card on the PC, the servo drive has an I/O port with the following configuration:

| Signal | Wire Color | AMC I/O Port Pin | Sensoray Port, Pin |
|-                              |-      |-   |-       |
|GND                            | Black | 2  | J3, 48 |
|Analog Output (180 rpm/V)      | TBD   | 7  | TBD    |
|Analog Input + (Vref)          | Red   | 4  | J1, 42 |
|Analog Input - (GND)           | Black | 5  | J1, 40 |
|Digital Input (Low to disable) | Red   | 11 | J3, 47 |


### Power Supply and Emergency-Stop-Actuated Relay
JIMEE's motor gets its power from a MEAN WELL USA `UHP-1000-36` 36V power supply. More information about the power supply can be found [here](https://www.digikey.com/en/products/detail/mean-well-usa-inc/UHP-1000-36/10056330).

Interrupting the flow of current between the power supply and the servo drive is a relay that is switched by the emergency stop on the accompanying [UR5e](UR5e.md). As such, **the UR5e must be turned on in order for power to be  delivered from the power supply to the servo drive.** I.e. if you want to spin the magnet, you have to turn on the UR5e. Once the UR5e is turned on, the relay will close the contacts and allow power to be delivered to the servo drive. If the emergency stop on the UR5e's teach pendant is pressed, the relay will lose power and the contacts will open, ceasing the delivery of power to the servo drive. 

The following table indicates the configuration of the relay and should be consulted before any modifications are made:

|Terminal Pair  | Configuration  | Use |
|-              |-               |-                       |
|(13, 14)       |Normally Open   | Servo Drive Power      |
|(23, 24)       |Normally Open   | Servo Drive GND        |
|(33/31, 34/32) |Normally Closed | Unused                 |
|(43/41, 44/42) |Normally Closed | Red Status Light Power |
|(A1, A2)       |Actuator        | Actuator               |

The terminal pair (A1, A2) is connected to the configurable output pair (0V, CO0) on the UR5e.

### Status Light
A status light is affixed to the robot base on which JIMEE stands. It consists of 3 colors whose semantic meanings are as follows:

|Status Light Color | Meaning                                |
|-                  |-                                       |
|Green              | Robot is on                            | 
|Flashing Amber     | Program is running  on robot           |
|Red                | System emergency stop has been pressed |

When the emergency stop has been pressed, everything on the robot is disabled, including JIMEE. Thus, if the red light is on, it is safe to be around the robot. 

The status light is connected to the UR5e Control Box via an aviation plug and a 6-conductor wire with the following configuration:

|Aviation Plug Terminal | Wire Color | Signal     | UR5e Pin |
|-                      |-           |-           |-         |
|8                      |Black       |GND         |0V        |   
|1                      |Brown       |Amber Light |DO1       |   
|2                      |Blue        |Green Light |DO0       |   
|3                      |Red         |Red Light   |Power 24V |   
|4                      |White       |Relay A1    |CO0       |   
|5                      |Green       |Relay A2    |0V        |   


---
## Mechatronics

### Motor
JIMEE has a Portescap `35GLT2R82-234E.1` brushed DC motor, with an `E9` Encoder that has 500 lines per revolution