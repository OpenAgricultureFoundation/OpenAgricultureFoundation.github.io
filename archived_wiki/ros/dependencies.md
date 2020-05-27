---
layout: wiki_archive
---
## Dependencies in ROS

Dependency management in [ROS](../ros.md).

High-level things to know:

  - ROS has it's own way of managing dependencies. `setup.py` and pip
    won't work because packages can be Python, C++, C, Lisp, or really
    anything else.
  - ROS supports fetching and installing packages with **apt-get**.
  - Fetching dependencies is different from installing them in the world
    of ROS.

### Best practices for dependencies

  - Source dependencies
      - Use wstool (see below)
      - Vendor dependencies or use `.rosinstall` files
      - Keep `.rosinstall` files version controlled
  - Binary dependencies
      - Use rosdep (see below)

### Fetching dependencies with rosdep

[rosdep](http://wiki.ros.org/rosdep) is a tool for installing 3rd party
binary and Python dependencies.

Typical use:

    rosdep install --from-paths ~/catkin_ws/src --ignore-src --rosdistro indigo -y -r --os=debian:jessie

Resources:

  - Tutorial <http://wiki.ros.org/ROS/Tutorials/rosdep>

Q\&A:

  - Q: can Python packages be bundled with install directory produced by
    [build\_tooling](build_tooling.md)?
      - A: it looks like no. It seems a rosdep install step is necessary
        for fully installing a package. See
        [update\_install\_self\_contained](/contributors/gordonb/update_install_self_contained)
        for more notes.

### rosinstall

[rosinstall](http://wiki.ros.org/rosinstall):
[.rosinstall](http://docs.ros.org/independent/api/rosinstall/html/)
files are yaml files that describe a list of git repositories or zip
files that point to source files for packages that the current workspace
depends on.

  - Q: why do you want this?
      - A: it is for catkin packages that are not available via rosdep,
        apt-get, or for managing a ROS project that is not a monorepo.
        You can also

Getting it:

    sudo apt-get install python-rosinstall

### rosinstall\_generator

You can generate `.rosinstall` files with
[rosinstall\_generator](http://wiki.ros.org/rosinstall_generator). The
tool catalogues dependencies recursively and creates a `.rosinstall`
file.

    sudo pip install rosinstall_generator

  - Q: is dependency searching recursive?
      - A: yes.

Example:

``` 
rosinstall_generator ros_comm rosserial rosserial_arduino usb_cam --rosdistro indigo --deps --wet-only --exclude roslisp --tar > indigo.rosinstall

```

You can exclude packages from other workspaces, or that have been
installed via `apt-get`, but adding them to your `ROS_PACKAGE_PATH`
(either manually or by sourcing a setup file) and use `--exclude RPP`.

### wstool

`wstool` is a tool for using `.rosinstall` files to set up a new
workspace (can be used for dependency installation).

Resources, examples:

  - <http://wiki.ros.org/wstool>
  - <http://sdk.rethinkrobotics.com/wiki/Baxter_Setup>
  - <http://sdk.rethinkrobotics.com/wiki/Workstation_Setup>
  - <http://sdk.rethinkrobotics.com/wiki/Workstation_Update>
  - <http://sdk.rethinkrobotics.com/wiki/Repository_Layout>

Getting it:

    sudo apt-get install python-wstool

Or:

    sudo pip install wstool

It must be initialized once:

``` 
wstool init ~/catkin_ws/src

```

Pulling in and installing dependencies from a `.rosinstall` file.

    wstool merge ~/catkin_ws/openag_brain/indigo.rosinstall

### Python Dependencies

#### Listing Python Dependencies

ROS has its own Python dependency management. **Don't use `pip`
directly.**

> If you have written non-ROS Python packages before, you have probably
> used the requires field in the distuils setup function. This field,
> however, has no meaning in ROS.

\>

> All your Python dependencies should be specified in package.xml as
> e.g. \<run\_depend\>python-numpy\</run\_depend\> (for older version 1
> of package.xml) or \<exec\_depend\>python-numpy\</exec\_depend\> (if
> you use format 2 of package.xml).

\>

> Not all Python or pip packages are mapped to ROS dependencies. For a
> quick check, try running rosdep resolve python-mypackage or rosdep
> resolve python-mypackage-pip if you want to add a dependency on
> mypackage Python package. If these calls return error, you may want to
> search through the python.yaml file in rosdep for similar names. If
> you don’t find the requested package, you may consider creating a Pull
> request to add it.
> 
> <http://docs.ros.org/api/catkin/html/user_guide/setup_dot_py.html>

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

This setup.py is only for use with catkin. Remember not to invoke it
yourself.

Put that script in the top directory of your package, and add this to
your CMakeLists.txt:

    catkin_python_setup()

#### What Python packages are supported by rosdep?

  - You can search for a package with `rosdep resolve python-mypackage`
  - A list can be found here
    <https://github.com/ros/rosdistro/blob/master/rosdep/python.yaml>
  - You can contribute new ones via PR
    <http://docs.ros.org/independent/api/rosdep/html/contributing_rules.html>

#### Installing Python Dependencies

Use rosdep from catkin workspace root:

    rosdep install --from-paths src --ignore-src --rosdistro indigo -y -r --os=debian:jessie

#### What do do if your Python package is unavailable

##### Contributing Python Dependencies to rosdep

You can contribute packages to the rosdep manifest. See
<http://docs.ros.org/independent/api/rosdep/html/contributing_rules.html>
for an overview.

You can also contribute python packages installable with pip by using
the `pip` keyword. For example, here's what it would look like to add
`quick2wire-api` to rosdep's manifest file
(<https://github.com/ros/rosdistro/blob/master/rosdep/python.yaml>):

    python-quick2wire-api:
      debian:
        pip:
          packages: [quick2wire-api]

###### Contributing Python Libraries to ROS Package Managers

ROS has a script to help package Python libraries and push them to the
various package managers ROS supports (apt, etc)
<https://github.com/ros-infrastructure/ros_release_python>. I'm not sure
this is frequently necessary, since you can also list pip sources.

Additionally, here are some links to APT resources:

  - Creating an APT package
    <https://debian-handbook.info/browse/stable/debian-packaging.html>
  - Creating an APT package repo
    <https://debian-handbook.info/browse/stable/sect.setup-apt-package-repository.html>

##### Adding your own list.d file

It should be possible to add your own YAML lists.

How to:
<http://docs.ros.org/independent/api/rosdep/html/contributing_rules.html#point-your-sources-list-d-at-your-forked-repository>

##### Vendoring Python Dependencies

How to: ?

### APT Repository

  - Q: does ROS have its own apt package repository that we can
    contribute to?
      - A:
        <http://answers.ros.org/question/12478/apt-get-source-for-packagesrosorg/>

See [Releasing Packages](releasing_packages.md) for more.

### List installed catkin packages (binary or source)

You can show the list of "seen packages" by running `rospack list` in
your current environment.
