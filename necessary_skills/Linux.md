[Home](../Home)
# Linux

Linux is a powerful operating system that is used in a great deal of robotic systems (it was the only OS supported by [ROS](ROS.md) until recently). Linux philosophy is quite different from more mainstream operating systems such as Windows and macOS that focus on a graphical user interface (GUI) as the primary means for users to interact with the system. This means it is rather easy for new users of Linux to become overwhelmed or confused even if they consider themselves pretty computer savvy, but don't let this deter you from learning! This page is intended to help you get up to speed with Linux and there are a lot of useful online resources at your disposal. Simply be prepared that your knowledge from other operating systems will not necessarily trivialize the transition for you. Also be aware that simple tasks like creating a new text file may at first take you longer than you are used to, but be patient as you become acquainted with the way Linux likes to do things. In Linux, the command line terminal is still a prominent part of user interaction and you will not be able to become a proficient user without taking the time to develop this skill. Although Linux may seem archaic or cumbersome at first, there is a reason it is still widely used today and you won't regret developing this skill as a robotics engineer.

## Background and Linux Distributions

### What is Linux?

Linux is what we call a [Unix-like][unixlike] operating system. Fun fact, macOS is also a Unix-like OS. [Unix][unix] is one of the first multitasking operating systems (developed by Bell Labs in 1969) and it came to be widely used sparking many variants (or Unix-like OSes) to be created. However, Unix was not completely open-source (you had to pay) and this bothered a lot of people. In response, the GNU project (the G is not silent) was created to build Unix from scratch with entirely open-source software. This project completed most of the software needed to make an OS useful (e.g. libraries, compilers, text editors, a command-line shell, and a windowing system), but stalled out on the actual OS itself (called a kernel). Eventually, a kernel was written by Linus Torvalds while he was in college and this kernel combined with the GNU software eventually became Linux (you will notice the word `gnu` appear frequently in Linux). Another fun fact, Linus had originally intended to call his kernel **Freax** (pronounced *freaks*), not surprising from a college student.

### Linux Distributions

There are many [flavors of Linux][distros], called **distributions**. A distribution is an operating system made from a software collection that combines the Linux kernel with a particular package management system and other software selections like a particular windowing system or GUI. The choice of package management system is important because this is what you use to install almost all software onto your system in Linux. The most common distributions are **RPM-based** or **DEB-based**. The choice of package management system is the primary distinction between these two families of distributions. RPM-based distributions use the RPM package manager and its associated command line utility `yum`. Software for these distributions will have the `.rpm` package file format. Examples of RPM-based distributions are Red Hat Linux, Fedora, SUSE Linux, and CentOS. DEB-based distributions use the APT (Advanced Packaging Tool) package manager and its associated command line utilities `dpkg` and `apt` (`apt` is a user friendly frontend that invokes `dpkg` for you). Software for these distributions will have the `.deb` package file format. Examples of DEB-based distributions are Debian, Ubuntu, and flavors of Ubuntu like Kubuntu and Linux Mint. This information is summarized below.

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

## Learning To Use Linux

There are many learning resources available online and it's up to you how you'd like to tackle learning Linux. In this section, several suggestions are made.

### Resources Available On This Wiki

This wiki contains several useful PDFs.

A few notes about these resources:
  1. The Linux for Beginners book is a great place to start. Read the Introduction and then you can skip down to the "Connecting Directly" section of the "Getting Connected" chapter. The "Getting Connected" chapter mostly deals with accessing a remote Linux server. Keep in mind that this book was probably written in about 2013 so the Ubuntu UI will look a bit different. The concepts should all still apply today. You can skip over information that is specific to a distribution family that you are not using (e.g. you can skip RPM-based info if you are using Ubuntu).
  2. The `apt` command is now generally preferred over `apt-cache` and `apt-get` since `apt` uses these other commands for you.
  3. The Linux Command Line Cheat Sheet Section 10 - Installing Packages only shows commands for RPM-based distributions. Package commands for DEB-based distributions are absent.
  4. The Linux Administration book is a great lookup reference when you need to do a particular thing or want to know more about a particular topic.

PDFs

- [Linux for Beginners](Linux_for_Beginners.pdf) by Jason Cannon
- [Linux Command Line Cheat Sheet](Linux_Command_Line_Cheat_Sheet.pdf) by Jason Cannon
- [Linux Administration](Linux_Administration.pdf) by Jason Cannon

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

[unixlike]: https://en.wikipedia.org/wiki/Unix-like
[unix]: https://en.wikipedia.org/wiki/Unix
[distros]: https://en.wikipedia.org/wiki/List_of_Linux_distributions
