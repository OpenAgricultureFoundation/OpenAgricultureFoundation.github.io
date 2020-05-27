---
layout: wiki_archive
---

## pid.py

  - Package: [/openag_brain/](../openag_brain.md)
  - Source Code:
    [openag\_brain.software\_modules.pid](https://github.com/OpenAgricultureFoundation/openag_brain/blob/master/src/openag_brain/software_modules/pid.py)
  - License: GPL 3.0
  - Issues: <https://github.com/OpenAgricultureFoundation/openag_brain/issues>

The
[openag\_brain.software\_modules.pid](https://github.com/OpenAgricultureFoundation/openag_brain/blob/master/src/openag_brain/software_modules/pid.py)
module is a Python implementation of a [PID
controller](https://en.wikipedia.org/wiki/PID_controller) for ROS. This
controller is useful for actuators that need to create a steady state in
a dynamic environment (for example, heating/cooling).

By default, it listens on a topic "desired" for the current set point
and a topic "state" for the current state of the plant being controller.
It then writes to a topic "cmd" with the output of the PID controller.
If the parameter `variable` is defined, these topics will be renamed as
follows. This makes it easy to integrate this PID controller with ROS
topics from firmware modules without remapping each of the topics
individually.

    desired -> /<environment_id>/desired/<variable>
    state -> /<environment_id>/measured/<variable>
    cmd -> /<environment_id>/commanded/<variable>

It also reads configuration from a number of other ROS parameters as
well. The controller gains are passed in as parameters `Kp`, `Ki`, and
`Kd`. It also accepts an `upper_limit` and `lower_limit` to bound the
control effort output. `windup_limit` defines a limit for the integrator
of the control loop. `deadband_width` can be used to apply a deadband to
the control effors. Specifically, commands with absolute value less than
`deadband_width` will be changed to 0.

### Configuration via Fixture

An example [fixture](0.1.0/fixtures.md) configuration for the PID
controller:

    {
      software_module: [
        {
           "_id": "air_temperature_loop",
           "type": "openag_brain:pid.py",
           "environment": "environment_1",
           "parameters": {
              "variable": "air_temperature",
              "Kp": 0,
              "Ki": 0,
              "Kd": 0,
              "upper_limit": 1,
              "lower_limit": -1,
              "windup_limit": 1000,
              "deadband_width": 0
           }
        }
      ]
    }

Note that `Kp`, `Ki`, and `Kd` (as well as `deadband_width`) would need
to be tuned for your given actuator to be useful. See [Wikipedia on PID
Controllers](https://en.wikipedia.org/wiki/PID_controller) for pointers
on how to tune a PID controller.

### PID with binary actuators

You can use a PID loop with
[openag\_binary\_actuator](https://github.com/OpenAgricultureFoundation/openag_binary_actuator)
by setting a `lower_limit` of 0, an `upper_limit` of 1 and a
`deadband_width` of 1.

    {
       "_id": "air_temperature_loop",
       "type": "openag_brain:pid.py",
       "environment": "environment_1",
       "parameters": {
           "variable": "air_temperature",
           "Kp": 0, // tune this
           "Ki": 0, // tune this
           "Kd": 0, // tune this
           "upper_limit": 1,
           "lower_limit": 0,
           "windup_limit": 1000,
           "deadband_width": 1
       }
    }

In your `binary_actuator` database record, it is also possible to set a
`multiplier` for a specific `input` or `output`. Commands from the
controller will be multiplied by this value before being passed to
actuator.

### Event Loop

Note that PID controller output is driven by sensor inputs. Each sensor
input produces one PID command output. This ensures that actuators are
driven by actual sensed environmental feedback.
