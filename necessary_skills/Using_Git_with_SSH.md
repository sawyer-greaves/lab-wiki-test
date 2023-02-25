[Home](../Home)
# Using Git with the SSH Protocol

SSH (Secure SHell) is a protocol alternative to HTTPS that can be used by Git to perform network
transactions (e.g. `git fetch`, `git pull`, `git push`). SSH uses public key
authentication instead of a traditional username and password. This involves
creating two text-based files: the private key and the public key. The public key is
then given to the Git hosting service. The combination of public and private key is used to verify your identity instead of a username and password.

**Contents**

[TOC]

---
## Setting Up SSH

Setting up SSH is done on a per computer user basis for each Git hosting service with which you wish to interact (e.g. Bitbucket, GitHub). In other words, each user on every computer you use will need to go through the following process in order to interact with repositories you have access to on Git hosting services. The process is generally as follows:

1. Generate a default private-public key pair for your computer user. This must be done on every user you use on every computer you use.
2. Add the public key to each Git hosting service you want to access.
3. If you have multiple accounts with the same Git Hosting Service and want to access them all from the same computer user, see the next section which contains instructions for this situation.

To create a private-public key pair you simply must use the `ssh-keygen` command on the command line on Linux. On Windows, the same command can be used from within [Git Bash](Git_Bash_Windows_Installation.md).

```
$ ssh-keygen
```

This command will ask you to specify a filename for the generated private-public key pair. Just press **Enter** to accept the default name. The command will then ask you for a passphrase. Again press **Enter** twice to avoid creating a passphrase. The command will create two files in a `.ssh` directory in your home directory: `id_rsa` and `id_rsa.pub`. These are both text files containing the private (`id_rsa`) and public (`id_rsa.pub`) keys.

Once the key pair is created, you must log in to the Git hosting service for which you wish to set up SSH access. In the **personal user settings** of the website, there should be a page to add SSH keys. Note, SSH keys are added to and associated with your personal account with the hosting service, not to any specific repository. Once at the SSH keys page, adding a key should be straight forward. Give the key a descriptive name describing the computer/user that the key is for (e.g. `MMRoboticsLabDeskWindows`, `MMRoboticsLabDeskUbuntu`, `MMRoboticsHelmholtzCoilsComputer`, etc.). Then copy the entire contents of `id_rsa.pub` into the key field. Once you have done this, you should be able to use SSH to interact with any repositories your hosting service account has access to.

Note that the first time you interact with a Git hosting service using SSH from a particular computer user, SSH will ask about the authenticity of the web server it is interacting with. Simply type **yes** and press **Enter** when this occurs. This authenticity request will only happen once.

---
## Using Multiple Accounts of a Git Hosting Service from the Same Operating System User on the Same Computer

