---
layout: wiki_archive
---

Continued work. See [build\_tooling](../../ros/build_tooling.md) and
[dependencies](../../ros/dependencies.md) for previous notes on [ROS](../../ros.md)
packaging. See also [builder pattern](../../docker/builder_pattern.md)

  - Working branch
    <https://github.com/OpenAgricultureFoundation/openag_brain/tree/monorepo_docker>

### Notes

Reverse-chron notes.

-----

I should probably make the Dockerfile do a wstool merge/wstool init as
in openag\_brain script. That way you'll be able to build Dockerfile
without having to catkin\_make first.

-----

Good news... the new Dockerfile is actually smaller than our previous
one when compressed. 367MB

-----

If I include the src files, it's a BIG image:

    REPOSITORY           TAG                 IMAGE ID            CREATED              SIZE
    test_openag_brain    latest              ce2d5b20c5d1        About a minute ago   1.251 GB

This is a little more than double the current image size.

-----

Ran into this problem on the devbot, where I've been doing a lot of
builds. Docker devicemapper eating disk space
<https://github.com/moby/moby/issues/3182>.

I deleted `/var/lib/docker/devicemapper` but now running into
<https://github.com/moby/moby/issues/31483>.

Per that issue, I deleted `/var/lib/docker` completely, but that caused
a new issue :D. The trick is to delete the files, but not the folders.
Had to recreate `/var/lib/docker/tmp`.

Once I understand the issue, write it up in [devicemapper eating up disk
space]().

-----

Now that I've discovered the [builder\_pattern](../../docker/builder_pattern.md)
I'm experimenting with implementing it on top of this PR.

-----

All dependencies now seem to be available. Two more issues with Docker
container:

  - Getting a persistent couchdb crash in the container.
      - Same crash every time. ``[error] [<0.132.0>] Error in
        replication `47694d85fdf8a0833bf6cbe4eb12bb2d` (triggered by
        document `testforreal2replication-recipe-id`): timeout``
  - usb\_cam error
      - `Unable to open camera calibration file
        [/home/user/.ros/camera_info/head_camera.yaml]`

Adding `/dev/video0` to compose file. See [docker](../../docker.md).

Ok, this couchdb crash is present in the current docker image too.

    [info] [<0.135.0>] Attempting to start replication `47694d85fdf8a0833bf6cbe4eb12bb2d` (document `testforreal2replication-recipe-id`).
    [info] [<0.135.0>] Attempting to start replication `c3ef89279dc372221e6c6cf5ca8a007b` (document `testforreal2replication-data-id`).

USB cam still crashes in docker image but differently. This is due to
the fact that usb\_cam is not in original docker container :/.

-----

Getting a missing module exception for "netifaces" in Docker container.

netifaces is a dependency of ROS. On the Pi it's installed not in the
Python packages, but in system. I wonder if it's a default part of
Raspbian?

This article on installing in Debian mentions netifaces
<http://wiki.ros.org/Debian/Installation/Source>.

    sudo apt-get install python-netifaces

  - Is netifaces part of raspbian?
  - If I do a catkin\_make\_isolated, will it be bundled in?

Installing via rosdep `--from-paths ~/catkin_ws/install` fixed it.

-----

Dockerfile:

  - check that environment is being sourced (maybe this is why we're not
    picking up libpython).
      - We do
  - check if isolated build includes libpython

-----

Filed issue with rosinstall\_generator for ability to exclude
metapackages
<https://github.com/ros-infrastructure/rosinstall_generator/issues/39>

Good news: there's a great workaround. See
[dependencies](../../ros/dependencies.md).

-----

