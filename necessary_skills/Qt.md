[Home](../Home)
# Qt Application Framework

Qt is pronounced "cute" not "cue tee".

## Installing the Qt Framework and Qt Creator

### Installing Using the Qt Online Installer

The Qt Company recommends to install Qt and Qt Creator using the Qt Online Installer application from [the Qt website][1]. The benefit of using this installer is that you can install any version of Qt you like and multiple versions can exist on your system without conflict. You can also install/update or unistall versions later whenever you wish using the Qt Maintenance Tool (installed with Qt). This installer can be tricky to find on their website. You want to go for the open source options wherever possible. As of the writing of these instructions, the following steps can get you to the correct download page:

1. Click *Download. Try.* on the top right of the [qt.io][1] main page.
2. Click *Go open source* in the "Downloads for open source users" section.
3. Scroll to near the bottom and click on *Download the Qt Online Installer* in the middle of the page.
4. You should now be at the download page. Download the Qt Online Installer for your platform.

Run the installer and follow the instructions. **Below are some specific instructions as you go though the process. Please follow them!**

1. The Qt Online Installer doesn't really configure things correctly to perform an installation for the entire system (i.e. to install it for every user). The installer is pretty much configured to install on a per-user basis. Furthermore, the online installer requires you to create an account with Qt. The Qt Maintenance Tool will also cache your login information and auto-populate these fields when you start it. With these facts in mind, make sure the installation directory is set as follows:

    - **Install Directory On Windows:** `C:\Users\your_user_folder\Qt`
        - Replace `your_user_folder` with the name of the folder associated with your user account (e.g. `C:\Users\John\Qt`).
        - Note that the above recommended directory is not the default used by the online installer on Windows (which happens to be`C:\Qt`). **You will need to change the install directory from the default to the recommended directory.**
    - **Install Directory on Linux:** `/home/you_user_folder/Qt`
        - This is the default directory for the online installer on Linux.
2. Choose a *Custom Installation*.
    - Choosing a custom installation allows you to specify exactly what you want to install. There are a huge number of components you could potentially install and you likely won't use most of them. This way you can reduce the size of the installation (which is helpful since having per-user installations means the files will be duplicated for every user that has Qt installed) and you can always use the Qt Maintenance Tool to add components you decide you need later.
    - The following are recommendations for your installation:
        - Whether installing Qt 5 or Qt 6 or both, select the latest version within that major version (e.g. the latest version of Qt 5 is 5.15).
        - Within a given version of Qt, **don't install**:
            - Components marked as deprecated
            - WebAssembly (unless you specifically need it)
            - Android (unless you specifically need it)
            - Prebuilt components for compilers you don't have or intend to use (e.g. if you are only going to use the MinGW compiler that comes with Qt, you can avoid installing prebuilt components for MSVC and UWP)
            - 32-bit components (just stick with 64-bit components)
        - Install the MinGW compiler (found in the *Developer and Designer Tools* section, the version(s) associated with your selected MinGW Qt components is recommended). This way you don't need to install a compiler separately (e.g. installing MSVC or UWP compilers by installing Visual Studio).
        - Install CMake and Ninja

Once the installation is complete you may delete the Qt Online Installer. The Qt Maintenance Tool will be used to manage your Qt installation in the future.

### Installing on Ubuntu using the Ubuntu Package Repositories and APT

It is recommended that you use the Qt Online Installer (see above) even on Ubuntu. However, for the sake of completeness and for reasons described in the next section, instructions for installing Qt using the Ubuntu Package Repositories and `apt` are given here. Note that using the Ubuntu Package Repositories means you will not be able to select your version of Qt and will not have access to bug fixes found in later versions.

1. 

### A Note About Qt Creator On Ubuntu Older Than 20.04

Qt 6 requires Ubuntu 20.04 or newer and Qt Creator version 6 or newer depends on Qt 6. The Qt Online Installer always installs the newest version of Qt Creator so if you have any version of Ubuntu older than Ubuntu 20.04, you will want to install Qt Creator from the Ubuntu Package Repositories using `apt` (See above). You will probably want to install Qt 5 with `apt` as well and forgo using the Qt Online Installer entirely. If you need a different Qt 5 version than the version provided by the Ubuntu repositories, you can use the online installer to install it. Keep in mind you will still need to install Qt Creator through the Ubuntu repositories and you will need to manually add the newly installed version of Qt (installed with the online installer) to your kits in Qt Creator. The versions of Qt installed through the online installer will not automatically appear in Qt Creator because the online installer is not aware of your Qt Creator installation for the Ubuntu Package Repositories.

[1]: https://www.qt.io/