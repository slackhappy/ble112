# BLE112 #

I bought a bluegiga BLE112 mounted on a breakout board from [hardwarebreakout.com](
http://store.hardwarebreakout.com/index.php?route=product/product&product_id=61).  It has turned out to be a fun embedded programming environment.

![BLE112 breakout board](http://cl.ly/image/0w0s1P2A2U2y/IMG_1118_annotated_sm.jpeg)

My goal is to be able to build an application on the built-in microcontroller, and communicate with my phone.  I have acheived the baseline goal: I can toggle timed LED from my phone.  There is still much exploring left to do.

See [notes.md](/notes.md), where I'm trying to put together all of the resources I am finding around the web about the BLE112, and the TI Bluetooth LE SoC in general.

See [programming.md](/programming.md), for information on programming the BLE112.  This is a bit specific to bluegiga devices.  This should give you the steps you need to try out any of the projects I have made.

Projects:

* [ancs](/ancs) - example implementation of a client for Apple Notification Center Service (e.g. smartwatch)
* [beacon](/beacon) - a programmable clone of an Apple iBeacon device
* [serial_debug](/serial_debug) - an example project for UART debugging
* [toggle_led](/toggle_led) - an LED that can be turned on or off with your phone
