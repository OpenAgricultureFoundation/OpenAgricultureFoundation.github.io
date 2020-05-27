## Installing openag\_brain Globally, From Source

  - **Audience**: makers, developers
  - **Skill Level**: beginner

Code:

  - License: GPL 3.0
  - GitHub:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi>
  - README:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi/blob/master/README.md>
  - Issues:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi/issues>

These install instructions cover how to install [](/openag_brain/) from
source. You probably want to do this if you want to do development work
on [](/openag_brain/) or modify the core system.

**Note:** unless you are going to be modifying the openag\_brain code,
you probably want to use the [Docker
installer](/openag_brain/installing/installing_with_docker) instead of
this script.

### Installing

#### 1\. Log in to Raspberry Pi

If you've been following [the install
tutorial](/openag_brain/installing), you should already have Raspbian
Jesse ([](/Raspberry%20Pi/)'s operating system\]\] installed. If you
don't, head over to
[openag\_brain/installing/installing\_the\_os](openag_brain/installing/installing_the_os),
install the OS, then come back here.

With the OS installed, we'll want to log on to the pi over ssh. If
you've never used ssh before, [raspberrypi.org has a great tutorial
page](https://www.raspberrypi.org/documentation/remote-access/ssh/).

We'll want to ssh into your [](/Raspberry%20Pi/) as user `pi`. By
default, Raspberry Pi sets up a hostname called `raspberrypi`, so you
can log in like this:

    ssh pi@raspberrypi.local

This should prompt you for your password. The default password for
Raspberry Pi is "raspberry". Type the password and hit "enter".

#### 2\. Clone openag\_brain Source Code

Next, we'll want to clone a copy of the git repository.

    git clone https://github.com/OpenAgInitiative/openag_brain.git ~/catkin_ws/src/openag_brain

(We want to clone the code into \`\~/catkin\_ws/src/openag\_brain\` for
reasons that will become clear in a bit).

#### 3\. Increase Swap Space

Since the Raspberry Pi is a small computer, we'll need to give it some
extra swap space so it doesn't run out of memory when installing.

To do this, open `/etc/dphys-swapfile` in your editor. Here, we'll use
the [Nano editor](https://www.nano-editor.org/dist/v2.8/nano.html) to do
this.

    sudo nano /etc/dphys-swapfile

You should see a line that says:

    CONF_SWAPSIZE=100

100 means 100MB. This is the default swap size for Raspberry Pi. Let's
increase it to 1024:

    CONF_SWAPSIZE=1024

Save the file and exit. Now, we'll restart the swapfile service:

    sudo /etc/init.d/dphys-swapfile stop && sudo /etc/init.d/dphys-swapfile start

#### 4\. Install and Compile

Time to run the install script.

    cd ~/catkin_ws/src/openag_brain
    ./scripts/developer_setup

This will install and compile [](/openag_brain/) and of its
dependencies, as well as creating a [build
workspace](/ros/build_tooling).

**Note: this will take a looooooong time**. Probably an hour or more.
The [](/Raspberry%20Pi/) is a tiny little computer and has to work very
hard to compile things. Be nice to it. It's trying as hard as it can\!

#### 5\. Congratulations\!

You made it\! Time to head over to [running
openag\_brain](/openag_brain/running%20openag_brain).

### Development

If you're interested in contributing to [](/openag_brain/) see our handy
[Contributor's guidebook](/contributing). You might also want to check
out [development](/food_computer_2/development) for useful resources. We
welcome contribution from anyone, and we're excited to have you as part
of the community\!
