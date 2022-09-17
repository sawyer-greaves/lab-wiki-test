[Home](../Home)
# CMake

>**IMPORTANT:** Although CMake will greatly simplify the process of building C/C++ projects for you, it is highly recommended that you have a strong understanding of how C/C++ programs are structured and built (e.g. compiling and linking) before you attempt to learn and use CMake. Ideally you should have at least some exposure to compiling and linking C/C++ programs by invoking the compiler/linker from the command line. It will also be tremendously helpful if you understand on a high level what [Make and Makefiles](https://www.gnu.org/software/make/) are and how they are used to build source code. 

CMake is a tool to manage building of source code. Originally, CMake was designed as a generator for various dialects of [Makefile](https://www.gnu.org/software/make/), today CMake generates modern buildsystems such as `Ninja` as well as project files for IDEs such as Visual Studio and Xcode.

CMake is widely used for the C and C++ languages, but it may be used to build source code of other languages too. It is a common misconception that the "C" in "CMake" refers to the C and C++ languages. In fact, the "C" stands for *cross-platform*.

**Contents**

[TOC]

---
## Official CMake Resources

- [CMake Website](https://cmake.org/)
- [CMake Documentation and Training Materials](https://cmake.org/documentation/)
    - [CMake Reference Documentation](https://cmake.org/cmake/help/latest/)
    - [Mastering CMake Book](https://cmake.org/cmake/help/book/mastering-cmake/)
    - [User Interaction Guide](https://cmake.org/cmake/help/latest/guide/user-interaction/index.html)
        - If you just want to learn how to build a source code package you downloaded from the internet
    - [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
        - If you want to learn how to create your own project using CMake
    - [Using Dependencies Guide](https://cmake.org/cmake/help/latest/guide/using-dependencies/index.html)
        - If you want to learn how to use a third-party library
    - [cmake-packages(7) manual](https://cmake.org/cmake/help/latest/manual/cmake-packages.7.html)
        - Explains how to create packages which can easily be consumed by other CMake-based projects
- [CMake Discourse Forum](https://discourse.cmake.org/) is a place to ask for help with CMake
- [CMake FAQ page](https://gitlab.kitware.com/cmake/community/-/wikis/FAQ)
- [CMake Wiki Page](https://discourse.cmake.org/)
- Source code is found in the [CMake/CMake](https://gitlab.kitware.com/cmake/cmake) repository on GitLab

---
## Third-Party Learning Resources

### Books

- [Professional CMake Reference Textbook](Professional_CMake_11th_Edition.pdf)
    - A complete learning and reference textbook
- Modern CMake Book - [Web](https://cliutils.gitlab.io/modern-cmake/) or [PDF](Modern_CMake.pdf)
    - A shorter learning textbook
    - The book is meant to be a living document online so the web link should be the most up-to-date way to access the book. A PDF copy has been added to the wiki for convenience.

### Tutorials

- [HSF CMake Tutorial](https://hsf-training.github.io/hsf-training-cmake-webpage/)
- [C++ Weekly - Intro to CMake](https://www.youtube.com/watch?v=HPMvU64RUTY) video introduction by Jason Turner
    - This introduction assumes quite a bit of existing C/C++ experience