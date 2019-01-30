# Oregon Museum of Science (OMSI) - giant LED wall

![splash](https://github.com/hydronics2/HDMI-to-FPGA-to-APA102-Pixels/blob/master/splash.JPG)
132 APA102 LED panels, 680 pixels per panel, 90,000 pixels, 300sqft, 4 Spartan 6 Mojo FPGAs


LED Wall at Oregon Museum of Science: https://photos.app.goo.gl/8hZoa7y9F9Lsg7Md9
The creative director wanted to put the LED display behind a wood grain pattern. That way when the LEDs are off, there persists an unobtrusive wall to look at. To make this happen we used APA102 LEDs for their brightness. 

The resolution is about 24' wide by 14' high. That's 408 pixels wide 220 pixels tall. Not quite VGA. 

The FPGA's boards are Spartan 6 on a Mojo development platform: https://alchitry.com/ The wall is broken down into 4 sections for 4 Mojo's and each Mojo receives the same HDMI signal but only grabs pixels for the section of LEDs it controls. 

Alchitry has an HDMI shield for the Mojo and the FPGA code is written in their programming environment in Lucid a form Verilog. It's great for beginners. This was my first FPGA project.

Once the HDMI signal is decoded and pixels arranged for each panel, the FPGA sends out an SPI clock and data signal to each panel of APA102's. The signal is imediatly fed into an RS485 transmitter so that the signals can be routed in differential pairs over 20-30 feet to where the panel resides. Once transmitted to the location of the LED panel, the signals are received with transceiver chips into clock and data lines and connected to thier respective LED panel. 

Mojo HDMI Shield: https://embeddedmicro.com/products/hdmi-shield

This design builds off of a lucid module example for decoding HDMI signal: https://embeddedmicro.com/blogs/tutorials/hdmi-shield-basics