Git hosting services typically don't allow you to add the same public key to
multiple accounts on the same hosting service. This is probably because the public key is likely also being used
by the hosting service to determine which hosting service account has initiated a Git network
transaction and thereby determine what permissions that account has (see
[Q & A](#QAndA)). Regardless, if you have multiple accounts with the same Git hosting
service (e.g. two GitHub accounts or two Bitbucket accounts) and you want to work
with repositories associated with two or more of these accounts from the same operating system
user on the same computer, the correct SSH key must be used for each account. By
default, Git and SSH won't know which SSH key to use when performing network
transactions and will use the default key associated with the operating system user.
This will cause authentication errors for the accounts not associated with the default
key.

There are two ways of handling this scenario: Using custom hosts with your SSH
config file or using conditional includes with your Git config file.

>Note that this problem will not arise if each operating system user on a particular
computer only interacts with repositories from **one** account from each Git hosting
service. This is part of why it is recommended to create your own operating system level user on each of the lab computers you are actively using. Doing so will also help avoid forgetting to update the `user.name` and `user.email` Git config variables when committing to repositories associated with two different accounts.

### Using Custom Hosts with Your SSH Config File

The idea here is to define host aliases (custom hosts) that have specific
identification files (SSH keys) associated with them. This method affects the
behavior of SSH overall, not just when Git uses SSH to perform a network
transaction. It does not affect how Git specifically behaves.

1. Generate SSH key pairs for all Git hosting accounts and add the public keys to
   each account on the hosting service like you normally would. Make sure each key
   pair has a unique name that helps identify what account it is for. You can chose
   one account to use the default `id_rsa` key if you like.

2. Create (or edit) the SSH configuration file `~/.ssh/config`. The basic format for
   a custom host is:
   ```
   Host {host-alias}
       HostName {actual-hostname}
       IdentityFile {path/to/private/key/file}
       IdentitiesOnly yes
   ```
   The alias `{host-alias}` can be anything you want, but there are two conventions
   people use:
   ```
   {actual-hostname}-{username}
   {username}.{actual-hostname}
   ```
   Let's assume you have two GitHub accounts: `mainuser` and `otheruser`. On
   GitHub.com, we've also assigned the `id_rsa` public key to the `mainuser` account
   and an `otheruser_key` public key to the `otheruser` account. We could then put
   the following in `~/.ssh/config`.
   ```
   # mainuser Account
   Host github.com
       HostName github.com
       IdentityFile ~/.ssh/id_rsa
       IdentitiesOnly yes

   # otheruser Account
   Host github.com-otheruser
       HostName github.com
       IdentityFile ~/.ssh/otheruser_key
       IdentitiesOnly yes
   ```

3. Once the configuration is set, the specified key will be used whenever you use a
   particular alias:
   ```
   git clone git@github.com:mainuser/repository.git
   git clone git@github.com-otheruser:otheruser/repository.git 
   ```
   The first `git clone` will use `id_rsa` for authentication and the second
   `git clone` will use `otheruser_key` for authentication. In both cases, the part 
   between `@` and `:` will be replaced by SSH with `github.com` because that is
   what is set for `HostName` for both aliases in `~/.ssh/config`, which is good
   because that is the actual hostname for GitHub. Keep in mind that
   `github.com-otheruser` is an **alias** and not a real hostname on the internet.
   Also keep in mind that in this example `github.com` is serving as an alias as
   well as a real world hostname; it just happens that this particular alias
   matches the actual hostname assigned to it.

4. Existing repositories should also use the custom host aliases. These can be
   updated using `git remote set-url`. For example:
   ```
   git remote set-url origin git@github.com-otheruser:otheruser/repository.git
   ```

5. Since the Git hosting service uses the email on each commit to determine which
   account to associate with the commit, you'll want to make sure the `user.email` Git
   configuration variable is set correctly for each repository:
   ```
   cd mainuser-repository
   git config user.name "Your Name"
   git config user.email "mainuser@email.com"

   cd otheruser-repository
   git config user.name "Your Name"
   git config user.email "otheruser@email.com"
   ```
   Notice the absence of the `--global` flag in each `git config` command. This
   sets the local configuration for each repository specifically. An alternative to
   setting the local Git configuration for each repository is to use "*conditional
   includes*" which are discussed next.

Source Blog: [Setting up multiple GitLab accounts](https://medium.com/uncaught-exception/setting-up-multiple-gitlab-accounts-82b70e88c437)

### Using Conditional Includes With Your Git Config File

The idea here is to override the default flags Git uses when it calls the SSH
command for performing network transactions. This is done by modifying your Git
config file using *conditional includes*. This method will not affect SSH behavior
overall, it will only affect SSH behavior when Git uses it with certain
repositories.

1. Generate SSH key pairs for all Git hosting accounts and add the public keys to
   each account on the hosting service like you normally would. Make sure each key
   pair has a unique name that helps identify what account it is for. You can chose
   one account to use the default `id_rsa` key if you like.

2. Modify the Git config file `~/.gitconfig`. Let's assume you have two GitHub
   accounts: `mainuser` and `otheruser`. On GitHub.com, we've also assigned the
   `id_rsa` public key to the `mainuser` account and an `otheruser_key` public key
   to the `otheruser` account. Since `id_rsa` is a default key, we only need to set
   up Git to use a different key when we are using a repository associated with the
   `otheruser` account. We could do this by putting the following in `~/.gitconfig`.
   ```
   [includeIf "gitdir:/path/to/otheruser/repository/"]
       [core]
           sshCommand = "ssh -i ~/.ssh/otheruser_key"
   ```
   The `[includeIf]` block makes Git override the global configuration when working
   with the repository at `/path/to/otheruser/repository/`. In this case it
   overrides the `core.sshCommand` Git config variable. This allows us to add the
   `-i` flag to the `ssh` command Git uses when performing network transactions for
   this repository. The `-i` flag takes the path to a private key file
   (identification file) to use for that particular SSH instance.
   The `[includeIf]` block will actually apply to all repositories in the directory
   of its argument if it ends in a `/`, so you could put all the repositories
   associated with the `otheruser` account into the same directory, thus avoiding a
   conditional include block for every `otheruser` repository on your computer. For
   example, if we put all the `otheruser` repositories into
   `~/otheruser-repositories/`:
   ```
   [includeIf "gitdir:~/otheruser-repositories/"]
       [core]
           sshCommand = "ssh -i ~/.ssh/otheruser_key"
   ```
   All repositories inside `~/otheruser-repositories/` will use the `otheruser_key`
   SSH key while all repositories outside the `~/otheruser-repositories/`
   directory will use the default Git configuration and therefore the default
   `id_rsa` SSH key. Therefore, repositories associated with the `mainuser` account
   are set up by default.

3. Since the Git hosting service uses the email on each commit to determine which
   account to associate with the commit, you'll want to make sure the `user.email` Git
   configuration variable is set correctly for each repository. This is set globally with:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "mainuser.email.com"
   ```
   this sets up the correct email when working with `mainuser` associated
   repositories. We then override the global configuration for `otheruser` associated
   repositories by adding to the `[includeIf]` block:
   ```
   [includeIf "gitdir:~/otheruser-repositories/"]
       [user]
           email = "otheruser@email.com"
       [core]
           sshCommand = "ssh -i ~/.ssh/otheruser_key"
   ```

Blog Source: [Setting up multiple GitHub accounts, the nicer way](https://dev.to/arnellebalane/setting-up-multiple-github-accounts-the-nicer-way-1m5m)

---
## Q & A
<a name="QAndA"></a>

**Why do GitHub and Bitbucket use the `git` user when using SSH (e.g. `git@github.com`)?**

The `git` user is an operating system level user. The custom Git service that is
running on the server is set up such that the `git` operating system user has
permission to interact with the Git service only. In other words, your GitHub or
Bitbucket account is not set up as an operating system level user such that you can log
into the server via SSH. Everyone uses the `git` user. See
[here](https://superuser.com/questions/1268850/why-does-ssh-to-github-require-the-git-user).

**If everyone uses the `git` user, then how does GitHub or Bitbucket know who I am and what repositories I have access to?**

I'm pretty sure the Git service on each of these platforms is set up to use the
public SSH authentication key to determine which user has made the request and
determine access permissions.