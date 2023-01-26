[Home](../Home)
# Qt Application Framework and Qt Creator

Qt is pronounced "*cute*", not "*cue tee*".

>**IMPORTANT:** A good understanding of [C++](C_and_Cpp.md) and [CMake](CMake.md) is a prerequisite for learning and using Qt!

**Contents**

[TOC]

---
## Introduction

Qt is a cross-platform **C++ framework** and a bunch of related **tools**. A *framework* is similar to a *library* in that it contains reusable code that you can use in your own project to avoid the need to write it yourself, but a framework is more than that. Whereas a library contains functionality you'd like to add to your application, a framework provides a skeleton for the entire application itself. The framework will typically define the structure and flow of an application and allow you specific ways to add the "meat" (i.e., what the application actually does).

The Qt Framework is an event driven framework that contains lots of useful features for easily creating graphical user interfaces (GUIs) although the framework can absolutely be used without the GUI features. It also contains a modular method for C++ classes to talk to each other called *signals and slots*. The Qt Framework is divided into many *modules* that can be selectively imported into your project. The modules of most interest are: [Qt Core][core], [Qt GUI][gui], [Qt Widgets][widgets], and [Qt Serial Port][serial]. Note that contrary to the name, Qt Widgets will typically be the module used most often to make simple GUIs, not Qt GUI. There are many other modules so be sure to check if Qt implements a functionality you want before looking elsewhere.

Qt also consists of a variety of tools to compliment the framework. Most of these tools are for tasks that are outside the scope of what we do in our research lab and can be ignored. However, a few are very important. [Qt Creator][creator] is an integrated development environment (IDE) for writing, building, and running your code, similar to Visual Studio, Visual Studio Code, the Arduino IDE, etc. Although it is absolutely possible  and easy to use something other than Qt Creator to write code that utilizes the Qt Framework, Qt Creator is recommended for beginners to Qt.

The links below can be used to explore the features/modules of the Qt Framework and its associated tools.

- [Qt Main Page][mainpage]
- [Qt Feature Overview][features]

---
## The Build Process for Qt-based Projects

Qt-based projects can be built using the [CMake](CMake.md) build system. In fact, CMake is the official build system as of Qt 6. Under CMake, your *project file* (the file describing the source files that make up your project, how to build them, and which libraries and Qt Framework modules to link to) is a simple `CMakeLists.txt` file. There are official CMake variables for configuring Qt-based projects (see the *Learning the Qt Framework and Qt Creator* section).

Although CMake can be used with Qt versions before Qt 6, the official build system before Qt 6 (Qt 5 and earlier) is [qmake][qmake]. qmake is similar to CMake but the project file has a `.pro` extension and its content uses a different syntax specific to qmake. Since CMake is now the official build system for Qt, **it is recommended to avoid qmake in favor of CMake for all new projects, even Qt 5 projects**. qmake is mentioned here because you may encounter older projects that still use it. Thus you should be familiar with qmake so you know how to identify qmake projects and have an idea of what to learn if you need to work with them or convert them to CMake projects.

You may wonder why we have to use CMake (or qmake) at all. Is CMake necessary to build a Qt-based project? The answer is no, but it tremendously simplifies the process. Compiling a Qt-based project is more involved than compiling a standard C++ project. The Qt Framework does a number of things to implement its features that require your source files to undergo preliminary processing before they are fed to the compiler. This preliminary processing actually generates code for you! The  programs that perform this preprocessing are the [Meta-Object Compiler][moc] (`moc`), the [User Interface Compiler][uic] (`uic`), and the [Resource Compiler][rcc] (`rcc`). The `moc` takes your header files as input and produces source files with auto-generated code that implements features like the signals and slots mechanism. Qt Creator has a GUI design feature that allows you to design a GUI using a GUI (i.e., you can pick and place widgets like buttons, check boxes, etc.). This graphical GUI designer produces an XML file with a `.ui` extension. Since the `.ui` file is not C++ code, the `uic` takes a `.ui` file as input and produces its C++ code equivalent. You are unlikely to need the `rcc` but should be aware of it nonetheless. If you want to compile a Qt-based project manually, you will need to make sure to run these preprocessing steps on the necessary files in addition to the normal compilation steps. That gets complicated fast. CMake (and qmake) has functionality you can enable that automatically identifies the files that need to undergo this preprocessing and performs it for you so you don't have to think about it.

---
## Installing the Qt Framework and Qt Creator

