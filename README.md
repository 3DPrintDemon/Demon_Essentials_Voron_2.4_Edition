
# WELCOME TO 3DPRINTDEMON 

# THE DEVILISHLY GOOD “DEMON ADAPTIVE VORON 2.4 (DAV) MACRO PACK”!!
## Made to make your printing life easier & your printer SMARTER!
### I hope you enjoy these automatic & highly adaptive macros! 
A lot of time, testing, love & coffee has been poured into them!
If you feel you’d like to support my efforts & help to enable me to continue sharing my ideas please consider buying me a beer/coffee at the provided “Support this project” link. Thanks!

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

These macros are smart & have adaptive properties & will shape themselves to what you’re printing. 
For example the `PRINT_START` macro knows if your printer is already homed so wont home it again, & can automatically shape itself to things like your printer’s bed size, what temperatures you’re printing at, & it even knows the current file’s first layer height so it’ll print the purge lines at the same height! It can automatically load the correct mesh for the temperature of your print, as your bed will slightly change shape, as well as choosing the correct settings for your chamber cooling system, & it will even check to see if you have filament loaded before starting a print! …We’ve all done that one haven’t we, be honest!!
Also it can decide decide if your chamber needs to be heat soaked or not before the print starts! This is fantastic for saving time, money & electricity between back-to-back prints where the system doesn’t require heat soaking as it’s already up to temperature!!

You have all this plus step by step adaptive on screen messages on any Mainsail web interface & KlipperScreen system so you know exactly what your machine is deciding to do at any time!
Some macros can be customised by changing the settings in the macro button options before you manually call the macro in the Mainsail or KlipperScreen interfaces!

Not only that, but all these features are user customisable within Macro Variables sections inside the files! Some functions can even be totally deactivated entirely & bypassed with a simple changing an option from `True` to `False` with above variables macros! This is very useful if your printer doesn’t have the hardware components installed at this time but leaves the configuration easily customisable with a few keystrokes in the future if you want to add to your machine!

With the new `_GOODNIGHT` macro you can even flick a GUI switch in Mainsail to let the printer know you want it to auto power down after it’s finished printing!! 
This can be done at ANY point during the print! You can even change your mind & cancel the auto shutdown at any point before the print completes!

**NOTE: Additional hardware & setup is required for this feature to work! How to do this is explained further on in this readme file.**

The `_RET_CALI_START` macro is used when calibrating your retraction settings with files generated at http://www.retractioncalibration.com/
All you need do is paste `_RET_CALI_START` into the website's "Custom Gcode" box next to the green "Generate Gcode" button
This is without a doubt the absolute BEST retraction test out there!

The `CLEAN_NOZZLE`, `LOAD_CLEAN`, & `UNLOAD_CLEAN` macros are for use with a nozzle cleaning brush found here:
https://www.printables.com/model/201999-nozzle-scrubber-with-a-little-bucket-for-voron-24
The original `CLEAN_NOZZLE` macro is posted on that link, I have simply adapted it to be used with variables in this macro set. The author has been informed on his model’s Printables page of its adaptation. The macro is also credited to him in the file posted here & anywhere else it is intended for use alongside his nozzle scrubber model, with links provided.
**BE SURE TO SET YOUR MACRO VARIABLES**  `_CLEAN_VARIABLES`

The rest of the macros are simple single click automations for running a series of tasks you’d normally have to remember the correct procedure for & are a hassle to run multiple times if done manually. They’re quality of life macros to help you get the best setup & results from your printer.  

# All sounds great right!? Ok well here’s the tricky bit! 
…Well its not that tricky because I got it all written down here for you to just copy/paste into your setup!

### FOR ANY FILE SPECIFIC INSTRUCTIONS & VARIABLES PLEASE CHECK THE FILE TEXT!

**Don’t just install & run them & wonder why they don’t work! They will NEED setting up once on your system. Damage to your machine may result if the macros are run without the prerequisites or without the correct setup before first use!** 

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

To make use of the `_GOODNIGHT` post print auto shutdown macro you must enable your RPI as a secondary MCU so it can control your shutdown relay hardware. Use this link to do that.
https://github.com/Klipper3d/klipper/blob/master/docs/RPi_microcontroller.md

## Word of warning! Adding a power control device like a power shutdown relay can sometimes involve working with & modifying your printer’s wiring that runs on mains level voltage!  This can be extremely dangerous with a definite risk of serious injury, fire, loss of property & even death! You have been warned. I accept no liability or responsibility for any loss, death or injury caused directly or indirectly by you or anyone else attempting this! This is all on you, attempt implementation ENTIRELY AT YOUR OWN RISK!

Example below for using the BTT Power Relay v1.2

See the install instructions for this product on the BTT Github! 
https://github.com/bigtreetech/BIGTREETECH-Relay-V1.2

However….
This link is far more helpful! 
https://www.youtube.com/watch?v=5wJff-hY90s

Then you will need to set your instance to be able to control your Pi’s GPIO pins as mentioned previously in this document. You need to choose which 2 pins to use. Then you need to SSH into your pi & run:
```
sudo nano /boot/config.txt
```
Then near the bottom of the file at the end of the first section & in the space BEFORE the start of the [CM4] section paste in:
```
gpio=16=op,dh # Example GPIO pin, chose a GPIO pin to control power device’s PSon pin
```
Then use the commands at the bottom of the screen to exit & save the file.

This will make sure that the GPIO pin you will use for the relay’s `PSon` pin is automatically pulled “high” when the Pi is first turned on at the beginning of the boot sequence. This in turn should keep your relay from automatically opening & shutting the printer down while the Pi is booting. It does this as at boot the power relay is not seeing a ‘keep switched on’ signal from the Pi, & it needs that signal. 
Trust me it is very annoying if you don’t do this!

You will then need to modify your `Moonraker.conf` file by adding these…
```
[power Printer Power]
type:gpio
pin:gpio16 # Example GPIO pin, you can choose your own here
initial_state:on
off_when_shutdown: True
locked_while_printing: True
restart_klipper_when_powered: True
restart_delay: 2
bound_services:

[power Reset Power]
type:gpio
pin:gpio12 # Example GPIO pin, you can choose your own here
locked_while_printing: True
initial_state:off
restart_klipper_when_powered: True
restart_delay: 2
Timer:2
```
After that add this macro to your `macros.cfg`
```
[gcode_macro M81]
gcode:
 {action_call_remote_method("set_device_power",device="Printer Power",state="off")}
```

Lastly this is used by the `PRINT_END` macro to select the Auto Shutdown feature.
```
[output_pin PRINTER_AUTO_OFF]
pin: ### <<<<<< Insert unused board pin for state change only, monitored by system
```
This will give you full macro control of your power relay unit via the `PRINT_END` & `_GOODNIGHT` macros.


Then once you’ve done that you’ll need to add a Chamber thermistor to your machine if you haven’t already.
To set this thermistor to be used as both a fan controller for cooling the Chamber & a sensor for the system to use add these to your printer.cfg adding the same board pin used & the sensor type your’e using.

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

Here is the required macro for your `macros.cfg` to run the filament sensor. The filament sensor check can be enabled & disabled in the `_START_VARIABLES` marco
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

To add menu buttons to KlipperScreen for your new Nozzle cleaning functions add these lines to your `KlipperScreen.conf` file:
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
