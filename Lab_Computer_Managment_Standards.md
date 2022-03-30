[Home](Home)
# Lab Computer Management Standards

## Users on Lab Computers

>**The lab's default password for computer user accounts is `telerobo2156`. Please use this password for all user accounts on lab computers except personal user accounts that are actively being used.**

Every computer in the lab must have a user for the purposes of lab computer administration according to the following rules:

- Username: `Telerobotics` or `telerobotics`
- Password: `telerobo2156`
- The `Telerobotics` user must have full administration privileges
- The `Telerobotics` user **must not** be used for anything other than general administration of the computer (e.g. creating and deleting other users, installing software for all users, etc.). **No lab work should be conducted from the `Telerobotics` user**.
- If a computer has multiple operating systems, there **must** be a `Telerobotics` user on each operating system.

By having a `Telerobotics` user on every computer, we can avoid lost data due to forgotten passwords and can create/delete users on the computer under which actual research/work should be taking place. The department IT team will usually also put a `localadmin` user on Windows operating systems. This user serves the same purpose that the `Telerobotics` user is meant to serve.

In general, each member of the lab should have a **personal user account** on the computer(s) that they regularly use. The reason for this is that things like [SSH authentication with Git](necessary_skills/Using_Git_with_SSH.md) and [mounting the lab network drive](#mounting) require passwords and authentication that is specific to a particular member of the lab and these things get very messy when multiple people are sharing the same user.

Exceptions to this rule would be computers on which no software development will be conducted (i.e. there will be no interaction with [Git repositories](necessary_skills/Git.md)) **and** mounting the lab network drive is not necessary. For example, a computer that is dedicated to **only** use and take data with a partcular piece of lab equipment would not need a user for every member of the lab that wants to use that computer to take data with the equipment. If someone wants to do something more on that computer, then that lab member should create a personal user on the computer.

>**Keep in Mind**: Since most people should be using their own personal user accounts on each computer, you should avoid hardcoding filepaths in your software projects that contain the user home directory. There are often ways to get the user home directory for whichever user is currently active (e.g. using the `$HOME` environment variable).

### Creating and Deleting Users on Windows

- Fully Delete a user (2 steps): 1 In the System properties window, click on settings in user profiles and then delete the user profile. This deletes the data associated with the profile. Then delete the user in the Accounts section of the settings app.

### Creating and Deleting Users on Linux

---
## Mapping/Mounting the Lab Network Drive (Group Drive)
<a name="mouting"></a>

### Windows

### Linux
    - https://wiki.ubuntu.com/MountWindowsSharesPermanently
    - `//chips.eng.utah.edu/telerobotics /home/adam/telerobotics-group cifs credentials=/home/adam/.smbcredentials,uid=adam,gid=adam,vers=2.0 0 0`
    - https://serverfault.com/questions/222074/fstab-and-cifs-mounting-possible-to-store-authentication-information-outside-of
    - https://askubuntu.com/questions/1262419/safer-alternative-to-using-smbcredentials
    - https://askubuntu.com/questions/1027271/secure-password-when-mounting-the-file-server-using-smbcredentials/1081421#1081421

---
## Remote Access to Lab Computers

### Through TeamViewer
[TeamViewer](https://teamviewer.com) is installed on many of the lab computers and can be used to initiate a remote session to control a computer as if you were in the lab. If TeamViewer is installed on a lab computer, it **must** be configured according to the following rules:

- **Do not** assign a TeamViewer account (found in the General options)
- **Do not** enable easy access (a TeamViewer account must be assigned to enable this anyway)
- **Disable** the random password (found in the Security options)
- If there is at least one computer in the "allow list" (see below), set the "personal password" to `telerobo2156` (found in the Advanced options). If no computers are in the "allow list" then the "personal password" should be **removed**.

The "allow list" (found in the Security options) is a list of unique TeamViewer IDs of the computers that we want to allow access to the lab computer. No computer other than those with IDs in the "allow list" can connect under any circumstances.

Currently, there are three ways to connect to a computer with TeamViewer: using an assigned account and easy access, using the randomly generated password, and using the personal password. The above rules are meant to make it impossible to remote login to a lab computer by disabling all of the three methods by default and only enabling the personal password method when the "allow list" is active and contains up-to-date computer IDs.

#### Setting Up Your Personal Computer to Access a Lab Computer
If the above rules are followed on each lab computer, you can set up a personal computer to remote login to a lab computer by following these steps:

- Add your personal computer's TeamViewer ID to the "allow list" of the lab computer in the TeamViewer Security options.
- Add the lab computer's TeamViewer ID and the personal password `telerobo2156` to your personal computer's contacts list.

>:exclamation: **Don't forget to remove the TeamViewer ID from the allow list of the lab computer, when your personal computer no longer needs access to it.**

Following these steps, you won't need to enter a password every time you login to the lab computer from your personal computer.