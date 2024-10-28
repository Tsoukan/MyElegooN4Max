# My Elegoo Neptune 4 configuration guide

## Description
This guide is to help new users get thier **Elegoo Neptune 4** running as best as it can on the stock firmware.  This guide should work on on any **Elegoo Neptune 4**.
## Background
After having sturggled with getting my **Elegoo Neptune 4 Max** running reliably I decided to document my steps here in the hopes that it will help others get thier printers up and running well as quickly and painlessly as possible.  Unfortunately Elegoo modified the Klipper firmware for thier printer in such a way that it no longedr works like "vanila" klipper and that leads to some problems and lots of confusion.
## Usage
To guide is written assuming you have a basic understanding of the stock GUI, **FLuidd** that runs on Elegoo Neptune 4 Printers as well as use of the touch pad.
## The guide
Once you have assembled and followed the setup instructions provided by Elegoo you are ready to proceed.  Now is a good time to make sure your build plate is perfectly clean - wash it with dishsoap and agressively scrub it using a clean coarse cloth or Scotchbright (or similar) sponge - I like a fresh blue one.  Rince and repeat to ensure it is completely clean.  Air dry or use paper towel to dry.  It is probably a good idea to have one dedicated to cleaning the print bed.  Also if you want to use IPA (isopropyl alcohol) to clean between prints use only paper towel, even a freshly laundered cloth seems to leave a residue that can keep prints for sticking.

**Note: Never use the update buttons in Fluidd to do any updates, they will break things and it is a headache to recover from.**
### Configuration
1. If you have not already done so update the printer to the latest Elegoo firmware.
    1. Go to Elegoo's [download](https://www.elegoo.com/pages/download) center and select your printer.  Download the firmware that is at the top of the list of firmwares
    2. Follow the instructions bundled with the firmware download.  Use the USB and TF card provided with the printer to avoid and issues.  Using newer USB3 or high capacity TF cards can cause issues.
    3. Update the main control board firmware.  After doing the update, check the 'update.log' that is written to the USB by the printer to ensure that it indicates success.  If not, try again...if it still fails contact Elegoo support.  They can be a bit slow, likely due to timezone difference, but are usually very helpful.
    4. Update the Touchscreen firmware.  Make sure that the display indicated success.  If not, try again...if it still fails contact Elegoo support.  They can be a bit slow, likely due to timezone difference, but are usually very helpful.
2. "Level" the printer from the touch screen.  See page 12 in the manual or the bottom section of the yellow sheet.  It is necessary to do this from the touchscreen at least once to ensure that the firmware gets updated to load the mesh correctly.
    1. Select 'Level' from the touch screen.
    2. Select the `Leveling Toggle` button in the upper right corner to the screen.  Make sure it is "pro" or 121 points.
    3. Adjust the `z-offset` - don't fuss too much at this point, we won't be relying on this for printing yet, you just want to feel a bit of resitance when moving the paper under the print head.  Take your time - I find the quickest way to do this is to select 1mm and move the head down one click at a time while moving the paper until it jams, move up one click, select 0.1mm and repeat the process of moving down until the paper jams and then back up.  Now select 0.01mm and move down until you fells a bit of drag when moving the paper.
    4. Do the `auxiliary leveling`.  Use the same paper technic as for the z-offset.  Again don't fuss too much.
    5. Do the `automatic leveling`.  Let the printer do it's thing, it will take a while.
