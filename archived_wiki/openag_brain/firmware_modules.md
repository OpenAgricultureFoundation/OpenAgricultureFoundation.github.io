## Firmware Modules

OpenAg interacts with the environment through many sensors and actuators
that are controlled by an [Arduino](https://www.arduino.cc/). Each of
these devices has a module in order to control them or read measurements
from them. Their interfaces are written in C++ and are compiled via a
pipeline of [openag\_python cli](/openag_python/cli) and
[PlatformIO](http://platformio.org/) commands.

Modules define classes that inherit from the [openag firmware
superclass](https://github.com/OpenAgInitiative/openag_firmware_module),
which is well documented
[here](http://openag-python.readthedocs.io/en/latest/firmware_modules.html).
Don't forget to check out some of the [firmware
examples](https://github.com/OpenAgInitiative/openag_firmware_examples).

### Sensors

  - [Atlas pH
    sensor](https://github.com/OpenAgInitiative/openag_atlas_ph)
  - [Atlas Oxidation-Reduction Potential (ORP)
    sensor](https://github.com/OpenAgInitiative/openag_atlas_orp)
  - [Atlas Electrical Conductivity (EC)
    sensor](https://github.com/OpenAgInitiative/openag_atlas_ec)
  - [Atlas Dissolved Oxygen (DO)
    sensor](https://github.com/OpenAgInitiative/openag_atlas_do)
  - [Atlas light spectrum and intensity
    sensor](https://github.com/OpenAgInitiative/openag_atlas_rgb)
  - [BH1750 digital light intensity (flux)
    sensor](https://github.com/OpenAgInitiative/openag_bh1750)
  - [AM2315 air temperature and humidity
    sensor](https://github.com/OpenAgInitiative/openag_am2315)
  - [DHT22 air temperature
    sensor](https://github.com/OpenAgInitiative/openag_dht22)
  - [DS18B20 temperature
    sensor](https://github.com/OpenAgInitiative/openag_ds18b20)
  - [MHZ16 CO2 sensor](https://github.com/OpenAgInitiative/openag_mhz16)
  - [GC0012 ambient CO2
    sensor](https://github.com/OpenAgInitiative/openag_gc0012)

### Actuators

  - [Binary (switch)
    actuator](https://github.com/OpenAgInitiative/openag_binary_actuator)
  - [PWM
    actuator](https://github.com/OpenAgInitiative/openag_pwm_actuator)
  - [Software-driven PWM
    actuator](https://github.com/OpenAgInitiative/openag_software_pwm_actuator)

### Calibration

TODO
