---
layout: wiki_archive
---

## Installing ROS on Raspberry Pi

  - **Audience**: developers
  - **Level**: intermediate

Developer notes and resources for installing [ROS](../ros.md) on
[Raspberry Pi](../raspberry_pi.md).

These notes are intended for developers. **If you just want to install
[openag_brain](../openag_brain.md) we recommend visiting the [openag\_brain
install](../openag_brain/installing.md)** page.

### Things to Know

  - Raspberry Pi Debian does not have binaries available for roscore,
    ros\_comm or dependencies.
      - This means you have to build everything from source.
  - There is a Ubuntu distro that can run on the Raspberry Pi. However,
    at the time of writing, we have opted to stick with Debian Jesse for
    the [Raspberry Pi](../raspberry_pi.md), since it is the "happy path" for most
    users.

### Resources

  - Official instructions for installing [ROS](../ros.md) indigo on the ROS
    wiki:
    <http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Indigo%20on%20Raspberry%20Pi>

Other projects and prior art:

  - There are some detailed instructions in this GitBook for a
    [Raspberry Pi](../raspberry_pi.md)-powered drone
    <https://dev.px4.io/en/ros/raspberrypi_installation.html>

### Related

  - [build tooling](../ros/build_tooling.md)
