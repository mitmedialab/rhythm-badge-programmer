# rhythm-badge-programmer
This repository describes severalm methods for programming the Rhythm Badges.

In general, you could use almost any JTAG/SWD debugger. Some cheap ones might fail because of the the capacitors and resistors that we placed on the programming pins (help reducing resets).
This document assumes that you are using the NRF51-DK (dev kit) from Nordic for programming.

Here, we cover three options for programming (starting with the simplest one to the most complex):
1. Adapter board + female header pins
2. Adapter board + hand-held pogo-pin programmer
3. Adapter board + programming rig

Schematics and files for creating a programmer for Rhythm badges

# 1 - Adapter board + female header pins
In this option, we use a custom PCB as ana adapter between the nRF51 dev kit and the badge, using a 2x3 male header connector.
It requires soldering female headers to the bottom of each badge. 
This option is great for testing, but not ideal for large batches. 

Bill of materials:
* nRF51 dev kit (nRF51-DK) 
* Custom PCB board. See the /eagle folder for schematics and gerber files
* Optional - LED + resistor. Package size is 0603.
* 1 x double row 2x3 male headers
* 2 x single row 1x8 **long** male headers
* 1 x single row 1x8 female headers
* double row 2x3 female header (for the badge)

First, create the custom PCB. You can either make it yourself, or order the PCB from your favorite supplier (e.g. PCBWay, IteadStudio, SeeedStudio).
Note that the project includes two variations:
1. /eagle/one_layer - Single sided board. If you fabricate the board yourself (for example, using a milling machine), it's easier to use this design. Note that you will need to solde two jumpers
2. /eagle/two_layers - Double sided design. If you order a PCB, use this design

Solder the two 1x8 male headers and 1x8 female headers in the right place. For reference, see these images:

![Top view](/images/adapter-top.jpg?raw=true "Top view")

![Bottom view](/images/adapter-bottom.jpg?raw=true "Bottom view")

TODO - new photos for adapter 

Next, solder a 2x3 female header to the **bottom** of the badge. Then simply place it on the adapter so that the pins are aligned (see images below). 
If it's a badge that has not been programmed yet, the red LED should turn on after about a second to indicate that the micro-controller is working.
 
TODO - photos of the badge with header, photos of the badge placed on the adapter   

# 2 - Adapter board + hand-held pogo-pin programmer
Bill of materials:
* Adapter board and header from option #1 above
* SparkFun ISP Pogo Adapter - https://www.sparkfun.com/products/11591
* 6-pin Socket/Socket IDC cable. For example - https://www.adafruit.com/product/371

In this method we simply use the pogo programmer kit form Sparkfun to program the badge. Follow the instructions on the product page and solder the kit.
Afterwards, use a 6-pin cable to connect the programmer to the adapter board. 

Once ready, place the programmer on the top side of the badge, and make sure you align the pins correctly (use VCC and GND for guidance).

TODO - add photos of pogo programmer and how it's placed on the badge

# 3 - Adapter board + programming rig
In this option, we create a small rig where you can place the badge and press it down against pogo pins. It makes it easier when you need to program large batches of badges.
Note that we use the same pogo programmer kit from SparkFun, but assemble it in a different way so it fits in the rig. 

Bill of materials:
* All parts from the previous options (adapter board, Pogo adapter, cable)
* Acrylic parts for rig frame. Requires 1mm and 3mm acrylic sheets 
* M3 spacers and screws (metal or plastic):
    * 4 x 10mm female-female spacers
    * 4 x 15mm female-male spacers
    * 4 x 2 or 2.5mm spacer
    * 2 x 5mm screws
    * 10 x 10mm M3 screws
    * 2 x 20mm female-female spacers
* 2.54mm (0.1") right angle double row male 2x3 headers (a total of 6 pins, 3 in each row) or https://www.amazon.com/uxcell-10-Pin-2-54mm-Connector-Sockets/dp/B013FMST70/ref=sr_1_1?ie=UTF8&qid=1542729677&sr=8-1&keywords=header+idc+10+pin+right+angle

## 3.1 - Laser cutting the rig
The rig has three parts - top, middle and bottom. Use 1mm for the top part and 3mm for the other two.

The files for these parts can be found under the /rig_frame

Laser cutting settings for EPILOG 120 Watt, Legend 36EXT:
* 3mm acrylic - 25% speed, 85% strength, 2500 freq
* 1mm acrylic - 50% speed, 85% strength, 2500 freq

TODO - add images of the three parts (before assembly)

## 3.2 - Soldering + assembly
Important! when soldering, make sure nothing sticks out from beneath the bottom red PCB. 
You can do this by mounting the red PCB board on bottom layer of the rig and do the soldering on the top of the PCB. 

Use 4 x 10mm screws to connect 4 x 15mm female-female spacers to the bottom part of the rig (see image for orientation.

Place the large red board from the pogo kit on the bottom part of the rig, and use 2 x 10mm screws + 2 x 20mm female-female spacers to mount it (see black spacers in teh image below) 

After the red PCB is secured, you can solder the right angle header or connector (grey component in the image below). If you are using a 10-pin connector, remove the outer pins and keep only the 6 pins in the center. If you are using simple 2x3 right angle pins you are good to go. 

![Step 1](/images/assembly_01.jpg?raw=true "Step 1")
 
Mount the top red PCB using 2 x 5mm screws (make sure the orientation is correct)

Solder the pogo pins.  Start from the back, and make your way forward. Be careful not to push them down - when they are hot they can metlt their way through the acrylic.

![Step 2](/images/assembly_02.jpg?raw=true "Step 2")

![Step 3](/images/assembly_03.jpg?raw=true "Step 3")


Connect the remaining 4 x 10mm female-female spacers to the 15mm spacers, and use the screws to mount the two remaining acrylic parts. 

For extra comfort you can use the 2.5mm spacers as well - they will lift the top layers a bit more. They should go between the top acrylic layers and the other spacers.

For smaller of the pins location, push a piece of paper under the lower red layer to change the angle of the pins.

![Final](/images/final.jpg?raw=true "Final 1")

![Final 2](/images/final_bottom.jpg?raw=true "Final 2")