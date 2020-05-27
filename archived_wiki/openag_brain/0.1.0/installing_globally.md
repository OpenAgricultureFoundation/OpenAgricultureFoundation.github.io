## Installing globally

  - License: GPL 3.0
  - GitHub:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi>
  - README:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi/blob/master/README.md>
  - Issues:
    <https://github.com/OpenAgInitiative/openag_brain_install_rpi/issues>

If you want to do development work on [](/openag_brain/) or modify the
core system, you can install it globally using the script at
[github.com/OpenAgInitiative/openag\_brain\_install\_rpi](https://github.com/OpenAgInitiative/openag_brain_install_rpi).

**Note:** unless you are going to be modifying the openag\_brain code,
you probably want to use the [Docker
installer](/openag_brain/installing/installing_with_docker) instead of
this script.

### Installing

To set up the project, simply clone the repository and run the
install.sh file.

    git clone https://github.com/OpenAgInitiative/openag_brain_install_rpi.git
    cd openag_brain_install_rpi
    ./install.sh

This will install the [ROS environment](/openag_brain/ROS), all
dependencies, [](/openag_python/) and [](/openag_brain/).

Source files for openag\_brain can be found in:
`~/catkin_ws/src/openag_brain`.

### Development

If you're interested in contributing to [](/openag_brain/) see our handy
[Contributor's guidebook](/contributing). You might also want to check
out [development](/food_computer_2/development) for useful resources. We
welcome contribution from anyone, and we're excited to have you as part
of the community\!