### Prerequisites for Linux

On Linux, neither the Qt Online Installer nor the Qt packages in the Ubuntu repositories come with a C++ compiler. You will need to separately install the GNU `gcc` compiler, `make` program, and other packages for software development. In addition, some Qt modules for graphical applications require the OpenGL libraries and headers to be installed. Before installing Qt and Qt Creator, you'll want to install the `build-essential` and `libgl1-mesa-dev` packages:
```
sudo apt install build-essential libgl1-mesa-dev
```

### Installing With the Qt Online Installer **(Recommended Method)**

The Qt Company recommends to install Qt and Qt Creator using the Qt Online Installer application from [the Qt website][mainpage]. The benefit of using this installer is that you can install any version of Qt you like and multiple versions can exist on your system without conflict. You can also install/update or uninstall versions later whenever you wish using the Qt Maintenance Tool (installed with Qt). The download for the online installer can be tricky to find on their website. You want to go for the open source options wherever possible. As of the writing of these instructions, the following steps can get you to the correct download page:

1. Click *Download. Try.* on the top right of the [qt.io][mainpage] main page.
2. Click *Go open source* in the "Downloads for open source users" section.
3. Scroll to near the bottom and click on *Download the Qt Online Installer* in the middle of the page.
4. You should now be at the download page. Download the Qt Online Installer for your platform.

Run the installer and follow the instructions. **Below are some specific instructions as you go though the process. Please follow them!**

1. **(Linux)** There may be a few extra steps to run the installer:
    - The downloaded installer file may need to be set as executable using `chmod +x <file_name>` before you are able to run it with `./<file_name>`.
    - You may need to install the `libxcb-xinerama0` package using `sudo apt install libxcb-xinerama0` before the installer will run. You will know the package needs to be installed if you get an error similar to:
        ```
        error while loading shared libraries: libxcb-xinerama.so.0: cannot open shared object file: No such file or directory
        ```
1. The Qt Online Installer doesn't really configure things correctly to perform an installation for the entire system (i.e., to install it once for all users). The installer is pretty much configured to install on a per-user basis. Furthermore, the online installer requires you to create an account with Qt. The Qt Maintenance Tool will also cache your login information and auto-populate these fields when you start it. With these facts in mind, make sure the installation directory is set as follows:
    - **Install Directory On Windows:** `C:\Users\your_user_folder\Qt`
        - Replace `your_user_folder` with the name of the folder associated with your user account (e.g., `C:\Users\John\Qt`).
        - Note that the above recommended directory is not the default used by the online installer on Windows (the default directory happens to be `C:\Qt`). **You will need to change the install directory from the default to the recommended directory.**
    - **Install Directory on Linux:** `/home/your_user_folder/Qt`
        - Replace `your_user_folder` with the name of the folder associated with your user account (e.g., `/home/john/Qt`).
        - This is the default directory for the online installer on Linux.
2. Choose a *Custom Installation*.
    - Choosing a custom installation allows you to specify exactly what you want to install. There are a huge number of components you could potentially install and you likely won't use most of them. This way you can reduce the size of the installation (which is helpful since having per-user installations means the files will be duplicated for every user that has Qt installed) and you can always use the Qt Maintenance Tool to add components later should you decide they are needed.
    - The following are recommendations for your installation:
        - Whether installing Qt 5 or Qt 6 (or both), select the latest version within each major version (e.g., the latest version of Qt 5 is 5.15).
        - Within a given version of Qt, **don't install**:
            - Components marked as deprecated
            - WebAssembly (unless you specifically need it)
            - Android (unless you specifically need it)
            - Prebuilt components for compilers you don't have or intend to use (e.g., on Windows, if you are only going to use the MinGW compiler that comes with Qt, you can avoid installing prebuilt components for MSVC and UWP)
            - 32-bit components (just stick with 64-bit components)
        - **(Windows)** Install the MinGW compiler which is found in the *Developer and Designer Tools* section (it is recommended to install the version(s) associated with your selected MinGW Qt components). This way you don't need to install a compiler separately (e.g., installing MSVC or UWP compilers by installing Visual Studio).
        - Install CMake and Ninja from the *Developer and Designer Tools* section.

Once the installation is complete you may delete the Qt Online Installer executable file. The Qt Maintenance Tool will be used to manage your Qt installation in the future.

### Installing on Ubuntu using the Ubuntu Package Repositories and APT

