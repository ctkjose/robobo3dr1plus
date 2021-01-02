# Sunlu S8 #

This is a collection of resources for [Sunlu's S8]() owners in hope they can keep their printers supported and shugging on! 

The Sunlu S8 follows the design (same kinematics) as the Ender 3 and CR-10S printers, size wise the S8 is like an CR10S.


## Kinematics ## 

## Mainboard ##

The printer uses a [MKS GEN 1 board](https://reprap.org/wiki/MKS_GEN_V1.1) like board that is mostly cross-over with a Creality CR10 boards. 
The layout is similar to MKS SGEN boards but actual pin headers, and functionality is more close to a Creality V2.1 mainboard.

![BOARD PINOUT](S8_PINOUT.png)

![BOARD WIRING](S8BOARD_WIRING.png)

Like most of the 8Bit boards out there, this is in escence is just a [RAMPS 1.4](https://reprap.org/wiki/RAMPS_1.4) board with an integrated Arduino 2560 all in one board. The main differances are:

- The board uses a L5970D power regulator allowing it to operate at 24V. Operating at 24V allows the hot-end and bed heater to use less current (about .25 less).

- This board only has support for one extruder.

References:<br>
[MKS GEN at GitHub](https://github.com/makerbase-mks/MKS-GEN/)<br>
[MKS GEN V1.4](https://github.com/makerbase-mks/MKS-GEN/blob/master/hardware/MKS%20GEN%20V1.4_004/MKS%20GEN%20V1.4_004%20PIN.pdf)<br>

The pin configuration for this board is the same as the RAMPS 1.4 in the Marlin Firmware.

The board uses [Pololu A4988](https://amzn.to/3aoiO4p) drivers.


## Issues ##

The Sunlu S8 is an affordable printer, yet some units come with issues that you need to look out for.

Make sure all the axis are thight and there is no wiggle. 

Check your noozle carriage and if it has an up and down wiggle, thight the ecentric nut at the bottom using the wrench provided, turn clockwise to tighten it.

Check the bed to see if there is wiggle to the sides, if so under you will find two ecentric nuts one on each of the plates holding the bed, the ecentric nuts are the ones in the inside. Start by tighting one and checking before tightening the other one.

Do the same with the Y axis.

When you put together the printer make sure that your X-Z gantry is square. I used a carpenter square to ensure the vertical t-2040 slots are square with the base.

In my case a limit switch had the paddle loose. Check your limit switches to ensure the metal paddle sits properly in the slot. You also have a spare switch that came with the printer.




