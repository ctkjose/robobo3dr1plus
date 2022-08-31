# MicroSwiss Direct Drive Extruder Upgrade for Sunlu S8 #

This document include my notes on upgrading a Sunlu-S8 (CR10 clone) to use the MicroSwiss direct drive [extruder kit](https://store.micro-swiss.com/collections/extruders/products/micro-swiss-direct-drive-extruder) with a the all [metal hotend](https://store.micro-swiss.com/collections/all-metal-hotend-kits/products/all-metal-hotend-kit-for-cr-10).

The official instructions to install this kit are available [here](https://cdn.shopify.com/s/files/1/1210/0176/files/Micro_Swiss_Direct_Drive_Extruder_Installation_Instructions.pdf?v=1592671102).

## Calibrating the extruder ##

A calibration guide for the new extruder is available [here](https://all3dp.com/2/extruder-calibration-6-easy-steps-2/).

Initialize the steps/mm of the extruder to the recomended value of 130mm by sending the [M92](https://marlinfw.org/docs/gcode/M092.html) gcode command.
```
M92 E130;
```

## PID Auto tunning ##

Run PID autotune for a temperature of 200 (PLA).

```
M303 S200 U1;
```

> Use the `U1` parameter to save the results automatically.

If the parameter `U1` is not supported by your firmware just run `M303 S200`. Then set your PID values with a `M301` command.

```
M301 P29.86 I3.37 D66.04;
```

The parameter `P` corresponds to the `Kp` value shown as the result of a M303 command. The parameter `I` is for `Ki` and `D` is for `Kd`.


From a flat surface like the extruder top or the filament gud
Amount to Extrude

M503 to see current steps per mm.
503
Issue a `G92` to reset the current position of the extruder as zero.

`G92 E0;` 

Issue a `G91` to put the printer in relative movement mode.

```
G91;
```
M92
Extrude 20mm of filament.
`G1 E20 F300;`

M92
```
M92 E130;
```



## Firmware ##

Change the direction of extruder:
```c
// For direct drive extruder v9 set to true, for geared extruder set to false.
#define INVERT_E0_DIR false
```



Before compiling ensure that you have the U8G2 Library installed. In Arduino IDE go to "Manage Libraries" and search for "U8g2", if the library is not installed press the "Install" button.


Change the language:
```c
#define LCD_LANGUAGE en
```

Change the default hotend temperature:
```c
#define PREHEAT_1_TEMP_HOTEND 210

#define BED_MAXTEMP 95

#define USE_ZMAX_PLUG
```


Enable thermal runaway protection:
```c
#define THERMAL_PROTECTION_HOTENDS // Enable thermal protection for all extruders
#define THERMAL_PROTECTION_BED     // Enable thermal protection for the heated bed
```

Set default Max Feed Rate (mm/s):
```c
#define DEFAULT_MAX_FEEDRATE          { 200, 200, 6, 70 }
```

Comment out the Z asix probe.
```c
//#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
```

Set probe edge:
```c
#define MIN_PROBE_EDGE 50
```

```c

#define UNKNOWN_Z_NO_RAISE // Don't raise Z (lower the bed) if Z is "unknown." For beds that fall when Z is powered off.

#define Z_HOMING_HEIGHT 0  // (in mm) Minimal z height before homing (G28) for Z clearance above the bed, clamps, ...
                             // Be sure you have this distance over your Z_MAX_POS in case.
```                         

Enable the following options by removing the double slash `//` in fron of each line:
```c

#define MESH_BED_LEVELING

#define LCD_BED_LEVELING

#define LEVEL_BED_CORNERS

#define FILAMENT_RUNOUT_SENSOR

#define NOZZLE_PARK_FEATURE
```

Set the number of grid points per dimension use in bed leveling to 4:

```c
#define MESH_INSET 10

#define GRID_MAX_POINTS_X 4
```

Edit the file `ultralcd_st7920_u8glib_rrd.h` in Arduino IDE. Find the following lines, remove the `//` in front and set the corresponding values as shown below:
```c

// If you want you can define your own set of delays in Configuration.h
#define ST7920_DELAY_1 DELAY_NS(0)
#define ST7920_DELAY_2 DELAY_NS(400)
#define ST7920_DELAY_3 DELAY_NS(0)

```


# BL Touch

```c
Starting and Ending GCode for Automatic Bed Leveler (3DTouch, BLTouch, CRTouch):

Starting G-code:
G28 ;Home
G92 E0 ;Reset Extruder
G1 E-1 F2700 ;Retract a bit
G29 ;abl
G92 E0 ;Reset Extruder
G1 Z1 F3000 ;Move Z Axis up
G1 X300 Y300 Z0.4 F5000.0
G1 X300 Y25 Z0.32 F1500.0 E30
G92 E0 ;Reset Extruder
G1 E-1 F2700 ;Retract a bit
G92 E0 ;Reset Extruder
G1 Z1.0 F3000 ;Move Z Axis up

Ending G-code:
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positioning
G1 X0 Y{machine_depth} ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed
M84 X Y E ;Disable all steppers but Z
```
