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

### openag\_brain flash

    Usage: rosrun openag_brain flash
    
      Flash the Arduino with firmware read from configuration.
    
    Options:
    
      -d --build_dir  (optional) a directory in which to put the source files

Example:

``` 
rosrun openag_brain flash -d ~/build
  
```

#### flashing yaml format fixtures

Install:

    git clone https://github.com/openaginitiative/openag_python.git
    cd openag_python
    pip install -e .[flash]

Usage:

    openag firmware flash -f openag_launch/personal_food_computer_v2.yaml -t upload -p ros
