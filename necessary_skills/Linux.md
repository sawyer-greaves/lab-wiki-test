[Home](../Home)
# Linux

[TOC]

Linux is a powerful operating system (OS) that is used in a great deal of robotic systems (it was the only OS supported by [ROS](ROS.md) until recently). Linux philosophy is quite different from more mainstream operating systems such as Windows and MacOS that focus on a graphical user interface (GUI) as the primary means for users to interact with the system. This means it is rather easy for new users of Linux to become overwhelmed or confused even if they consider themselves pretty computer savvy, but don't let this deter you from learning! This page is intended to help you get up to speed with Linux and there are a lot of useful online resources at your disposal. Simply be prepared that your knowledge from other operating systems will not necessarily trivialize the transition for you. Also be aware that simple tasks like creating a new text file may at first take you longer than you are used to, but be patient as you become acquainted with the way Linux likes to do things. In Linux, the command line terminal is still a prominent part of user interaction and you will not be able to become a proficient user without taking the time to develop this skill. Although Linux may seem archaic or cumbersome at first, there is a reason it is still widely used today and you won't regret developing this skill as a robotics engineer.

---
## Background and Linux Distributions

### What is Linux?

Linux is what we call a [Unix-like][unixlike] operating system. Fun fact, MacOS is also a Unix-like OS. [Unix][unix] is one of the first multitasking operating systems (developed by Bell Labs in 1969) and it came to be widely used, sparking many Unix-like variants to be created. However, Unix was not completely open-source (you had to pay) and this bothered a lot of people. In response, the GNU project (the G is not silent) was created to build Unix from scratch with entirely open-source software. This project completed most of the software needed to make an OS useful (e.g. libraries, compilers, text editors, a command-line shell, and a windowing system), but stalled out on the actual OS itself (called a kernel). Eventually, a kernel was written by Linus Torvalds while he was in college and this kernel combined with the GNU software eventually became Linux (you will notice the word `gnu` appear frequently in Linux). Another fun fact, Linus had originally intended to call his kernel **Freax** (pronounced *freaks*), not surprising from a college student.

### Linux Distributions

There are many [flavors of Linux][distros], called **distributions**. A distribution is an operating system made from a software collection that combines the Linux kernel with a particular package management system and other software selections like a particular windowing system or GUI. The choice of package management system is important because this is what you use to install almost all software onto your Linux system. The most common distributions are **RPM-based** or **DEB-based**. The choice of package management system is the primary distinction between these two families of distributions. RPM-based distributions use the RPM package manager and its associated command line utility `yum`. Software for these distributions will have the `.rpm` package file format. Examples of RPM-based distributions are Red Hat Linux, Fedora, SUSE Linux, and CentOS. DEB-based distributions use the APT (Advanced Packaging Tool) package manager and its associated command line utilities `dpkg` and `apt` (`apt` is a user friendly frontend that invokes `dpkg` for you). Software for these distributions will have the `.deb` package file format. Examples of DEB-based distributions are Debian, Ubuntu, and flavors of Ubuntu like Kubuntu and Linux Mint. This information is summarized below.

>**IMPORTANT:** You must make yourself aware of which package management system your distribution uses so you are able to select the correct package type for software that is installed by downloading a package file from the internet (e.g. Google Chrome, TeamViewer). **Our lab usually uses Ubuntu or some flavor of Ubuntu which are DEB-based distributions.**

#### RPM-based Distributions

- **Package Management System** - RPM package manager
- **Package Management Command Line Utility** - `yum`
- **Package File Format** - `.rpm`
- **Example Distributions** - Red Hat Linux, Fedora, SUSE Linux, openSUSE, CentOS

#### DEB-based Distributions

- **Package Management System** - APT (Advanced Packaging Tool) package manager
- **Package Management Command Line Utility** - `dpkg` and `apt`
- **Package File Format** - `.deb`
- **Example Distributions** - Debian, Raspberry Pi OS, Ubuntu, and flavors of Ubuntu like Kubuntu and Linux Mint

[unixlike]: https://en.wikipedia.org/wiki/Unix-like
[unix]: https://en.wikipedia.org/wiki/Unix
[distros]: https://en.wikipedia.org/wiki/List_of_Linux_distributions

