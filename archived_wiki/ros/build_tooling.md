---
layout: wiki_archive
---

## ROS Build Tooling

  - **Audience**: developers
  - **Skill Level**: advanced

Notes about [ROS](../ros.md) build tooling.

### Packages (what they are, etc)

  - <http://wiki.ros.org/ROS/Concepts>
  - <http://wiki.ros.org/Packages>

#### Stacks vs Packages vs Metapackages

  - A collection of related packages used to be called a "stack"
  - Stacks have been phased out
    <http://wiki.ros.org/groovy#Removal_of_Stacks>
  - To preserve some of the benefits of stack, the concept of
    "metapackages" replaces the concept of stacks. A metapackage is not
    a container of packages like rosbuild stacks were, but a named set
    of references to packages. <http://www.ros.org/reps/rep-0127.html>

### Dependencies: fetching, installing 3rd party packages

See [dependencies](dependencies.md).

### catkin build tool

Catkin is a bit of tooling gloss over [CMake](https://cmake.org/). It
searches a build space recursively, builds a graph of dependencies and
builds things in the correct order.

catkin packages can be built as a standalone project, in the same way
that normal cmake projects can be built, but catkin also provides the
concept of [workspaces](http://wiki.ros.org/catkin/workspaces), where
you can build multiple, interdependent packages together all at once.

  - A brief history of catkin:
    <http://catkin-tools.readthedocs.io/en/latest/history.html>
  - A useful set of instructions for common tasks with catkin
    <http://docs.ros.org/jade/api/catkin/html/howto/format2/index.html>
  - An overview of Catkin project layouts
    <http://catkin-tools.readthedocs.io/en/latest/mechanics.html>
  - <http://wiki.ros.org/catkin_or_rosbuild> is about catkin vs it's
    predecessor tool, but contains some good info on the motivations
    behind catkin.
  - <http://wiki.ros.org/catkin/CMakeLists.txt>

### Building packages, creating distributions

Short answer: **distributions are placed in the `catkin_ws/install`
dir**.

A [workspace](http://wiki.ros.org/catkin/workspaces) full of packages is
built with
[catkin\_make](http://wiki.ros.org/catkin/commands/catkin_make).

  - Q: what build artifacts does `catkin_make` produce? Can we package
    them up as a dist without src?
      - A: `catkin_make` puts build targets in `catkin_ws/devel` prior
        to being installed, and puts the compiled distribution in the
        `catkin_ws/install` folder
        [(source)](http://wiki.ros.org/catkin/workspaces#Development_.28Devel.29_Space).
        `install` is an [FHS compliant
        installation](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard).
  - Q: how can catkin/cmake be integrated with build farms? What about
    compiling for ARM?
      - A: [ROS Build Farm](http://wiki.ros.org/buildfarm). (see build
        farm section below)
  - Q: how can we automate the production of a full RPi image, or at
    least an apt-get installable package?
      - A: we should be able to copy the `install` directory after a
        build and treat that as the release. ROS will still need to be
        installed on the host system.
  - Q: does `catkin_make install` also package up
    [dependencies](dependencies.md) in the self-contained install
    directory?
      - A: ?

From
<http://answers.ros.org/question/226581/deploying-a-catkin-package/>

1.  Both machines must have the same instruction set architecture and
    run the same OS.
2.  Most likely, you do need the same ROS distro installed on both
    machines, A and B.
3.  The simplest approach is using CMake to install your packages in a
    location that can be the same on each machine.
      - Define a CMAKE\_INSTALL\_PREFIX for some location like:
        /opt/your\_ros\_install.
      - Run sudo make install to allow installing there.
      - Copy the install directory from machine A to machine B, using
        scp or tar or some other technique.
4.  To run your installed ROS packages on either machine: `source
    /opt/your_ros_install/setup.bash`

From <http://wiki.ros.org/catkin/workspaces>

> One of the main reasons for moving away from rosbuild is that it
> lacked a proper install target. This prevented ros packages from being
> used like canonical system packages and made distribution more
> difficult. Catkin encourages standard compliant install layouts via
> CMake. Therefore, when you are ready, you can install your packages to
> the system for others to use, or you can more easily package your
> packages for distribution systems like deb or rpm.

#### Installing data files (launch, yaml, etc) from package

  - Q: how to include launch directory in install?
      - A:
        <http://wiki.ros.org/catkin/CMakeLists.txt#Installing_roslaunch_Files_or_Other_Resources>

Macro:

    # Install everything in the launch directory.
    install(DIRECTORY launch/
      DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
      PATTERN ".svn" EXCLUDE)

#### Where are ROS packages installed?

ROS executables are installed in a per-package directory, not the
distributions’s global bin/ directory. They are accessible to rosrun and
roslaunch, without cluttering up the shell’s $PATH, and their names only
need to be unique within each package. There are only a few core ROS
commands like rosrun and roslaunch that install in the global bin/
directory.

(<http://docs.ros.org/kinetic/api/catkin/html/howto/format2/installing_python.html>)

### Installing Python scripts in ROS packages

#### Installing Python dependencies

See [dependencies](dependencies.md).

#### Installing Python modules

Standard ROS practice is to place Python modules under the
`src/your_package` subdirectory, making the top-level module name the
same as your package. Python requires that directory to have an
`init.py` file, too.

Catkin installs Python packages using a variant of the standard Python
setup.py script. Assuming your modules use the standard ROS layout, it
looks like this:

    ## ! DO NOT MANUALLY INVOKE THIS setup.py, USE CATKIN INSTEAD
    
    from distutils.core import setup
    from catkin_pkg.python_setup import generate_distutils_setup
    
    # fetch values from package.xml
    setup_args = generate_distutils_setup(
        packages=['your_package'],
        package_dir={'': 'src'})
    
    setup(**setup_args)

Assuming the above `setup.py` script is configured, if you put modules
under `src`, they will get installed via `catkin_make`.

  - Q: catkin doesn't seem to install subdirectories of the Python
    module. Why?
      - A: you must explicitly list all python packages. So a
        subdirectory of the python package must be explicitly listed in
        `packages` like this `packages=['your_package',
        'your_package.subpackage']`

#### Installing Python entry-point scripts

Don't use `setup.py` `console_scripts`. There is a CMake command [I have
found](https://github.com/ros/ros_comm/commit/6405793196e0ee74dd7a937af5ba392b9700cf7e):
`catkin_install_python`.

The [Catkin documentation has instructions for installing Python along
with the rest of your ROS
package](http://docs.ros.org/kinetic/api/catkin/html/howto/format2/installing_python.html).

Standard ROS practice is to place all executable Python programs in a
package subdirectory named nodes/ or scripts/. Their usage is the same,
the two names distinguish ROS nodes from other executable Python
scripts. To keep the user API clean, executable script names generally
do not include a .py suffix. Your CMakeLists.txt should install all the
scripts explictly using the special install function
catkin\_install\_python. This will make sure that shebang lines are
updated to use the specific Python version used at configure time:

    catkin_install_python(PROGRAMS nodes/your_node scripts/another_script
                          DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

##### Avoiding listing all of your scripts by hand

The `install(PROGRAMS files... )` cmake macro takes list of files. So
does the `catkin_install_python(PROGRAMS files...)`. But what if you
don't want to list the files by hand. Listing by hand is gross, and
means you can trip yourself up when adding/removing files.

You can install all the nodes and scripts under a directory using the
`FILE(GLOB ...)` macro:

    FILE(GLOB openag_script_files "${CMAKE_CURRENT_SOURCE_DIR}/scripts/*")
    catkin_install_python(PROGRAMS
      scripts/main scripts/flash scripts/install_pio
      ${openag_script_files}
      DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
    
    FILE(GLOB openag_node_files "${CMAKE_CURRENT_SOURCE_DIR}/nodes/*")
    catkin_install_python(PROGRAMS
      ${openag_node_files}
       DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

  - <https://cmake.org/cmake/help/v3.7/command/install_programs.html>
  - <https://cmake.org/Wiki/CMake:Install_Commands>
  - <https://cmake.org/cmake/help/v3.7/command/file.html>
  - <https://cmake.org/cmake/help/v3.5/command/install.html#id4>

Another good practice is to keep executable scripts very short, placing
most of the code in a module which the script imports and then invokes:

    #! /usr/bin/env python
    import your_package.main
    if __name__ == '__main__':
        your_package.main()

  - Q: is our package set up this way?
      - A: yes, it appears to follow the conventions described in
        <http://docs.ros.org/kinetic/api/catkin/html/howto/format2/installing_python.html>
        and
        <http://docs.ros.org/api/catkin/html/user_guide/setup_dot_py.html>,
        but the script install macro was missing from CMakeLists.txt.
        I'm adding it.

#### Installing Python ROS nodes

The same way you install `scripts`, but instead keep them in a `nodes`
directory. See
<http://docs.ros.org/kinetic/api/catkin/html/howto/format2/installing_python.html>.

#### Troubleshooting Python install

  -  catkin do not install python packages \#500
    <https://github.com/ros/catkin/issues/500>

### Releasing APT Packages / Release Automation

See [Releasing Packages](releasing_packages.md).

### Project layout

This answer outlines some helpful guidelines:
<http://answers.ros.org/question/257855/git-strategy-for-catkin-and-package-folders/>

  - You can have multiple packages in one repo
  - All packages in a single git repository must be released together.
  - The src folder should always be created by the user when he creates
    a workspace and decides what sources to put into that workspace.
      - The workspace itself (the src folder and the CMakeLists.txt file
        in the root of the source space) should not be part of your
        repository.
      - The rational is that users might want to clone your repository
        together with other repositories and build them together in a
        workspace.
      - That wouldn't be possible if your repo already contains this.
        Also the CMakeLists.txt file only applies to the case when you
        are using catkin\_make. But there are other build tools (e.g.
        catkin\_make\_isolated and catkin\_tools) which don't use that
        file.

#### Prior Art

  - <https://github.com/RethinkRobotics/baxter>
      - <http://sdk.rethinkrobotics.com/wiki/Baxter_Setup>
      - <http://sdk.rethinkrobotics.com/wiki/Workstation_Setup>
      - <http://sdk.rethinkrobotics.com/wiki/Workstation_Update>
      - <http://sdk.rethinkrobotics.com/wiki/Repository_Layout>
  - <https://github.com/ros-industrial-consortium/godel>
  - <https://github.com/labust/labust-ros-pkg>

Using `rosinstall` and `wstool merge` seems like a popular approach. See
[dependencies](dependencies.md) for more.

#### What we do now

Currently, the project looks like this, more or less:

    openag_brain/
      Dockerfile
      doc/
      launch/ # ROS .launch files
      msg/ # message type descriptions compiled into typecasting code by ROS
      srv/ # service type descriptions compiled into typecasting code by ROS
      test/
      scripts/ # bash utility scripts
      src/
        openag_brain/ # python package
      package.xml # ros buildtime and runtime dependency manifest used by catkin
      setup.py

To build an image [the
Dockerfile](https://github.com/OpenAgricultureFoundation/openag_brain/blob/master/Dockerfile)
places the root openag\_brain folder under `catkin_ws/src/openag_brain`
and installs dependencies by generating a \`.rosinstall\` file
dynamically after checking out some sourcecode manually.

#### Proposed Layout (WIP)

  - `.rosinstall` files should be checked into the repo and managed with
    version control. They define our dependencies.
  - Moving dependencies into a monorepo and creating scripts to produce
    distributions allows us to create reproducible distributions (a
    problem with the current setup that relies on a lot of http fetching
    and git cloning to produce a Docker build)

<!-- end list -->

    openag_brain/
      CMakeLists.txt
      package.xml
      master.rosinstall
      dev.rosinstall
      src/
        openag_brain/
      nodes/
        pid.py
        ...
      scripts/
        main
        flash
        make_apt_release
        ...
      openag_ui/
      firmware/
        lib/
          openag_am2315
          ...
        platformio.ini
      docker/
        Dockerfile
        Dockerfile_db
        ...
