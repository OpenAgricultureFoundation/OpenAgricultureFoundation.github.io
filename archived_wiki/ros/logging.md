---
layout: wiki_archive
---

## Logging

[ROS](../ros.md) has it's own configurable logging utilities
<http://wiki.ros.org/rospy_tutorials/Tutorials/Logging>.

rospy has several methods for writing log messages, all starting with
"log":

    rospy.logdebug(msg, *args)
    rospy.logwarn(msg, *args)
    rospy.loginfo(msg, *args)
    rospy.logerr(msg, *args)
    rospy.logfatal(msg, *args)

These levels have a one-to-one correspondence to the rosout verbosity
levels. There are four potential places a log message may end up
depending on the verbosity level:

``` 
stdout: loginfo
stderr: logerr, logfatal, logwarn (ROS 0.9)
your Node's log file: all
the /rosout Topic: loginfo, logwarn, logerr, logfatal 
```
