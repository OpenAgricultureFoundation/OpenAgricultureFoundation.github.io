---
layout: wiki_archive
---
This is a simple design pattern for creating a polling node in
[ROS](../ros.md).

    #!/usr/bin/env python
    import rospy
    from std_msgs.msg import Float64
    
    if __name__ == '__main__':
        pub = rospy.Publisher("some_topic", Float64, queue_size=10)
        rate = rospy.get_param("~rate_hz", 1)
        # Set polling rate to 1Hz (once-per-second)
        r = rospy.Rate(rate)
        # Keep looping as long as ROS is running
        while not rospy.is_shutdown():
            # Do something...
            # Publish the result
            pub.publish(temp)
            # Use rate timer instance to sleep until next turn
            r.sleep()

Note: nodes must be executable. Don't forget to `chmod +x` your file:

    chmod +x nodes/my_node
