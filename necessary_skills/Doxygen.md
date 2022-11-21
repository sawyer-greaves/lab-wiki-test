[Home](../Home)
# Doxygen

**Contents**

[TOC]

## Introduction

Doxygen is a documentation generator and static analysis tool for software source trees. When used as a documentation generator, Doxygen extracts information from specially-formatted comments within the code. When used for analysis, Doxygen uses its parse tree to generate diagrams and charts of the code structure. Doxygen can cross reference documentation and code, so that the reader of a document can easily refer to the actual code.

Documentation generation with Doxygen is tremendously easy. All you need to do is write good specially-formatted comments in your code and then run Doxygen on your source files to produce nicely formatted documentation in formats such as HyperText Markup Language (HTML), Microsoft Compiled HTML Help (CHM), Rich Text Format (RTF), Portable Document Format (PDF), LaTeX, PostScript or man pages. The HTML format is likely the most useful format because it creates a local browsable website that's similar to web-based documentation you have likely encountered previously. Examples of software that uses Doxygen for its online documentation include [OpenCV](https://docs.opencv.org/4.x/), [Eigen](https://eigen.tuxfamily.org/dox/), and the [rclcpp](https://docs.ros2.org/latest/api/rclcpp/) library from ROS 2.

Programming languages supported by Doxygen include C, C++, C#, Python, Fortran, Java, and a few others. Other languages can be supported with additional code.

Doxygen has built-in support to generate inheritance diagrams for C++ classes which can be tremendously helpful for understanding the structure of a code base. For more advanced diagrams and graphs, Doxygen can use the `dot` tool from [Graphviz](https://graphviz.org/). Doxygen can also be easily invoked automatically with [CMake](CMake.md) as part of the build process.

## Learning Doxygen

Learning Doxygen is a matter of learning the simple special formatting to use in the comments in your code and learning how to invoke Doxygen to generate the documentation. Similar to Git, Doxygen is a command-line program called `doxygen`, but comes with a graphical user interface called `doxywizard`. The Doxygen website contains everything you need to get started. The recommended place to start is the Doxygen manual. Note that on **Linux**, the easiest way to install Doxygen is using `apt`
```
sudo apt install doxygen
```

- [Doxygen Home Page](https://www.doxygen.nl/index.html)
- [Doxygen Downloads Page](https://www.doxygen.nl/download.html)
- [Doxygen Manual](https://www.doxygen.nl/manual/index.html)