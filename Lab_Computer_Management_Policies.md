[Home](Home)
# Lab Computer Management Policies

**Contents**

[TOC]

## User Accounts on Lab Computers

>**The lab's default password is `FlamencoMagnet`. This password should be used for lab administrator accounts on all lab computers. Actively used personal user accounts on lab computers should have personal passwords. When you no longer need to use a personal account (e.g. when you graduate or will no longer be working with the lab) it should be removed from the computer, but at the very least its password should be changed to the lab default password.**

>**The lab administrator account was previously called `Telerobotics` or `telerobotics`. Previous lab default passwords are: `telerobo2156`. Computers with old administrator accounts and/or passwords do not need to be updated to comply with the rules outlined below, however, doing so would help reduce confusion. Regardless, lab members should be aware that these old accounts and passwords exist.**

>**Passwords on Linux:** You may need to bypass password complexity requirements to set a password on Linux. To do so use `sudo passwd <username>` from the command line where you replace `<username>` with the username of the account whose password is being changed.

Every computer in the lab must have a user for the purposes of lab computer administration according to the following rules:

- **Username:** `labadmin` (on Linux, set *Full Name* to `Lab Admin`)
- **Password:** `FlamencoMagnet`
- The `labadmin` user must have full administration privileges
- The `labadmin` user **must not** be used for anything other than general administration of the computer (e.g. creating and removing other users, installing software for all users, etc.). **No lab work should be conducted from the `labadmin` user**.
- If a computer has multiple operating systems, there **must** be a `labadmin` user on each operating system.

By having a `labadmin` user on every computer, we can avoid lost data due to forgotten passwords and can create/remove users under which actual research/work should be taking place. The department IT team will usually also put a `localadmin` user (or similar) on Windows operating systems. This user serves the same purpose that the `labadmin` user is meant to serve but we have the `labadmin` users to avoid contacting IT whenever we need to create/remove a user, etc.

In general, each member of the lab should have a **personal user account** on the computer(s) that they regularly use. The reason for this is that things like [SSH authentication with Git](necessary_skills/Using_Git_with_SSH.md) and [mounting the lab network drive](Lab_Network_Drive.md) require passwords and authentication that is specific to a particular member of the lab and these things get very messy when multiple people are sharing the same user. It also makes it easy to remove any sensitive personal information such as saved web browser login info (Google Chrome login, etc.), saved cloud drive syncing login info (e.g. Google Drive, OneDrive, etc.), and other similar items when a member of the lab leaves/graduates by simply removing any of their personal user accounts from lab computers.

Exceptions to this rule would be computers on which **all** of the following applies:

- No software development will be conducted (i.e. there will be no interaction with [Git repositories](necessary_skills/Git.md))
- Mounting the lab network drive is not necessary
- Logging into web browsers, cloud drive syncing apps, or anything similar is not necessary

For example, a computer that is dedicated to **only** use and take data with a particular piece of lab equipment would not need a user for every member of the lab that wants to use that computer to take data with the equipment. If someone wants to do something more on that computer (including develop software related to using that piece of lab equipment), then that lab member should create a personal user on the computer.

>**Keep in Mind**: Since most people should be using their own personal user accounts on each computer, you should avoid hardcoding filepaths in your software projects that contain a user home directory. There are often ways to get the user home directory for whichever user is currently active (e.g. using the `$HOME` environment variable).

### Creating and Removing Users on Windows

Administrator privileges are required to perform the steps in this section.

**Create a user:**

1. Open Settings.
2. Navigate to *Accounts* and then *Family & other users*.
3. Click on *Add someone else to this PC*.
4. Windows will prompt you for a personal Microsoft account. If you have a personal Microsoft account, enter that information now and follow the on screen instructions. If you do not want to use a personal Microsoft account and instead want to create a local user account:
    1. Click on *I don't have this person's sign-in information*.
    2. Click on *Add a user without a Microsoft account*.
    3. Enter a user name. Avoid spaces in the username.
    4. Enter a password.
    5. Enter security questions.
    6. Click *Next*.
5. Click on the new account created in *Family & other users* and then click on *Change account type*.
6. Change the account type to *Administrator* and click *OK*.


**Remove a user:**

1. Open Settings.
2. Navigate to *Accounts* and then *Family & other users*.
3. Click on the account you wish to remove.
4. Click on *Remove*.
5. Click on *Delete account and data*. **This will delete the account, the user's home folder under `C:\Users\`, and all data associated with the user. Make sure you have stored any data that you don't want to lose in another location.**

