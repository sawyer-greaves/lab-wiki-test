# Utah Telerobotics Lab Wiki

Welcome to the Utah Telerobotics Lab Wiki!

The Utah Telerobotics Lab Wiki is part of a Git repository on Bitbucket dedicated for the purpose of hosting the lab wiki. Every Bitbucket repository comes with a wiki and the `lab-wiki` repository is simply an empty repository in which we are utilizing only the wiki feature to host this wiki.

This Home page acts as the wiki's table of contents and every wiki page should have a `Home` link at the top to return here. As an additional navigation option, Bitbucket displays a breadcrumb trail above each page. Clicking on an item in the trail will allow you to browse the directory structure of the wiki and open desired wiki pages directly.

If you're a new student, please read and follow the onboarding page:

- [Onboarding](Onboarding.md)

Please see [How to Edit this Wiki](necessary_skills/Editing_the_Wiki.md) for instructions on contributing to the wiki. The [Bitbucket documentation](https://confluence.atlassian.com/x/FA4zDQ) also has more information about using a wiki. The [Lab Wiki TODO List](Todo.md) contains a list of to-do items for the wiki itself. **Please keep this list up to date.**

---
## Lab Policies, Standards, and Procedures

- [Lab Computer Management Policies](Lab_Computer_Management_Policies.md)
- [Git Standards](Git_Standards.md)
- [Lab Network Drive (Group Drive)](Lab_Network_Drive.md)

---
## Necessary Skills

### All Lab Members

- [How to Edit this Wiki](necessary_skills/Editing_the_Wiki.md)
- [Markdown Syntax](necessary_skills/Markdown.md)
- [Git](necessary_skills/Git.md)
    - [Git Cheatsheet](necessary_skills/Atlassian_Git_Cheatsheet.pdf)
    - [Pro Git Reference Textbook](necessary_skills/Pro_Git.pdf)
    - [Using Git with the SSH Protocol](necessary_skills/Using_Git_with_SSH.md)

### Most Lab Members

#### Computer Science Skills
- [Linux](necessary_skills/Linux.md)
    - [Linux for Beginners Book](necessary_skills/Linux_for_Beginners.pdf)
    - [Linux Command Line Cheat Sheet](necessary_skills/Linux_Command_Line_Cheat_Sheet.pdf)
    - [Linux Administration Book](necessary_skills/Linux_Administration.pdf)
    - [Computer Science from the Bottom Up Book](necessary_skills/Computer_Science_from_the_Bottom_Up.pdf)
- [C/C++ Programming Language](necessary_skills/C_and_Cpp.md)
- [CMake](necessary_skills/CMake.md)
    - [Professional CMake Reference Textbook](necessary_skills/Professional_CMake_11th_Edition.pdf)
- [Python](necessary_skills/Python.md)
- [Qt Application Framework and Qt Creator](necessary_skills/Qt.md)
- [Doxygen](necessary_skills/Doxygen.md)
- [ROS](necessary_skills/ROS.md)

#### Magnetics Skills
- [Working with Strong Magnets](necessary_skills/Working_with_Strong_Magnets.md)

---
## Useful Resources

- [Visual Studio Code](useful_resources/Visual_Studio_Code.md)
- [Eigen Linear Algebra Library for C++](useful_resources/Eigen_Library.md)
- [OpenCV Computer Vision Library](useful_resources/OpenCV.md)


---
## Lab Custom Common Software Libraries

- [libmatlab](https://bitbucket.org/utahtelerobotics/libmatlab/src/master/)
    - A collection of libraries of MATLAB functions useful for robotics and magnetics applications.
- [RoboticsFramework](https://bitbucket.org/utahtelerobotics/roboticsframework/src/master/) **(Linux Only**)
    - A ROS-like, single-process robotics framework for [C++](necessary_skills/C_and_Cpp.md) based on top of the [Qt Application Framework](necessary_skills/Qt.md) and Qt's signal-slot features
    - Can be used in conjunction with [ROS](necessary_skills/ROS.md) within a ROS node
    - Components can be selectively built and installed so you can use only what is needed and avoid installing unnecessary dependencies
    - Contains the following functionality:
        - The Robotics Toolbox, a collection of types and functions for linear algebra and mathematical operations in robotics
        - A collection of utility classes for timing, threading, optimization, signal processing and filtering, and magnetics
        - ROS-like message passing between objects (in the same process), "real-time" data visualization, and data recording
        - Robot and hardware implementations (Yaskawa Motoman robot arm, SAMM, Space Explorer 3D Mouse)
        - A framework for writing and managing control loops and controllers
        - Computer vision workflows built on top of [OpenCV](useful_resources/OpenCV.md) including a substantially featured computer vision GUI, camera calibration workflows, support for ROI's and ROI servoing, and camera drivers (Flea3)

---
## Lab Equipment

- [Universal Robots UR5e Robot Arm](lab_equipment/UR5e.md)
- [Sensoray 826 (s826) PCIe Data Acquisition Card](https://bitbucket.org/utahtelerobotics/s826-daq/src/master/)
- [Sensoray 626 (s626) PCI Data Acquisition Card](https://bitbucket.org/utahtelerobotics/s626-daq/src/master/) (**This card is EOL, prefer using the s826 above**)
- [JIMEE - Junk Immobilizng Magnetic End Effector](lab_equipment/JIMEE.md)
- [Teensy-based Magnetometer](https://bitbucket.org/utahtelerobotics/teensy-magnetometer/src/main/)

---
## Logistical

- [Lab Wiki TODO List](Todo.md)
