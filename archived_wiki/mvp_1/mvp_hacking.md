---
layout: wiki_archive
---

## Hacking the MVP

The MVP code is almost all Python. Cron is used to schedule events
(lights ON and OFF), and some shell scripts (see: /home/pi/MVP/scripts)
are used to cluster activities.

Code is roughly divided into these groups:

  - Sensors
  - Actuators
  - Controllers
  - Utilities
  - Variables
  - Reports

Sensors are the code that interact with the physical sensors - things
that create information: thermometers, humidity sensors, ... Most of
this code was sourced from the internet, often from the vendor who sells
the sensor (ie. [Adafruit](https://www.adafruit.com/)). Some of this
code has been slightly modified for the MVP.

  - si7021.py (temperature/humidity sensor)

Actuators are physical things that get controlled: lights, fans, etc.
There is usually one or more files per object. Often these are wrappers
for the relay, as a relay is used for most of the switching
functionality. These are usually.

  - thermostat.py (controls the fan)
  - setLightOn.py (turns the lights On - called by cron)
  - setLightOff.py (turns the lights Off - called by cron)

Controllers are the business logic that connects Sensors and Actuators

  - adjustThermostat.py (responds to the temperature for fan adjustments
    - called by cron)

Utilities are miscellaneous functions that are helpers to other code:

  - logSensors.py (calls the sensors and records to the database)
  - logData.py (writes data to the database)

Variables persist state information and hold global variables used by
multiple programs. These are either dictionaries or JSON structures.

  - env.py (MAC address and location information, reservoir levels)
  - variable.py (target temperature, fan state (On or Off))

Reports create charts. These programs query the database and organize
the data into a chart file. These are run from
/home/pi/MVP/scripts/render.sh, which is called by cron.

  - getTempChart.py
  - getHumidityChart.py

### Code Design

There is some inconsistency in the code, which reflects changes in
knowledge and philosophy over time. Some code is organized as objects,
while other has function declarations.

Generally the code is self testing. At the end of the program there is a
test function which is run via:

` if name=="main":  `
