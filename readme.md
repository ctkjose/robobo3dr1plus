# All things Robo3D R1 Plus #

This is a collection of resources for [Robo3D R1 Plus]() owners.


# Specs and Parts #

The R1 is pretty much a traditional RAMPS 1.4 3D printer as such is fairly easy to find parts and hack it.

## Arduino Board ##

The R1 uses a standard Arduino MEGA 2560 board.

## RAMPS Board ##
The R1+ may come with a RAMPS 1.3 or RAMPS 1.4 board. These two boards are almost the same.

The R1+ uses a [RAMPS 1.4](https://reprap.org/wiki/RAMPS_1.4) board.
![RAMPS WIRING](R1WIRINGDIAG.png)

The ramp board in your robo may have different connectors to a traditional RAMPS 1.4 that may confuse people:

On R1+ 1.4.3 board the fan connects to D10, which is a connector labeled "FAN0". This connector is actually connected to Arduino's PIN 9 like regular RAMPS.

On R1+ 1.4.3 board the extruder heater is connected to the plug labeled D9. This connector behaves like the original D10 of RAMPS and still responds to Arduino's PIN 10.

## Hot End ##

The R1+ comes with a "hexagon hotend".
The nozzle is a 0.4mm for 1.75mm filament, a M6 thread, 1mm thread pitch.
Thermistor is EPCOS 100k ohms, 4.7k pullup. You may use others but must be configured on the firmware.
Heater Cardrige is a 12v/30w. 

Available at: [reprapdiscount](http://www.reprapdiscount.com/hotends/67-hexagon-hotend-set.html) and [partsbuilt](https://www.partsbuilt.com/r1-hotend-assembly-robo).

Nozzles compatible with E3D V6 should also work with the stock hexagon hotend as long as its for 1.75mm filament.

## Other Hotends ##

The [filament throats](https://reprap.org/forum/read.php?14,846189,846189) may be full metal or PTFE (teflon) lined.
A general accepted opinion is that PTFE lined throaths limits your tempetures but for most people the range is fine and may cause jams. Example hotends with teflon: models HE280 and E3D V6 clones may also use PTFE. When possible stick to all aluminum/metal.

### E3D V6 Hotend Upgrade ###

[Robo Forum Post](http://community.robo3d.com/index.php?threads/e3d-v6-information-installation-guides-and-review.3407/)<br>
[Robo Forum Post](http://community.robo3d.com/index.php?threads/e3d-v6-information-and-installation-guide.17598/)<br>
[Novice Expert Assemble Youtube Video](https://www.youtube.com/watch?v=0FB3MmgvWrw)<br>
[Novice Expert Installation Youtube Video](https://www.youtube.com/watch?v=sZM6MIuPorQ)<br>

# Firmware #



# Tutorial and Mods #

[Smart LCD Controller Robo](https://www.youtube.com/watch?v=8yWX7Pn-Sg0)

# STL Files for R1+ Parts #