It is recommended that you use the Qt Online Installer (see above) even on Ubuntu. However, for the sake of completeness and for reasons described in the *A Note About Qt Creator On Ubuntu Older Than 20.04* section, instructions for installing Qt using the Ubuntu Package Repositories and `apt` are given here. Note that using the Ubuntu Package Repositories means you will not be able to select your version of Qt and therefore will not have access to features or bug fixes introduced in later versions. This method will install Qt and Qt Creator for your entire system (unlike the Qt Online Installer which does a per-user installation). Note that installations from APT and the Qt Online Installer can coexist on your system.

#### Installing Qt 5

1. Install the Qt 5 Framework:
    ```
    sudo apt install qt5-default
    ```
2. Install Qt Creator
    ```
    sudo apt install qtcreator
    ```
3. **(Optional)** Install Qt and Qt Creator documentation
    ```
    sudo apt install qt5-doc qtbase5-doc-html qtcreator-doc
    ```

#### Installing Qt 6
Note that Qt 6 does not exist in the Ubuntu Repositories until Ubuntu 22.04 or later.

1. Install the Qt 6 Framework:
    ```
    sudo apt install qt6-base-dev
    ```
2. Install Qt Creator
    ```
    sudo apt install qtcreator
    ```
3. **(Optional)** Install Qt Creator documentation
    ```
    sudo apt install qtcreator-doc
    ```

### A Note About Qt Creator On Ubuntu Older Than 20.04

Qt 6 requires Ubuntu 20.04 or newer and Qt Creator version 6 or newer depends on Qt 6. The Qt Online Installer always installs the newest version of Qt Creator so if you have any version of Ubuntu older than Ubuntu 20.04, you will want to install Qt Creator from the Ubuntu Package Repositories using `apt` (see above). You will probably want to install Qt 5 with `apt` as well and forgo using the Qt Online Installer entirely. If you need a different Qt 5 version than the version provided by the Ubuntu repositories, you can use the online installer to install it. Keep in mind you will still need to install Qt Creator through the Ubuntu repositories and you will need to manually add the newly installed version of Qt (installed with the online installer) to your kits in Qt Creator (see the *Qt Creator Project Configuration and Kits* section below). The versions of Qt installed through the online installer will not automatically appear in Qt Creator because the online installer is not aware of your Qt Creator installation from the Ubuntu Package Repositories.


---
## Learning the Qt Framework and Qt Creator

The documentation offered by Qt is one of the best ways to learn the Qt Framework and Qt Creator. Below is a link to the documentation, along with a list of the most important topics to learn. Qt is vast and you don't need to learn everything it has to offer, but you definitely need to learn the core concepts.

>**Note:** Whenever viewing the Qt documentation, make sure to set the documentation to the version of Qt you are using. Currently, this is done using a dropdown at the top of the navigation tree on the left side of the page.

**Learning Resources from Qt**

- [Qt Documentation][docs]
- [Build with CMake][cmake_and_Qt]
    - A guide on how to use CMake to build Qt-based projects.
- Other Qt Build Tools
    - [qmake][qmake]
    - [Meta-Object Compiler (moc)][moc]
    - [User Interface Compiler (uic)][uic]
    - [Resource Compiler (rcc)][rcc]
- [Qt Creator][creator]
    - You should understand what [kits][kitsdef] are and how to create/edit them and you should understand how to configure a project properly. All of this is covered in the Qt Creator Manual but is also covered in the *Qt Creator Project Configuration and Kits* section below for convenience. The more familiar you are with your IDE, the smoother the programming process becomes.
- [Getting Started][getstarted]
- [Supported Platforms][platforms]
- [Important Core Concept Overviews][overviews]
    - [Core Internals][coreoverview]
        - The **most important** concepts to learn. It is vital that you understand the Object Model, Object Tree, the QObject class, the Meta-Object System, the Event System, the Signals and Slots System, Timers, and Container Classes. It is also vital to become familiar with and read the Detailed Description for the [QCoreApplication][QCoreApp], [QApplication][QApp], and [QEvent][Qevent] classes. You will also want to learn the Threading topic as well. The Property System is much less important than the other topics.
    - [User Interfaces][uioverview]
        - Focus on Qt Widgets. Qt Widgets is for desktop UIs (Qt Quick is geared more toward touch screen UIs).
    - [Development Tools][devtools]
    - [Data Storage][datastorage]
        - I/O and working with files.
