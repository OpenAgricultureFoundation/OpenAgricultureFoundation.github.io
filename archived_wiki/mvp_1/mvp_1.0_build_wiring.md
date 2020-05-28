---
layout: wiki_archive
---

### MVP 1.0 Wiring

The following are instructions for connecting jumper wires between the
Raspberry Pi, the SI7021 sensor and the relay; and well as instructions
for wiring up the fan and lights to the relay.

Materials:

  - Raspberry Pi
  - SI7021 sensor
  - Female-Female jumper wires

**NOTE**: The inner row of pins on the Raspberry Pi, starting at the end
away from the USB ports, are numbered 1, 3, 5, 7, ....; the outer row
are numbered 2, 4, 6, 8 .... See the
following|[diagram](https://docs.particle.io/datasheets/raspberrypi-datasheet/):
![](/static/images/wiki/mvp/pi-pinout-diagram-01.png)

Fritzing Diagram ![](/static/images/wiki/mvp/mvp-1.0_bb.jpg)

#### Si7021

1.  Wire pin 1 (3V) to sensor pin 2 (3vo)
2.  Wire pin 3 (SDA) to sensor pin 5 (SDA)
3.  Wire pin 5 (SCL) to sensor pin 4 (SCL)
4.  Wire pin 9 (GND) to sensor pin 3 (GND)

#### Relay

1.  Wire pin 2 (5V) to relay pin 6 (VCC)
2.  Wire pin 29 to relay pin 5 (IN4) – used by lights
3.  Wire pin 31 to relay pin 4 (IN3) – not used at this time
4.  Wire pin 33 to relay pin 3 (IN2) – not used at this time
5.  Wire pin 35 to relay pin 2 (IN1) – used by fan
6.  Wire pin 39 to relay pin 1 (GND)

\=== Relay to Fan === == Material:==

  - Relay board
  - Fan
  - Jumper wire (with ends clipped off and stripped)
  - Screw plug

**NOTE**: The fans I have, have three wires. The middle wire is voltage,
and the ground is on the outside (right facing the plug).
![](/static/images/wiki/mvp/img_20170629_095103.jpg) ![](/static/images/wiki/mvp/img_20170629_095134.jpg)

1.  Clip the ends of a jumper wire and strip the plastic coating off,
    exposing 3/8 inch of the wire.
2.  Unscrew the middle (second) terminal of relay 1, insert one end of
    the jumper wire, and tighten the terminal screw back down.
3.  Unscrew the power side of the plug, insert the other end of the
    jumper wire, and tighten.
4.  Clip the plugs from the fan.
5.  Unscrew the right ( 3rd) terminal of relay 1, insert the jumper
    wire, and tighten the terminal screw back d(f) 
6.  Test the fan: plug in a 12v transformer into the plug. Since the 3rd
    terminal of the relay is the ‘LOW ON’ terminal, the fan should come
    on even if there is no power to the Raspberry and relay.

##### Relay to Lights

###### Material:

  - Relay board
  - Extension Cord
  - Cable Tie

**NOTE**: You are working with 110V circuitry. Make sure the Raspberry
Pi and the extension cord are NOT plugged in while working on the wires.

1.  Fold the extension cord in half to find the middle.
2.  ![](/static/images/wiki/mvp/img_20170629_101515.jpg)
3.  Carefully split the outer covering of the extension cord 4 inches in
    each direction from the middle (total of 8 inch cut), exposing the
    wires inside. The wires are wrapped in paper, so there is a bit of
    safety to avoid cutting the wires. Remove the paper.
4.  Cut the white wire (power) in the middle.
5.  ![](/static/images/wiki/mvp/img_20170629_101837.jpg)
6.  Loop the extension cord in the middle where the covering was split
    and secure the loop with a 4 inch cable tie. The base of the white
    wires should be near each other, fold the ends out so they are easy
    to work with.
7.  Strip 3/8 inch of covering off the exposed ends of the white wire.
8.  Unscrew the middle terminal of the 4th relay.
9.  Insert the end of the white wire coming from the wall plug (power
    coming in). Push it in so that no bare wire is exposed and tighten
    the terminal.
10. Loosen the 3rd terminal of the 4th relay. Insert the end of the
    white wire going to the lights into the 3rd terminal of the 4th
    relay and tighten. 
11. ![](/static/images/wiki/mvp/img_20170629_102842.jpg)

Finished wiring ![](/static/images/wiki/mvp/img_20170630_203414.jpg)
