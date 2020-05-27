## openag\_brain CLI

[](/openag_brain/) commands are typically accessed through
[rosrun](http://wiki.ros.org/rosbash#rosrun).

For example: `rosrun openag_brain main personal_food_computer_v2.launch`

### openag\_brain main

To start running the openag\_brain system:

    usage: main [-h] [-A API_SERVER] [-D DB_SERVER] [--screen] launch_file

    Runs the entire software project. In particular, it initializes the database
    (init_db) and runs the roslaunch file.
    
    positional arguments:
      launch_file           The path to the .launch file to use
      
    optional arguments:
      -h, --help            show this help message and exit
      -A API_SERVER, --api_server API_SERVER
                            Address of the API from the api module
      -D DB_SERVER, --db_server DB_SERVER
                            Address of the database server
      --screen              Passes the --screen flag to the roslaunch call, which
                            forces all node output to the screen. Useful for
                            debugging.

Load a built-in fixture before starting by putting it in the (default)
`catkin_ws/src/openag_brain/launch/personal_food_computer_v2.launch`
file.

### openag\_brain firmware

Used to build the firmware and flash it to the Arduino board. The latest
[details are
here.](https://github.com/OpenAgInitiative/openag_brain/blob/master/doc/firmware.rst)

You must initialize the platform I/O system one time:

``` 
rosrun openag_brain init_pio

```

Firmware help:

``` 
rosrun openag_brain firmware -h

```

To just build the firmware:

``` 
rosrun openag_brain firmware launch/personal_food_computer_v2.yaml

```

To build the firmware and flash it to the Arduino board:

``` 
rosrun openag_brain firmware –target upload launch/personal_food_computer_v2.yaml

  
```