- [Qt Framework Modules][modules]
    - [Qt Core][core]
    - [Qt GUI][gui]
    - [Qt Widgets][widgets]
    - [Qt Serial Port][serial]
    - [All Qt Classes][classes]
- [Qt Forum][forum]
    - A forum for talking about Qt.
- [Qt Wiki][wiki]
    - A wiki created and maintained by the community.

**Other Resources**

- In-Depth Meta-Object Compiler and Signals and Slots
    - [Inside the Qt Object Model](https://www.youtube.com/watch?v=9gVd4hLSnUY&t=1081s) - Talk from CppCon 2017
        - Explains how events and signals and slots work! **A must watch**.
    - [DIY moc](https://www.youtube.com/watch?v=rtIBjTPE45Q) - Talk from Qt Developer Days 2014


---
## Qt Creator Project Configuration and Kits

In the context of Qt Creator, project configuration refers to specifying a build directory for each build configuration in your project. It also refers to making a selection for the Qt Framework version, the compiler executable, the debugger executable, and the CMake executable to use with the project. A Qt Creator **kit** is a predefined set of selections for these items.

There are tabs within the options menus of Qt Creator that display the catalog of installed Qt versions, C++ compilers, debuggers, and CMake executables available for creating new kits. When Qt Creator is installed, it attempts to auto-populate these catalogs by inspecting your system. This process sometimes misses installed items. In this case, you will need to add them manually to Qt Creator's catalog if you want to use them in a kit. You will also need to manually add items if you install them after installing Qt Creator. Fortunately, Qt Creator has an option to re-detect compilers which should make adding these items easier.

The entire project configuration is saved in a file with the same name as the project file (including its extension) with `.user` appended to it (e.g., `CMakeLists.txt.user` for CMake-based project files and `myproject.pro.user` for qmake-based project files). This file is saved in the same directory as the project file. The `.user` files should be **excluded** from Git repositories as these files often contain hardcoded paths and therefore will often not work on other computers or with other users. When you open an existing project with Qt Creator and it doesn't find a `.user` file (which should always be the case the first time you open a project from a newly cloned repository), Qt Creator will ask you to configure the project. Thanks to kits, this configuration simply involves selecting a kit and confirming that the build directory for each build configuration is acceptable. Therefore, make sure you have an appropriate kit configured before you try to open a project that does not have a `.user` file in Qt Creator.

Note that for CMake-based projects, Qt Creator will automatically put the path to the Qt version of the selected kit into the `CMAKE_PREFIX_PATH` CMake variable so CMake should automatically find the correct Qt version to build against.


[mainpage]: https://www.qt.io/
[features]: https://www.qt.io/product/features
[modules]: https://doc.qt.io/qt-6/qtmodules.html
[core]: https://doc.qt.io/qt-6/qtcore-index.html
[gui]: https://doc.qt.io/qt-6/qtgui-index.html
[widgets]: https://doc.qt.io/qt-6/qtwidgets-index.html
[serial]: https://doc.qt.io/qt-6/qtserialport-index.html
[classes]: https://doc.qt.io/qt-6/classes.html
[creator]: https://doc.qt.io/qtcreator/index.html
[kitsdef]: https://doc.qt.io/qtcreator/creator-glossary.html#glossary-buildandrun-kit
[qmake]: https://doc.qt.io/qt-6/qmake-manual.html
[moc]: https://doc.qt.io/qt-6/moc.html
[uic]: https://doc.qt.io/qt-6/uic.html
[rcc]: https://doc.qt.io/qt-6/rcc.html
[docs]: https://doc.qt.io/
[cmake_and_qt]: https://doc.qt.io/qt-6/cmake-manual.html
[getstarted]: https://doc.qt.io/qt-6/qt-intro.html
[platforms]: https://doc.qt.io/qt-6/supported-platforms.html
[overviews]: https://doc.qt.io/qt-6/overviews-main.html
[devtools]: https://doc.qt.io/qt-6/topics-app-development.html
[uioverview]: https://doc.qt.io/qt-6/topics-ui.html
[coreoverview]: https://doc.qt.io/qt-6/topics-core.html
[datastorage]: https://doc.qt.io/qt-6/topics-data-storage.html
[QCoreApp]: https://doc.qt.io/qt-6/qcoreapplication.html
[QApp]: https://doc.qt.io/qt-6/qapplication.html
[QEvent]: https://doc.qt.io/qt-6/qevent.html
[forum]: https://forum.qt.io/
[wiki]: https://wiki.qt.io/Main