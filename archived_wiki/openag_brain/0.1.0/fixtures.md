## Fixtures

[](/openag_brain/) can be configured with different sensors, actuators
and control loops using **fixtures**. This can be used to customize the
software for the [](/openag/food_computer_2.0/) or, in future, the [Food
Server](/openag/Food%20Server).

Fixtures for [](/openag_brain/) are written as JSON files. These files
are loaded into the [database](database) when [](/openag_brain/) starts.

### Default fixtures

[](/openag_brain/) ships with some useful default fixtures. They can be
found in
<https://github.com/OpenAgInitiative/openag_brain/tree/master/fixtures>.

### Starting openag\_brain with fixtures

You can start [](/openag_brain/) with a specific set of fixtures. Note
this is typically taken care of for you by
[Docker](/openag_brain/Docker), so this is mostly useful when
[developing](/food_computer_2/development) or customizing the
[](/openag/food_computer_2.0/).

  - `-f` will load one of the default fixtures by name (e.g. `-f
    default`)
  - `-F` will load a fixture file from the given file path

Starting openag\_brain with the default fixture:

    rosrun openag_brain main -f default

Starting openag\_brain with a custom fixture:

    rosrun openag_brain main -F ~/path_to_my_fixture.json

### Loading fixtures

You can also load fixtures any time CouchDB is running using the
[openag\_brain command line tool](/openag_brain/cli). To load a default
fixture from [](/openag_brain/):

    rosrun openag_brain load_fixture [fixture_name]

For example to load fixture `default`:

    rosrun openag_brain load_fixture default

(Note: you'll need to activate the [ROS workspace](/openag_brain/ros)
before you can use `rosrun` commands.)

To load a fixture file at its path, you can use the [openag\_python
command line tools](/openag_python/cli):

    openag db load_fixture ~/path/to/my_fixture.json

### Fixture schema

Default configurations for the database can be created with
\*fixtures\*. Fixtures are JSON documents that describe records that
should be added to the database.

You can find the default JSON fixtures in
<https://github.com/OpenAgInitiative/openag_brain/tree/master/fixtures>.

Fixtures follow the format::

    {
      database_name: [
        {
          _id: 'couchdb_doc_1',
          ...
        }
      ]
    }

Where each key in the top level object is the name of a Couch database
and each object in the array is a Couch document.

### Firmware Module Fixtures

One place where fixtures come in handy is configuring a [firmware
module](/openag_brain/firmware_modules) setup for a particular Food
Computer or Food Server model. Let's look at an example
`firmware_module` database fixture:

    {
      "firmware_module": [
        {
          "_id": "dht22_1",
          "type": "dht22",
          "environment": "environment_1",
          "arguments": [5],
          "outputs": {
            "air_temperature": {"variable": "air_temperature"},
            "air_humidity": {"variable": "air_humidity"}
          }
        }
      ]
    }

`firmware_module` is the database we're creating a fixture for. Within
it is a list of JSON documents.

  - `_id`: an id for the record
  - `type`: the firmware module ID, as defined in the
    `firmware_module_type` database. This tells the system what firmware
    module code to flash the Arduino with for this piece of firmware.
  - `environment`: the ID of the environment this sensor or actuator has
    been installed in. For most setups, this is `environment_1`.
  - `arguments`: configuration arguments to pass to the firmware module.
    These are typically pin numbers. See the firmware module's
    documentation or class definition for specifics.
  - `outputs`: a dictionary of keyed output ports. In the case of the
    example, the `dht22_1` outputs two sensing points (`air_temperature`
    and `air_humidity`). We map these outputs to environmental variable
    types.
  - `inputs`: some firmware may receive inputs for configuration or
    actuation.

Default values for `arguments`, `outputs` and `inputs` can be configured
for each firmware type in the `firmware_module_type` database, so you
don't always have to specify all of these to configure a module.

### Firmware Type Fixtures

The `firmware_module_type` database describes module types installed and
supported by the system. It acts as a package manager and glue layer for
the C++ firmware code that is flashed on to the Arduino.

Let's look at an example `firmware_module_type` database fixture:

    {
      "firmware_module_type": [
        {
          "_id": "atlas_do",
          "repository": {
            "type": "git",
            "url": "https://github.com/OpenAgInitiative/openag_atlas_do.git"
          },
          "description": "",
          "header_file": "openag_atlas_do.h",
          "class_name": "AtlasDo",
          "arguments": [
            {
              "name": "i2c_address",
              "type": "int",
              "default": 97
            }
          ],
          "inputs": {
            "atmospheric_calibration": {
              "type": "std_msgs/Empty",
              "categories": ["calibration"]
            },
            "zero_calibration": {
              "type": "std_msgs/Empty",
              "categories": ["calibration"]
            }
          },
          "outputs": {
            "water_dissolved_oxygen": {
              "type": "std_msgs/Float32"
            }
          },
          "dependencies": [
            {"type": "git", "url": "https://github.com/OpenAgInitiative/openag_firmware_module.git"}
          ]
        }
      ]
    }

Let's go over these fields:

  - `_id`: an id for the record. This is the same ID used in the `type`
    field of `firmware_module` records.
  - `repository`
      - `type`: this should nearly always be `git`
      - `url`: the url of the Git repository
  - `description`: a friendly description of the module
  - `header_file`: the path to the C++ header file for the module.
  - `class_name`: the name of the class defined by the module file.
  - `arguments`: an array of named arguments to the module.
      - `name`: the name key of the argument
      - `type`: datatype (int, bool, ...)
      - `default`: (optional) a default value for this argument.
  - `inputs`: a object of named inputs for the module (if any). The key
    is the name of the argument. The value should be an object with two
    fields:
      - `type`: the datatype (usually a ROS topic type)
      - `categories`: an array of category keywords.
  - `outputs`: an object of named outputs for the module. The key should
    be the name of the output. The value should be an object with one
    field:
      - `type`: the datatype (usually a ROS topic type) 
  - `dependencies`: an array of other OpenAg modules this module depends
    on. Each dependency is an object of:
      - `type`: usually `git`.
      - `url`: the url of the repository.
