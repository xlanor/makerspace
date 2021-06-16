# Makerspace@AcePointer
Just a changelog of all the modifications we've done to the Ender 3 so far. For reference for my colleagues who may take over the printer.

# Printer
- [Creality Ender 3](https://www.creality.com/goods-detail/ender-3-3d-printer)
We actually got the Ender 3S, which is basically the Ender 3 that comes pre-assembled sold on taobao. For all intents and purposes flashing the Ender 3 firmware works fine on the Ender 3s.

# Bed Mount / Bed
- The ender has been retroffited with siliconed bed mounts to reduce bed shifting during prints, as the standard springs have a tendency to shift over long print times
- The stock bed was already burned, so we replaced the default bed with a creality glass bed. The z offset needs to be compensated for this.
- The clips have been replaced with third party clips that do not bump the nozzle / fan duct.
- Do NOT print PETG without blue tape on the glass bed, to prevent it from fusing with the bed.

# BLTouch mount
- Autobed levelling has been added by purchasing the bl-touch leveller.
- First, level the bed manually (as accurate as you can make it). 
- Constantly tweak the z-offset until you are able to find a satisfactory z-offset value.
- The x, y, and z offset of the bltouch will vary depending on the type of mount printed

# Fan Duct
- The fan duct is printed in ABS with 100% infill. We use this: [Satsana Ender 3 Remix with bltouch and 5015 blower fan](https://www.thingiverse.com/thing:4647053).
- The fans have been snipped off and re-soldered with new fans, with heat shrink over the solder joints for insulation.
- The hotend fan has been replaced with an Orion Knight (24Dba). These can be bought from mouser.
- The Part cooling fan has been replaced with a 5015 blower I had lying around.
- It is important to note that any replacement fans should be 24V and NOT 12V, because we did not install a buck converter, and because I don't want to undercool things.
- Do not use noctua, it does not cool the hotend enough!
- Simply desolder, twist, resolder if fans need to be replaced.
- For this fanduct and bltouch mount, the offsets are as follows:  X-43.65 Y-10 Z-1.25 

# Mainboard replacement
- The Ender 3 stock stepper motors sounds like R2D2 when it's printing. It's not acceptable because we're placing it in the office.
- The motherboard was replaced with Creality's 4.2.7 silent motherboard. By default, the stock motherboard was a 1.1.3, so this means that we were also upgrading the motherboard to a 64bit motherboard, together with the silenced motors.
- The hotend tuning got completely fucked, and Creality support claims that "PID tuning is not officially supported"
- We have to retune the pid using OctoPrint to issue marlin commands, and once again saving to the SD card didn't seem to work, so we have to note the values and run them each time the printer is restarted. For simplicity's sake, I added it to my Cura's printer profile as a pre-printing code.
- To redo PID tuning, I ran `M303 C8 E0 S200 U1` to tune the hotend for 8 cycles to 200 degrees, and saved the values generated from `M303` to use in `M301`.
- For tuning to 200degs, my values were around `P16.70 I0.98 D70.94`.
- This step was crucial because without this the Ender would not maintain a constant temperature  and constantly end up with a thermal runaway.

# Mainboard Mounting
- The mainboard in its stock mounting position is blocked by the bed which makes it extremely annoying to do any rewiring.
- We moved it to the back and added a raspberry pi with a PoE hat to run octoprint.

