# Sunlu S8 #

This is a collection of resources for [Sunlu's S8]() owners in hope they can keep their printers supported and shugging on! 

The Sunlu S8 follows the design (same kinematics) as the Ender 3 and CR-10S printers, size wise the S8 is like an CR10S.


## Kinematics ## 

## Mainboard ##

The printer uses a [MKS](https://reprap.org/wiki/MKS_GEN_V1.1) like board. When it comes to asthetics and layout the board is mostly a cross-over with of  Creality CR10 boards, MKS Base 1.X and SKR.


![BOARD PINOUT](S8_PINOUT.png)

For more details on the pinout check my [RAMPS Pinout Page](ramps_mainboard.md). 

![BOARD WIRING](S8BOARD_WIRING.png)

Like most of the 8Bit boards out there, this is in escence is just a [RAMPS 1.4](https://reprap.org/wiki/RAMPS_1.4) board with an integrated Arduino 2560 all in one board. The main differances are:

- The board uses a L5970D power regulator allowing it to operate at 24V. Operating at 24V allows the hot-end and bed heater to use less current (about .25 less).

- This board only has support for one extruder.

References:<br>
[MKS GEN at GitHub](https://github.com/makerbase-mks/MKS-GEN/)<br>
[MKS GEN V1.4](https://github.com/makerbase-mks/MKS-GEN/blob/master/hardware/MKS%20GEN%20V1.4_004/MKS%20GEN%20V1.4_004%20PIN.pdf)<br>

The pin configuration for this board is the same as the RAMPS 1.4 in the Marlin Firmware.

The board uses [Pololu A4988](https://amzn.to/3aoiO4p) drivers. They are non replacable soldered in the board.


## Issues ##

The Sunlu S8 is an affordable printer, yet some units come with issues that you need to look out for.

Make sure all the axis are thight and there is no wiggle. 

Check your noozle carriage and if it has an up and down wiggle, thight the ecentric nut at the bottom using the wrench provided, turn clockwise to tighten it.

Check the bed to see if there is wiggle to the sides, if so under you will find two ecentric nuts one on each of the plates holding the bed, the ecentric nuts are the ones in the inside. Start by tighting one and checking before tightening the other one.

Do the same with the Y axis.

When you put together the printer make sure that your X-Z gantry is square. I used a carpenter square to ensure the vertical t-2040 slots are square with the base.

In my case a limit switch had the paddle loose. Check your limit switches to ensure the metal paddle sits properly in the slot. You also have a spare switch that came with the printer.

Springs in the bed do NOT offer enough tension which makes it difficult to level the bed and to keep the bed leveled. Putting one or more nuts (or washers) allows a temporary fix to give you more tension to level the bed. By my experience and comments of others this is the first thing you need to replace if you want a happy relationship with this printer. Get some sturdy 20mm or 25mm springs, same as the ones used on CR10 and Ender3 printers.
