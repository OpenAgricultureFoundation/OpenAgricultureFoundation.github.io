---
layout: wiki_archive
---
## openag\_brain Configuration

  - **Audience**: makers, developers
  - **Skill Level**: beginner

Developer documentation for configuring [openag\_brain](/archived_wiki/openag_brain.md).

### Launch Files

[openag\_brain](/archived_wiki/openag_brain.md) is a [ROS](/archived_wiki/ros.md) program, and like all ROS programs,
it's made up of many small nodes, configured by a [Launch
file](/archvied_wiki/ros/launch_files.md). When we run `rosrun openag_brian main
personal_food_computer_v2.launch`, the
`personal_food_computer_v2.launch` bit denotes the launch file we're
asking ROS to run. This is a file that configures the various components
that make up openag\_brain. See
[configuration](configuration.md) for more information.

Right now there is only one configuration (for the [Food
Computer 2](/archived_wiki/food_computer_2.md)), but openag\_brain can be customized
by writing your own launch file. The purpose of this architecture is to
allow multiple "species" of Food Computer to be run from the same
codebase. If you're a developer interested in exploring this more, see
openag\_brain's [configuration](configuration.md) page.
