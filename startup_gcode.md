<style>
fn { color: #5cd6ae; font-size: 1.5em; display: block; border-bottom: 1px solid #5cd6ae;  }
.note_err {  border: 1px solid transparent; background-color: #f8d7da; color: #842029; border-color: #f5c2c7; font-size: 1em; display: block; position: relative; padding: 0.25rem 0.5rem; margin-bottom: 1rem; border-radius: .25rem; }

.gcode {  border: 1px solid transparent; color: #055160;
	background-color: #cff4fc;
	border-color: #b6effb; font-size: 1em; position: relative; padding1: 0.25rem 0.25rem; margin-bottom: 1rem; border-radius: .25rem; }

</style>

# Start Up Gcode

The following sections covers fragments of GCODE that you can use in your startup gcode.

## Setup

Basic setup of units and others that are always used.

| GCODE | Description |
| --- | --- |
| `G28;` | Runs homing axis. |
| `G21;` | Set units to millimeters. |
| `G90;` | Use absolute values when moving in the coordinate space. |


## Auto Bed Leveling (ABL)

<span class="note_err">
Only use if you have a BL-Touch or similar ABL sensor installed.
</span>

Run ABL before each print. This adds more time to the print but gives you the most accurate result and it is specially a good idea if your table or printer setup is not steady. This code must be after the <code class='gcode'>G28</code> (*homing*).

| GCODE | Description |
| --- | --- |
| `G29;` | Run the ABL cycle. |

## Reuse stored Auto Bed Leveling (ABL)

<span class="note_err">
Only use if you have a BL-Touch or similar ABL sensor installed.
</span>

If your printer is steady and firm you can opt to run auto bed leveling once and reuse the resulting leveling mesh in future prints.

1. Using your Software (MatterControl, Cura) you send the following gcodes to your printer to store an ABL mesh:

| GCODE | Description |
| --- | --- |
| `G28` | Run an auto homing cycle. Wait for homing to finish. |
| `G29` | Run the Auto Bed Leveling cycle. Wait for homing to finish. |
| `M500` | Save the leveling mesh to your boards EEPROM. |

2. Modify your startup gcode with the following:

| GCODE | Description |
| --- | --- |
| `M420 S1;` | Enables bed leveling. Use if you have manually stored the leveling mesh of G29 with a M500. Do not use M420 and G29 together. |

## Prime and Wipe

You can add this optional gcode to your startup to prime your nozzle.

| GCODE | Description |
| --- | --- |
| `G1 X2 Y200 Z0.4 F5000.0;` | Moves to the side 2mm and back 200mm, get nozzle close to bed. |
| `G1 X2 Y5.0 Z0.32 F1500.0 E30;` | Extrude 30mm of filament while lifting nozzle |
| `G92 E0;` | Reset extruder to 0 |
| `G1 E-1 F2700;` | Retract some filament so we have less problems with oozing and leveling. |

## Get ready for printing

| GCODE | Description |
| --- | --- |
| `G92 E0;` | Reset extruder to 0 |
| `G1 Z1.0 F3000;` | Move Z Axis up |
| `M78;` | OPTIONAL Sends info back to your software. Useful if you print a lot directly from the computer. |

## Correct endstop position

**OPTIONAL** In some cases the x-asis dont quite align with the edge of the bed. When I home my printer the nozzle lands outside the bed. We can use a [M206](https://marlinfw.org/docs/gcode/M206.html) to set an offset for our X-Asis. You can do the same with your Y-Asis.

| GCODE | Description |
| --- | --- |
| `M206 X-8;` | Offset X-Asis endstop. Moves bed 8mm to the right. |


