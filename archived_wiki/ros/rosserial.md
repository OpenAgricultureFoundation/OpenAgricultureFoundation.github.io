---
layout: wiki_archive
---

## rosserial Developer Notes

  - **Audience**: developers
  - **Level**: advanced

We use the rosserial\_arduino [ROS](../ros.md) package to communicate with the
[Arduino](/Arduino). It provides a way to talk to the Arduino over typed
[ROS Topics](http://wiki.ros.org/Topics).

  - <http://wiki.ros.org/rosserial>
  - <http://wiki.ros.org/rosserial_arduino>
  - **GitHub**: <https://github.com/ros-drivers/rosserial>

### Things to Know & Gotchas

  - rosserial has a hard limit on the number of topics it supports
  - rosserial has a limited buffer size. If you send too many messages,
    or messages that are too large, it will lose sync with the Arduino.
      - In [openag_brain](../openag_brain.md), we use error codes (numbers) rather than
        error messages for this reason.
  - The [Food Computer 2](../food_computer_2.md) is right up against the limit in terms
    of number of topics used and size of messages sent.

### Resources & Links

  - Best practice guidelines for using rosserial
    <https://github.com/ros-drivers/rosserial/issues/83>
  -  how to increase rosserial buffer size
    <http://answers.ros.org/question/73627/how-to-increase-rosserial-buffer-size/>

### Related

  - [contributors/troubleshooting\_rosserial](contributors/troubleshooting_rosserial)
