[Home](../Home)
# C/C++ Programming Language

**Contents**

[TOC]

---
## Introduction

The C/C++ (pronounced "cee" and "cee plus plus") programming languages are very popular in robotics, especially for writing software that interacts more directly with hardware (e.g. for writing a robot or camera driver). The reason for this popularity is that C/C++ programs are compiled rather than interpreted like MATLAB or Python. This means programs often execute much faster than MATLAB and Python. These languages are also very well established with a large ecosystem of libraries and support. C++ is one of the two main languages supported directly by ROS.

C/C++ is quite a bit more difficult to become proficient with when compared to MATLAB or Python, but there exist a large number of free online learning resources. This page is intended to provide you with the resources necessary to become proficient with C/C++ and to point out important topics people often neglect that usually leads to a lot of unnecessary confusion and frustration.

---
## How To Learn C/C++

We use the term **C/C++** to refer to two similar languages: C and C++. C++ is a language based on C that adds important features like object-oriented programming and templates (you may have never heard of these features, but you will learn about them soon). Although it is not completely true, you can consider C++ to be a superset of C and therefore if you learn C++, you'll pretty much be learning C at the same time. Thus, we focus on learning C++ here.

Learning C++ consists of three equally important pillars:

- **Pillar 1:** Understand how C++ programs are **compiled** and understand the structure of C++ source code and library files themselves.
- **Pillar 2:** Understand the C++ **language** (i.e. the syntax and language features).
- **Pillar 3:** Understand the C++ **Standard Library**.

It is common for people learning C++ to primarily focus on the language syntax itself (pillar 2 above) because this is arguably sufficient when you're working with MATLAB or Python, but these people quickly realize that this is not enough to feel confident writing programs in C++. There is some overlap between the pillars which means you can't really learn them in sequence, so the point here is that you are aware of them and that you are giving each of them enough attention in your learning. Let's examine each pillar individually.

### Pillar 1: Compilation and Source Code Structure

This pillar is the most often neglected and therefore the source of the most confusion/frustration for beginners. The reason for this is that the compilation of your program *can* be set up once and never thought about again. This makes it tempting to develop an attitude of "I don't care or need to know how the program compiles, I just need to get this code running because I've got a deadline." This attitude is fine most of the time, until you need to use a third-party library to do some task you don't want to implement yourself. Then a task that you think should be simple (which it is if you know what you're doing) turns into a problem you waste a lot of time fixing. Further, once you've fixed it, you likely didn't really learn anything for next time and the cycle repeats later.

Here is a list of topics you should make sure to understand:

- The stages of compilation: *preprocessing*, *compiling*, *assembling*, *linking*
    - The types of input and output files for each stage of compilation
- Types of C++ source files
    - Header files, `.h`
    - Source files, `.cpp`
- The purpose of header files and what should go in header files
- The purpose of source files and what should go in source files
- *Including* a header file in a source file or another header file
- The concept of a *translation unit*
- What files constitute a library and what they're all for
- Types of library files and the role they play in compilation/linking
    - Static library files, `.a` on Linux and `.lib` on Windows 
    - Dynamic library files, `.so` on Linux and `.dll` on Windows (on Windows there is also another file necessary to use `.dll` files that has the same `.lib` extension as static library files)
- How to link against a library
- Build systems (their purpose and how to use them) with particular focus on learning [CMake](CMake.md) and obtaining at least a high-level understanding of [Make and Makefiles](https://www.gnu.org/software/make/).


Unfortunately, there is no good single source to find the information of everything listed above. See the *Learning Resources* section for a list of resources that can help you learn these topics.

### Pillar 2: C++ Language

This is the bread and butter of learning C++. Here is a list of language elements you should learn:

- Keywords
- Preprocessor directives
- Expressions
- Declaration
- Types
- Pointers and References
- Initialization
- Functions
- Statements
- Classes
- Inheritance
- Overloading
- Templates
- Exceptions

### Pillar 3: C++ Standard Library

The C++ Standard Library is a set of header files that you can include in your source code to gain access to functionality that is considered standard for C++, but isn't a part of the language itself. Here is a small list of the functionality it contains:

- Utilities to work with strings
- Containers like lists, arrays, maps, etc.
- Common math functions
- File system I/O
- Concurrency/parallel programming
- Date and Time utilities

---
## Learning Resources

There are a huge number of resources to learn C++ online. However, none of them are perfect. At the moment, probably the best method of learning C++ is to use [The Cherno's C++ playlist](https://www.youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb) on YouTube. 

By far, the best source as a reference for the C++ language and the C++ Standard Library is [cppreference.com](https://en.cppreference.com/w/). 

Below is a list of further resources that members of the lab have found useful.

- [The Cherno's C++ playlist](https://www.youtube.com/playlist?list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb)
    - The clearest and most thorough tutorial video series for C++ we've found online.
- [cppreference.com](https://en.cppreference.com/w/)
    - The C++ language and standard library reference.
- [stack overflow](https://stackoverflow.com/)
    - A Q & A website packed with answers to questions you may have.

## C++ Third-party Libraries and Frameworks

- [Boost](https://www.boost.org/)
    - A huge collection of libraries that aren't in the standard library
- [Qt](https://doc.qt.io/)
    - An application framework that includes ways to make user interfaces
- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)
    - A header template library for linear algebra