# mojo_fpga

This design takes an HDMI signal and outputs a 34 long x 20 high grid of APA102 leds.

The hardware consists of a Spartan 6 FPGA on an Mojo development board by Embedded Micro... using their IDE written in Lucid which is similar to Verilog: https://embeddedmicro.com/products/mojo-v3

Also uses the HDMI shield for the Mojo by Embedded Micro: https://embeddedmicro.com/products/hdmi-shield

This design builds off of a lucid module example for decoding HDMI signal: https://embeddedmicro.com/blogs/tutorials/hdmi-shield-basics


There is something wrong with the vsync signal so I imported the dvi_decoder directly into the top module and teased out a start frame indicator.
