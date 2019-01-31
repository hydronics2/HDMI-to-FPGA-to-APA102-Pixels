# Custom Circuit Boards

We used 3 types of circuit boards.
* A simple shield for the mojo that broke out all the SPI and Clock signals to the LED panels.*
* A transmitter board that sends the clock and data signal out over RS485*
* A receiver board that has transceiver chips, takes the signals *



![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/hdmi_shield.JPG)
Alchitry has an HDMI shield for the Mojo and the FPGA code is written in their programming environment in Lucid a form Verilog. It's great for beginners. This was my first FPGA project.

![overview](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/FPGA_overview2.JPG)

The HDMI signal is decoded and pixels arranged for each panel in local memory (RAM). There is just enough memory to save about 30% of the pixels so it takes 3 passes to arrange and output all the pixels... 60HZ / 3 gives us 20 frames per second.

The SPI clock speed for writing to the APA102 also has speed limits as we 'race the beam.' Here's a great article by [Paul Stoffregen (teensy)](https://www.pjrc.com/why-apa102-leds-have-trouble-at-24-mhz/) on these limits. The gist is the clock signals start to deteriorate between the pixels. For our 680 pixels in each stand/panel I was able to write confidently at about 6.25 MHZ. You can see how this clock signal is generated in any one of the 32 SPI modules in the source file under Mojo.

![rs485_transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/RS_485%20trasmitter2.JPG)

The signals are immediately fed from a simple shield to another custom PCB with [RS485 transmitters](https://www.digikey.com/product-detail/en/texas-instruments/AM26LV31EIDR/296-24690-1-ND/2092512) shown above.

The transmitter chips output differential signal pairs that pass easily in ethernet cords over 20-30 feet to each panel location. At the LED panel, the signals are received with [transceiver](https://www.digikey.com/product-detail/en/maxlinear-inc/SP485EN-L-TR/1016-1829-1-ND/3586546) chips

![tranceivers](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/rs_485%20receiver%20board.JPG)


Mojo HDMI Shield: https://embeddedmicro.com/products/hdmi-shield
