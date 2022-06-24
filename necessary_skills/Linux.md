[Home](../Home)
# Linux

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
