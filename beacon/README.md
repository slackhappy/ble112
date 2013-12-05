# BLE112 Programmable iBeacon #

An iBeacon advertiser using a Bluegiga BLE112

![BLE112 iBeacon](http://cl.ly/image/2Z1V3i3R1A3j/IMG_1201.JPG)

## Flashing Pinout ##
Here is the CC Debugger Pinout:

![CC Debugger Pinout](http://cl.ly/image/2B2s3R0V0Y0R/target-connector-pinout.png)

Here is the BLE Breakout Pinout, with the 6 CC Debugger Pin numbers indicated in black:

![BLE Breakout Pinout](http://cl.ly/image/1V0k2P0G1m3j/ble-breakout-pinout-cc-debugger.png)

## Flashing instructions ##
1.  Attach your CC Debugger using the pinout above.  Your CC debugger light should be green.  Open the BLE Update Tool (called BLE SW Update Tool after install).  Click info.  You will get your Serial Number.  Click the "Request License Key" link under license key to get a license key.  I had to right-click and copy the link location, then paste that into my browser.  It is actually a `mailto:` link, so you need to wait a day to get your license key back from support.
 ![BLE SW Update Tool](http://cl.ly/image/38393t310u41/BLESWUpdateTool.PNG)
2. From the beacon directory, `C:\Bluegiga\ble-1.2.0-88\bin\bgbuild.exe project.xml`.

3. Flash the device using the BLE SW Update Tool and `out.hex` from the beacon directory.

You can now connect a 3.3v battery if you would like.

## Programming instructions ##
1. Using [LightBlue](https://itunes.apple.com/us/app/lightblue-bluetooth-low-energy/id557428110?mt=8), find the device.  It should be called "iBeacon Demo"
2. Find the service labeled "7548d6e0-3476-11e3-aa6e-0800200c9a66"
3. "7548d6e1-3476-11e3-aa6e-0800200c9a66"  sets the UUID.  The default AirLocate program for iPhone uses `E2C56DB5DFFB48D2B060D0F5A71096E0` as one of its UUIDs when searching.  Set this or any other 16-byte (32-char) hex value using "Write Hex"
4. "7548d6e2-3476-11e3-aa6e-0800200c9a66"  sets the Major Id.  Write any 2-byte (4 char) hex value.
5. "7548d6e3-3476-11e3-aa6e-0800200c9a66"  sets the Minor Id.  Write any 2-byte (4 char) hex value.
6. "7548d6e4-3476-11e3-aa6e-0800200c9a66"  sets the Tx Power.  It is a 1-byte field.  The "Calibration" section of AirLocate will tell you how to fill this out.  Take the 2's complement of the number it gives you.
7. "7548d6e5-3476-11e3-aa6e-0800200c9a66" displays the full advertising payload.  This includes AD Flags and iBeacon headers, as well as the values you have set.

Remember to disconnect from the GATT/quit LightBlue, otherwise the device will not advertise!

All values are saved to the persistent store, so your values will survive a reset.


## Acknowledgements ##

I simply put 2 and 2 together.

[BGScript Custom Advertisements example code](https://bluegiga.zendesk.com/entries/23130518-BGScript-custom-advertisement-Custom-advertisement-packet-creation)

[iBeacon protocol analysis on StackOverflow](http://stackoverflow.com/questions/18906988/what-is-the-ibeacon-bluetooth-profile/)
