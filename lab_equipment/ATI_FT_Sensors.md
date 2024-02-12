[Home](../Home)
# ATI Force/Torque Sensors

---

## Introduction

Our lab has several 6 degree-of-freedom (6 DOF) force/torque transducers produced by ATI Industrial Automation. This page concerns the information related to these sensors and covers their use within our lab.

---

## ATI Nano17 Titanium

### Overview

>:warning: **Each ATI Nano17 Titanium sensor costs in excess of $10,000, and each sensor is very easily damaged. Accordingly, it is compulsory to thoroughly read this entire wiki page prior to using one of these sensors.**

At present, we have three [ATI Nano17 Titanium](https://www.ati-ia.com/products/ft/ft_models.aspx?id=Nano17+Titanium) force/torque sensors with the `SI-8-0.05` calibration. 'Titanium' means the sensors are made from titanium, so as to be minimally affected by magnetic fields. The calibration corresponds to both the sensitivity of the sensor and the maximum loads it can handle. The `SI-8-0.05` calibration is the most sensitive and has the lowest maximum load limits. The limits can be read from the above link. Be very careful when operating the sensor. 

Each ATI Nano17 Titanium sensor consists of three parts: the transducer, the amplifier, and the amplifier cable. The collection of these three parts is herein referred to as "the sensor." 

It is important to note that the sensor is used by reading the amplifier's output voltages. To date this has been performed by a Data Acquisition (DAQ) card that has been installed in a computer. This is probably what you will want to do. For this purpose, we have purchased three National Instruments DAQ cards. These are complex devices, and the sensor is, in principle, agnostic to the DAQ card that reads its voltage output, so the specifics of procedures related to the DAQ card are not covered in this page of the wiki. When the term "sensor" is used herein, it is understood that the equipment referred to by this term does not include the DAQ card.

### Precautions for use

There are several safety precautions for using the ATI Nano17 Titanium sensor, listed here:
* **Handle with care:** As mentioned above, each sensor costs in excess of $10,000. As a result you must be extraordinarly cautious when using the sensor. One small mistake may end up being a third of your (student) salary.
* **Serialization:** Each sensor package (transducer, amplifier) has a serial number. You must pay attention to this, as the calibration of each sensor refers to the serialized package. **Do not connect transducers and amplifiers with different serial numbers.** The serial number follows the form `FTXXXXX` where `X` is a single digit integer, _e.g._ `FT42918`. All software that turns instantaneous sensor voltages into a 6 DOF wrench relies on a `.cal` calibration file which informs the software of the correct scaling, and this calibration file is specific to each transducer/amplifier pair.
* **Screw insertion depth:** The most common way in which the sensors are damaged is by using mounting screws that intrude too far into the sensor body. The maximum screw insertion depth is listed on the sensor's [technical drawing](https://www.ati-ia.com/app_content/Documents/9230-05-1336.auto.pdf). For clarity's sake, this depth is **3.5mm**. _The prudent engineer applies a factor of safety to all of their calculations, especially those which carry an associated risk._
* **Tool transform/moment arm:** Another common way to damage these sensors is to over-torque them, _i.e._ to subject them to a torque that is significantly beyond their saturation limit. This often happens when the sensor is subject to a force applied through a moment arm, which creates a torque on the sensor. Even a small moment arm can seriously amplify the torque that the sensor is subjected to, so be cautious of this fact and plan for it when designing the apparatuses that surround the sensor in your experiment. 

>:warning: **Remember - one small mistake when using these sensors can cost our lab $10,000. Think, be intentional, and make every move a careful one.**

--- 

## Calibration Files

The calibration files for the sensors that we own are stored in a [repository](https://bitbucket.org/mmrobotics/calib-ati-ft-sensors/src/main/) in the COTS Hardware section of the Lab's bitbucket.

If for some reason these files are lost or unavailable, the calibration files for each sensor can be found [here](https://www.ati-ia.com/Library/Software/FTDigitaldownload/getcalfiles.aspx). You simply need the sensor's serial number.


---

## Software Implementations

### ROS2 Node/NI-DAQmx - Recommended

Our lab has developed a stand-alone ROS2 node that reads the gauge voltages output by a sensor's amplifier, converts them to a 6 DOF wrench based on that sensor's `.cal` file, and publishes them on a ROS2 topic, provided the computer that runs this node has NI-DAQmx installed and contains an NI-DAQmx compatible DAQ card. Source code and documentation are found [here][ros2-node]. 

### ATIConvertFT

`ATIConvertFT` is a C library that uses a sensor's `.cal` file to convert gauge voltages output by the sensor's amplifier into a 6 DOF wrench. Source code and documentation are found [here][docs]. This library does not contain any code for reading the sensor's gauge voltages.

[docs]: https://bitbucket.org/mmrobotics/ati_ft_sensor/src/master/
[ros2-node]: https://bitbucket.org/mmrobotics/ati_ft_sensor_nidaqmx_ros2_node/src/master/