# toggle_led #

![Toggle LED Result](http://cl.ly/image/1L1c0E043M43/ToggleLED_Breadboard.JPG)

This project toggles an LED attached to the device on and off every second you can disable the toggling using a Bluetooth LE program on your phone that supports the Generic Attribute Profile.  I made a modified version of the toggle_led project from [Programming the BLE112 using BGScript](http://blog.bluetooth-smart.com/2012/09/16/programming-the-ble112-using-bgscript/) from bluetooth-smart.com, which is an excellent tutorial.

The toggle_led script from bluetooth-smart.com will toggle an LED, but the bluetooth radio seems to be mostly disabled.  This is because that tutorial uses the TI SmartRF programmer.  That programmer overwrites a region that where the bluegiga license key is supposed to reside, and I believe this disables most of the BGScript functionality.  If you accidentally use the SmartRF programmer, just use the BLE SW Update tool again, and paste your license back in, and you should be good to go.

## Flashing Pinout ##
Here is the CC Debugger Pinout:

![CC Debugger Pinout](http://cl.ly/image/2B2s3R0V0Y0R/target-connector-pinout.png)

Here is the BLE Breakout Pinout, with the 6 CC Debugger Pin numbers indicated in black:

![BLE Breakout Pinout](http://cl.ly/image/1V0k2P0G1m3j/ble-breakout-pinout-cc-debugger.png)


## Flashing instructions ##
1. Connect a 1K resistor from P0_7 to the positive (longer lead) end of an LED, and connect the negative end of the LED to ground.
2. From the toggle_led directory, `C:\Bluegiga\ble-1.2.0-88\bin\bgbuild.exe project.xml`
3. Flash the device using the BLE SW Update Tool and `out.hex` from the toggle_led directory.  Your LED should now be blinking.
4. Using [LightBlue](https://itunes.apple.com/us/app/lightblue-bluetooth-low-energy/id557428110?mt=8), find the device.  It should be called "Toggle LED Demo".  Navigate to the service starting with "384ABBC5".  This is a GUID that I generated for my service (I used [GUIDGen.com](http://www.guidgen.com/)).  There should be one characteristic found.  Press Write.  In the "Write Hex" box, write `00`.  This should make the LED stay solid on.  Now write `01`.  The LED should now blink again.


