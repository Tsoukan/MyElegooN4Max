# Custom macros descriptions
You need to add `[include ./Custom_Macros/*.cfg]` to the start of your printer.cfg for the *.cfg files to be included in printer.cfg  
You need to add `[include ./Custom_Macros/*.conf]` to the start of your moonraker.conf for the *.conf files to be included in moonraker.conf  
## Bed_leveling_Macros.cfg  
Used to enable Klipper BED_SCREWS_ADJUST and SCREWS_TILT_CALCULATE  
Adds LEVEL_MY_BED macro which allows updating the elegoo created bed mesh 11 (advanced level mode) with my typical PLA temps of 210/60  
After you install KAMP you will need to rename edit the `BED_MESH_CALIBRATE PROFILE=11` to be `_BED_MESH_CALIBRATE PROFILE=11`  
## Flashlight_On_Macros.cfg  
Macros needed to enable turning on the overhead LED strip when the printer boots.  
Relies on sled2_on.sh  
## Homeseer_config.conf  
Enables control power control through Homeseer home automation.  See https://moonraker.readthedocs.io/en/latest/configuration/#power  
## KAMP_Settings.cfg  
The KAMP configuration to printer.cfg.  File is created by following the KAMP install from https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.  
***Important***: When following the instructions to install KAMP replace all the instances of `printer_data/config/` in the paths with the path to the directory that contains your printer.cfg file, 'klipper_config' for the V1.2.2.65 Elegoo Neptune 4 MAX firmware.  
i.e. `ln -s ~/Klipper-Adaptive-Meshing-Purging/Configuration/ ~/klipper_config/KAMP`  
## KAMP_update_manager.conf  
Adds the update manager entries for KAMP to moonraker  
## Power_Control_macros.cfg  
Adds a macro to power off device  
Adds macros to activate power off at end of print and to deactivate it if needed.  See https://github.com/tinntbg/auto-power-off-klipper.git  
## Print_start_end macros.cfg  
Since Elegoo runs the print_start and print_End macros automatically these can be added to the Start/End gcode for the printer.  If you do, the start macro will run after the PRINT_START  
## sled2_on.sh  
shell script to turn on the overhead LED.  
