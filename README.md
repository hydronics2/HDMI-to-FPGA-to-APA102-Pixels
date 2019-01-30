# Oregon Museum of Science (OMSI) - giant LED wall

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/splash.JPG)
132 APA102 LED panels, 680 pixels per panel, 90,000 pixels, 300sqft, 4 Spartan 6 Mojo FPGAs


LED Wall at Oregon Museum of Science: https://photos.app.goo.gl/8hZoa7y9F9Lsg7Md9
The creative director wanted to put the LED display behind a wood grain pattern. That way when the LEDs are off, there persists an unobtrusive wall to look at. To make this happen we used APA102 LEDs for their brightness. 

The resolution is about 24' wide by 14' high. That's 408 pixels wide 220 pixels tall. Not quite VGA. 

The FPGA's boards are Spartan 6 on a Mojo development platform: https://alchitry.com/ The wall is broken down into 4 sections for 4 Mojo's and each Mojo receives the same HDMI signal but only grabs pixels for the section of LEDs it controls. 

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/hdmi_shield.JPG)
Alchitry has an HDMI shield for the Mojo and the FPGA code is written in their programming environment in Lucid a form Verilog. It's great for beginners. This was my first FPGA project.

![overview](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/FPGA_overview2.JPG)
The HDMI signal is decoded and pixels arranged for each panel in local memory (RAM). There is just enough memory to save about 30% of the pixels so it takes 3 passes to arrange and output all the pixels... 60HZ / 3 gives us 20 frames per second.  

The SPI clock for the APA102 is also limits our write speed.  Here's a great article by [Paul Stoffregen (teensy)](https://www.pjrc.com/why-apa102-leds-have-trouble-at-24-mhz/) on trying to write fast to APA102 pixels in long strips. 
The gist is the clock signals start to deteriorate between the pixels. For our 680 pixels in each stand/panel I was able to write confidently at about 6.25 MHZ. You can see how this clock signal is generated in any one of the 32 SPI moduels in the source file under Mojo.

![rs485_transmitter](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/RS_485%20trasmitter2.JPG)
The FPGA generates an SPI clock and data signal to each LED panel. The signals are immediatly fed from a simple shield to another custsom PCB with [RS485 transmitters](https://www.digikey.com/product-detail/en/texas-instruments/AM26LV31EIDR/296-24690-1-ND/2092512) shown above. . so that the signals can be routed in differential pairs over 20-30 feet to where the panel resides. Once transmitted to the location of the LED panel, the signals are received with transceiver chips into clock and data lines and connected to thier respective LED panel. 

Mojo HDMI Shield: https://embeddedmicro.com/products/hdmi-shield

This design builds off of a lucid module example for decoding HDMI signal: https://embeddedmicro.com/blogs/tutorials/hdmi-shield-basics

