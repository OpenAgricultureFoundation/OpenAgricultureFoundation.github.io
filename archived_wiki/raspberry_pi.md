---
layout: wiki_archive
---

## Raspberry Pi

[Raspberry Pi](https://www.raspberrypi.org/) is a single-board Linux
computer. The [Food Computer 2.0](food_computer_2.md) uses the Raspberry Pi
3.

![26281560492\_18c34260af\_k.jpg](/static/images/wiki/raspberry_pi/26281560492_18c34260af_k.jpg)

(Photo: [Raspberry Pi 3 by Decio "desmodex" on
Flickr](https://www.flickr.com/photos/desmodex/26281560492/in/photolist-G3pSij-dbEyXN-r9CWsr-r9wxJU-qszMrG-rqYb4H-qu6kVL-dm4Jec-r6fiN4-r9CWT6-r7LzZ6-qszjeL-quiw8V-rnh8Qs-rqZBKG-esey2Y-dijNpn-opqnji-meFnrf-gv7pTG-cZzxcj-gNS6UT-qu6oNQ-qu6kYG-rr5Z1v-r9vvj3-r9vrTW-r9wwqS-rqZzVE-roN1h5-quisoR-r811TE-r9CTHt-qsMENB-r88sNH-quiwCx-r7ZpmC-qsMwRz-qszshu-rqYc9P-rpzuv8-rr5YzR-r9wuqQ-r9CXvi-rqYbF4-quisHi-gVeh8G-quivpF-gn6Xhd-rnhqhf))

### Setting up

The Raspberry Pi runs its operating system off of a [Micro SD
card](https://en.wikipedia.org/wiki/Secure_Digital). Before working with
the Pi, you'll need to install an operating system on to a Micro SD. See
[Installing the OS](openag_brain/installing/installing_the_os.md) for
details.

### Working with the Pi

The Raspberry Pi is a Linux computer, so if you know Linux, the same
stuff holds. For people new to the Rasbperry Pi and command line, here
are some useful things to know:

#### openag\_brain and openag\_python

Some useful resources for working with [/openag_brain/](openag_brain.md) on the
Raspberry Pi's command line:

  - [/openag_brain/](openag_brain.md)
  - [API](openag_brain/api.md)
  - [API Cookbook](openag_brain/api_cookbook.md)
  - [openag\_brain CLI](openag_brain/cli.md)
  - [ROS](openag_brain/ros.md)
  - [docker](docker.md)
  - [](/openag_python/)
  - [openag\_python CLI](/openag_python/CLI)

#### Finding the IP address of your Pi

Once your Raspberry Pi is connected to the network, how do you find it's
IP address?

If you've got terminal access to the Pi (e.g. a keyboard and monitor
hooked up to it), you can type this command into the terminal:

    ifconfig

This will list all the network connections. Look for the one that says
`wlan0` and the line that says `inet connection`. This is your IP.

To find the Raspberry Pi's IP from your laptop, try [AdaFruit's Pi
Finder app](https://github.com/adafruit/Adafruit-Pi-Finder).

#### ssh into Raspberry Pi

By default, the ssh credentials for the Raspberry Pi are:

  - username: `pi`
  - password: `raspberry`

You can ssh into the Pi with:

    ssh pi@<IP ADDRESS>

When prompted, type the password `raspberry`.

#### Restart

    sudo reboot

#### Shutdown

``` 
sudo shutdown now

```

#### Hardware shutdown

If Raspbian Jesse (full version with desktop) is installed, then you can
use GPIO pins 3 and 5 to send the shutdown signal. Short 3 and 5 with a
GPIO pin connector, or with some wire. See
<http://www.makeuseof.com/tag/add-reset-switch-raspberry-pi/>.

#### Finding a file

``` 
find -name myfile.txt

```

#### Editing a file

    nano path/to/file.txt

This will open up the [Nano editor](https://www.nano-editor.org/) in the
terminal.

If the computer complains that you don't have privileges to edit the
file:

    sudo nano path/to/file.txt

#### Connecting to Wifi on Raspbian Lite

Rasbpian Lite doesn't have a desktop. We recommend using the full
version of Raspbian with desktop, but if you're using Lite, here's how
to connect to a network.

Tutorials:

  - <https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md>
  - <https://thepihut.com/blogs/raspberry-pi-tutorials/83502916-how-to-setup-wifi-on-raspbian-jessie-lite>

In a nut:

``` 
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf 
```

In the case of the example network, we would enter:

    network={
        ssid="testing"
        psk="testingPassword"
    }

Note these have to be double-quotes. If your keyboard is outputting `@`
instead of double-quotes, you might have to reconfigure your locale and
keyboard with `sudo raspi-config`. (Usually you should choose the 101
key keyboard.)

At this point, wpa-supplicant will normally notice a change has occurred
within a few seconds, and it will try and connect to the network. If it
does not, either manually restart the interface with `sudo ifdown wlan0`
and `sudo ifup wlan0`, or reboot your Raspberry Pi with `sudo reboot`.

You can verify if it has successfully connected using ifconfig wlan0. If
the inet addr field has an address beside it, the Pi has connected to
the network. If not, check your password and ESSID are correct.

#### Creating backup images

See
<http://raspberrypi.stackexchange.com/questions/311/how-do-i-backup-my-raspberry-pi>.

In a nut:

    diskutil list
    dd if=/dev/rdiskN of=/path/to/my_image.img bs=1m

Tip: if you zip the image, it will be much smaller.

### See Also

  - [Installing ROS on Raspberry Pi (Developer
    Notes)](/ROS/Installing%20on%20Raspberry%20Pi)
