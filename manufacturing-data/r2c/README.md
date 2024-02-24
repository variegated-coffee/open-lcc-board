# How to order and assemble

## PCB and PCBA manufacturer

This directory contains Gerber files for the PCB, a BOM file with LCSC numbers for ordering with JLCPCB, and a CPL file. When ordering, it's *highly* recommended to also order a debug board. It is possible to flash the boards without one, but you'll have to solder on a USB cable to test points.

### Orientations

Be careful with the orientation of the debug board FPC connector. Pin 1 is indicated on the board. When placed correctly on both the Open LCC and Debug board, you should use an FPC cable with *connectors on opposite sides*. If for some reason the connector is incorrectly oriented, you'll still be able to use the boards, but you may need an FPC cable with connectors on the *same* side. 

Orientations in general are a bit of a pain. I recommend checking the "Confirm production files" option on JLCPCB, to be able to verify that the orientations of all the components match the PCB and schematic.

## Parts you'll need from other vendors

The BOM in the file isn't complete; you'll need a few other parts, some of which are hand soldered. Below is a table, including links to Digikey when the item is available there.

Of special note is the display. You can use either a Color TFT or an OLED. The OLED matches what's in the stock LCC, and is easy to install. The TFT requires some soldering skills to install, but is a lot higher resolution. Pick one. Also, at least the OLED (or rather a compatible one) is also available on Digikey, but it's *a lot* more expensive than on AliExpress.

| Designator  | Part name                   | Notes                                                                                                             | URL (for one vendor, usually there are others)                                            |
|-------------|-----------------------------|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| J1          | TE 280372-1                 | You *can* use a standard 2.54 mm pin header instead, but this is highly recommended.                              | https://www.digikey.se/en/products/detail/te-connectivity-amp-connectors/280372-1/2276004 |
| SW1, SW2    | Omron B3S-1000              |                                                                                                                   | https://www.digikey.se/en/products/detail/omron-electronics-inc-emc-div/B3S-1000/20686    |
| J7          | CH147QV01A                  | This is the Color TFT. Buy either this, or the OLED display, not both. Don't get the module, get the bare screen. | https://aliexpress.com/item/1005003771379232.html                                         |
| -           | WEO012864A                  | This is the OLED. There are a *lot* of different manufacturers for this. Make sure the pinout and pitch matches.  | https://aliexpress.com/item/1005003108880951.html                                         |
| -           | 05-24-D-0203-A-4-06-4-T     | FPC cable to connect to Debug board                                                                               | https://www.digikey.se/en/products/detail/gct/05-24-D-0203-A-4-06-4-T/21266839            |
| -           | AFAG2220-SW2                | WiFi/Bluetooth Antenna (220 mm cable)                                                                             | https://www.digikey.se/en/products/detail/abracon-llc/AFAG2220-SW2/9603584                |

## Assembly

J1, SW1 and SW2 need to be soldered on. These are fairly easy to solder by hand, but be careful with the orientation of J1. It needs to match the orientation of the same header on the stock LCC. If you're using the TFT, that also needs to be soldered on, after which you should put kapton tape on the connector. You'll need to use double sided tape to attach the display to the board, but I'd recommend using a fairly tiny pad of it. That way, if your display is crooked, you'll probably be able to remove it without destroying it (speaking from experience).

The easiest way to flash the boards is with the debug board, which contains Micro-USB connectors for both the RP2040 and the ESP32-S3. It also has push-buttons for reset, RP2040 bootsel, and ESP32 GPIO0. Like I said, highly recommended.

Once everything is flashed, the board is ready to be installed. 