### Creating and Removing Users on Linux (Ubuntu)

Administrator privileges are required to perform the steps in this section.

**Create a user:**

1. Navigate to the *Users* menu in Settings.
2. Unlock the Settings window. There is usually a button that says *Unlock...* at the top of the window. Unlocking the window is like typing `sudo` on the command line.
3. Click on *Add User...*
4. Specify a name and username. Note that the name can have spaces and can be changed later on, but **the username cannot have spaces, cannot be changed, and should typically be all lowercase**. For example, the name can be `John Doe` and the username can be `johndoe` or `john`. The username is typically automatically populated from the name field so make sure the username is something you're okay with. The name will be what is displayed on the login screen. The username will be used as the name of your home directory.
5. Give administrator privileges to the user if necessary.
6. Specify a password. Be sure to follow the rules as explained above.
7. Assign necessary groups to the user ([see the Linux page for instructions](necessary_skills/Linux.md)). If the new user has administrator privileges, they can perform this step from their own user.

**Remove a user:**

1. Navigate to the *Users* menu in Settings.
2. Unlock the Settings window. There is usually a button that says *Unlock...* at the top of the window. Unlocking the window is like typing `sudo` on the command line.
3. Select the user you wish to remove. You cannot remove the currently logged in user.
4. Click on *Remove User...*
5. Choose to delete all user files. **This will remove the user's home directory and everything associated with this user. Make sure you have stored any data that you don't want to lose in another location.**

---
## Remote Access to Lab Computers

>:warning: **This section is incomplete! TeamViewer is no longer the primary method of remote access to lab computer because it is common for TeamViewer to revoke the free license due to triggers indicating falsely that it is being used commercially. In its place, the department recommends using Remote Desktop Connection to access Windows computers and AnyDesk to access Linux computers.**

### Via Remote Desktop Connection (Windows Only)

To download the VPN software for accessing the University of Utah network remotely, go to [vpn.utah.edu](https://vpn.utah.edu) and login with your university CIS login credentials. This will take you to a page where you can download and install the GlobalProtect Portal VPN software from Palo Alto Networks.

### Via TeamViewer
[TeamViewer](https://teamviewer.com) is installed on many of the lab computers and can be used to initiate a remote session to control a computer as if you were in the lab. If TeamViewer is installed on a lab computer, it **must** be configured according to the following rules:

- **Do not** assign a TeamViewer account (found in the General options)
- **Do not** enable easy access (a TeamViewer account must be assigned to enable this anyway)
- **Disable** the random password (found in the Security options)
- If there is at least one computer in the "allow list" (see below), set the "personal password" to the lab default password `FlamencoMagnet` (found in the Advanced options). If no computers are in the "allow list" then the "personal password" should be **removed**.
- You may turn on the option to start TeamViewer with the operating system

The "allow list" (found in the Security options) is a list of TeamViewer IDs, which is a number that is computer-specific rather than person-specific, of the computers that we want to allow access to the lab computer. No computer other than those with IDs in the "allow list" can connect under any circumstances.

Currently, there are three ways to connect to a computer with TeamViewer: (1) using an assigned account and easy access, (2) using the randomly generated password, and (3) using the personal password. The above rules are meant to make it impossible to remote login to a lab computer by disabling all of the three methods by default and only enabling the personal password method when the "allow list" is active and contains up-to-date computer IDs. If a personal password is set and no items are in the "allow list" then it may be possible for any computer to remote login using the personal password.

#### Setting Up Your Personal Computer to Access a Lab Computer Via TeamViewer
If the above rules are followed on each lab computer, you can set up a personal computer to remote login to a lab computer by following these steps:

- Add your personal computer's TeamViewer ID to the "allow list" of the lab computer in the TeamViewer Security options. TeamViewer may ask you to login with a TeamViewer account when adding to the allow list, but if you say you don't want to you should be able to get to a point where you can add TeamViewer IDs (which are computer-specific rather than person-specific) to the allow list. **Remember, do not assign a TeamViewer account to any lab computer by logging in.**
- Add the lab computer's TeamViewer ID and the personal password `FlamencoMagnet` to your personal computer's contacts list or your personal TeamViewer account's contact list.

>:exclamation: **Don't forget to remove the TeamViewer ID from the allow list of the lab computer when your personal computer no longer needs access to it.**

Following these steps, you won't need to enter a password every time you login to the lab computer from your personal computer.