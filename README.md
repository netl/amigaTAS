# Software

requires https://github.com/MHeironimus/ArduinoJoystickLibrary

~~~~
capture.py devfile            : record a series of events
playback.py devfile           : playback previously captured series of events
remoteServer.py devfile       : listen for inputs from remote client
remoteClient.py devfile server: send inputs from joystick to remote server
~~~~

# Hardware

intput pinout
~~~~
\ 1 2 3 4 5 /
 \ 6 7 8 9 /
~~~~

| Pin | Name  | Input | Output |
| --- | ----- | ----- | ------ |
| 1   | UP    | A0    | 8      |
| 2   | DOWN  | A1    | 9      |
| 3   | LEFT  | A2    | 10     |
| 4   | RIGHT | A3    | 11     |
| 5   | -     | -     | -      |
| 6   | FIREA | A4    | 12     |
| 7   | -     | +5V   | +5V    |
| 8   | -     | GND   | GND    |
| 9   | FIREB | A5    | 13     |

output pins should be driven with an open-collector to imitate the controllers switches.
This could be fixed in code, but has been left for hardware to handle in order to simplify the firmware.

# Firmware

For TAS mode, hold *FIREA* on reset. For USB joystick mode hold *FIREB* on reset.  
All joystick input is sent over serial as a single byte (active low): [0, 0, FIREB, FIREA, RIGHT, LEFT, DOWN, UP]

# Notes

A separate configuration button should be added in order to avoid using the reset button unnecessarily. for example hot-swapping TAS mode when playing as an USB joystick can cause problems.
