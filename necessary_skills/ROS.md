[Home](../Home)
# ROS (Robot Operating System)

**The Robot Operating System (ROS) is a set of software libraries and tools for building robot applications.** Despite the name, ROS is **not** an operating system. It would be more accurate to call it a *framework* or *middleware*. It is an ecosystem of software that contains drivers and state-of-the-art algorithms as well as powerful open-source developer tools (visualizers, message-passing, package management) meant to help you write scalable, distributed robotics applications without reinventing the wheel.

---
## Prerequisites to Learn ROS

In order to learn ROS you need to have relatively strong exisiting knowledge in computer science and programming. You do not need to be an expert, but you will need to know more than you might think and you shouldn't expect to pick it up in just a few days, especially if you're coming from a mechanical engineering background. Frankly, knowing MATLAB and Arudino is a great start, but if that's all you have experience with, you will find yourself lost very quickly. To make sure you're prepared to succeed, the following is a list of things you **must** be comfortable with before you attempt to learn ROS:

 - Using a [terminal and command line tools](Linux.md)
 - Strong programming knowledge in **at least one**, but ideally both of:
    - [C++](C_and_Cpp.md) and [CMake](CMake.md)
    - [Python](Python.md)

All in all, the more you understand about programming with computers, the better off you are. So don't shy away from that computer science goodness.

---
## ROS Versions and Distributions

There are currently two major versions of ROS: **ROS 1** and **ROS 2**. Within each version, there are *distributions* which are versioned sets of ROS packages and can be thought of as minor versions or releases. These distributions have clever code names similar to the names given to [releases of Ubuntu Linux](https://wiki.ubuntu.com/Releases). Just like with Ubuntu, the first letter in the code name goes in alphabetical order with each new distribution. See below for the current list of distributions for each ROS version:

 - [**ROS 1 Distributions**](https://wiki.ros.org/Distributions)
 - [**ROS 2 Distributions**](https://docs.ros.org/en/rolling/Releases.html)

 Although ROS is becoming increasingly compatible with other operating systems and architectures (ROS 1 only targets Ubuntu and ROS 2 targets Ubuntu, MacOS, and Windows 10), it is most widely used with Ubuntu Linux. Below is a table describing which ROS distributions you should expect to use with a given Ubuntu LTS release:

 Ubuntu Release | 18.04 (Bionic)                     | 20.04 (Focal)  | 22.04 (Jammy)
 :--------------|:----------------------------------:|:--------------:|:------------:
 **ROS 1**      | Melodic                            | Noetic         | - 
 **ROS 2**      | Bouncy, Crystal, Dashing, Eloquent | Foxy, Galactic | Humble

 The documentation for each distribution states in detail which operating systems it supports. Noetic Ninjemys is the final distribution for ROS 1 and has an end-of-life set for 2025. In ROS 2 there is a special distribution called **Rolling Ridley**. This is the [development distribution](http://docs.ros.org/en/rolling/Releases.html#rolling-distribution) which contains all the newest features but is not considered a stable release.


**ROS Home Website** - [ros.org](https://www.ros.org/)

**ROS Documentation** - [Launch Page](https://docs.ros.org/)

**ROS 1 Documentation (ROS Wiki)** - [wiki.ros.org](https://wiki.ros.org/)

**ROS 2 Documentation** - [docs.ros.org](https://docs.ros.org/en/rolling/)

**ROS Package Index** - [index.ros.org](https://index.ros.org/)

**ROS Answers: A Q&A site for ROS** - [answers.ros.org](https://answers.ros.org/)

**ROS Discourse: A forum for ROS** - [discourse.ros.org](https://discourse.ros.org/)
