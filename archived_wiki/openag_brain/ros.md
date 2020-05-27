---
layout: wiki_archive
---

## ROS and openag\_brain

  - **Audience**: makers, developers
  - **Level**: intermediate

[openag\_brain](https://github.com/OpenAgricultureFoundation/openag_brain) runs
on [ROS (Robot Operating System)](../ros.md), an open source robotics system
that is used in many commercial robots.

  - The current version of
    [openag\_brain](https://github.com/OpenAgricultureFoundation/openag_brain)
    uses ROS Indigo.
  - Detailed ROS documentation can be found on the [ROS
    Wiki](http://wiki.ros.org/)

### Workspaces

ROS has a concept called workspaces (see
<http://wiki.ros.org/catkin/Tutorials/using_a_workspace>). Before
working with a ROS project, you have to activate its workspace. The
default OpenAg workspace is located in `~/catkin_ws/`. To activate it,
run:

    source ~/catkin_ws/devel/setup.bash

(This also works within the openag\_brain Docker container. See
[docker](../docker.md) for more.)

Once you activate the workspace, you can interact with ROS.

### Topics

[Topics](http://wiki.ros.org/Topics) are the core concept of ROS.
They're named channels over which many different scripts and processes
can communicate.

[/openag_brain/](../openag_brain.md) uses ROS topics to tie together sensors, actuators
and controllers into closed feedback loops.

To list available [ROS topics](http://wiki.ros.org/Topics):

``` 
 rostopic list
```

To log output from a ROS topic:

``` 
 rostopic echo <topic name>
```

### Raw Data CSV Output for Experiments

When running experiments, it can be convenient to log data from a topic
and export it as a csv. An easy way to do this is with a rosbag subset.
Creating a rosbag will typically log data from all the topics unless you
specify a subset of topic(s). To create this subset log, make a new
directory and start a rosbag subset when you want to start logging data.

``` 
mkdir ~/bagfiles
cd ~/bagfiles
rosbag record -O subset /topic

```

When the experiment ends and you want to stop logging data, simply exit
with:

    ctrl + c

The data in the rosbag subset does not default to a .csv format so you
can quickly convert it with the following command.

``` 
rostopic echo -b subset.bag -p /topic

```

### More

  - Unordered List ItemTo learn more about ROS, check out the [ROS
    wiki](http://wiki.ros.org/).
  - For ROS development tips and design patterns, visit the [/ros/](../ros.md)
    page on this wiki.
