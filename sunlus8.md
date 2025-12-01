# Sunlu S8 #

This is a collection of resources for [Sunlu's S8]() owners in hope they can keep their printers supported and shugging on!

The Sunlu S8 follows the design (same kinematics) as the Ender 3 and CR-10S printers, size wise the S8 is like an CR10S.


## Kinematics ##

### Mainboard ###

The printer uses a [MKS](https://reprap.org/wiki/MKS_GEN_V1.1) like board. When it comes to asthetics and layout the board is mostly a cross-over with of Creality Ender 3/CR10 boards, MKS Base 1.X and SKR.


![BOARD PINOUT](S8_PINOUT.png)

For more details on the pinout check my [RAMPS Pinout Page](ramps_mainboard.md).

The board has a EXP1 connector for the Smart Controller LCD, the following image has its pinout:
![S8_EPX1_CONNECTOR](SUNLUS8_EXP1_PINOUT.png)


![BOARD WIRING](S8BOARD_WIRING.png)

Like most of the 8Bit boards out there, this is in escence is just a [RAMPS 1.4](https://reprap.org/wiki/RAMPS_1.4) board with an integrated Arduino 2560 all in one board. The main differances are:

- The board uses a L5970D power regulator allowing it to operate at 24V. Operating at 24V allows the hot-end and bed heater to use less current (about .25 less).

- This board only has support for one extruder.

References:<br>
[MKS GEN at GitHub](https://github.com/makerbase-mks/MKS-GEN/)<br>
[MKS GEN V1.4](https://github.com/makerbase-mks/MKS-GEN/blob/master/hardware/MKS%20GEN%20V1.4_004/MKS%20GEN%20V1.4_004%20PIN.pdf)<br>

The pin configuration for this board is the same as the RAMPS 1.4 in the Marlin Firmware.

The board uses [Pololu A4988](https://amzn.to/3aoiO4p) drivers. They are non replacable soldered in the board.


### Motors: ###
The S8 uses for NEMA-17 bi-polar stepper [motors](motors.md). Since the S8 is based on a RAMPS 1.4 controller board any motor that works with RAMPS works on the S8.

## Extruder ##

The extruder in the S8 is called a **bowden** extrusion (vs **direct drive** extrusion). In **bowden extrusion** the extruder pushes the filament through a PTFE Bowden tube into the MK8 nozzle. The extruder is mounted in the side of the printer. directly into the nozzle. In **direct drive extrusion** the extruder is mounted with the nozzle and the filament is pushed directly into the nozzle.

The extruder in the S8 is called a **"MK8 extruder drive"**. It uses a 40 teeth gear attached to the motor shaft to push the filament. Any MK8 extruder drive meant for Ender 3/3Pro CR-10, CR-10 S4 or CR-10 S5 will fit the S8.

This is [my guide](sunlus8_microswiss_direct_drive_extruder.md) on upgrading to a Micro Swiss Direct Drive extruder.

## Hotend ##

The hotend is a MK8. The stock hotend has an aluminum cooling block. One good design choice in the S8 is that the throut into the heating block is a PTFE lined screw that goes from the top directly to the heating block, this helps avoid leaks and clogging.

The heater block is also aluminum with a standrad 4.0mm brass plated noozle.

## Cooling Fans ##

The Cooling Fan on the S8 is a 40mm x 40mm x 10mm fan. It is a 24V and should be rated around 0.6A.

## Power Supply ##

The S8 uses a standard 24V power supply found in many 3D printers. The power supply is rated at 360W and delivers from to 14.6A to 15A depending in the model that came in your printer.

To find a replacement just  search for "360w 24v 3d printer power supply" you will find a lot of options. The case is around 4.52in x 8.64in which is the common dimensions for a 3D printer power supply. The amperage of your power supply may be higher than 15A and thats ok. For better performance check that the replacement has a fan and even better if the fan is automatic (is off by default and turn-on only when the power supply is hot).


## Bed Leveling ##

I created a guide of how I got my S8's bed level. It includes some pointer on how to handle the captchas. The guide is available [here](SUNLUS8_BED_LEVELING.pdf).

The basic steps to level the bed on your Sunlu S8 are available [here](https://www.youtube.com/watch?v=ail-0E_LtV0) in a YouTube video form Sunlu, you may also want to watch other videos on YouTube that cover more details. Also the steps to level the bed in the S8 are the same for Ender 3 and CR10 printers.

I like this video in particular:

[Thomas Sanladerer](https://www.youtube.com/watch?v=AaF28dnDgKA)

## Issues ##

The Sunlu S8 is an affordable printer, yet some units come with issues that you need to look out for.

Make sure all the axis are thight and there is no wiggle.

Check your noozle carriage and if it has an up and down wiggle, thight the ecentric nut at the bottom using the wrench provided, turn clockwise to tighten it.

Check the bed to see if there is wiggle to the sides, if so under you will find two ecentric nuts one on each of the plates holding the bed, the ecentric nuts are the ones in the inside. Start by tighting one and checking before tightening the other one.

Do the same with the Y axis.

When you put together the printer make sure that your X-Z gantry is square. I used a carpenter square to ensure the vertical t-2040 slots are square with the base.

In my case a limit switch had the paddle loose. Check your limit switches to ensure the metal paddle sits properly in the slot. You also have a spare switch that came with the printer.

Springs in the bed do NOT offer enough tension which makes it difficult to level the bed and to keep the bed leveled. Putting one or more nuts (or washers) allows a temporary fix to give you more tension to level the bed. By my experience and comments of others this is the first thing you need to replace if you want a happy relationship with this printer. Get some sturdy 20mm or 25mm springs (these are the same used on CR10 and Ender3 printers).

# Marlin Firmware

The Sunlu S8 stock mainboard is a [RAMPS 1.4/1.6](ramps_mainboard.md) clone with integrated ATMEGA2560 and sdcard on a single board. This board is similar to the [MKS Base](https://reprap.org/wiki/MKS_BASE_1.0), and Creality 3D V1.x boards found in Ender 3/5 and CR10. This board only have the EXP1 connector (no EXP2) for a RepRap Full Graphic Smart Controller LCD without a SDCard reader.

Modification to `Configuration.h` (V1.x,V2.x)

```c
//Configuration.h
#ifndef MOTHERBOARD
  #define MOTHERBOARD BOARD_RAMPS_14_EFB
#endif

#define DEFAULT_MAX_FEEDRATE { 80, 80, 400, 140 }

// The size of the printable area
#define X_BED_SIZE 310
#define Y_BED_SIZE 310

#define X_MIN_POS 0
#define Y_MIN_POS 0
#define Z_MAX_POS 410

#define INVERT_X_DIR true
#define INVERT_Y_DIR true
#define INVERT_Z_DIR false

#define INVERT_E0_DIR true    //For stock extruder
#define INVERT_E0_DIR false   //For MSWISS Direct Drive V9

#define HOMING_FEEDRATE_MM_M { (80*60), (80*60), (6*60) }

//Enable manual bed leveling if not using BLTouch
#define MESH_BED_LEVELING

//Enable bed leveling menu
#define LCD_BED_LEVELING

//Raise the default hotend temperature for PLA
#define PREHEAT_1_TEMP_HOTEND 210

//Enable LCD
#define REPRAP_DISCOUNT_FULL_GRAPHIC_SMART_CONTROLLER

//Enable the SDCard
#define SDSUPPORT

//Enable M500 and M501
#define EEPROM_SETTINGS

// Add PID editing to the "Advanced Settings" menu.
//#define PID_EDIT_MENU
// Add PID auto-tuning to the "Advanced Settings" menu.
#define PID_AUTOTUNE_MENU
```
> Using the ` MOTHERBOARD BOARD_RAMPS_14_EFB` will load the default pins for RAMPS defined in `pins_RAMPS.h` or `pins/ramps/pins_RAMPS.h` on V2.x firmwares.

## Endstops

> **Important:** Read my [wiki page](https://reprap.org/wiki/Mechanical_Endstop) at RepRap to learn more about endstops.

In Marlin endstops are enabled by these options, which are usually enabled by default in your "Configuration.h" file:
```c
#define USE_XMIN_PLUG
#define USE_YMIN_PLUG
#define USE_ZMIN_PLUG
```

Endstops on the S8 are installed on

Sunlu uses common  MakerBot V1.2 Endstops which have a resistor-capacitor circuit and a Pull-up Resistor.

Nevertheless these endstops are wired as plain mechanical switches. That is the input (Common) is wired to ground and the output (the signal) is wired to the NC (Normally Closed) pin.

That is the `S` pin is connected to the `NC/VCC` (NC, last pin on the endstop) and the `G` pin is connected to the `S` (first pin on the endstop).

This means that when the endstop is not depressed a 5V (HIGH) will be seeing in the `S` pin and when the switch is pressed the `S` will go to 0V (LOW).

This is configured differently on V1 and V2 firmwares:

In V1.x we have to set inverting:
```c
 // set to true to invert the logic of the endstop.
#define X_MIN_ENDSTOP_INVERTING true
#define Y_MIN_ENDSTOP_INVERTING true
#define Z_MIN_ENDSTOP_INVERTING true
```

In V2.x Marlin provides an option to define the logical state that triggers the endstop:
```c
#define X_MIN_ENDSTOP_HIT_STATE LOW
#define Y_MIN_ENDSTOP_HIT_STATE LOW
#define Z_MIN_ENDSTOP_HIT_STATE LOW
```

> If using BLTOUCH then `Z_MIN_ENDSTOP_HIT_STATE` is set to HIGH.

## Filament Runout Sensor

The filament runout sensor in Sunlu's S8 is just a plain switch (same as the one used for end stops) that is normally closed (NC). While there is filament the switch is depressed indicating that we have filament (high signal). When the filament runs out the switch is released and the signal goes low indicating that we ran out of filament.

In RAMPS boards the runout sensor is connected to pin `D4` (know as `SERVO3_PIN`) or to pin `D2` (know as `Z_MAX_PIN`).

The Sunlu S8 mainboard has the plug "MT DET" (Material Breakage Detection) to connect the runout sensor. This plug is connected to pin `D2` in RAMPS. The pin `D2` is actually Z-Max Endstop.

The actual pin is defined with `FIL_RUNOUT_PIN` in the firmware.

### 1.x Firmware
```c

//#define FILAMENT_RUNOUT_SENSOR
#if ENABLED(FILAMENT_RUNOUT_SENSOR)
  #define NUM_RUNOUT_SENSORS   1 // Number of sensors.
  #define FIL_RUNOUT_PULLUP // Use internal pullup for filament runout pins.

  #define FIL_RUNOUT_PIN 2 //connected to Z-Max endstop

  // Set one or more commands to execute on filament runout.
  // (After 'M412 H' Marlin will ask the host to handle the process.)
  #define FILAMENT_RUNOUT_SCRIPT "M600"

  //By default the firmware assumes HIGH=FILAMENT PRESENT.
  #define FIL_RUNOUT_INVERTING false // set to true to invert the logic of the sensor.

#endif
```

### 2.x Firmware
```c
#if ENABLED(FILAMENT_RUNOUT_SENSOR)
  #define NUM_RUNOUT_SENSORS   1 // Number of sensors.
  #define FIL_RUNOUT_PULLUP // Use internal pullup for filament runout pins.

  #define FIL_RUNOUT_PIN 2 //connected to Z-Max endstop

  // Set one or more commands to execute on filament runout.
  // (After 'M412 H' Marlin will ask the host to handle the process.)
  #define FILAMENT_RUNOUT_SCRIPT "M600"

  //By default the firmware assumes HIGH=FILAMENT PRESENT.
  #define FIL_RUNOUT_STATE LOW // Pin state indicating that filament is NOT present.


  #define FIL_RUNOUT_ENABLED_DEFAULT true // Enable the sensor on startup.
#endif
```

# Set Z Aixs

```c

M280 P0 S10;      Extend BL Touch Probe
M211 S0;          Turn off software endstops
G91               Enable relative positioning
G1 Z-1;
M211 S1;
```

# BLTOUCH

The SunluS8 does not have a dedicated connector for the BLTouch. In this installation the BLtouch will use the connector for the Z_MIN_ENDSTOP and the PWM control of the BLTouch connects to `SERVO0` (pin D11).

See Teaching Tech BLTouch [guide](https://teachingtechyt.github.io/upgrades.html#bltouch) for more details.

![board](images/bltouch_sunlus8.png)
<br>
*(Warning: Colors of cables may/will be different.)*

## Basic configurations

This changes to the configuration are the same regardless of the physical mount used.

```c
//Configuration.h

#define BLTOUCH

PROBE_DEPLOY_STOW_MENU

// This indicates that our z-probe cables (pin 4 and 5)
// are connected to our Z-endstop in the mainboard.
#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN

//Un comment for BLTOUCH logic to work
#define AUTO_BED_LEVELING_BILINEAR

//IMPORTANT: Comment out other bed leveling configured
//#define MESH_BED_LEVELING

#define PROBING_MARGIN 50

#define LCD_BED_LEVELING
#define Z_SAFE_HOMING

//Minimal z height before homing (G28)
#define Z_CLEARANCE_FOR_HOMING  4 //On V2.1.x
#define Z_HOMING_HEIGHT         4 //On V2.0.x


#define Z_MIN_ENDSTOP_HIT_STATE HIGH
#define Z_MIN_PROBE_ENDSTOP_HIT_STATE HIGH
```

In `Configuration_adv.h` we make further optimizations.

```c
//Configuration_adv.h

// Enable babystepping to be able to make small
// adjustments to our z-axis.
#define BABYSTEPPIN



// Enable the wizard on the LCD
#define PROBE_OFFSET_WIZARD

// Set a start value for the Z axis
#define PROBE_OFFSET_WIZARD_START_Z -4.0
```

You can optionally enable the baby stepping menu:
```c
// Combine M851 Z and Babystepping
#define BABYSTEP_ZPROBE_OFFSET

// Display total babysteps since last G28
#define BABYSTEP_DISPLAY_TOTAL
```

## Configuring offsets

Depending on how you mount your BLTouch will to the left or the right of the nozzle and the center of the BLTouch would be a little to the front or back of the nozzle.

![image_offset](images/bltouch_offset.png)

We need to tell Marlin the location of the BLTouch center in relation to the nozzle center. These are offsets that Marlin uses to adjust the bed-leveling values to the actual nozzle location.

Here we will use the [Mini Satsana for MicroSwiss](https://www.thingiverse.com/thing:4689712) with a BLTouch bracket which puts the BLTouch to the left side of the nozzle.

The distances of the nozzle to the BLTouch center are specified for the X, Y and Z axis. When the BLTouch is to the left of the nozzle the X offset is a negative number and if the BLTouch tip to the back of the nozzle the Y offset is negative.

With version1.x of the firmware we change the following:

```c
#define X_PROBE_OFFSET_FROM_EXTRUDER -40
#define Y_PROBE_OFFSET_FROM_EXTRUDER 0
#define Z_PROBE_OFFSET_FROM_EXTRUDER -10
```

With a newer version 2.x of the firmware we use the following:

```c
/* Specify a Probe position as { X, Y, Z } */
#define NOZZLE_TO_PROBE_OFFSET { -40, -10, -2}
```

More [info](https://marlinfw.org/docs/gcode/M851.html) on setting the probe offset.

# Machine Calibration

## Run PID autotune

- Navigate to Configuration on the main menu.
- Select Advanced Settings.
- Go to Temperature.
-  Select either `PID Autotune E1` for the hotend or PID Autotune Bed for the heated bed.

```c
M303; PID Autotune
```

## Calibrate E-Steps

- Mark 100mm on the filament from the top of the extruder, then make another mark at 200mm.
- Extrude 100mm with the command `G1 E100 F100`.
- Calibrated E-Steps should stop when mark is at top of extruder. If it went pass it is over-extruding, if mark did not reach the top is under-extruding.
- Compute how much we actually extruded:
- If under-extruded, measure the distance from top of extruder to the mark. The amount extruded is 100mm - that distance.
- If over extruded, measure the distance from top of extruder to the next 200mm mark. The amount extruded is 100mm + (100mm - that distance).
- Compute how many steps it took. The formula is (E-Steps * 100mm). For example, if my E-steps is 98 then the machine took 9800 steps to extrude 100mm.
- Calculate the correct steps/mm value by dividing the steps taken by the actual length extruded. For example, if the machine under-extruded only 70mm, the corrected e-step value is 9800/70 which will give me a new e-steps of 140.

### Helpful commands
```c
G1 E100 F100;       Extrude 100mm at 100mm/s
M92;                Show current E-Steps
M92 E140.0;         Sets e-steps
M500;               Save configuration
```

### General formula to compute steps/mm

`NEW_VALUE = (CURRENT_STEPS_VALUE * ACTUAL_LENGHT) / DESIRED_LENGTH`


# Ref

Link to TeachingTech calibration [guide](https://teachingtechyt.github.io/calibration.html).

Here is a practical calibration print [cube](https://www.printables.com/model/139216-filament-calibration-cylinder), for more details check this [video](https://www.youtube.com/watch?v=SJdj-EQCM7c), or check the gist of it [here](https://wiki.layerfused.com/en/general/troubleshoot/calibration).

Simplify3D maintains a good [list](https://www.simplify3d.com/resources/print-quality-troubleshooting/) of common issues that can point you in the right direction.

Good calculators [here](https://www.layerfused.com/3d-printer-calibration).

## Issue: Vibrations and Ringing