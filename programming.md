# Programming the BLE112 #

## Parts ##
1.  [Breakout Board with BLE112](
http://store.hardwarebreakout.com/index.php?route=product/product&product_id=61)
2.  [CC Debugger](http://www.ti.com/tool/cc-debugger) - [User Guide](http://www.ti.com/lit/swru197) - swru197
3.  [bluegiga BLE Update Tool](http://www.bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/documentation/) - under "the PC Tools" section.  Create an account and log in using the little gear widget in the top-right to access.
4.  [bluegiga Bluetooth Smart Software and SDK v1.2](http://www.bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/documentation/) - under the "Software Releases" section.  Create an account and log in using the little gear widget in the top-right to access.

I followed [Programming the BLE with C code using IAR](http://blog.bluetooth-smart.com/2012/09/11/programming-the-ble112-with-c-code-using-iar/) almost exactly.  The pinout is only slightly different.

## Pinout ##
Here is the CC Debugger Pinout:

![CC Debugger Pinout](http://cl.ly/image/2B2s3R0V0Y0R/target-connector-pinout.png)

Here is the BLE Breakout Pinout, with the 6 CC Debugger Pin numbers indicated in black:

![BLE Breakout Pinout](http://cl.ly/image/1V0k2P0G1m3j/ble-breakout-pinout-cc-debugger.png)

A word of caution: I used the included ribbon cable initially, but I think the pins get flipped, so I ended up just using female-to-male jumper wire.  With the CC Debugger plugged in to my laptop, as soon as I connected the 3.3V pin, the LED on the debugger changed to green immediately.

## Running an example project ##
1.  Attach your CC Debugger using the pinout above.  Your CC debugger light should be green.  Open the BLE Update Tool (called BLE SW Update Tool after install).  Click info.  You will get your Serial Number.  Click the "Request License Key" link under license key to get a license key.  I had to right-click and copy the link location, then paste that into my browser.  It is actually a `mailto:` link, so you need to wait a day to get your license key back from support.
 ![BLE SW Update Tool](http://cl.ly/image/38393t310u41/BLESWUpdateTool.PNG)
2. Build one of the example projects: in `cmd`:
 * `cd \Bluegiga\ble-1.2.0-88\example\find_me\`
 * `..\..\bin\bgbuild.exe project.bgproj`
 * open `C:\Bluegiga\ble-1.2.0-88\example\find_me\out.hex` in the BLE SW Update Tool. An click "Update".  The screen should show a green "Update completed" panel.
 * On your iOS device with BLE (iPhone 4S and up), if you have one, download [BTL Explorer](https://itunes.apple.com/us/app/btlexplorer/id532751145?mt=8).  You should see "Bluegiga Find Me" in the peripherals list.

 ![BTLExplorer showing Bluegiga Find Me in the list](http://cl.ly/image/2R1z2c383u0G/BTLExplorer.PNG.jpg)


## toggle_led project ##

Now for some fun stuff.  The [toggle_led](/toggle_led) project toggles an LED attached to the device on and off every second you can disable the toggling using a Bluetooth LE program on your phone that supports the Generic Attribute Profile.  I made a modified version of the toggle_led project from [Programming the BLE112 using BGScript](http://blog.bluetooth-smart.com/2012/09/16/programming-the-ble112-using-bgscript/) from bluetooth-smart.com, which is an excellent tutorial.

Head over to the [toggle_led](/toggle_led) project to program it.
