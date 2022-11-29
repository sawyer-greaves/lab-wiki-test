[Home](../Home)
# Python

**Contents**

[TOC]

---
## Introduction

Python is an interpreted programming language (i.e. not compiled like [C++](C_and_Cpp.md)) in which a *Python script* is written and subsequently executed via a Python interpreter. In this sense, Python is similar to MATLAB. Python is well known as a language that is easy to learn with a concise and easy-to-read syntax. It is used most commonly for data science applications (e.g. machine learning, deep learning, computer vision, etc) and is one of the two main languages used to write programs with [ROS](ROS.md). The major drawback of Python is its speed. Python tends to rely on bindings to compiled C-based libraries to improve performance. It is recommended to install Python using some flavor of Conda distribution (see the *Anaconda and Conda* section below).

---
## Python Documentation and Resources

- [Python 3 Documentation](https://docs.python.org/3/index.html)
- [The Python Tutorial](https://docs.python.org/3/tutorial/index.html)
- [PyPA - Python Packaging Authority](https://www.pypa.io/en/latest/)
- [PyPI - Python Package Index](https://pypi.org/)
    - A repository of python packages meant to be installed using pip.
- [Python Packaging User Guide](https://packaging.python.org/en/latest/)
    - This guide contains vital information to learn standard practices related to python development, particularly installing and creating python packages correctly.
- [pip Documentation](https://pip.pypa.io/en/stable/)
    - pip is the package installer for Python. It can be used to install packages from the Python Package Index and other indexes.
- [Virtualenv Documentation](https://virtualenv.pypa.io/en/stable/)
    - Virtualenv is a tool to create isolated Python environments. Since Python 3.3, a subset of it has been integrated into the Python Standard Library under the [venv module](https://docs.python.org/3/library/venv.html).
- [Setuptools Documentation](https://setuptools.pypa.io/en/latest/index.html)
    - Setuptools is a fully-featured, actively-maintained, and stable library designed to facilitate packaging Python projects. This documentation is where you can go to learn about the format of python packages (such knowledge is very useful for users of [ROS](ROS.md)).
    - Be aware that `setup.py` files were the norm until `setuptools` version 61.0.0 (released early 2022) when they were superseded by `pyproject.toml` files (see [PEP-621](https://peps.python.org/pep-0621/)). The use of `setup.py` files is now discouraged but is still used by ROS python packages.
    - Here is a useful [blog post](https://ianhopkinson.org.uk/2022/02/understanding-setup-py-setup-cfg-and-pyproject-toml-in-python/) by Ian Hopkinson explaining `setup.py`, `setup.cfg`, and `pyproject.toml` files.

---
## Learning Python

There are many ways to learn Python, but perhaps the most complete way is using the Python documentation itself (above). At the bare minimum, it is recommended to complete the **entire** tutorial offered by the Python documentation which covers the Python language and introduces the Python Standard Library. In addition to the Python language and its standard library, the Python package manager (pip) and the concept of *virtual environments* are vital topics to understand in order to become proficient with Python. Finally, below is a list of common Python packages you'll want to be familiar with.

### Common Python Packages

- [NumPy](https://numpy.org/doc/)
    - A Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more.
- [pandas](https://pandas.pydata.org/docs/)
    - Provides high-performance, easy-to-use data structures and data analysis tools for tabular, time series, or matrix data (e.g. work with Excel spreadsheets or machine learning datasets).
- [Numba](https://numba.readthedocs.io/en/stable/)
    - A just-in-time  compiler for Python meant to drastically improve performance of Python code. It works best on code that uses functions, loops and NumPy arrays.
- [Tk and tkinter](https://docs.python.org/3/library/tk.html)
    - Part of the Python Standard Library. A robust and platform independent windowing toolkit to create graphical user interfaces (GUIs).
- [Matplotlib](https://matplotlib.org/stable/index.html)
    - A comprehensive library for creating static, animated, and interactive visualizations in Python (e.g. plotting data, etc).
- [Pillow (Python Imaging Libary (PIL) fork)](https://pillow.readthedocs.io/en/stable/)
    - The Python Imaging Library adds image processing capabilities to your Python interpreter. The library provides extensive file format support, an efficient internal representation, and fairly powerful image processing capabilities.

---
## Anaconda and Conda

Anaconda is a set of repositories filled with data science packages (including a Python interpreter/distribution) and mostly consists of Python packages. Conda is a package and environment manager (it can be thought of as some sort of combination of pip and Virtualenv) used to interact with the Anaconda package repositories and manage virtual environments composed of Anaconda packages. While Conda is designed to work with Anaconda repositories out of the box, it is not restricted to them and acts as a general purpose package and virtual environment manager for many programming languages. Anaconda and its Python distribution are very commonly used in robotics research and applications. It is recommended to install Python using some flavor of Conda distribution.

### Anaconda and Conda Resources

- [Anaconda.org](https://anaconda.org/)
- [conda Documentation](https://conda.io/en/latest/)
- conda Cheatsheet
    - [4.12.x](conda_4.12_cheatsheet.pdf)
    - [4.6.x](conda_4.6_cheatsheet.pdf)
- [Conda: Myths and Misconceptions](http://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)

### Several Ways To Install: Anaconda, Miniconda, Miniforge, and Mambaforge

There are many ways to install and use conda (you might consider each as a distribution of sorts): Anaconda, Miniconda, Miniforge, and Mambaforge.

#### Anaconda

Anaconda is a downloadable, free, open-source, high-performance, and optimized Python and R distribution. Anaconda includes conda, conda-build, Python, and 250+ automatically installed, open-source scientific packages and their dependencies that have been tested to work well together, including SciPy, NumPy, and many others.

#### Miniconda

A free minimal installer for conda. Miniconda is a small, bootstrap version of Anaconda that includes only conda, Python, the packages they depend on, and a small number of other useful packages, including pip, zlib, and a few others. You can still install packages that come included with Anaconda by using `conda install`.

#### Miniforge

Miniforge is basically the same as Miniconda except for the following changes:

- conda-forge set as the default (and only) channel.
    - Packages in the base environment are obtained from the conda-forge channel.
- Optional support for PyPy in place of standard Python interpreter (the standard Python interpreter is called "CPython").
- Optional support for Mamba in place of Conda.
- An emphasis on supporting various CPU architectures (x86_64, ppc64le, and aarch64 including Apple M1).

Miniforge is installed using the installers that can be downloaded from the [Miniforge Github Repository](https://github.com/conda-forge/miniforge).

#### Mambaforge

Mambaforge is the same as Miniforge but comes with mamba pre-installed (in addition to conda). Effectively, you can turn a Miniforge installation into a Mambaforge installation by using `conda` to install `mamba`:

    conda install mamba -n base -c conda-forge

 >:warning: **WARNING:** Installing mamba into any other environment than base can cause unexpected behavior!
 
 Mamba is a drop-in replacement for conda that uses the same commands and configuration options but is faster and gives better error messages. Almost anywhere you use `conda` you can use `mamba` instead. **The only difference is that you should still use `conda` for activation and deactivation.**

- [Mamba Documentation](https://mamba.readthedocs.io/en/latest/index.html)
- [Mamba Github Repository](https://github.com/mamba-org/mamba)

Mambaforge is installed using the installers that can be downloaded from the [Miniforge Github Repository](https://github.com/conda-forge/miniforge).
