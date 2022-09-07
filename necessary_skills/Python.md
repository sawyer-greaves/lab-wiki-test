[Home](../Home)
# Python

- [Python 3 Documentation](https://docs.python.org/3/index.html)
- [The Python Tutorial](https://docs.python.org/3/tutorial/index.html)
- [PyPA - Python Packaging Authority](https://www.pypa.io/en/latest/)
- [PyPI - Python Package Index](https://pypi.org/)
    - A repository of python packages meant to be installed using `pip`.
- [Python Packaging User Guide](https://packaging.python.org/en/latest/)
    - This guide contains vital information to learn standard practices related to python development, particularly installing and creating python packages correctly.
- [pip Documentation](https://pip.pypa.io/en/stable/)
    - pip is the package installer for Python. It can be used to install packages from the Python Package Index and other indexes.
- [Virtualenv Documentation](https://virtualenv.pypa.io/en/stable/)
    - Virtualenv is a tool to create isolated Python environments. Since Python 3.3, a subset of it has been integrated into the Python Standard Library under the [venv module](https://docs.python.org/3/library/venv.html).
- [Setuptools Documentation](https://setuptools.pypa.io/en/latest/index.html)
    - Setuptools is a fully-featured, actively-maintained, and stable library designed to facilitate packaging Python projects. This documentation is where you can go to learn about the format of python packages (such knowledge is very useful for users of [ROS](ROS.md)).
    - Be aware that `setup.py` files were the norm until `setuptools` version 61.0.0 (released early 2022) when they were superseded by `pyproject.toml` files (see [PEP-621](https://peps.python.org/pep-0621/)). The use of `setup.py` files is now discouraged but is still used by ROS python packages.
    - Here is a useful [blog post](https://ianhopkinson.org.uk/2022/02/understanding-setup-py-setup-cfg-and-pyproject-toml-in-python/#:~:text=toml%20file%20was%20introduced%20in,the%20idea%20that%20the%20pyproject.) by Ian Hopkinson explaining `setup.py`, `setup.cfg`, and `pyproject.toml` files.

## Anaconda and Conda (a package and environment manager)

- [Anaconda.org](https://anaconda.org/)
- [Conda Documentation](https://conda.io/en/latest/)
- Conda Cheatsheet
    - [4.12.x](conda_4.12_cheatsheet.pdf)
    - [4.6.x](conda_4.6_cheatsheet.pdf)
- [Conda: Myths and Misconceptions](http://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)

### Several Ways To Install: Anaconda, Miniconda, Miniforge, and Mambaforge

There are many ways to install and use Conda (you might consider each as a distribution of sorts): Anaconda, Miniconda, Miniforge, and Mambaforge.

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

#### Mambaforge

The same as Miniforge but comes with Mamba.
