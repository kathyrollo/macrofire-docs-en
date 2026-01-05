MacroFire 3.2.9

# Table of Contents

* Introduction
* Overview
* Supported Environments
* Installation
* Launch Order
* How to Use
* Features
* Configuration Files
* Specifications
* Future Plans
* Final Notes
* Acknowledgements

=================================================

## Introduction

This program is a plugin that runs on PSP custom firmware.
It does not work on standard Sony official firmware.

As always, use at your own risk.
If the system freezes or progress is lost during gameplay, there is no recourse.

## Overview

MacroFire provides button remapping, configurable rapid-fire for any button,
and macro functions that allow repeated automated input sequences.

Rapid-fire settings can also configure hold states,
allowing automatic actions in RPGs without rubber bands or weights.

Macro functions can record specific actions and repeat them.

Analog stick adjustments and remapping can help compensate for worn sticks or broken buttons.

## Supported Environments

Custom Firmware 5.50 GEN-D3
Custom Firmware 5.00 M33-6

Does not appear to work on 3.71M33 or lower.
PSP-2000 and PSP-3000 compatibility is untested.
Extended RAM is not required.

## Installation

Copy the following files to ms0:/seplugins:

```
macrofire.prx  
macrofire.ini  
```

Then, add the path below to each of the following in ms0:/seplugins:

```
vsh.txt  
game.txt  
pops.txt  

ms0:/seplugins/macrofire.prx  
```

If these text files do not exist, create them.

(Placement in the file may affect other plugins. See “Launch Order” below.)

After saving, go to Recovery Mode and enable MacroFire in the Plugins menu.

Note: The rapid-fire and macro functions do not work while the PSP Internet Browser is active in VSH.
This is a precaution to prevent unintended actions on other websites.

The remap_sample folder contains example button remapping files:
- analog_to_dpad.ini: map analog stick to D-pad
- dpad_to_analog.ini: map D-pad to analog stick
- ss_to_home.ini    : map SELECT + START to HOME
- lr_to_vol.ini     : map L/R buttons to volume controls

This folder is not required for MacroFire to operate.

## Launch Order

MacroFire uses the `sceSysconSetDebugHandlers` API for control,
which allows only one plugin to register a handler at a time.

MacroFire can coexist with one other plugin using this API if it launches first.

Example: HOLD+ plugin also uses this API.
To coexist:
- MacroFire must launch first
- HOLD+ launches afterward

Plugin load order is determined by the line order in vsh.txt/game.txt/pops.txt.

```
  ...other plugins  
  ms0:/seplugins/macrofire.prx  
  ...other plugins  
  ms0:/seplugins/hold.prx  
```

Only one other plugin can coexist. If multiple plugins use the API, behavior is unpredictable.

## How to Use

Start the game and press the two buttons configured for volume (+/-) to open the menu.
These buttons can be changed in the configuration file (see Configuration Files below).

Basic menu controls:

```
↑↓←→       : Move cursor  
(○/×)/□   : Change options  
(○/×)      : Confirm selection  
(×/○)      : Go back  
START      : Close menu immediately  
```

○/× buttons are automatically swapped according to the PSP registry.

Some features may require additional controls, displayed at the bottom of the screen.

## Features

MacroFire Engine
Toggle the plugin itself. Controls all functions including rapid-fire and macros.
Default is OFF at game launch; use ○/□ to enable.

Buttons to launch the menu
Configure which buttons open the MacroFire menu in-game.

Buttons to toggle the engine
Configure buttons to turn MacroFire Engine ON/OFF without opening the menu.

Status notification
Display MacroFire status on screen when engine or macros change state.

Analog stick sensitivity adjustment
Adjust center position, sensitivity, and dead zones.
See manual_analogsens.txt for details.

Remap settings
Configure button remapping. See manual_remap.txt for details.

Rapidfire settings
Configure button rapid-fire. See manual_rapidfire.txt for details.

Macro settings
Configure and execute macros. See manual_macro.txt for details.

## Configuration Files

MacroFire.ini (main configuration), rapid-fire, and macro files mostly share the same format.
See manual_ini.txt for detailed instructions.

## Specifications

* MacroFire does not activate immediately after game launch,
  waiting up to ~10 seconds to avoid interfering with game load.
  VSH and POPS detection allows immediate activation.

* MacroFire pauses other threads when the menu is displayed,
  but threads started before MacroFire are not paused.
  Some plugins (e.g., screenshotbmp) may interfere and cause freezes.
  Ensure MacroFire is loaded before these plugins or only use them when the menu is closed.

* Opening the menu during file access may leave the memory stick access light blinking.
  This is harmless, but file lists may fail to load and macro/rapid-fire save/load may time out.
  Retry after returning to the game.

* English translations may be poor.

## Future Plans

* Allow relative paths in macrofire.ini file settings.
* Enable rapid-fire on remapped buttons in Remap settings.
* Improve the Remap settings interface.
* Enhance file save/load dialog functionality.

## Final Notes

Remember, plugins are unofficial and games are not designed for them.
Always save frequently to avoid data loss.

For users willing to help with debugging, use the “Debug MacroFire” version:

```
  http://classg.sytes.net/products/psp/#MACROFIRE  
```

See its readme.txt for instructions and bug reporting.

## Acknowledgements

This software benefited greatly from the following projects:
PSPLink
PSP VSH extender / SYSCON override example 070910 by Booster

Thanks also to PSPSDK, custom firmware developers, and the broader PSP community.

Special thanks to all developers of PSP VSH extender, PSPLink, CFW, and PSPSDK.

---

pen@ClassG
[http://classg.sytes.net](http://classg.sytes.net)
