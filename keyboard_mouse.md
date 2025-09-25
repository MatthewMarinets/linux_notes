# Keyboard and Mouse configuration
## Mouse changing the repeat rate/delay
I like a short delay and fast repeat. As of writing this, I'm using 180ms delay, 60Hz repeat.

```sh
xset r rate 180 60
```

The first input is the delay in milliseconds. The second is the repeat rate in Hz.

This only sets it until reboot. To apply generally,
[schedule the task to run on startup](#scheduling-script-on-startup).

## Middle Mouse Button
In windows, middle mouse button allows for fast scrolling.

In Linux, it's used for a fast "paste selection" (with a click).

To get something Windows like, you have to modify some xinput parameters:

### Get the device name
```sh
$ xinput --list
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ Glorious Model O                        	id=8	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Power Button                            	id=7	[slave  keyboard (3)]
    ↳ Glorious Model O Keyboard               	id=9	[slave  keyboard (3)]
    ↳ Logitech G513 RGB MECHANICAL GAMING KEYBOARD	id=10	[slave  keyboard (3)]
    ↳ Logitech G513 RGB MECHANICAL GAMING KEYBOARD Keyboard	id=11	[slave  keyboard (3)]
    ↳ 1080P Web Camera: 1080P Web Cam         	id=12	[slave  keyboard (3)]
```

Here the device name is "Glorious Model O". That then gets used later

### Check properties
You can run `xinput --list-props "Glorious Model O"` to see the available properties

### Change property
Enabling a fast scroll requires changing the "libinput Scroll Method Enabled" property:
```sh
xinput --set-prop "Glorious Model O" "libinput Scroll Method Enabled" 0 0 1
```

### Result
This should allow for a different form of fast-scrolling --
click and hold the middle mouse button and drag up or down to scroll very fast.

[Schedule the task to run on startup](#scheduling-script-on-startup).

## Scheduling script on startup
Using [cron](./cron.md) didn't quite work, as these commands have to run on-login / on-desktop initialization
rather than on startup.

Linux Mint has a GUI "Startup Applications" manager.
Adding a script there with Startup delay: 0 executes things on login.
I still included a `sleep 3` at the start of the script to play it safe.
Seems to work consistently.