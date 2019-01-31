# Custom Circuit Boards

We used 3 types of circuit boards.
* A simple shield for the mojo that broke out all the SPI and Clock signals to the LED panels.
* A transmitter board that sends the clock and data signal out over RS485
* A receiver board that has transceiver chips, takes the signals 


![shield](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/custom_circuit_boards/mojo_shield.png)
Mojo Shield has all the pins broken out. We needed 33 SPI Data pins and the clock pin was shared across all the Panels.  The pins are broken out to 5.08mm phoenix connectors. The HDMI shield fits on the Mojo and this shield connects ontop of the HDMI shield. [Oshpark](https://oshpark.com/shared_projects/AGi8q5pp)



![transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/custom_circuit_boards/RS485_transmitter_board.png)

The transmitter board that takes two SPI signals (Clock and Data), passes the signals through a RS485 transmitter chip. The differential signals are routed to an ethernet jack. This board could have been integrated into the Mojo shield to reduce noise but my disigning, programming, prototyping, and installing timelines compressed the schedule and I had to learn as I went. [Oshpark](https://oshpark.com/shared_projects/nhExJAWv)


* transmitter chip: Texas Instrument AM27LV31 296-24690-1-ND
* RJ45 ethernet jack: 380-1316-5-ND



![receiver](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/custom_circuit_boards/RS845_receiver_board.png)
The receiver board receives RS485 signals via a RJ485 ethernet jack. Converts the two differential pairs back into clock and data SPI signals and connects to one LED panel. The board also has a DC-to-DC converter that takes 45V to 5V to supply to the LED panel. [Oshpark](https://oshpark.com/shared_projects/qSwC1Fum)

* Trnsceiver Chip: SP485EN, 1016-1829-1-ND
* RJ45 Ethernet Jack: 380-1316-5-ND
* DC-DC converter - PYB20-Q48-S5



* [Mojo Development Board](https://alchitry.com/products/mojo-v3)
* [HDMI Shield](https://alchitry.com/products/hdmi-shield)
* [RS485 transmitter chips](https://www.digikey.com/product-detail/en/texas-instruments/AM26LV31EIDR/296-24690-1-ND/2092512) shown above.
* [RS485 transceiver chips](https://www.digikey.com/product-detail/en/maxlinear-inc/SP485EN-L-TR/1016-1829-1-ND/3586546) chips
* [Mojo HDMI Shield](https://embeddedmicro.com/products/hdmi-shield)

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/hdmi_shield.JPG)
![rs485_transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/RS_485%20trasmitter2.JPG)
![tranceivers](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/rs_485%20receiver%20board.JPG)
