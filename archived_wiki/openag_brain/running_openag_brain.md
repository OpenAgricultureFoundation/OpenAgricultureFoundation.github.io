---
layout: wiki_archive
---

## Running openag\_brain

Now that you have [openag\_brain installed from
source](installing/installing_globally.md), let's get it up
and running.

### Running as a Service

In most cases (aside from troubleshooting and development), you'll want
to run [openag_brain](/archived_wiki/openag_brain.md) as a startup service. To run openag\_brain as
a service, run the following command from the Raspberry Pi terminal:

    sudo service openag_brain start

To stop the service at any time, run:

    sudo service openag_brain stop

### Running in the Terminal

On the Raspberry Pi:

    rosrun openag_brain main personal_food_computer_v2.launch

You can stop it at any time by hitting `ctl+C`.

### Reconfiguring openag\_brain

When we run `rosrun openag_brain main personal_food_computer_v2.launch`,
`personal_food_computer_v2.launch` marks the [Launch
File](/archived_wiki/ros/launch_files.md) we're asking ROS to run. This is a file that
configures the various components that make up openag\_brain. In future,
will be used to support multiple hardware configurations. See
[configuration](configuration.md) for more information.