---
## Introduction to Ubuntu

Ubuntu is currently the most commonly used Linux distribution in robotics. Practically all software packages useful for robotics support Ubuntu at a minimum. Ubuntu is released in three editions: Desktop, Server, and Core. Typically you will want to have the Desktop edition. Ubuntu is released every six months in April and October with long-term support (LTS) releases every two years. The version numbering reflects this release pattern where the first number indicates the year and the second number indicates the month. For example, Ubuntu 22.04 was released in April (04 part) of 2022 (22 part). The LTS version is always the April release of even years (i.e. Ubuntu 18.04, 20.04, and 22.04 are LTS releases). **It is recommend to stick to LTS releases only**. In addition to the version number, every release is assigned a two word code name where both words start with the same letter. With each new release, this code name letter is incremented. For example, Ubuntu 22.04 is code named **Jammy Jellyfish**. Here is a list of [releases of Ubuntu Linux](https://wiki.ubuntu.com/Releases) with their code names.

### System Updates

Once you have a particular version of Ubuntu installed, you should **never avoid updates to the system**. Ubuntu will periodically remind you to install updates and this will not require a system reboot unless the update includes updates to the Linux kernel. Despite what some may believe, routine operating system updates **are unlikely to break software you've written or installed** and are critical for security among other things. In the unlikely event your software does break, it is better to adjust your software to the updates than it is to avoid the inconvenience of fixing your code.

However, upgrading to a new release of Ubuntu (e.g. from 20.04 to 22.04) is a substantial update and is more likely to cause problems. Upgrading to a new release should be done at the latest when LTS support for your current version has expired (usually 5 years from release). It is recommended when upgrading to a new release that you install the new release from scratch rather than use Ubuntu's internal upgrade mechanism. It is also recommended that you make sure any libraries and software you rely on is supported on the new release before upgrading. Upgrading can be a bit tedious, but it is usually very important to keep up with modern releases because compatibility with new useful software and hardware will become very limited.

---
## Learning To Use Linux

There are many learning resources available online and it's up to you how you'd like to tackle learning Linux. In this section, several suggestions are made. If you've found a resource not in this section that has been useful to you, please share it with the lab by adding it here.

### Resources Available On This Wiki

This wiki contains several useful PDFs.

- [Linux for Beginners](Linux_for_Beginners.pdf) by Jason Cannon
    - This book is a great place to start! Read the Introduction and then you can skip down to the "Connecting Directly" section of the "Getting Connected" chapter. The "Getting Connected" chapter mostly deals with accessing a remote Linux server. Keep in mind that this book was probably written in about 2013 so the Ubuntu UI will look a bit different, however, the concepts should all still apply today. You can skip over information that is specific to a distribution family that you are not using (e.g. you can skip RPM-based info if you are using Ubuntu).
    - The `apt` command is now generally preferred over `apt-cache` and `apt-get` since `apt` is a more user-friendly combined interface for these two tools.
- [Linux Command Line Cheat Sheet](Linux_Command_Line_Cheat_Sheet.pdf) by Jason Cannon
    - Section 10 - Installing Packages only shows commands for RPM-based distributions. Package commands for DEB-based distributions are absent.
- [Linux Administration](Linux_Administration.pdf) by Jason Cannon
    - This book is a great lookup reference when you need to perform a particular task or want to know more about a particular topic.
    - The `apt` command is now generally preferred over `apt-cache` and `apt-get` since `apt` is a more user-friendly combined interface for these two tools.
- [Computer Science from the Bottom Up](Computer_Science_from_the_Bottom_Up.pdf)
    - This is an **excellent** resource to dive deeper into Linux as an operating system and to better understand the writing and running of software. **It is highly recommended reading for those with limited computer science background**. Note the author uses UK English.

### Free Online Resources

- [UNIX Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/)
    - This quick tutorial is recommended by the [ROS](ROS.md) tutorials.
    - The tutorial mostly focuses on teaching commands for the command line but contains a lot of useful contextual/background information too.
    - Tutorial **seven** is particularly useful and covers material related to building source code which is not covered by the Jason Cannon resources.

### Paid Online Resources

- Linux courses offered by Jason Cannon on Udemy
    - Udemy is almost always offering sales on courses so you should be able to get lifetime access to these for $10-$20 each
    - [Learn Linux in 5 Days and Level Up Your Career](https://www.udemy.com/course/learn-linux-in-5-days/)
    - [Linux for Beginners](https://www.udemy.com/course/linuxforbeginners/)
    - [Linux Shell Scripting: A Project-Based Approach to Learning](https://www.udemy.com/course/linux-shell-scripting-projects/)

---
## Linux and Ubuntu Reference and Documentation

This section lists websites that are useful as Linux and Ubuntu reference and documentation.

- [Linux Kernel Documentation](https://www.kernel.org/doc/html/latest/)
    - The official documentation of the Linux kernel.
- [Linux Manpages](https://www.kernel.org/doc/man-pages/)
    - Search manpages for software on Linux systems.
- [Ubuntu Manpage Repository](https://manpages.ubuntu.com/)
    - Search manpages for software on Ubuntu systems.
- [Ubuntu Packages Search](https://packages.ubuntu.com/)
    - Search the Ubuntu package repositories for available packages/software.
- [POSIX Standard](https://pubs.opengroup.org/onlinepubs/9699919799/)
    - Standards most Unix-like operating systems follow to improve compatibility across systems.
- [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/fhs.shtml)
    - Standard for how the directories on a Unix-like system should be organized. Very useful for programmers.
- [Debian Policy Manual](https://www.debian.org/doc/debian-policy/index.html#) 
    - Policies like the POSIX Standard but specific to Debian distributions.
    - Useful for Ubuntu since it is Debian-based.

---
## Installing software (DEB-based Distributions)

The standard method of installing software on Linux is quite different from the way it is typically done on Windows or MacOS. On Windows or MacOS you may be used to downloading and running an installer executable from the internet. This method is not common on Linux.

### APT Package Manager Tool and online software/package repositories
Linux uses a *package manager* to install software and software dependencies for you. On DEB-based distributions of Linux (like Ubuntu) the package manager is most often invoked using the command line tool `apt`. Ubuntu manages a set of online package repositories (servers) that `apt` uses to download a requested software package. These repositories will contain most of the software you will need. Some software is not hosted on the Ubuntu repositories and instead may be hosted in an online repository managed by the software publisher. This is the case for Visual Studio Code, Google Chrome, and ROS to name a few examples. In these cases, the publisher website will often give instructions to install the software. These instructions may at first seem confusing, but they usually consist of a few simple commands to download a repository authorization key (usually using `wget` or `curl` commands), add the repository to the list `apt` uses to search for software, and then use `apt` to download and install the software package itself. What's nice about this method is that once the publisher's repository is added to the list for `apt`, all of the software packages offered on that publisher's repository are available through `apt` You can forget about which repository a package comes from. `apt` will be your single interface for installing and updating packages from all of the repositories in its list.

Here are some useful commands to search for and install software using `apt` (you may need to prepend some commands with `sudo` if you need root privileges):

**Updating and Upgrading**
```
apt update
apt upgrade
```
`apt update` causes `apt` to update its knowledge of what is available on the package repositories. This means `apt` will become aware of new packages as well as new versions of packages so it can let you know if installed packages could be updated to newer versions. `apt update` does not actually install or update any packages. `apt upgrade` will take the new knowledge from `apt update` and actually perform the updates to packages that could be updated to a newer version. Neither `apt update` nor `apt upgrade` will  update your system to a new release of Linux (e.g., Ubuntu 20.04 to 22.04).

**Listing packages**
```
apt list                 # List all available packages
apt list --installed     # List all installed packages
```
The output of the above commands is usually too much to sift through. You can pipe the output into `grep` to filter the lines of the output to only show lines with some specific text.
```
apt list | grep <specific-text>
apt list --installed | grep <specific-text>
apt list | grep python     # Show only lines containing the word "python"
```

**Getting information about a specific package**
```
apt show <package-name>
```

**Installing a package**
```
apt install <package-name>
# To install multiple packages, simply list them
apt install <package1> <package2> <package3>
```

**Uninstalling a package**
```
apt remove <package-name>
apt autoremove
```

`apt autoremove` is used to remove packages that were installed as a dependency, but are no longer a dependency to any package (perhaps because you uninstalled a package that depended on it).

### Installing with DEB Package Files (`.deb`)

Sometimes a software publisher will simply provide you a DEB package file with the `.deb` file extension. Often, installing the DEB package file will add the publisher's software repository to `apt` automatically (this happens with Google Chrome and Visual Studio Code for example). In this case, there will be no need to use a newer DEB file to update the software later (updates would be taken care of automatically by `apt`). There are two main methods on Ubuntu to install DEB packages.

#### Install using the Ubuntu Software GUI

Simply double-clicking on the DEB file in the file explorer will open the Ubuntu Software GUI and guide you through the installation.

#### Install with the Command Line using `dpkg`

The `dpkg` command is the package manager program used behind the scenes by `apt` and the Ubuntu Software GUI. The difference between `dpkg` and `apt` is that the first does not automatically resolve dependencies required by a package. If a package relies on dependencies that are not on the system, `dpkg` returns an error. You’ll need to install dependencies manually before you can install the DEB package using `dpkg`.

To install a DEB package using `dpkg` run the command:
```
sudo dpkg -i <package_path>
```

#### Uninstalling software installed using a DEB Package File

This can be a tricky process because you need to know the official name of the software package that was installed by the DEB package file, not the `.deb` file name. You may be able to search your installed packages with `dpkg` or `apt` to find the official package name. Once you have it, you can uninstall the software using the command
```
sudo dpkg -r <package_name>
```
If you used `dpkg` to install the package, you should use `dpkg` to remove it. Similarly, if you used `apt` to install the package, you should use `apt` to remove it.

---
## Managing Groups

Groups are a way to specify file permissions and other privileges broadly for all users that are members of the group. For example, if a group has some set of permissions on a file, a user that is a member of the group will have the same permissions on that file even if the file does not give permissions to that user specifically. Every user is associated with a *primary group* and zero or more *secondary groups*. Typically, the primary group for a user defaults to a group with the same name as the user. The primary group is the group that will be assigned to new files created by that user.

Some common group-related tasks are explained below. You may need to prepend the commands with `sudo` for elevated privileges.

### List Groups

    groups <username>
    
Lists the groups that a particular user belongs to. If you omit the `<username>` argument, the command will list groups for the current process (This essentially means groups for the currently logged in user, but keep in mind that if you've modified the groups you belong to in the same terminal instance, this change is not reflected in that terminal instance. Therefore, omitting the `<username>` argument will not show the changes you have made).

    id <username>

This is the same as using `groups` but will show IDs in addition to names.

    getent group

Lists all groups on the system. The output will also show you which user accounts are members of which groups.

### Add/Remove Group for User

    usermod -a -G <groupname> <username>
    
Adds user `<username>` to group `<groupname>`. Specifically, `<groupname>` will be a secondary group for `<username>`.

    usermod -a -G <groupname1>,<groupname2>,<groupname3> <username>

Used to add a user to multiple groups in the same command. Simply separate the groups with commas. You may list as many groups as you like.

    usermod -g <groupname> <username>
    
Sets `<groupname>` as the primary group for `<username>`.

    gpasswd --delete <username> <groupname>

Removes the user `<username>` from the group `<groupname>`. This is safer than using `deluser` since it is possible to accidentally delete the user with that command.

### Create a Group

    groupadd <new_groupname>

Creates a new group on the system with the name `<new_groupname>`. It is unlikely you will need to use this command.

---
## Change the Default Terminal in Ubuntu

It is possible to install alternative terminal emulation programs (e.g. [Terminator](https://terminator-gtk3.readthedocs.io/en/latest/)) and it is possible to decide which of these emulators is set as the default (e.g. which terminal is started with Ctrl+Alt+T). To set the default terminal emulator, run the following command in a terminal and follow the instructions (Note that the GNOME terminal is the terminal emulator that ships by default with Ubuntu):
```
sudo update-alternatives --config x-terminal-emulator
```