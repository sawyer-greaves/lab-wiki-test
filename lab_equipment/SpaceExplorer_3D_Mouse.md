[Home](../Home)
# SpaceExplorer 3D Mouse

The 3Dconnexion SpaceExplorer 3D Mouse is a USB mouse with 6-DOF spatial input. This product is discontinued by 3Dconnexion. The [spaceexplorer-3d-mouse][docs] repository contains the contents of a CD-ROM that came with the mouse. It contains documentation and drivers, but the drivers are quite old and there is no guarantee that they will work on modern operating systems. The 3Dconnexion website has a page for [discontinued devices][discontinued] that has links to downloading the latest drivers for these devices, however, it appears that the drivers are only available for Windows. The primary purpose of the driver is to customize the mouse, etc.

## Usage from Software

The drivers found in the [spaceexplorer-3d-mouse][docs] repository are not useful for developing software that uses the mouse. They are meant for customizing the mouse's functions. 3Dconnexion offers an SDK that may be able to work with the discontinued SpaceExplorer 3D Mouse, but this is unknown. Further, their SDK may not be free to use. On Linux, there is a free third-party SDK called [spacenav][spacenav] that is known to work.

### SpaceNav Driver and SDK (Linux Only)

The [spacenav][spacenav] project provides a free, compatible alternative to the proprietary 3Dconnexion device driver and SDK, for their 3D input devices. The driver and SDK can be installed using APT by installing the `spacenavd` and `libspnav-dev` packages:

```
sudo apt install spacenavd libspnav-dev
```

The installed library is called `libspnav` (link against the library using `-lspnav`) and [API documentation][libspnav-api] is found on the project website.

The [Robotics Framework][rob] uses `libspnav` to interact with the SpaceExplorer 3D Mouse.

[docs]: https://bitbucket.org/mmrobotics/spaceexplorer-3d-mouse/src/master/
[discontinued]: https://3dconnexion.com/us/support/faq/3dconnexion-discontinued-devices/
[spacenav]: https://spacenav.sourceforge.net/
[libspnav-api]: https://spacenav.sourceforge.net/man_libspnav/
[rob]: https://bitbucket.org/mmrobotics/roboticsframework/src/master/