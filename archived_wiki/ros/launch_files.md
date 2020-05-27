---
layout: wiki_archive
---

## Launch Files

  - **Audience**: developers
  - **Level**: beginner

[ROS](../ros.md) programs are made up of a bunch of small modules called
[Nodes](http://wiki.ros.org/Nodes). To make a ROS program like
[openag\_brain](../openag_brain.md), you configure a set of nodes with a
[.launch XML file](http://wiki.ros.org/roslaunch/XML).

[openag\_brain](../openag_brain.md) contains default launch files designed
for the [Food Computer 2](../food_computer_2.md).

### Resources

More background on roslaunch and launch files can be found on the ROS
wiki:

  - <http://wiki.ros.org/roslaunch>
  - <http://wiki.ros.org/Nodes>
  - <http://wiki.ros.org/roslaunch/XML>

### Launching ROS at startup

Launching ROS at startup can be accomplished in a couple different ways:

  - [Configure a Linux service to run ROS at
    startup](https://www.digitalocean.com/community/tutorials/how-to-configure-a-linux-service-to-start-automatically-after-a-crash-or-reboot-part-1-practical-examples)
  - Use a Docker container for ROS and have Docker manage running at
    startup.

[openag\_brain](../openag_brain.md) will configure a service automatically
when [installed globally](../openag_brain/installing/installing_globally.md).
When [installing with
Docker](../openag_brain/installing/installing_with_docker.md),
`docker-compose` handles restarting across reboots.

### Launching ROS in background

To run ros in the background, you can use a program like
[screen](https://www.gnu.org/software/screen/).
