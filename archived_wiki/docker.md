---
layout: wiki_archive
---

## Docker

The OpenAg system runs within 2 [Docker](http://docker.com/) containers:
one for the openag\_brain ROS system, and one for CouchDB.
`docker-compose` coordinates between the 2 containers.

See [docs.docker.com](https://docs.docker.com/) for detailed Docker
documentation.

### Handy Docker commands

See which containers are running:

    docker ps

The [Docker install
script](openag_brain/installing/installing_with_docker.md) creates and
runs 2 docker containers. You should see them listed when running docker
ps:

    openagbraindockerrpi_brain_1
    openagbraindockerrpi_db_1

Stoping and starting the containers is done in the usual way:

    docker-compose start
    docker-compose stop
    docker-compose restart

You can get logs for the containers via docker's logging command:

    docker logs -f openagbraindockerrpi_brain_1

### Running commands in containers

You can run bash commands within a container with `docker exec`:

    docker exec <container> <command>

For example:

    docker exec openagbraindockerrpi_brain_1 rosrun openag_brain load_fixture default

#### "Shelling into" running containers

OpenAg Brain is powered by ROS. Sometimes, you might want to interact
with ROS in the Docker container directly. To do so, first shell into
the Docker container:

    docker exec -it openagbraindockerrpi_brain_1 bash

Then, activate the catkin workspace within the Docker container:

    source catkin_ws/devel/setup.bash

Now, you can interact with ROS. For more, see [ros](openag_brain/ros.md).

Note that Docker containers are stateless, so if your Docker container
restarts, it will lose the changes you make. If you need the changes to
stick, build a new Docker image (see below).

### Building new Docker images

If you're [contributing to openag\_brain](food_computer_2/development.md),
you might want to build new Docker images. To build new Docker images
from [](/openag_brain/), you'll want to install the Docker command line
tools. Running the `install_docker.sh` script from
[openag\_brain\_docker\_rpi](https://github.com/OpenAgInitiative/openag_brain_docker_rpi)
on your [Raspberry Pi](raspberry_pi.md) will take care of installing these for you.

Once Docker is installed, building images is easy. Just:

    cd ~/catkin_ws/src/openag_brain

and

    docker build -t openag/rpi_brain .

You can provide your own tag/name in place of openag/rpi\_brain. See
[Docker's docs on the build
command](https://docs.docker.com/engine/reference/commandline/build/)
for more.

Note: we've had trouble with Raspbian's Pixel desktop freezing while
building Docker images. We've also had problems with Docker builds
failing on Rasberry Pi 2 when no swapfile is configured. We recommend
the following build setup for best results:

  - Use a Raspberry Pi 3
  - Make sure to configure a swapfile
  - Use Raspbian Jesse Lite (not the Desktop version)
  - ssh into your Pi and start the build over ssh

### Exposing USB Devices

Docker containers are isolated from the host environment by default. For
a container to communicate with USB devices, you have to give them
explicit access to the device.

With docker-compose, this is done using by adding the `devices` key to
your service in `docker-compose.yml`:

    ...
    services:
      brain:
        devices:
        - "/dev/ttyACM0:/dev/ttyACM0"
        ...

You may also need to [add the `privileged` key to the
service](https://docs.docker.com/compose/compose-file/compose-file-v2/#cpushares-cpuquota-cpuset-domainname-hostname-ipc-macaddress-memlimit-memswaplimit-memswappiness-memreservation-oomscoreadj-privileged-readonly-restart-shmsize-stdinopen-tty-user-workingdir).

If running the container via `docker run`, you can use the `device` flag
to explicitly expose host devices to the container.

Resources:

  - <https://docs.docker.com/engine/reference/commandline/run/>
  - <http://stackoverflow.com/questions/24225647/docker-any-way-to-give-access-to-host-usb-or-serial-device>

### Design Patterns

  - [Builder Pattern](docker/builder_pattern.md)

### More Resources

  - [/openag_brain/](openag_brain.md)
  - [/ros/](ros.md)
  - <http://wiki.ros.org/docker/Tutorials/Docker>
