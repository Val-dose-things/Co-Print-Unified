# Co-Print-Unified

# !!NOT READY!!

basic macros and configs for all printers. 


<a href='https://ko-fi.com/T6T517TCF6' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://storage.ko-fi.com/cdn/kofi6.png?v=6' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

# this will get you to a working starting point. anything else you will need to work on. please use the issues tab to let me know of any fixes that should be made. good luck. sorry for the sub-par how to. 

place all files into your config folder of your printer. 

# use the offical wiki for more help:

https://wiki.coprint3d.com/orcaslicer

https://github.com/coprint

if you have more then 4 you need ecm_1.cfg. more then 8 you need ecm_2.cfg. and so on

---------------------------

i like to use PuTTY https://www.putty.org/

you should update the devices to
use /dev/serial/by-id/

Unplug the KCM usb and then run this in the ssh shell.

```ls -la /dev/serial/by-id/```
This will show the host mcu

Then plug in the KCM usb with the toolhead disconnected

```ls -la /dev/serial/by-id/```
The new one is the KCM pad mcu

Plug in the toolhead

```ls -la /dev/serial/by-id/```
This will show the toolhead mcu.

Plug in the ECM usb

```ls -la /dev/serial/by-id/```
This will show the ecm mcu.

![482081274_1935388256864842_4292328743022954373_n](https://github.com/user-attachments/assets/e5e69390-d015-4c42-af3b-f177bbb7415c)
![481957638_1935388526864815_1304757567423387391_n](https://github.com/user-attachments/assets/215391a9-d271-4905-8d6e-a1f0cf646454)
![483917301_1935388723531462_1055497483776585922_n](https://github.com/user-attachments/assets/1a6300e8-9b05-4c00-b187-564002229834)

-------------------

you will need to use this in your slicer start gcode.
```
G28
G90
T{initial_extruder}
SET_HEATER_TEMPERATURE HEATER=extruder TARGET=150
M140 S[bed_temperature_initial_layer_single] ;set bed temp
M190 S[bed_temperature_initial_layer_single] ;wait for bed temp

HEATSOAK

START_PRINT EXTRUDER=[initial_extruder]

G92 E0.0 ; reset extruder
G1 X{first_layer_print_max[0]-80} Y{first_layer_print_max[1]+10} Z0.8 F6000.0 ; position 10mm behind print
M104 S[nozzle_temperature_initial_layer] ;set extruder temp
M109 S[nozzle_temperature_initial_layer];wait for extruder temp
M400

G1 E65 F600 ; set filament 
G92 E0.0 ; reset extruder
G1 X{first_layer_print_max[0]-80} Y{first_layer_print_max[1]+10} Z0.8 F6000.0 ; position 10mm behind print
G1 X{first_layer_print_max[0]-120} Y{first_layer_print_max[1]+10} E50 F360.0 ; extrude 60mm of filament in the x direction
G92 E0.0 ; reset extruder
G1 X{first_layer_print_max[0]-120} Y{first_layer_print_max[1]+7} Z0.8 F6000.0 ; position 7mm behind print
G1 X{first_layer_print_max[0]-80} Y{first_layer_print_max[1]+7} E50 F360.0 ; extrude 60mm of filament in the x direction
G92 E0.0 ; reset extruder
G1 E-0.5 F2100 ; small retraction
G1 X{first_layer_print_max[0]-40} F6000.0 ; move an additional 10mm without extruding
G92 E0.0 ; reset extruder

```
also add 

In Layer change Gcode add:
```SET_PRINT_STATS_INFO CURRENT_LAYER={layer_num + 1}```

and

In Change filament Gcode add:
```FILAMENT_CHANGE LAYER_NUM=[layer_num] NEXT_EXTRUDER=[next_extruder]```

update the following in orca

![image](https://github.com/user-attachments/assets/5b50e0ec-133e-4502-a620-4fecfcaa50c7)

# this will be different based on your printer

![image](https://github.com/user-attachments/assets/e09d8b17-201c-4d35-b1d2-fed8ed58c63d)

open the others folder here(https://github.com/Val-dose-things/Co-Print-SV08-Config/tree/main/other). download them on to your compute.
for the backup-mainsail.json go to settings and restore. this will geve you a better lay out for the macros. 

![image](https://github.com/user-attachments/assets/9809aca9-20bd-45c0-b9a3-3022e0cd867e)

![image](https://github.com/user-attachments/assets/2b44681d-eef4-4a0a-b7ed-48b44488b696)

# On some printers to get input shaper working you need to switch to mainline or use the BIGTREETECH S2DW V1.0 or the Co-Print Input Shaper Module.




