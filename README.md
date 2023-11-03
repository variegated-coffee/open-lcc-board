# Open LCC Board

Schematics and PCB files for the main Open LCC hardware. Licensed under the CERN OHL-P license.

This is an evolution of [magnusnordlander/smart-lcc](https://github.com/magnusnordlander/smart-lcc).

## Disclaimer

Anything you do with this, you do at your own risk. Components have been fried already during the course of this project. Your machine uses both line voltage power, high pressured hot water, steam and other dangerous components. Risks include but are not limited to, damaging the machine, personal injury, property damage and summoning dead Cthulhu from his sleep at R'lyeh.

## Architecture and feature set

* RP2040 MCU communicating over UART with the Control Board
  * 2 MB Program Flash
  * 2 MB Settings Flash
  * Micro SD Card Slot
  * 2x QWIIC expansion ports
* ESP32-S3-WROOM-1U-N16R8 MCU
  * Connector for SSD1309 128x64px OLED display (only one display can be used at a time)
  * Solder pads for ST9987V 1.47" Round Rectangle TFT display (only one display can be used at a time)
  * Two push buttons
  * 1x QWIIC expansion port
  * Antenna connector (Espresso machines are basically faraday cages, so an external antenna is a good idea)
* 5 wire bus between RP2040 and ESP32-S3
	* RX, TX, CTS, RTS, Serial Boot
* Debug port
  * Exposes RP2040 USB, RP2040 SWD, RP2040 BOOTSEL, RP2040 ~RESET, ESP32 USB, ESP32 JTAG, ESP32 GPIO0, ESP32 EN and power rails.

## Hardware revisions

### Smart LCC (various revisions, not maintained in this repository)

The earliest revisions of this board. Based around Arduino RP2040 Nano.

### R1A (r1a branch)

This design is NOT RECOMMENDED for any purpose. It relies on the Control Board providing 3V3 to the board, but the Control Board is not able to supply enough power. As such, it *does not work as intended*. 

It is however a major redesign from the Smart LCC, and added most of the features described above.

### R2A (r2a branch)

Latest manufactured revision, though if you want one of the boards, you may want to wait for R2B.

#### Changes from R1A

* Added I2C pull-up resistors for QWIIC expansion ports
* Added on-board DC-DC converter to step down 12V to 3V3.
* Added back side connector for 1.47" TFT
* Moved test points for display connector to back side
* Added full bus to RP2040 settings flash (n.b. not the program flash), allowing for QSPI via PIO instead of regular SPI
* Added QWIIC expansion port to ESP32-S3
* Added Test Points for unused RP2040 GPIOs
* Removed 3V3_OLED from debug port

#### Errata

* The Schottky diodes do not provide adequate power supply reverse current protection. **DO NOT SUPPLY POWER FROM BOTH A DEBUG BOARD AND A CONTROL BOARD SIMULTANEOUSLY**
* It is unnecessary to connect both SD_DET_A and SD_DET_B to an MCU.

### R2B (main branch)

This revision hasn't been completely manufactured, and I don't intend to do that either. I have ordered non-assembled PCBs, and will verify that the OR-ing controller design works as intended.

#### Changes from R2B

* Replaced the Schottky Diodes with two LM5050-1 OR-ing controllers.
* Connected SD card DET_A to GND, and removed the connection from the RP2040. 
* Widened traces and trace clearances, and added copper pours for improved manufacturability.