[Home](../Home)
# ROS (Robot Operating System)

[TOC]

**The Robot Operating System (ROS) is a set of software libraries and tools for building robot applications.** Despite the name, ROS is **not** an operating system. It would be more accurate to call it a *framework* or *middleware*. It is an ecosystem of software that contains drivers and state-of-the-art algorithms as well as powerful open-source developer tools (visualizers, message-passing, package management) meant to help you write scalable, distributed robotics applications without reinventing the wheel.

---
## Prerequisites to Learn ROS

In order to learn ROS you need to have relatively strong existing knowledge in computer science and programming. You do not need to be an expert, but you will need to know more than you might think and you shouldn't expect to pick it up in just a few days, especially if your background doesn't include much computer science. Frankly, knowing MATLAB and Arudino is a great start, but if that's all you have experience with you will find yourself lost very quickly. None of this is meant to deter you from learning this very important and useful tool. Rather it is meant to make sure you are successful and help you avoid becoming frustrated and overwhelmed (one must learn to walk before they learn to run). To make sure you're prepared to succeed, the following is a list of things you **must** be comfortable with before you attempt to learn ROS:

 - Using a [terminal and command line tools](Linux.md)
 - Strong programming knowledge in **at least one**, but ideally both of:
    - [C++](C_and_Cpp.md) and [CMake](CMake.md)
    - [Python](Python.md)

All in all, the more you understand about programming and the logistics of programming, the better off you are. So don't shy away from that computer science goodness.

---
## ROS Versions and Distributions

There are currently two major versions of ROS: **ROS 1** and **ROS 2**. Within each version, there are *distributions* which are versioned sets of ROS packages and can be thought of as minor versions or releases. These distributions have clever code names similar to the names given to [releases of Ubuntu Linux](https://wiki.ubuntu.com/Releases). Just like with Ubuntu, the first letter in the code name goes in alphabetical order with each new distribution. See below for the current list of distributions for each ROS version:

 - [**ROS 1 Distributions**](https://wiki.ros.org/Distributions)
 - [**ROS 2 Distributions**](https://docs.ros.org/en/rolling/Releases.html)

 Although ROS is becoming increasingly compatible with other operating systems and architectures, it is most widely used with Ubuntu Linux (ROS 1 only targets Ubuntu and ROS 2 targets Ubuntu, MacOS, and Windows 10). Below is a table describing which ROS distributions you should expect to use with a given Ubuntu LTS (Long Term Support) release:

  Ubuntu Release | ROS 1 Release(s)  | ROS 2 Release(s)
 :-------------- |:-----------------:|:-----------------------------------:
 18.04 (Bionic)  | Melodic           | Bouncy, Crystal, Dashing, Eloquent
 20.04 (Focal)   | Noetic (EOL 2025) | Foxy (LTS), Galactic
 22.04 (Jammy)   | -                 | Humble (LTS)

 The documentation for each distribution states in detail which operating systems it supports. Noetic Ninjemys is the final distribution for ROS 1 and has an end-of-life set for 2025. In ROS 2 there is a special distribution called **Rolling Ridley**. This is the [development distribution](http://docs.ros.org/en/rolling/Releases.html#rolling-distribution) which contains all the newest features but is not considered a stable release. New distributions of ROS 2 will release once each year where the distributions releasing in the same year as an Ubuntu LTS release will be considered LTS distributions (e.g., Foxy Fitzroy and Humble Hawksbill are LTS distributions).

 A summary of the differences between ROS 1 and ROS 2 can be found [here](https://roboticsbackend.com/ros1-vs-ros2-practical-overview/).

---
## Important ROS Resources

Below are important web-based resources for learning and using ROS.

- **ROS Home Website** (ROS 1, ROS 2) - [ros.org](https://www.ros.org/)

    - ROS 1 and ROS 2 product landing page, with high-level description of ROS and links to other ROS sites

- **ROS Documentation** (ROS 1, ROS 2)- [docs.ros.org](https://docs.ros.org/)

    - A landing page from which you can access documentation for any ROS version

- **ROS 1 Documentation** (ROS 1) - [wiki.ros.org](https://wiki.ros.org/)

    - Also called the **ROS Wiki**
    - ROS 1 documentation and user modifiable content
    - Active until at least the last ROS 1 distribution is EOL

- **ROS 2 Documentation** (ROS 2)

    - **Rolling** - [docs.ros.org/en/rolling/](https://docs.ros.org/en/rolling/)
    - **Humble** - [docs.ros.org/en/humble/](https://docs.ros.org/en/humble/)
    - **Galactic** - [docs.ros.org/en/galactic/](https://docs.ros.org/en/galactic/)
    - **Foxy** - [docs.ros.org/en/foxy/](https://docs.ros.org/en/foxy/)
    - Change the distribution the documentation is for at the bottom of the navigation tree on the left of the page

- **ROS Package Index** (ROS 1, ROS 2) - [index.ros.org](https://index.ros.org/)

    - Indexed list of all packages (i.e. [Python Package Index (PyPI)](https://pypi.org/) for ROS packages)
    - See which ROS distributions a package supports
    - Link to a package's repository, API documentation, or website
    - Inspect a package's license, build type, maintainers, status, and dependencies
    - Get more info for a package on ROS Answers

- **ROS Answers** (ROS 1, ROS 2) - [answers.ros.org](https://answers.ros.org/)

    - A Q&A community site for ROS, similar to [Stack Exchange](https://stackexchange.com/)

- **ROS Discourse** (ROS 1, ROS 2) - [discourse.ros.org](https://discourse.ros.org/)

    - Forum for general discussions and announcements for the ROS community

- **ROS Enhancement Proposals (REPs)** (ROS 1, ROS 2) - [ros.org/reps/](https://ros.org/reps/rep-0000.html)

    - Proposals for new designs and conventions

---
## Learning ROS

Below are some recommendations on how to learn ROS. **It is strongly recommended that you give priority to learning ROS 2 given that ROS 1 is near EOL**.

### ROS 1 Learning Resources

This section still needs to be filled out.

### ROS 2 Learning Resources

#### Free Online Resources

- [The ROS 2 Documentation](https://docs.ros.org/en/rolling/)
    - Make sure to set the documentation to the distribution you are using.
    - Start with the [installation guides](https://docs.ros.org/en/rolling/Installation.html).
    - The [Tutorials](https://docs.ros.org/en/rolling/Tutorials.html) included in the ROS 2 Documentation are an excellent way to get started!
    - The ROS 2 Documentation also contains [How-to Guides](https://docs.ros.org/en/rolling/How-To-Guides.html) which can be used to learn how to complete specific tasks. **Do the tutorials first if you are new to ROS 2**.
    - The [Concepts](https://docs.ros.org/en/rolling/Concepts.html) section of the ROS 2 Documentation is a great way to get background information and a deeper understanding of ROS 2. Use this section as you are doing the tutorials.

#### Paid Online Resources
