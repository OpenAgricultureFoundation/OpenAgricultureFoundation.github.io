---
layout: wiki_archive
---

## ROS

  - **Audience**: developers
  - **Level**: intermediate

[openag\_brain](openag_brain.md) is written on top of [ROS (Robot
Operating System)](http://ros.org).

These pages contain useful notes and design patterns for ROS. For
details specific to openag\_brain, see [openag\_brain](openag_brain.md).
For up-to-date details on ROS, see the [ROS Wiki](http://wiki.ros.org/).

### Design Patterns

  - [Polling node](ros/polling_node.md) design pattern
  - [Logging](ros/logging.md) from nodes

### About ROS

  - [Launch files](ros/launch_files.md)
  - [Build tooling](ros/build_tooling.md)
  - [Releasing packages](ros/releasing_packages.md)
  - [Dependencies](ros/dependencies.md)
  - [msgs](ros/msgs.md)
  - [ROS and libboost](ros/boost.md)

#### Notes on Packages We Use

  - [rosserial](ros/rosserial.md)

#### ROS and Python

Currently, [ROS indigo only supports
Python 2](http://wiki.ros.org/python_2_and_3_compatible_code), so
[openag_brain](openag_brain.md) is written in Python 2.

#### ROS on Single-Board Computers

  - [Installing on Raspberry Pi](ros/installing_on_raspberry_pi.md)
      - We currently only support Raspberry Pi for [](/openag_brain/)
        but are exploring support for other platforms.
  - [Installing on Beaglebone](/ROS/Installing%20on%20Beaglebone)
  - Note that ARM Ubuntu distros have binary packages for roscore and
    ros\_comm available, as well as some dependencies.

### See Also

  - [/openag_brain/](openag_brain.md)
  - [/Docker/](docker.md)
