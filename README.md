# Oregon Museum of Science (OMSI) - giant LED wall

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/splash.JPG)
132 APA102 LED panels, 680 pixels per panel, 90,000 pixels, 300sqft, 4 Spartan 6 Mojo FPGAs
[hackaday.io](https://hackaday.io/project/163657-hdmi-to-fpga-to-apa102)

LED Wall at Oregon Museum of Science: https://photos.app.goo.gl/8hZoa7y9F9Lsg7Md9
The creative director wanted to put the LED display behind a wood grain pattern similar to the wall at Microsoft HQ. When the LEDs are off the visitor sees a seemless, unobtrusive wall. To make the LEDs pop behind the wood grain graphic we used a very brigtht APA102.

The resolution is about 24' wide by 14' high. That's 408 pixels wide 220 pixels tall. Not quite VGA. 

The FPGA's boards are Spartan 6 on a Mojo development platform: https://alchitry.com/ The wall is broken down into 4 sections for 4 Mojo's and each Mojo receives the same HDMI signal but only grabs pixels for the section of LEDs it controls. 

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/hdmi_shield.JPG)
Alchitry has an HDMI shield for the Mojo and the FPGA code is written in their programming environment in Lucid a form Verilog. It's great for beginners. This was my first FPGA project.

![overview](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/FPGA_overview2.JPG)

The HDMI signal is decoded and pixels arranged for each panel in local memory (RAM). There is just enough memory to save about 30% of the pixels so it takes 3 passes to arrange and output all the pixels... 60HZ / 3 gives us 20 frames per second. Thanks to [David Hulton](https://www.meetup.com/PNW-FPGA-Hackers-Meetup/) and Devin Boyer for sharing their mad FPGA memory tricks at [Toorcamp 2018](https://toorcamp.toorcon.net/).

The SPI clock speed for writing to the APA102 also has speed limits as we 'race the beam.' Here's a great article by [Paul Stoffregen (teensy)](https://www.pjrc.com/why-apa102-leds-have-trouble-at-24-mhz/) on these limits. The gist is the clock signals start to deteriorate between the pixels. For the 680 LEDs in our panel, I was able to write confidently at 6.25 MHZ. You can see how this clock signal is generated in any one of the 32 SPI modules in the source file under Mojo.

![rs485_transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/RS_485%20trasmitter2.JPG)

The FPGA generates an SPI clock and data signal to each LED panel. The signals are immediately fed from a simple shield to another custom PCB with [RS485 transmitters](https://www.digikey.com/product-detail/en/texas-instruments/AM26LV31EIDR/296-24690-1-ND/2092512) shown above. The transmitter chips output differential signal pairs that pass easily in ethernet cords over 20-30 feet to each panel location. At the LED panel, the signals are received with [transceiver](https://www.digikey.com/product-detail/en/maxlinear-inc/SP485EN-L-TR/1016-1829-1-ND/3586546) chips bacck into clock and data lines and connected to their respective LED panel. This custom PCB also has a small DC-DC voltage transformers that take a 45VDC buss down to the 5V required for the LEDs.  The below PCB has tranceiver chips and three DC-DC transformers serving 3 LED panels. Thanks to Tom Moxon with [Pattern Agents](http://patternagents.com/) for help designing this circuit.

![tranceivers](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/rs_485%20receiver%20board.JPG)


The led panels themselves are little more than strip LEDs that have been connected together.  We had them customized for our particular geometry by the [supplier](https://www.aliexpress.com/store/product/30-40-pixels-RGB-full-color-WS2812B-Flexible-LED-Pixel-Panel-Light-DC5V/701799_32601735218.html).

![sample](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/example_led_panel.JPG)


Mojo HDMI Shield: https://embeddedmicro.com/products/hdmi-shield

This design builds off of a lucid module example for decoding HDMI signals: https://embeddedmicro.com/blogs/tutorials/hdmi-shield-basics

![exposed](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/led_wall_exposed.JPG)

Thanks to Walsh Construction for making it look easy to hang giant pieces of Acrylic exactly on target.


