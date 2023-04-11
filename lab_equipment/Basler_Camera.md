[Home](../Home)
# Basler Camera

>:warning: **This page is incomplete! Please add any information that may be missing or useful!**

The Basler camera is a machine vision camera with an IEEE 1394 (Firewire) interface for connecting to a computer. This camera is not commonly used in our lab anymore due to IEEE 1394 becoming a much less common interface.

- [Documentation][docs]

    Contains:

    - Specs sheet
    - Documentation from the manufacturer

## Usage from Software

### libdc1394

The [`libdc1394`][libdc1394] library provides a C++ library that can be used to interact with the camera from software. This library has been used previously in this lab and it may be possible to find old code utilizing this library. On Linux you will use APT to install the `libdc1394-dev` package and on Windows you will need to compile the library from source.

### OpenCV

It is also possible to obtain images from the camera using the `VideoCapture` class. However, this method provides very limited functionality. It is basically limited to obtaining images from the camera only.


[docs]: https://bitbucket.org/mmrobotics/docs-cameras/src/master/
[libdc1394]: https://damien.douxchamps.net/ieee1394/libdc1394/