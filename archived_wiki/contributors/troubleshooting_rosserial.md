---
layout: wiki_archive
---

## rosserial troubleshooting

  - **Audience**: developers
  - **Status**: notes

### Loose notes

  - We can remove arduino\_handler node and replace with simple call to
    rosserial

### Issues

  - rosserial:
      - Max possible number of topics is fewer than we need
          - Hard limit is associated with the architecture of the
            microcontroller
          - For Arduino the limit is 25 (dig up rosserial\_arduino help
            page that explicitly goes over this)
      - Buffer overflow can easily happen in communication channel
        between Arduino and Pi.
      - tcip timeout issues
          - "Inbound TCIP connection failed. Connection terminated
            before handshake received"
              - This could be due to exiting a rostopic echo.
      - serial port permission error / TERMIOS.error: flush input by
        rosserial. Acts like it doesn't have access to serial port
        anymore.
          - <https://github.com/OpenAgInitiative/openag_brain/issues/169>
  - Arduino-specific issues:
      - If I2C crashes, Wire library can not recover (does not try to
        reconnect).
      - You have to flash the Pi and the Arduino. This means lots of
        dependencies and more complex install experience.
  - Message checksum doesn't match after being received by the
    RaspberryPi
      - \[INFO\] \[WallTime: 1494245506.863639\] wrong checksum for
        topic id and msg
  - firmware:
      - PH actuator (pump):
          - <https://trello.com/c/99HgSuYq/999-debug-water-potential-hydrogen-firmware-issue-causing-lose-sync-to-arduino-and-raspberrypi-2d>
          - Publish desired ph
          - loses sync
          - reconnects every 15-30s
          - Hypothesis:
              - maybe some infinite loop here? Do we have ph solution?
              - Could be blocking firmware?

<!-- end list -->

  - New Error:

\[WARN\] \[WallTime: 1494400740.918298\] Serial Port read returned short
(expected 8 bytes, received 0 instead). \[WARN\] \[WallTime:
1494400740.929768\] Serial Port read failure: \[WARN\] \[WallTime:
1494410198.026585\] Serial Port read returned short (expected 485 bytes,
received 462 instead).
