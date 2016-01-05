# E-Ink for Arduino

Table of contents

* [Introduction](#introduction)
* [Connecting Arduino to the ePaper Board](#connecting-arduino-to-the-epaper-board)
* [Development Tools](#development-tools)
* [Libraries](#libraries)
* [Example Programs](#example-programs)
  * [Demo Sketch](#demo-sketch)
  * [Command Sketch](#command-sketch)
  * [Flash Loader Sketch](#flash-loader-sketch)

## Introduction

This project officially supports the Arduino-based platform. The Ti LaunchPad support that is 
available in the original [repaper/gratis](https://github.com/repaper/gratis) repository 
has been commented out and is completely untested.

The examples have been verified on [Arduino Leonardo](http://arduino.cc/en/Main/ArduinoBoardLeonardo) (R3) and [Arduino Uno](http://arduino.cc/en/Main/ArduinoBoardUno) (R2) boards using
the 1.0.5 version of the IDE.

## Connecting Arduino to the ePaper Board

> See: Schematics for the [2.7 inch E-paper Display Module](http://www.embeddedartists.com/products/displays/lcd_27_epaper.php), Arduino Leonardo ([PDF](http://arduino.cc/en/uploads/Main/arduino-leonardo-schematic_3b.pdf)) and Arduino Uno ([PDF](http://arduino.cc/en/uploads/Main/Arduino_Uno_Rev3-schematic.pdf))

The display module have two 14-pin connectors (J2 is 50mil and J3 is 100mil) and one 26-pin
connector (J5). Any one of them can be used to connect the display board to the Arduino board.

One way to connect the display module is to use [jumper wires](http://www.embeddedartists.com/products/acc/acc_wire_fm.php). The table below shows where each wire should be connected:

<table>
  <tr><th colspan="2">Arduino Leonardo</th><th colspan="2">Arduino Uno</th><th colspan="2">Arduino Mega 2560</th><th colspan="2">Display, 14-pin connector</th></tr>
  <tr><th>Pin #</th><th>Signal</th><th>Pin #</th><th>Signal</th><th>Pin #</th><th>Signal</th><th>Pin #</th><th>Signal</th></tr>
  <tr><td>GND</td><td>GND</td>     <td>GND</td><td>GND</td>     <td>GND</td><td>GND</td>  <td>1</td><td>GND</td></tr>
  <tr><td>3V3</td><td>3V3</td>     <td>3V3</td><td>3V3</td>     <td>3V3</td><td>3V3</td>  <td>2</td><td>3V3</td></tr>
  <tr><td>ICSP-3</td><td>SCK</td>  <td>ICSP-3</td><td>SCK</td>  <td>52</td><td>SCK</td>   <td>3</td><td>SCK</td></tr>
  <tr><td>ICSP-4</td><td>MOSI</td> <td>ICSP-4</td><td>MOSI</td> <td>51</td><td>MOSI</td>  <td>4</td><td>MOSI</td></tr>
  <tr><td>ICSP-1</td><td>MISO</td> <td>ICSP-1</td><td>MISO</td> <td>50</td><td>MISO</td>  <td>5</td><td>MISO</td></tr>
  <tr><td>8</td><td>GPIO</td>      <td>8</td><td>GPIO</td>      <td>8</td><td>GPIO</td>   <td>6</td><td>SSEL</td></tr>
  <tr><td>7</td><td>GPIO</td>      <td>7</td><td>GPIO</td>      <td>7</td><td>GPIO</td>   <td>7</td><td>Busy</td></tr>
  <tr><td>10</td><td>GPIO</td>     <td>10</td><td>GPIO</td>     <td>10</td><td>GPIO</td>  <td>8</td><td>Border Ctrl</td></tr>
  <tr><td>SCL/3</td><td>SCL</td>   <td>SCL/A5</td><td>SCL</td>  <td>21</td><td>SCL</td>   <td>9</td><td>SCL</td></tr>
  <tr><td>SDA/2</td><td>SDA</td>   <td>SCL/A4</td><td>SDA</td>  <td>20</td><td>SDA</td>   <td>10</td><td>SDA</td></tr>
  <tr><td>9</td><td>GPIO</td>      <td>9</td><td>GPIO</td>      <td>9</td><td>GPIO</td>   <td>11</td><td>CS Flash</td></tr>
  <tr><td>6</td><td>GPIO</td>      <td>6</td><td>GPIO</td>      <td>6</td><td>GPIO</td>   <td>12</td><td>Reset</td></tr>
  <tr><td>5</td><td>GPIO</td>      <td>5</td><td>GPIO</td>      <td>5</td><td>GPIO</td>   <td>13</td><td>Pwr</td></tr>
  <tr><td>4</td><td>GPIO</td>      <td>4</td><td>GPIO</td>      <td>4</td><td>GPIO</td>   <td>14</td><td>Discharge</td></tr>
</table>

The only difference in pinning between the Leonardo and Uno boards is where to connect the I2C/Wire pins (SDA/SCL).


## Development Tools

This project officially supports the Arduino-based platform.

The [Arduino web site](http://www.arduino.cc) has download links for
Windows, Mac OS/X and other operating systems.

Note: [Java](http://java.com) is necessary to run the GUI, but it is
possible to install a command line only version.

## Libraries

> Link to the [libraries source](https://github.com/embeddedartists/gratis/tree/master/Sketches/libraries).
(copy all of these to you local libraries folder)

* **Images** - Sample XBM files.  The demo program includes two of
  these directly.  The Command program can use these files for its
  upload command.
* **FLASH** - Driver for the SPI FLASH chip on the EPD eval board.
* **EPD2** - E-Ink Panel driver (COG V2) *experimental*.
* **LM75** - Temperature sensor driver.


# Example Programs

**IMPORTANT NOTES for COG V2**

1. The programs below only support the COG V2 using the `EPD2` library.
2. The COG V2 does not use PWM - the pin is used as chip select for the
   onboard SPI-NOR flash instead.


## Demo Sketch

> Link to the [demo2 source](https://github.com/embeddedartists/gratis/tree/master/Sketches/demo2).

This example first clears the screen, then toggles between two images.
It needs the serial port (9600 8N1) connected and displays the version,
temperature and compensation values on each cycle.

This is built upon the EPD2 API in the libraries folder and shows how
to use the API to display images from the MCU FLASH.  Only a few images
are possible to be stored since the on-chip FLASH is limited.


## Command Sketch

> Link to the [command2 source](https://github.com/embeddedartists/gratis/tree/master/Sketches/command2).

A command-line example that accepts single character command from the
serial port (9600 8N1).  Functions include XBM upload to the SPI FLASH
chip on the display board, display image from this FLASH and
several other functions.

Use the `h` command on the serial port (9600 8N1) to obtain a list of
commands.  Some of the commands are shown like `e<ss>` this *<ss>*
represents a two digit FLASH sector number in the range *00..ff* (a
total of 256 sectors).  The 1.44" and 2.0" display images take one sector
but the 2.7" displays take *two* adjacent sectors - this means that 
it is necessary to issue both `e00` and `e01` before uploading a 2.7" image
with `u00`.

When using the serial monitor on Arduino/Energia IDE any command that
take a hex number as parameter needs a `<space>` character after it, as
the **Send** button will not automatically add a CR/LF.  For single
letter commands like the `t` temperature sensor read just type the
character and click **Send**.

The 4 stage display cycle is split into two separate commands. The `r`
command removes an image and the `i` command displays an image.
e.g. if the current image was from sector 30 and you wanted to change
to sector 43 then type `r30<space>i43<space>` into the serial monitor
and click **Send**.

The upload command `u` need a terminal emulator with ASCII upload
capability or the ability to respond to a paste of the entire contents
of an XBM file.  Also note that the `u` command does not erase the
sector before uploading.  To use the upload to upload an XBM into
sector 3b for example type `u3b<space>` then start the ASCII upload or
paste the contents of the XBM file into the terminal window on upload
completion an image size message is displayed.

The image stored is compatible with the flash_loader sketch as
described below and that program can be used to cycle through a set of
images uploaded by this program.

Typical use: `h` to bring up the help, `t` to check that the temperature
is working and then `w` to clear the display. To upload an image do `e00`,
`e01` and then `u00`. Send the image file from the terminal program and then
type `i00` to display it.

## Flash Loader Sketch

> Link to the [flash loader source](https://github.com/embeddedartists/gratis/tree/master/Sketches/flash_loader2).

This program has two modes of operation:

1. Copy a #included image to the FLASH chip on the eval board.  define
   the image name and the destination sector.  After programming the
   image will be displayed

2. Display a sequence of images from the FLASH chip on the eval board.
   A list of sector numbers an millisecod delay times defined by the
   `DISPLAY_LIST` macro to enable this mode.  In this mode the flash
   programming does not occur.  The images are stored in the same
   format as the command program above, so any images uploaded by it
   can be displayed by this program

The configuration of both modes is handled in this block of code:

<pre><code>// select image from:  text_image cat ea aphrodite venus saturn
// select a suitable sector, (size 270 will take two sectors)
#define IMAGE         ea
#define FLASH_SECTOR  0

// if the display list is defined it will take priority over the flashing
// (and FLASH code is disbled)
// define a list of {sector, milliseconds}
//#define DISPLAY_LIST {0, 3000}, {2, 3000}, {4, 3000}
</code></pre>

Note: To show three different images with the `DISPLAY_LIST` as shown 
above you will have to upload the program four times to the Arduino:

1. `DISPLAY_LIST` not defined, `IMAGE` is e.g. *ea*, `FLASH_SECTOR` is *0*
2. `DISPLAY_LIST` not defined, `IMAGE` is e.g. *cat*, `FLASH_SECTOR` is *2*
3. `DISPLAY_LIST` not defined, `IMAGE` is e.g. *venus*, `FLASH_SECTOR` is *4*
4. `DISPLAY_LIST` defined and set to *{0, 3000}, {2, 3000}, {4, 3000}*
