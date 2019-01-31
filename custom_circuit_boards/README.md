# Custom Circuit Boards

We used 3 types of circuit boards.
* A simple shield for the mojo that broke out all the SPI and Clock signals to the LED panels.*
* A transmitter board that sends the clock and data signal out over RS485*
* A receiver board that has transceiver chips, takes the signals *

![shield](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/custom_circuit_boards/mojo_shield.png)
Mojo Shield has all the pins broken out. We needed 33 SPI Data pins and the clock pin was shared across all the Panels.  The pins are broken out to 5.08mm phoenix connectors. The HDMI shield fits on the Mojo and this shield connects ontop of the HDMI shield. [Oshpark](https://oshpark.com/shared_projects/AGi8q5pp)

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/hdmi_shield.JPG)

[Mojo Development Board](https://alchitry.com/products/mojo-v3)

[HDMI Shield](https://alchitry.com/products/hdmi-shield)


![transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/custom_circuit_boards/RS485_transmitter_board.png)

The transmitter board that takes two SPI signals (Clock and Data), passes the signals through a RS485 transmitter chip. The differential signals are routed to an ethernet jack. This board could have been integrated into the Mojo shield to reduce noise but my disigning, programming, prototyping, and installing timelines compressed the schedule and I had to learn as I went. [Oshpark](https://oshpark.com/shared_projects/nhExJAWv)

*transmitter chip: Texas Instrument AM27LV31 296-24690-1-ND*
*RJ45 ethernet jack: 380-1316-5-ND*

https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels

The HDMI signal is decoded and pixels arranged for each panel in local memory (RAM). There is just enough memory to save about 30% of the pixels so it takes 3 passes to arrange and output all the pixels... 60HZ / 3 gives us 20 frames per second.

The SPI clock speed for writing to the APA102 also has speed limits as we 'race the beam.' Here's a great article by [Paul Stoffregen (teensy)](https://www.pjrc.com/why-apa102-leds-have-trouble-at-24-mhz/) on these limits. The gist is the clock signals start to deteriorate between the pixels. For our 680 pixels in each stand/panel I was able to write confidently at about 6.25 MHZ. You can see how this clock signal is generated in any one of the 32 SPI modules in the source file under Mojo.

![rs485_transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/RS_485%20trasmitter2.JPG)

The signals are immediately fed from a simple shield to another custom PCB with [RS485 transmitters](https://www.digikey.com/product-detail/en/texas-instruments/AM26LV31EIDR/296-24690-1-ND/2092512) shown above.

The transmitter chips output differential signal pairs that pass easily in ethernet cords over 20-30 feet to each panel location. At the LED panel, the signals are received with [transceiver](https://www.digikey.com/product-detail/en/maxlinear-inc/SP485EN-L-TR/1016-1829-1-ND/3586546) chips

![tranceivers](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/rs_485%20receiver%20board.JPG)


Mojo HDMI Shield: https://embeddedmicro.com/products/hdmi-shield
