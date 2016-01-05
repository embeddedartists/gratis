# gratis

This is a fork of the [repaper/gratis](https://github.com/repaper/gratis) repository that has been 
modified and tested to work with the [2.7" ePaper display module](http://www.embeddedartists.com/products/displays/lcd_27_epaper.php) from Embedded Artists.

The following changes have been made:

1. Removed TI LaunchPad and BeagleBone support as it has not be verified
2. Changed examples to default to the 2.7" display size
3. Removed images for the 1.44" and 2.0" displays
4. Updated documentation to reflect that the COG v2 is used
5. Removed examples that were not applicable
6. Replaced the S5813A temperature library with a LM75 library for the Arduino
7. Modified the flash driver to handle the Winbond W25Q32 that is mounted

## Sketches

The [Sketches](Sketches) folder contain example programs that will compile and run on the following platforms

1. Arduino Leonardo using the [Arduino](http://arduino.cc) IDE
2. Arduino Uno using the [Arduino](http://arduino.cc) IDE

## PlatformWithOS

The [PlatformWithOS](PlatformWithOS) folder contain contains an example driver and Python demo programs that can be
compiled and run on:

1. [Raspberry Pi](http://www.raspberrypi.org/)

======

Gratis is a Repaper.org repository, initiated by E Ink and PDI for the purpose of making sure ePaper can go everywhere.
