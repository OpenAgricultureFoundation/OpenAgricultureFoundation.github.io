---
layout: wiki_archive
---

## ROS and libboost

[ROS](../ros.md) [uses libboost extensively](http://wiki.ros.org/boost), so ROS
environments need to have it installed.

libboost can be installed via `apt-get`.

  - Q: does the ROS source install process install libboost?
  - Q: does the Raspbian Jessie ship with libboost?
  - Q: does the apt-get package for ros install libboost as a
    dependency?
  - Q: do you need to install libboost when building a Docker container?
      - A: most Docker container images are minimal, so it's likely
        you'll need to install it via apt-get.
