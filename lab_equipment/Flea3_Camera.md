[Home](../Home)
# Flea 3 Camera

**Contents**

[TOC]

---
## Introduction
The Flea 3 camera is a machine vision camera that connects to a computer with USB 3.0, Gigabit Ethernet, or a Firewire interface. The camera was originally designed by a company called Point Grey Research which was acquired by Teledyne FLIR (formerly FLIR Systems). In this lab we have the following product variations:

- FL3-U3-13S2C-CS (1.3 Megapixel Color CMOS camera with USB 3.0 interface) **Discontinued**

The following links can be used to obtain information about the USB 3 variant of the camera. Note that if the product details page or the product support page links become invalid, it may still be possible to access the information by going to FLIR's website and searching "Flea 3" in the support section. The documentation link below points to our copy of documentation for the USB 3 variant. Our copy is stored in a repository on Bitbucket. It consists of specs sheets, manuals, CAD drawings and models, camera firmware, and the FlyCapture2 SDK.

- [Flea 3 USB 3 Product Details Page][product-page]
- [Flea 3 USB 3 Product Support Page][product-support]
- [Flea 3 USB 3 Documentation][docs]

When using a USB 3.0 camera, you may want to make sure to verify that the USB 3.0 slot the camera is plugged into is actually running at 3.0 speeds. Sometimes a USB Host Controller can have more physical USB 3.0 ports than it has logical USB 3.0 ports. Devices connected to a physical port when no logical USB 3.0 ports are left available, will revert to slower speeds. On Linux, the speed at which a USB port is running can be checked using the `lsusb` command.

---
## Configure USBFS Buffers

The buffers allocated for storing incoming USB messages are restricted to 16 MB on Ubuntu by default. When using USB cameras, the incoming data rates are very high and will easily overrun these buffers. Therefore it is important to increase the default buffer limit. FLIR recommends configuring USBFS to use 1000 MB of buffer memory to ensure incoming images can be buffered. An even higher limit may be required when using multiple USB cameras at the same time. Sufficiently high buffer limits will help prevent crash issues associated with buffer allocation when starting the camera.

When using Spinnaker (see below), the installation steps should automatically set the appropriate USBFS memory settings. Otherwise, increasing the buffer limit can be done with the following steps.

1.  If the `/etc/rc.local` file does NOT already exist on your system, run the following commands to create and make it executable

    ```
    sudo touch /etc/rc.local
    sudo chmod 744 /etc/rc.local
    ```

2. Open the `/etc/rc.local` file in any text editor

    ```
    sudo nano /etc/rc.local
    ```

    If this file was just created add the following to it

    ```
    #!/bin/sh -e
    echo 1000 > /sys/module/usbcore/parameters/usbfs_memory_mb
    exit 0
    ```
    If this file already existed then add the following before the `exit 0` line

    ```
    echo 1000 > /sys/module/usbcore/parameters/usbfs_memory_mb
    ```

3. Save your changes and close the file.

4. Restart the machine.

    To confirm that the memory limit has been updated, run the command

    ```
    cat /sys/module/usbcore/parameters/usbfs_memory_mb
    ```

    If this fails to set the memory limit, one can TEMPORARILY modify the USBFS memory until the next restart by running the following command

    ```
    sudo sh -c 'echo 1000 > /sys/module/usbcore/parameters/usbfs_memory_mb'
    ```

The above instructions were copied from [this FLIR application note](https://www.flir.com/support-center/iis/machine-vision/application-note/understanding-usbfs-on-linux/). This note contains additional helpful information about USBFS and USB cameras.

---
## Usage from Software

### FlyCapture2 SDK **(Discontinued)**

> :warning: **New projects that don't already use FlyCapture2 should instead use Spinnaker (see below).**

The FlyCapture2 SDK is used to write C++ or Python software that interacts with Flea 3 cameras. This SDK is no longer supported in favor of the newer Spinnaker SDK (see below), but it is currently used by the `Flea3Camera` class of the [Robotics Framework][rob]. The SDK is not supported on Ubuntu Linux after 18.04 LTS.

Compressed archives with Debian packages for Linux can be found on the FLIR website or in our [Documentation Repository][docs] and instructions for installation are included in the archives. Use the provided installation scripts as indicated in the installation instructions. Also, make sure to say "yes" if and when the installation scripts ask if you want to add a `udev` entry. The `udev` entry allows users that are members of the `flirimaging` group to interact with the cameras without root permissions. Therefore, other users on a computer with FlyCapture2 installed will need to be added to the `flirimaging` group if they intend to use a Flea 3 camera. The SDK for Windows can also be found on the FLIR website.

Since (on Linux) the FlyCapture2 SDK is a set of Debian packages, FLIR's installation scripts are simply installing each package with the `dpkg` command. This means that you will have access to all the package meta information through `dpkg`, `apt-cache`, and `apt`. For example you can list the installed FlyCapture2 packages with the following command:

      apt list --installed | grep -i flycap

You can also list the install locations of files in each of those packages with the following command:

      dpkg -L <package-name>

Listing the files in a package in this case is useful if you need to see the location of the header files and the library to link to in your software project.

The library's documentation is installed as part of the SDK and can be found though a shortcut to a PDF created in the applications menu when FlyCapture2 is installed. If you are having trouble finding the installed documentation, the command above can be used on the `flycapture-doc` package to find the install location.

### Spinnaker SDK

The Spinnaker SDK is a newer SDK and can be downloaded from the FLIR website. This SDK should be used for new projects that don't already use FlyCapture2 or for projects that need to be able to run on Ubuntu later than 18.04.

### OpenCV

It may be possible to obtain images from the camera using the `VideoCapture` class of OpenCV. However, this method would provide very limited functionality and would basically be limited to obtaining images from the camera only. This method has not been used in this lab to interact with a Flea 3 camera.

[docs]: https://bitbucket.org/mmrobotics/docs-cameras/src/master/
[product-page]: https://www.flir.com/products/flea3-usb3/?vertical=machine%20vision&segment=iis
[product-support]: https://www.flir.com/support/products/flea3-usb3/?vertical=machine+vision&segment=iis#Overview
[rob]: https://bitbucket.org/mmrobotics/roboticsframework/src/master/