## Overview
This version of Marlin contains my own personal changes to support my 3d Printer.  
It is based off the [bugfix-2.1.x branch](https://github.com/MarlinFirmware/Marlin/tree/bugfix-2.1.x), specifically [commit d5cf0b3348](https://github.com/MarlinFirmware/Marlin/tree/d5cf0b334802cf825e501135a55d1d63884004a1).  Please see the original Marlin repo for information about the firmware itself.

3D Printing has been a very challenging hobby for me.  Plenty of people have had good luck with the stock Creality Ender3 Pro, but for me I was plagued with adhesion and other issues from the start.  As a result I have many upgrades, some necessary, some not.  My current setup is listed below to provide context on the specific firmware I am using and to let others know how my printer is now configured.  It is technically still an Ender3 Pro, but the only original parts are the frame, bed carriage, screen, and Z/Y motors.

## My Printer
Links are direct to the products I used for easy reference and are not sponsored nor do I any compensation for any products purchased from them.

* Creality Ender3 Pro, purchased Jan 2021 [(link)](https://www.creality.com/products/ender-3-pro-3d-printer)
* BL Touch, Antclabs upgrade kit for Creality [(amazon link)](https://www.amazon.com/gp/product/B0859T6JVC/)
* Micro Swiss NG™ Direct Drive Extruder for Creality CR-10 / Ender 3 Printers (includes all metal hotend) [(link)](https://store.micro-swiss.com/products/micro-swiss-ng-direct-drive-extruder)
* BIGTREETECH SKR MINI E3 V3.0 32 Bit Control Board for Ender 3/Ender 3 Pro/Ender 5/Ender 5 plus/CR-10 [(link)](https://biqu.equipment/collections/control-board/products/bigtreetech-skr-mini-e3-v2-0-32-bit-control-board-for-ender-3)
* Various fans.  I'm real good at breaking them.  [(link 4020 extruder fan)](https://www.amazon.com/gp/product/B005T7CQHO/) [(link 4010)](https://www.amazon.com/gp/product/B09VL2MDQN/)
* PEI bed. It came with the glass bed but recently I got the PEI and like it a lot.  [(link)](https://www.amazon.com/gp/product/B09Y1WDKM9/)
* Silicone springs [(link)](https://www.amazon.com/gp/product/B09M82KJ1S)

## Marlin Configuration Changes

### Baseline
* Downloaded the latest Marlin from bugfix-2.1.x branch.  For me this was [commit d5cf0b3348](https://github.com/MarlinFirmware/Marlin/tree/d5cf0b334802cf825e501135a55d1d63884004a1)
* Downloaded the Marlin/Configuration branch at [commit 0ee781981a](https://github.com/MarlinFirmware/Configurations/tree/0ee781981a7708a84e9a6ea804cfd0f15be38e99), and copied configuration.h and configuration-adv.h for the Creality/Ender-3 Pro/BigTreeTech SKR Mini E3 3.0.  
<br>
### BL Touch modifications, basic Install
* Used the guide at [Teaching Tech > Upgrade Guides > BL Touch](https://teachingtechyt.github.io/upgrades.html#bltouch)  
<br>
#### Updates to configuration.h
* Enabled
```
   #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN   
   #define BLTOUCH
   #define AUTO_BED_LEVELING_BILINEAR
   #define Z_SAFE_HOMING
```
* Changed
```
   #define NOZZLE_TO_PROBE_OFFSET { -43, -11, -1.85 }  -- XY values match my offset for BL Touch and the shroud that came with the Microswiss NG
```
* Commented
```
   // #define MESH_BED_LEVELING
```  
#### Updates to configuration_adv.h 
* Enabled
```
   #define PROBE_OFFSET_WIZARD              // Add a Probe Z Offset calibration option to the LCD menu
   #define BABYSTEP_ZPROBE_OFFSET           // Combine M851 Z and Babystepping
```