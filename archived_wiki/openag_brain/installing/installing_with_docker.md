## Installing openag\_brain with Docker

  - **Audience**: everyone
  - **Level**: beginner

Code:

  - License GPL 3.0
  - GitHub:
    [openag\_brain\_docker\_rpi](https://github.com/OpenAgInitiative/openag_brain_docker_rpi)
  - README:
    <https://github.com/OpenAgInitiative/openag_brain_docker_rpi/blob/master/README.md>
  - Issues:
    [openag\_brain\_docker\_rpi/issues](https://github.com/OpenAgInitiative/openag_brain_docker_rpi/issues)

### What you'll need

  - A Raspberry Pi 3 with [Raspbian
    installed](/openag_brain/installing/installing_the_os).
      - [Here is a
        link](https://learn.adafruit.com/adafruit-raspberry-pi-lesson-1-preparing-and-sd-card-for-your-raspberry-pi/overview)
        to a tutorial from on how to flash your Pi with Raspian Jessie
        Lite
      - For maximum stability, it's highly recommended you use Jessie
        Lite.
  - Shell access to the Raspberry Pi
  - An Arduino Mega
  - A USB Camera
  - A USB cable to connect the Arduino to the Raspberry Pi

### Before you start

  - Plug your Arduino Mega into one of the Raspberry Pi's USB ports.
  - Plug the USB Camera into one of the Raspberry Pi's USB ports.
  - Connect via SSH, or open a terminal session to your Raspberry Pi.

### 1\. Get Install Script

First, clone this repository on your Raspberry Pi:

    sudo apt-get install git
    git clone http://github.com/OpenAgInitiative/openag_brain_docker_rpi
    cd openag_brain_docker_rpi

### 2\. Install Docker with Script

Now it's time to install docker and docker-compose. This repository has
a script that does this for you. It leverages a repository set up by
Hypriot which provides the necessary packages.

    sh install_docker.sh

### 3\. Restart Raspberry Pi

After installing docker, you will have to refresh your user groups in
order to contact the docker daemon. The easiest way to do this is to
restart the Raspberry Pi (or if connected via SSH, log out and log back
in).

### 4\. Start openag\_brain

Now, the project can be started as follows:

    docker-compose up -d

### 5\. Congratulations\!

Congratulations\! You have installed the OpenAg Food Computer software.
Head over to [food\_computer\_2](/food_computer_2). It's time to
configure your Food Computer and start growing.

### Docker Tips and Tricks

Two docker containers will be started in the background and will persist
across reboots. (Note if you don't have your Arduino connected, you will
see an error. If this happens, connect the Arduino and run the command
again). You can see the two containers with this command:

``` 
docker ps

```

Let's check the logs to see if it started up correctly. Type this
command:

    docker logs -f openagbraindockerrpi_brain_1

Your screen will fill with a long list of all of the things including
ROS topics/sensors/actions that have been initialized. Scroll through it
to see if you have any errors. Don't worry if you get an error saying
you can't communicate with the "device" or Arduino, we are about to fix
that.

``` 
[ERROR] [WallTime: 1492142142.507275] Unable to sync with device; possible link problem or link software version mismatch such as hydro rosserial_python with groovy Arduino

```

Let's tunnel into the openag\_brain docker container and start
configuring. Start by using this command:

``` 
docker exec -it openagbraindockerrpi_brain_1 bash

```

You will notice your cursor prompt will have different text in front of
it. You may also get a few short errors. Disregard them. You are now
INSIDE the docker container where ROS and the OpenAg brain are running\!

Before you can do anything here, you need to initialize the workspace.
Type this command:

    source catkin_ws/devel/setup.bash

Now let's get that Arduino up and working.

To flash the Arduino you need to unplug the USB cord from the Raspberry
Pi and plug it into a different USB port. Alternatively you can wait 30
seconds and plug it into the same port. This frees the port from other
services blocking our way.

Once you've plugged the Arduino back in and type this command:

``` 
rosrun openag_brain flash

```

Make sure the process exits with SUCCESS. You may need to try this
process a few times. Once it does reach around and pat yourself on the
back. You've got a OpenAg brain running\!\!\!

Let's restart the docker container to make sure it's clean and happy and
explore ROS.

Type this command to leave the docker container:

``` 
exit

```

Then restart the docker containers. Don't worry you won't lose your
changes.

    docker-compose restart

Now let's go back into the container with this command:

``` 
docker exec -it openagbraindockerrpi_brain_1 bash

```

Re-initialize your workspace. You have to do this everytime you restart
the docker container for now.

``` 
source catkin_ws/devel/setup.bash

```

Let's take a look at the ROS topics:

``` 
rostopic list

```

You can see the data flowing by typing this:

    rostopic echo <topic name>

Like this:

    rostopic echo diags
