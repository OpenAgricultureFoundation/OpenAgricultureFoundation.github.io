## Installing Raspbian Jesse OS on Raspberry Pi

### Step 1: Install the Operating System

The [food\_computer\_2](/food_computer_2) runs on the standard
[Raspberry Pi](/Raspberry%20Pi) Linux distribution: [Raspbian
Jesse](https://www.raspberrypi.org/downloads/raspbian/). If you're
setting up the Food Computer from scratch, you'll want to install
Raspbian on an SD card first.

What you'll need:

  - A Raspberry Pi 3
  - A micro SD card (32GB or more is best)
  - An SD card reader
  - An HDMI monitor
  - A keyboard
  - A mouse
  - A computer with internet access

Instructions:

1.  [Download Rasbpian
    Jesse](https://www.raspberrypi.org/downloads/noobs/). **We recommend
    using the NOOBS installer**.
      - We don't recommend using Raspbian Jesse Lite because it's
        missing some libraries.
2.  Follow the [Setup
    guide](https://www.raspberrypi.org/learning/software-guide/).
    There's also a helpful [video
    walkthrough](https://www.raspberrypi.org/help/videos/#noobs-setup)
    if you get lost.

Once you have Raspbian Jesse installed on your Raspberry Pi, connect it
to the internet. Now you're ready to install the Food Computer software.

**Note:** *If you've purchased and installed the Adafruit TFT
touchscreen you can download an image from Adafruit.com that includes
the TFT drivers allowing you to skip the process of setting the
touchscreen up.*

[Adafruit install image instructions are
here\!](https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install)

[Here is the link to copy RPI images to SD
cards](http://elinux.org/RPi_Easy_SD_Card_Setup)

[Here is a handy how/why guide to setup your .local domain for your
RaspberryPI](https://www.howtogeek.com/167190/how-and-why-to-assign-the-.local-domain-to-your-raspberry-pi/)
- No more IP address lookups for you\!

### Step 2: Configuration

What you'll need:

  - A Raspberry Pi 3
  - Shell access to the Raspberry Pi

Now that your Raspberry Pi has an operating system, we'll want to log on
to the pi over ssh. If you've never ssh before, [raspberrypi.org has a
great tutorial
page](https://www.raspberrypi.org/documentation/remote-access/ssh/).

We'll want to make sure Git is installed (if you installed Raspbian
Jesse Lite, you will probably have to install Git, otherwise, it will
already be installed). In terminal, or over ssh, run:

    sudo apt-get update
    sudo apt-get install git

### Step 3: All Set\!

Time to head over to [installing](/openag_brain/installing) and install
the software.
