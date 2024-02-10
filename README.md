# My Elegoo Neptune 4 Max customizations

## Description
This the configuration for my **Elegoo Neptune 4 Max**.  It includes the modified stock configurations files as well as my customizations.  Most of the customizations should work on any printer that runs Klipper except the "bed leveling" and "print start end" macros - these will need to be edited to ensure they are compatible with your printers geometry.
## Background
After having my customized configuration wiped out after firmware updates I have moved my customizations to the sub-directory `Custom_Macros` in the `klipper_config` directory. The customizations are logically grouped in seperate `.cfg` and `.conf` files for easier management.  
## Usage
To implement the customizations in this way create a sub directory called `Custom_Macros` in the `klipper_config` directory and copy the `.cfg` and `.conf` files to it and modify the `printer.cfg` and `moonraker.conf` files as appropriate.  You only need to modify the file(s) where you are doing customizations.  If a customization is causing problems simply appending a .txt to the end of the filename .cfg or .conf file and restarting/rebooting will remove it from the configuration.

To add the Klipper customizations, add the following lines to the top of the `printer.cfg` file immediately after the initial comment block.
```
[include ./Custom_Macros/*.cfg]
```
For Moonraker customizations add the following lines to the top of the `moonraker.conf` file. 
```
[include ./Custom_Macros/*.conf]

```
## Disclaimers
All this is provided as is and should you choose to use any of it you do so at your own risk.  Always backup your configs before making changes.

**Always** review the Elegoo and Klipper release note before doing any firmware updates to ensure none of the changes impact your customizations.