3. Enable "Screw Tilt Adjust" so we can use the printers sensor to do the "auxiliary leveling" and not have to do the paper thing.  This makes it much easier and consistent.
    1. Connect to Fluidd
    2. Select `{...}` (Configuration) from the tabs on the left.
    3. Right click on the `printer.cfg` file and select duplicate and give it a name (I usually just add the date and time to the end of the filename i.e. `printer.cfg 2024-10-25_1215`).  Click save.
    4. Click on the printer.cfg to open it for editing.
    5. In the `[probe]` section and edit the `samples: 2` to be `samples: 3`.  This increases the number to times the bed is probed each time, it takes longer but you get a better reading, increasing beyond 3 did not make a material diffence in my experience.
    6. In the `[probe]` section and edit the `samples_result: median` to be `samples_result: average`
    7. Copy and paste the approprate block from [Neptune 4 screws_tilt_adjust](https://github.com/Tsoukan/MyElegooN4Max/blob/main/Neptune%204%20screws_tilt_adjust) below the last line of the `bed_mesh` block.
    8. Click `save and restart` at the top.
4.  Confirm that the changes have been applied by looking for the macro `SCREWS_TILT_CALCULATE` shows up in the macros section of the dashboard.
5.  Using the touch pad go to `settings` > `advanced settings` > `Vibration pattern optimization` and perform both the X and Y optimizations.  This should be done with your printer in the exact location you will be using it, with a spool of filament on the holder.  If you move your printer to another location, perform this again since the table/desk also contributes to vibrations.  If you notice the the table/desk is moving a lot during this test you should probably find a sturdier place to put your printer.

### Leveling the bed
1. Warm the bed to your prefered/typical temperature.  For example 60C for PLA, 70C for PETG
2. Wait 20-30 minutes for the bed to "heat soak".  This ensures that the bed is heated as evenly as possible.
3. Heat the nozzle to your prefered/typical printing temperature.  For example 205C for PLA, 230C for PETG
4. Click on your new `SCREWS_TILT_CALCULATE`.  The printer will probe the middle of the bed (Plus and Max only) then above each adjustment screw.  In the console you will see the progress and then a report telling you how much to turn each screw in hours (complete turns) and minutes (partial turns) and the direction (CW or CCW as viewed from above).  Repeat this until you are within 6 minutes.  Here is an example - think analog clock.

```
SCREWS_TILT_CALCULATE
01:20 means 1 full turn and 20 minutes, CW=clockwise, CCW=counter-clockwise
front left screw (base) : x=-5.0, y=30.0, z=2.48750
front right screw : x=155.0, y=30.0, z=2.36000 : adjust CW 01:15
rear right screw : y=155.0, y=190.0, z=2.71500 : adjust CCW 00:50
rear left screw : x=-5.0, y=190.0, z=2.47250 : adjust CW 00:02
ok   
```

5. Cut a strip of paper ~2.5CM/1" wide
6. From the touch screen click level, do the `z-offset` and `automatic leveling` only, do not do the auxiliary leveling, it has been replace by the `SCREWS_TILT_CALCULATE`.
For the z-offset do a paper test (note that since we are doing it with everything hot the nozzle will need to be much closer to the bed since we don't have to account for thermal expansion), using the strip of paper, place it under the print nozzle lower it as you did in step 2(iii), this time you want to be able to pull the paper, it move with a fair bit of resistance, but it should buckle when you push it back.  Don't pull the paper out from under the nozzle, just pull and push a couple of CM/", if it does come out you may need to raise the printhead a bit to get it back under.  Once the zoffset is set do the automatic leveling.
7. **Click the save icon in the upper right hand corner**.  The printer will restart.
8. You are now ready to proceed with fine tuning.  At this point you can try your first print, you will still need to tweak the z-offset a bit for a good first layer but the printer should be capable of producing a halfway decent print at this point.
### Fine tuning
This is well outside the scope of this guide and there are excellent ones already out there. Have a look at [Ellis' Print Tuning Guide](https://ellis3dp.com/Print-Tuning-Guide/ ), it is an excellent resource and can answer a lot of questions.

### Tips and Tricks
1. You can view your bed levelness on the `Tune` tab.  The picture exagerates any contours in your bed, what you should really look at is the "range" of eh active mesh under the "Bed Mesh Controls".  On my max I have found that a range below 0.3 produces very good prints.  To put this number in perspective, that sheet of paper you used to set your zf-offset is likely about 0.2mm thick.  Also, for Plus and Max, bigger beds will always have a larger range and be a bit more work to level, you may want to try and get withing 3 minutes doing the screws tilt calculate.
2. You can perform the mesh measurements from the `tune` tab.  For it to work with the Elegoo firmware you **must** save it using the name Elegoo uses for it to load properly.  This is usually simply the number **_11_**.  After doing the calibrate click the save as button and enter **11** for the profile name and hit save.  You can also select the "remove default profile" check box to elimiate any future confusion.
3. While simply turning off the power is usually OK, it is best to shutdown the host before killing the power, in Fluidd you can do so using the 3 dots menu in the upper right corner and selecting Host > Shutdown
4. Power failure recovery is pretty useless since your print will likely pop off your build plate when it cools, it is only good for momentary power blibs while you are present since you need to click resume once the power come back on.  It can also cause some problems since there is can be a momentary pause during printing as the printer writes the recovery point every layer.  Unless you know you will be able to resume after a short power outage it is best to turn it off - `Settings` > `Advanced settings` > `Resume printing`.


Once your comfortable with the basic functions of your printer and configuring it have a look at [My Elegoo Neptune 4 Max customizations](https://github.com/Tsoukan/MyElegooN4Max/blob/main/customizations.md) for some tips and advanced configurations.  This is how I had my printer configuration before I switched to [OpenNeptune](https://github.com/OpenNeptune3D/OpenNept4une).  At that time my printer was working reliably and I could just send a print, make sure the first 10 or so layers where good (good bed adhesion, no lifting, etc.) and walk away.  The longest print I have done is about 34 hours.
While I would recommend OpenNeptune to anyone, it is quite an advanced task and may be well outside the comfort level of a lot of makers.  It can also affect warranty and support from Elegoo since it is a modification (most manufactures warranties stipulate not modifications).  The guide that the OpenNeptune team has written is excellent and if diligently followed is quite painless.  It took me about 4 hours to install, but you have to have the requisite knowledge and comfort working with Linux, doing hardware modifications, etc.  If you are not comfortable or confident in your level of knowledge and abilities I do not recommend you attempt installing OpenNeptune.  Just stick with the Elegoo firmware which does work.


## Disclaimers
All this is provided as is and should you choose to use any of it you do so at your own risk.  Always backup your config files before making changes.

**Always** review the Elegoo and Klipper release note before doing any firmware updates to ensure none of the changes impact your customizations.  It seems that Elegoo updates seem to replace your modified printer.cfg with a default one.  See my [customizations](https://github.com/Tsoukan/MyElegooN4Max/blob/main/customizations.md)  for an easy way to workaround this.
