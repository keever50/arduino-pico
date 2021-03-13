# arduino-pico
Raspberry Pi Pico Arduino core, for all RP2040 boards

This is an under-development port of the RP2040 (Raspberry Pi Pico processor) to the Arduino ecosystem.

It uses a custom toolset with GCC 10.2 and Newlib 4.0.0, not depending on system-installed prerequisites.  https://github.com/earlephilhower/pico-quick-toolchain

The biggest hurdle was getting a working build system outside of the pick-sdk CMake environment.
Presently, a manually build `pico.a` file is generated using objects compiled by `cmake` in the pico-examples repo, but in the future this will be scripted and automated.

There is automated discovery of boards in bootloader mode, so they show up in the IDE, and the upload command works using the Microsoft UF2 tool (included).

To install:
````
mkdir -p ~/Arduino/hardware/pico
git clone https://github.com/earlephilhower/arduino-pico.git ~/Arduino/hardware/pico/rp2040
cd ~/Arduino/hardware/pico/rp2040
git submodule init
git submodule update
cd pico-sdk
git submodule init
git submodule update
cd ../system
python3 ./get.py
`````

Lots of things are working now!
* digitalWrite/Read (basic sanity tested)
* shiftIn/Out (tested using Nokia5110 https://github.com/ionpan/Nokia5110)
* SPI (tested using SdFat 2.0 https://github.com/greiman/SdFat ... note that the Pico voltage regulator can't reliably supply enough power for a SD Card so use external power)
* analogWrite/PWM (tested using Fade.ino)
* Wire/I2C (tested using DS3231 https://github.com/rodan/ds3231)
* EEPROM (tested examples)

If you want to contribute or have bugfixes, drop me a note at <earlephilhower@yahoo.com> or open an issue/PR here.

-Earle F. Philhower, III
 earlephilhower@yahoo.com