I suspect our libboost issue is because of Docker's minimal environment.

  - <http://wiki.ros.org/docker>
  - <http://wiki.ros.org/docker/Tutorials/Docker>
  - <http://answers.ros.org/question/243710/rosdep-to-work-with-sources-instead-of-binaries/>
  - Install script for beaglebone that apt-get installs libboost
    <https://gist.github.com/mhaberler/621bc9df63a8f5800b64>
  - ROS2 docker image installs libboost via apt-get
    <https://hub.docker.com/r/osrf/ros2/~/dockerfile/>
  - <https://github.com/UAVenture/ros-setups/tree/master/intel-edison>

-----

Earle is a ROS drone project that runs on BeagleBone
<https://erlerobotics.gitbooks.io/erlerobot/en/index.html>.

> Inspired by the BeagleBone development board, we have designed a small
> computer with about 36+ sensors, plenty of I/O and processing power
> for real-time analysis. Erle is the enabling technology for the next
> generation of aerial and terrestrial robots that will be used in
> cities solving tasks such as surveillance, enviromental monitoring or
> even providing aid at catastrophes.

-----

<http://rancher.com/docker-based-build-pipelines-part-1-continuous-integration-and-testing/#1_Containerizing_your_build_environment>

-----

build now failing on usb\_cam (though nothing has been changed?\!)

    CMake Error at /home/pi/catkin_ws/build/std_msgs/cmake/std_msgs-genmsg.cmake:385 (add_custom_target):
      add_custom_target cannot create target "std_msgs_generate_messages_cpp"
      because another target with the same name already exists.  The existing
      target is a custom target created in source directory

  - <http://answers.ros.org/question/66320/generate_messages-fails-with-ros_comm/>
  - <http://answers.ros.org/question/100036/error-while-catkin_make-common_msgs/>
  - <https://github.com/ros/catkin/issues/477>

Recreated catkin ws from scratch. Same problem. Upstream issue?

I was able to get the build to work again with the following change:

    diff --git a/CMakeLists.txt b/CMakeLists.txt
    index 3dcd8fb..8b74981 100644
    --- a/CMakeLists.txt
    +++ b/CMakeLists.txt
    @@ -6,7 +6,7 @@ project(openag_brain)
     ## is used, also find other catkin packages
     find_package(catkin REQUIRED COMPONENTS
       rospy
    -  std_msgs
    +  # std_msgs
       message_generation
     )

I don't know why this should have suddenly stopped working. It was no
different from master.

-----

Running into missing libboost in docker container. Is this included in
`install`? Do I need to `apt-get` install it?

-----

  - Q: Do I need to copy src to Dockerfile for rosdep to be able to find
    package.xml? Or are these also included and findable in the install
    space?
      - A: package.xml is in share directory of install.
      - A: rosdep --from-paths can find them and install deps.

-----

This answer has some good background on managing ROS projects that are
built from source
<http://answers.ros.org/question/109656/maintaining-a-ros-source-install-add-packages-update-release/>

-----

Instead of trying to separate ross\_comm from the rest, we could just
make one big ws `.rosinstall` and distribute an install that includes
ros bundled in.

In this world, we would no longer base our Docker image on the ROS
docker image. We would just use a vanilla Raspbian docker image.

I think this is what makes the most sense at this point.

-----

Having some trouble getting `rosinstall_generator` to do what it is
supposed to do. I think the `--exclude` flag only applies to individual
packages, not stacks.

-----

`rosinstall_generator --from-path`
<https://github.com/ros-infrastructure/rosinstall_generator/issues/25>

-----

New emerging picture:

