[<img width="171" alt="kofi_s_tag_dark" src="https://github.com/3DPrintDemon/Demon_KLIPPER_Essentials/assets/122202359/6538fcbf-b866-4e33-81c6-f9c95428bca4">](https://ko-fi.com/3dprintdemon)

# WELCOME TO 3DPrintDemon 

# THE DEVILISHLY GOOD “Demon_Essentials_Voron_2.4_Edition”!! 
## New version re-written with many new features added & improved!


### Made to make your printing life easier & your printer SMARTER!
### I hope you enjoy these automatic & highly adaptive macros! Don't forget if you like & use this project you can buy me a beer/coffee to say thanks. https://ko-fi.com/3dprintdemon
A lot of time, testing, love & coffee has been poured into them!
If you feel you’d like to support my efforts & help to enable me to continue sharing my ideas please consider buying me a beer/coffee at the provided “Sponsor this project” link. Thanks!

### This macro relies on you setting the correct filament type in your slicer! BE SURE YOU DO THIS!

### NEW! Now includes the Demon Bed Fans Monitor!
- Smart & fully adaptive Bed Fans control system!
- Full instructions available here:

### NEW! The Demon AES System! 
- Save your printer from damage from homing errors when using a Z Endstop switch
- Full instructions avaiable here: https://github.com/3DPrintDemon/Voron_2.4_AES_System_Auto_Emergency_Stop_For_Z_Endstop_Switch

### NEW! Start Macro handling for Smart Filament Sensor Encoder
- Disables the sensor until the macro completes

### NEW! Support for Klipper's `ADAPTIVE_MESH` system in the latest Klipper update
- NOTE you need the latest version of Klipper to use this!

### NEW! Adaptive Pressure Advance Mode! - APA - ORCA SLICER ONLY

- Why have only 1 single setting for Pressure Advance trying to work across the whole print when you can have 6!!

- 6 settings per filament, 30 in total!

- Each setting is automatically selected by filament for different types of extrusions during the print.

- Settings for Perimeter, External Perimeter, Internal Infill, Solid Infill, Top Solid Infill, & filament default.

- Print tuning towers for the speed of each extrusion type & apply them to the Adaptive Pressure Advance (APA) modifiers!

- Disable or enable individual modifiers, you don't have use them all, use any number in any combination!

- Or disable modifiers by filament or the whole module at once!

- All settings in one easy to edit place, no need to edit macro code!

- Verbose mode, read back all APA commands to the console!


### NEW! Mesh Auto Builder!

- Auto build all 5 meshes at different temperatures with included heat soak waits & message prompts! Inspired by a community contribution from Karl L! Thank you for sharing!

## Included macros:

- `PRINT_START`
- `PRINT_END`
- `_RET_CALI_START`
- `_GOODNIGHT`
- `CLEAN_NOZZLE`
- `LOAD_CLEAN`
- `UNLOAD_CLEAN`
- `Z_Switch_Calibrate`
- `Z_Probe_Calibrate`
- `Z_Probe_Accuracy`
- `Pressure_Advance_Test_Mode`
- `Stepper_Buzz_Cycle`
- `PID_Tune_Mode_FULL`
- `Auto_Shaper_Calibrate`

## Introduction

These macros are smart & have adaptive properties & will shape themselves to what you’re printing. 
For example the `PRINT_START` macro knows if your printer is already homed so wont home it again, & can not only automatically shape itself to simple things like your printer’s bed size & what temperatures you’re printing at, but it will even know the current file’s first layer height so it’ll print the purge lines at the same height! Plus it can automatically choose & load the correct mesh for the temperature of your print, as your bed will slightly change shape the hotter it gets. 

Not only that but it will choose the correct settings for your chamber cooling system, & it will even check to see if you have filament loaded before starting a print! …We’ve all done that one haven’t we, be honest!!

Also it can decide if your chamber needs to be heat soaked or not before the print starts! This is fantastic for saving time, money & electricity between back-to-back prints where the system doesn’t require heat soaking as it’s already up to temperature!! 

You have all this plus step by step adaptive on screen messages on any Mainsail web interface & KlipperScreen system so you know exactly what your machine is deciding to do at any time! Some macros can be customised by changing the settings in the macro button options before you manually call the macro in the Mainsail or KlipperScreen interfaces!

It doesn't end there, as all these features are user customisable within the Macro Variables sections inside the files! Some functions can be totally deactivated entirely & bypassed with a simple changing an option from `True` to `False`! This is very useful if your printer doesn’t have the hardware components installed at this time but leaves the configuration easily customisable with a few keystrokes in the future if you want to add to your machine!

With the new `_GOODNIGHT` macro you can even flick a GUI switch in Mainsail to let the printer know you want it to auto power down after it’s finished printing!! 
This can be done at ANY point during the print! You can even change your mind & cancel the auto shutdown at any point before the print completes!

**NOTE: Additional hardware & setup is required for this feature to work! How to do this is explained further on in this readme file.**

The `_RET_CALI_START` macro is used when calibrating your retraction settings with files generated at:

http://www.retractioncalibration.com/

All you need do is paste `_RET_CALI_START` into the website's "Custom Gcode" box next to the green "Generate Gcode" button
This is without a doubt the absolute BEST retraction test out there!

The `CLEAN_NOZZLE`, `LOAD_CLEAN`, & `UNLOAD_CLEAN` macros are for use with a nozzle cleaning brush found here:

https://www.printables.com/model/201999-nozzle-scrubber-with-a-little-bucket-for-voron-24

The original `CLEAN_NOZZLE` macro is posted on that link, I have simply adapted it to be used with variables in this macro set. The author has been informed on his model’s Printables page of its adaptation. The macro is also credited to him in the file posted here & anywhere else it is intended for use alongside his nozzle scrubber model, with links provided.

**BE SURE TO SET YOUR MACRO VARIABLES**  `_CLEAN_VARIABLES`

The rest of the macros are simple single click automations for running a series of tasks you’d normally have to remember the correct procedure for & are a hassle to run multiple times if done manually. They’re quality of life macros to help you get the best setup & results from your printer.  

## All sounds great right!? Ok well here’s the tricky bit! 
…Well its not that tricky because I got it all written down here for you to just copy/paste into your setup!

### FOR ANY FILE SPECIFIC INSTRUCTIONS & VARIABLES PLEASE CHECK THE FILE TEXT!

**Don’t just install & run them & wonder why they don’t work! They WILL need setting up once on your system. Damage to your machine may result if the macros are run without the prerequisites or without the correct setup before first use!** 

You will need to add some lines to your slicer's `Start G-code` & `End G-code` boxes to get the `PRINT_START` macro to work correctly. 

These are in the `demon_print_start_end.cfg` file.

# Prerequisites
You must download & `[include]` these two additional files along with these Demon Adaptive Voron 2.4 (DAV) Macros or they will NOT work correctly.

These additional macros are prerequisites:

- https://github.com/rkolbi/voron2.4/blob/main/non-blocking_wait.md
- https://github.com/VoronDesign/Voron-Stealthburner/blob/main/Firmware/stealthburner_leds.cfg

Also the `PRINT_START` macro is intended for use on a printer that has been fitted with the above nozzle scrubber model. 
You can if you wish disable this functionality but you will have to manually go through the macro & comment out all the `CLEAN_NOZZLE` calls.
If this is the case do not `[include]` the `clean_load.cfg` macros without the nozzle scrubber installed on your machine.

****************************************************************************************************************************
# IF YOU RAN V1.0-V2.5 BE SURE TO UPDATE YOUR SLICER'S START GCODE AS PER V2.6 FILE OR NEW FEATURES WONT WORK!
****************************************************************************************************************************


# INSTALL

Copy the files here into a folder called `Demon_Essentials` in your config folder on your printer. 

Then, paste into your printer.cfg
```
[include ./Demon_Essentials_Voron_2.4_Edition/*.cfg]
```

This will include all files in a folder called Demon_KLIPPER_Essentials in your `~/config` folder.

Or you can use...

```
cd /home/pi/printer_data/config
```
NOTE: the above command is for a real Raspberry Pi, if you're using a cloned system that "/pi" folder will change to `mks` or `btt` or similar.

```
git clone https://github.com/3DPrintDemon/Demon_Essentials_Voron_2.4_Edition.git
```

Then, paste into your printer.cfg
```
[include ./Demon_Essentials_Voron_2.4_Edition/*.cfg]
```

This will bring these files into your system, be sure to comment out & NOT delete your current START & END PRINT Macros just yet!

# Additional Configuration

## Auto Shutdown Moonraker Power Device

To make use of the `_GOODNIGHT` post print auto shutdown macro you must enable your RPI as a secondary MCU so it can control your shutdown relay hardware. Use this link to do that.

- https://github.com/Klipper3d/klipper/blob/master/docs/RPi_microcontroller.md

After you've followed the process in that link be sure that this is added to your `printer.cfg` file.
```
[mcu host]
serial: /tmp/klipper_host_mcu
```

## Word of warning! Adding a power control device like a power shutdown relay can sometimes involve working with & modifying your printer’s wiring that runs on mains level voltage!  This can be extremely dangerous with a definite risk of serious injury, fire, loss of property & even death! You have been warned. I accept no liability or responsibility for any loss, death or injury caused directly or indirectly by you or anyone else attempting this! This is all on you, attempt implementation ENTIRELY AT YOUR OWN RISK!

## Connections

Example below for using the BTT Power Relay v1.2

See the install instructions for this product on the BTT Github! 

- https://github.com/bigtreetech/BIGTREETECH-Relay-V1.2

However….

This link is far more helpful! 

- https://www.youtube.com/watch?v=5wJff-hY90s

You will need ensure that you have set your instance to be able to control your Pi’s GPIO pins as mentioned previously in this document. Then you need to choose which 2 GPIO pins on your Rpi to use to control the relay, connect the `Printer Power` GPIO pin along with a single ground pin to the PSon plug on the relay board. You have to then connect the Pi's `Reset Power` GPIO pin to the `reset` pin on the relay board, leave the 5v pin next to it empty.

Then if you wish you can add a physical momentary switch to a 3rd GPIO pin & another ground pin. Then mount it somewhere of your choice on your printer. This button will act as an instant on button & re-power the printer with a single push, norammly you have to manually switch both pins on yourself but now Moonraker will now activate both pins at the same time for you! Magic!

## Setup

Then you need to SSH into your pi & run:
```
sudo nano /boot/config.txt
```
Then near the bottom of the file at the end of the first section & in the space BEFORE the start of the `[CM4]` section paste in:
```
gpio=16=op,dh # Example GPIO pin, choose a GPIO pin to control power device’s PSon pin
```
Then use the commands at the bottom of the screen to exit & save the file.

This will make sure that the GPIO pin you will use for the relay’s `PSon` pin is automatically pulled “high” when the Pi is first turned on at the beginning of the host boot sequence. This in turn should keep your relay from automatically opening & shutting the printer down while the Pi is booting. It does this at boot because the power relay is not seeing the ‘keep switched on’ signal from the Pi, & it needs that signal. 
Trust me it is very annoying if you don’t do this!

You will then need to modify your `Moonraker.conf` file by adding these…
```
[button PowerUp]
type: gpio
pin: ^gpio21 # Example GPIO pin, you can choose your own here
minimum_event_time: .05
on_press:
  {% do call_method("machine.device_power.post_device", device="Reset Power", action="on") %}
  {% do call_method("machine.device_power.post_device", device="Printer Power", action="on") %}

[power Printer Power]
type:gpio
pin:gpio16 # Example GPIO pin, you can choose your own here
on_when_job_queued: True
initial_state:on
off_when_shutdown: True
locked_while_printing: False
restart_klipper_when_powered: False
# restart_delay: 2
bound_services:

[power Reset Power]
type:gpio
pin:gpio12 # Example GPIO pin, you can choose your own here
on_when_job_queued: True
locked_while_printing: True
initial_state:off
restart_klipper_when_powered: True
restart_delay: 2
Timer:2
```
You need these two pins as the BTT relay firmware requires a reset command while the `PSon` pin is high. If this is not the case & the `PSon` pin is low (off) & you hit reset the relay power up but trip out again after 8 seconds. This is normal. The `PSon` pin must be high (on) when the reset is pressed. The PowerUp physical button will activate both GPIO pins together when pushed meaning you only need a single push of the physical button to control both pins & re-power the printer instanly.

After that add this macro to your `macros.cfg`
```
[gcode_macro M81]
gcode:
 {action_call_remote_method("set_device_power",device="Printer Power",state="off")}
```

Lastly this is used by the `PRINT_END` macro to select the Auto Shutdown feature & should be pasted into your `printer.cfg` file.
```
[output_pin PRINTER_AUTO_OFF]
pin: ### <<<<<< Insert unused board pin for state change only, monitored by system
```
This will give you full control of your power relay unit via the GUI Switch & the `PRINT_END` & `_GOODNIGHT` macros.

## Chamber Monitoring & Fan Control

Then once you’ve done that you’ll need to add a Chamber thermistor to your machine if you haven’t already.
To set this single thermistor to be used as both a fan controller for cooling the Chamber & a regular sensor for the system to use add these sections to your printer.cfg, adding the same board pin & the sensor type your’e using.

**NOTE: if you’re using a single thermistor these should be the same for all 3 sections below. If you have 2 thermistors you can omit the `[duplicate_pin_override]` section and use a different thermistor for each section. But just one is fine.**
```
# This single pin will be used by both [temperature_fan chamber] as well as [temperature_sensor Chamber_Temp]
[duplicate_pin_override]
pins: ### <<<<<< Insert Your Chamber temp sensor pin

# This is used for the pla & asa_chamber_temp values in the PRINT_START macro & can be enabled & disabled in the _START_VARIABLES marco
[temperature_fan chamber]
pin: ### <<<<<< Insert board pin for sensor
max_power: 1.0
shutdown_speed: 0.0
kick_start_time: 5.0
cycle_time:0.01
off_below:0.1
sensor_type: ### <<<<<< Insert thermistor type
sensor_pin: PA3
min_temp: 5
max_temp: 70
target_temp: 40
control: watermark
gcode_id: C 

# This is used by the heat_soak_threshold variable in the PRINT_START macro & can be enabled & disabled in the _START_VARIABLES marco
[temperature_sensor Chamber_Temp]
sensor_type: ### <<<<<< Insert thermistor type
sensor_pin: ### <<<<<< Insert board pin for sensor
min_temp: 5
max_temp: 70
gcode_id: CH
```

## Filament Sensor
If you have or are going to install a filament sensor this must be added to your `printer.cfg` file to run the filament sensor. The filament runout check in the `PRINT_START` macro can then be enabled & disabled in the `_START_VARIABLES` marco if you dont have one or dont want to perform the check at the start of the print.
```
[filament_switch_sensor filament_sensor]
switch_pin: ### <<<<<< Insert board pin for sensor
pause_on_runout: True
insert_gcode:
    { action_respond_info("Insert Detected") }
runout_gcode:
    { action_respond_info("Runout Detected") }
pause_delay: 0.5
```
## Modifying KlipperScreen Menus For New Features
To add main screen menu buttons to KlipperScreen for your new Nozzle cleaning functions add these lines to your `KlipperScreen.conf` file:
```
[menu __main custom]
name: Filament
icon: spoolman

[menu __main custom load]
name: Load Clean
icon: arrow-down
method: printer.gcode.script
params: {"script":"load_clean"}

[menu __main custom unload]
name: Unload Clean
icon: arrow-up
method: printer.gcode.script
params: {"script":"unload_clean"}

[menu __main custom clean]
name: Nozzle Clean
icon: toolchanger
method: printer.gcode.script
params: {"script":"clean_nozzle"}
```
The icons are appropriate if you use with the material-darker theme. Other theme’s icons may differ.

You can also add your chamber temp to the menubar in KlipperScreen, this to your `KlipperScreen.conf` file:
```
titlebar_items: chamber
```

## Extra Bonus...
As an added bonus you can add a second physical button to a 4th GPIO pin to use as a physical Emergency Stop button!

```
[button estop]
type: gpio
pin: gpio26 # Example GPIO pin, you can choose your own here
on_press:
  {% do call_method("printer.emergency_stop") %}
```

## v2.6! Updated to include the new integrated KLIPPER Adaptive Mesh option. There is no longer any need for a separate KAMP install.

For the Adaptive Mesh feature to work you must have:
- The latest version of Klipper!*
- Enabled your Slicer for `Exclude Objects`
- Added the `Exclude Objects` section to your `moonraker.conf` file
- Added the `Exclude Objects`section to your `printer.cfg` file

Add this to your `moonraker.conf` file:
```
[file_manager]
enable_object_processing: true
```

Add this to your `printer.cfg` file:
```
[exclude_object]
```

Save & restart!

## To use adaptive meshing all files MUST have been sliced with `Exclude Objects` active.
## IF NOT YOU WILL RECEIVE THE FOLLOWING ERRORS!!

If you use ORCA SLICER:

`Error evaluating 'gcode_macro PRINT_START:gcode': gcode.CommandError: This error is caused by the sliced file not having EXCLUDE_OBJECT enabled! Please disable Adaptive_Meshing in the user_settings.cfg or re-slice the file with it enabled and restart the print!`

If you use another slicer:

`Internal error on command:"PRINT_START"`

`Internal error on command:"BED_MESH_CALIBRATE"`


## Fin...
If you made it to the end here congrats! 

I hope this macro pack makes a nice difference to your printing life, dont forget, if you feel its valuable enough to use please consider hitting that "sponser this project" button & buying me a beer/coffee. Its always very much appreciated. Thank you & happy printing!!

[<img width="171" alt="kofi_s_tag_dark" src="https://github.com/3DPrintDemon/Demon_KLIPPER_Essentials/assets/122202359/6538fcbf-b866-4e33-81c6-f9c95428bca4">](https://ko-fi.com/3dprintdemon)

# WANT MORE...??
Whats that I hear you cry, you want more?! Ok I got you covered!

How about fully automated power on/off control with auto cool down & shutdown after a print finishes?! Plus have full control even after Klipper is in shutdown! What is this black magic?!!!

Find out here!

https://github.com/3DPrintDemon/BTT-Relay-v1.2-Moonraker_INSTANT_Power-On-Button

Or maybe you're using Klicky Probe & sensorless homing & you want an AUTO E STOP system so that if your nozzle misses your endstop switch the printer knows there's a problem!

https://github.com/3DPrintDemon/Voron_2.4_AES_System_Auto_Emergency_Stop_For_Klicky_Probe

If thats not enough how about creating your very own online auto updating backup of all your config files here on Github in your own private repo?!

https://github.com/3DPrintDemon/Auto_Backup_Your_Klipper_Printer
