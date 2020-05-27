---
layout: wiki_archive
---

## ROS Messages

[ROS](../ros.md) uses strongly-typed messages for
[topics](http://wiki.ros.org/Topics).

  - Each package can define its own message types
  - Packages define messages using `.msg` files that are then compiled
    into executable code for your language (C++, Python, etc) that will
    box and translate the data from one node to another.
  - `.msg` files go in the `msg/` subdirectory of your package. ROS will
    automatically find them there.

ROS also has messages for common datatypes:

  - [std\_msgs](http://wiki.ros.org/std_msgs) for basic types (Boolean,
    Float32, etc)
  - [common\_msgs](http://wiki.ros.org/common_msgs) for common robotics
    message types

### Defining new message types

(See <http://wiki.ros.org/msg>)

Each field consists of a type and a name, separated by a space, i.e.:

    fieldtype1 fieldname1
    fieldtype2 fieldname2
    fieldtype3 fieldname3

For example:

    int32 x
    int32 y

#### Defining Defaults

Fields are assigned 0-values (or empty strings, etc) when initialized.
You can't customize the default value in the message definition file,
but you could derive a class constructor in Python that initializes
these values. Here's a basic example:

    from openag_brain.msg import Foo
    class MyFoo(Foo):
        def __init(x=1, y=2, z=3):
            self.x = x
            self.y = y
            self.z = z

### Calling Message Constructors

What does it look like to call the constructor for a custom message
type? See
<http://wiki.ros.org/rospy/Overview/Messages#Message_initialization>.

You can initialize an empty message and add the fields after
([source](http://wiki.ros.org/ROS/Tutorials/CustomMessagePublisherSubscriber\(python\))):

    msg = Person()
    msg.name = "ROS User"
    msg.age = 4

You can use ordered arguments. The argument order is the same as the
order of the fields in the Message.

    msg = std_msgs.msg.String("hello world")
    msg = std_msgs.msg.ColorRGBA(255.0, 255.0, 255.0, 128.0)

Keyword arguments (in Python):

``` 
msg = std_msgs.msg.String(data="hello world")

```

you only initialize the fields that you wish to provide values for. The
rest receive default values (e.g. 0, empty string, etc...).

### Union/Enum/Optional Types

  - Q: can messages describe union/enum types?
      - A: No, but [you can use
        constants](http://wiki.ros.org/msg#Constants).
      - See <http://answers.ros.org/question/9427/enum-in-msg/>.
      - It may be added to next-gen ROS
        <https://discourse.ros.org/t/optional-fields-in-message/991>

> "I know users generally assign a sentinel value (i.e. NaN or 0xFFFF),
> when there no value is present; but it would be more semantic to build
> it into the message."
> ([source](https://discourse.ros.org/t/optional-fields-in-message/991))

### Resources

  - <http://wiki.ros.org/msg>