ros core is a black box in Dockerland, so:

  - Create a rosinstall file for ros\_comm that is built with
    make\_isolated. This will give us the same ros that is in the Docker
    container.
  - Create a rosinstall file for openag\_brain rosserial usb\_cam
    (anyone else?)
  - Install script boostraps wstool, sets up 2 workspaces: one for
    roscore and one for openag\_brain project.
  - Build both
  - Copy the install folder into Docker (it doesn't contain ros\_comm)

This way, install contains everything we need.

-----

Very puzzled.

  - The install script includes rosserial and rosserial\_arduino in the
    ROS build
  - The Dockerfile includes ros from a parent container (which
    presumably includes angles, etc... are they part of core?) and
    instead clones rosserial and installs python-rosserial via apt-get.
  - Ok, if you clone rosserial, you get the whole stack (including
    rosserial and rosserial\_arduino). In docker land, we build the
    whole rosserial stack in catkin\_ws.
    <https://github.com/ros-drivers/rosserial>
  - Maybe we should do the same thing in both places.

-----

Emerging picture:

  - use (wstool?) to clone ros core directories
  - use (wstool?) to set up project catkin\_ws
  - Build ROS core dependencies in an isolated catkin ws
  - Build project deps in a separate catkin\_ws
  - copy ros install to Docker
      - Maybe?
  - copy install to Docker

-----

  - Indigo from source on Raspberry Pi
    <http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Indigo%20on%20Raspberry%20Pi>
      - Indigo is built from source because of Raspberry Pi
        architecture.
      - They recommend building it isolated
  - Kinetic from source on Raspberry Pi
    <http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi>
  - If we use [Ubuntu Mate](https://ubuntu-mate.org/), which is a
    Raspberry Pi-supported Ubuntu, we can just apt-get ROS core. They
    even have a Kinetic SD image.
      - What about rasppi-config? GPIO/I2C, etc?
      - It appears even our Docker image has abandoned ROS on Raspbian
        <https://hub.docker.com/r/pablogn/rpi-ros-core-indigo/>.
        Building on Ubuntu now. This probably explains why we can
        apt-get the ros packages.

-----

after `source ~/catkin_ws/install/setup.bash`:

    echo $PYTHONPATH
    /home/pi/catkin_ws/install/lib/python2.7/dist-packages:/opt/ros/indigo/lib/python2.7/dist-packages
    ls /home/pi/catkin_ws/install/lib/python2.7/dist-packages
    actionlib                                    genpy                             rosclean                    rosmake                     rosserial_client-0.6.4.egg-info  sensor_msgs
    actionlib-1.11.7.egg-info                    genpy-0.5.10.egg-info             rosclean-1.11.14.egg-info   rosmake-1.11.14.egg-info    rosserial_msgs                   sensor_msgs-1.11.9.egg-info
    actionlib_msgs                               geometry_msgs                     roscpp                      rosmaster                   rosserial_python                 std_msgs
    camera_calibration_parsers                   message_filters                   roscreate                   rosmaster-1.11.21.egg-info  rosserial_python-0.6.4.egg-info  std_srvs
    camera_calibration_parsers-1.11.12.egg-info  message_filters-1.11.21.egg-info  roscreate-1.11.14.egg-info  rosmsg                      rosservice                       tf
    catkin                                       openag_brain                      rosgraph                    rosmsg-1.11.21.egg-info     rosservice-1.11.21.egg-info      tf-1.11.8.egg-info
    catkin-0.6.19.egg-info                       openag_brain-0.1.0.egg-info       rosgraph-1.11.21.egg-info   rosnode                     rostest                          tf2_msgs
    diagnostic_msgs                              openag_lib                        rosgraph_msgs               rosnode-1.11.21.egg-info    rostest-1.11.21.egg-info         tf2_py
    gencpp                                       pluginlib-1.10.4.egg-info         roslaunch                   rosparam                    rostopic                         tf2_py-0.5.15.egg-info
    gencpp-0.5.5.egg-info                        ros                               roslaunch-1.11.21.egg-info  rosparam-1.11.21.egg-info   rostopic-1.11.21.egg-info        tf2_ros
    genlisp                                      rosbag                            roslib                      rospy                       rosunit                          tf2_ros-0.5.15.egg-info
    genlisp-0.4.15.egg-info                      rosbag-1.11.21.egg-info           roslib-1.11.14.egg-info     rospy-1.11.21.egg-info      rosunit-1.11.14.egg-info         topic_tools
    genmsg                                       rosboost_cfg                      roslz4                      rosserial_arduino           roswtf
    genmsg-0.5.8.egg-info                        rosboost_cfg-1.11.14.egg-info     roslz4-1.11.21.egg-info     rosserial_client            roswtf-1.11.21.egg-info

  - Q: Um, so it looks like the python dependencies of ROS packages are
    somehow making it into `install`. So how do I do that?
      - A: it's because they aren't pip dependencies. They are part of
        the ROS package.

-----

I think it may be possible to use `wstool` to do one-shot installation
from a `rosinstall` file (including the package you're working on), by
pointing it to a `rosinstall` file that is hosted remotely and includes
your package.

If not one shot, then perhaps 2-shot with `rosdep` python dependencies.

-----

lol. ROS core contributor
<https://github.com/ros-industrial-consortium/godel/pull/127#discussion_r96516197>

> Do you have any good resources on the differences between all of the
> different ros dependency tools? rosdep vs rosinstall vs wstool? I'm
> slowly starting to care about being able to on-board others easily and
> would like to get this sorted out.

No kidding.

-----

This is actually pretty helpful. How to install ros, but covers the main
items I think we'll need to cover to package everything up.
<http://wiki.ros.org/kinetic/Installation/Debian>

-----

I should look into [bloom](../../ros/bloom.md).

-----

It's possible that `catkin_make_isolated` might be what I'm looking for
(self-contained package, including Python dependencies).
<http://www.ros.org/reps/rep-0134.html>

-----

This might be useful: gitbook install instructions for a robot based on
ROS
<https://github.com/erlerobot/erle_gitbook/blob/master/en/ros/tutorials/rosinstall.md>

-----

A GH issues thread about packaging python dependencies in distributions
<https://github.com/gerkey/ros1_external_use/issues/7>

Conclusion: it looks like this is not handled\!

Here's a catkin issue from the same poster
<https://github.com/ros/catkin/issues/746>

-----

If python dependencies aren't bundled with cmake, can we use rosdep to
install them?
<http://answers.ros.org/question/229250/catkin_make-not-installing-python-dependencies/>

### Map of the problem

What we want to do:

  - Same install script for Docker and global
  - Make the result as self-contained as possible
  - Script any installs that have to happen beyond just packaging the
    system.

This is how I think from-source install needs to work:

  - `install_from_source.sh`
      - Add ros apt source
      - Add openag apt source
      - Install installers (wstool or whatever)
      - Install ros (can this be done with wstool? apt-get?)
          - Ubuntu has binaries, but Raspbian has to build from source
      - Build ros in an isolated catkin ws.
      - run wstool or rosinstall to install ROS packages not available
        via rosdep
          - openag\_brain, usb\_cam, etc
          - Q: can we dispense with wstool if we version the entire
            catkin ws?
      - run rosdep to install Python and ROS packages not covered by
        wstool

This is how I think a minimal dev setup should work:

  - Build separate apt-packages for ros, openag\_brain, usb\_cam, etc
  - Host them on our own package repo
  - `developer_setup.sh`
      - Add ros apt source
      - Add openag apt source
      - Install installers (wstool or whatever)
      - run wstool `openag_brain_dist.rosinstall` to install
        openag\_brain
      - run rosdep to install Python and ROS packages not covered by
        wstool

This is how I think packaged install should work:

  - Build separate apt-packages for ros, openag\_brain, usb\_cam, etc
  - Host them on our own package repo
  - `install_dist.sh`
      - Add ros apt source
      - Add openag apt source
      - Install brain apt package
          - Installs dependencies (ros, usb\_cam, etc)

### Spin-off Pages

Pages started from these notes:

  - [Releasing Packages](../../ros/releasing_packages.md)
  - [ros/installing\_on\_raspberry\_pi](../../ros/installing_on_raspberry_pi.md)
  - [docker/builder\_pattern](../../docker/builder_pattern.md)
