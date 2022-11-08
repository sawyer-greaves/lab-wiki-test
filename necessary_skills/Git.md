[Home](../Home)
# Git

**Contents**

[TOC]

---
## Introduction

Git is a distributed Version Control System (DVCS) used primarily to keep track of
changes in source code. Learning how to use Git is required by everyone in the lab
even if they never write any code because this wiki is
[managed as a Git repository of Markdown files](Editing_the_Wiki.md).

Those who write code (including MATLAB code) during their time in the lab must
manage their code in Git repositories. There are several advantages when using Git.

#### Git will help you keep your code clean and organized

Since Git allows you to store and recall previous versions of your code, you do not
need to keep commented lines just because you think you might need them one day.
Furthermore, let's say you want to keep a copy of your code corresponding to a
particular journal publication, but you want to be able to continue changing your
code for future work. You don't need to keep a separate copy of you code (e.g.
using a ZIP file; the lab group drive is a mess filled with versions of code kept
in ZIP files) for this purpose because a Git repository contains your entire project
history! Instead, you can tag a version (called a commit) with a descriptive name
and easily switch between that version and the version you're currently working on.

#### Git repositories can be hosted in the cloud

You can push your local changes to a cloud-based Git repository and mitigate the
chances of lost work due to data loss on your physical computer. A cloud-based Git
repository also allows you to easily share your work and collaborate with other
students because they can clone the repository to their computer, make changes, and
push those changes too, provided you've given them permissions to do so. Common Git
hosting services include GitHub, Bitbucket, and GitLab.

#### Our lab has a Bitbucket workspace

For these reasons, our lab has a workspace on Bitbucket. Repositories created in this
workspace belong to the lab and can be modified by members of the workspace. Once
you learn Git, please see the lab
[Standards and Procedures](../Standards_and_Procedures.md) for standards relating to
Git repositories.

---
## Using Git

Git is a program that is invoked via the command-line command `git`. As such the primary way many people use Git is on the command-line. However, there exist a myriad of graphical user interfaces (GUIs) that invoke the `git` command under the hood for you and therefore simplify the use of Git for people more comfortable with graphical user interfaces. Don't feel obligated to use the command line to use Git, however, doing so will help enrich your understanding of Git.

### Using Git on the Command Line

#### Git Bash on Windows

Git Bash allows you to use Git in a Bash shell for Windows (i.e. on the command line like you would on Linux). The easiest way to install and use Git Bash on Windows is to install it from the [Git for Windows](https://gitforwindows.org/) project. Installing Git Bash can be a bit confusing so see [Installing Git Bash on Windows](Git_Bash_Windows_Installation.md).

Once Git Bash is installed, you can pull up a Git Bash terminal in any directory using the **Git Bash Here** option in the right-click context menu, as shown below.

![Launching Git Bash from Right-CLick Context Menu](images/Git_Bash_Windows_context_menu.webp)

#### Installing Git on Linux

Installing Git on Linux is easy. Simply install it with the APT package manager:

```
sudo apt install git
```

### Using Git with Graphical User Interfaces (GUIs)

Git keeps a list of popular Git GUI clients [here](https://git-scm.com/downloads/guis).

Of particular interest in this list are:

- GitKraken (Linux, Mac, Windows)
- SourceTree (Mac, Windows)


---
## Learning Git

### What You Need to Know

Given there are many ways to use Git either through the command line or the wide variety of GUI interfaces, it makes sense to list general Git concepts that you should make yourself familiar with. YOu should know the following concepts and how to interact with them through your chosen method of using Git.

- Configuration variables
    - Know how to set them and how to see what values are active in a given context.
    - Know the difference between the three configuration variable context levels **local** (i.e. repository), **global** (i.e. user), and **system** (i.e. computer). Note: It is uncommon to use the **system** context level.
    - Know where these configuration variable values are stored (i.e. know what `.gitconfig` files are and where to find them).
    - Know the function of these configuration variables at a minimum: **user.name**, **user.email**, **core.editor**.

### Learning Resources

- [ProGit Textbook](Pro_Git.pdf)
- [Git Cheatsheet](Atlassian_Git_Cheatsheet.pdf)
