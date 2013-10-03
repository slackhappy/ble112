# Programming the BLE112 #

## Parts ##
1.  [Breakout Board with BLE112](
http://store.hardwarebreakout.com/index.php?route=product/product&product_id=61)
2.  [CC Debugger](http://www.ti.com/tool/cc-debugger) - [User Guide](http://www.ti.com/lit/swru197) - swru197


I followed [Programming the BLE with C code using IAR](http://blog.bluetooth-smart.com/2012/09/11/programming-the-ble112-with-c-code-using-iar/) almost exactly.  The pinout is only slightly different.

Here is the CC Debugger Pinout:

![CC Debugger Pinout](http://cl.ly/image/2B2s3R0V0Y0R/target-connector-pinout.png)

Here is the BLE Breakout Pinout, with the 6 CC Debugger Pin numbers indicated in black:

![BLE Breakout Pinout](http://cl.ly/image/1V0k2P0G1m3j/ble-breakout-pinout-cc-debugger.png)

A word of caution: I used the included ribbon cable initially, but I think the pins get flipped, so I ended up just using female-to-male jumper wire.  With the CC Debugger plugged in to my laptop, as soon as I connected the 3.3V pin, the LED on the debugger changed to green immediately.  I usually run OS X, so I downloaded and compiled cc-tool to check if the target worked:

1.  Download the tgz from [sourceforge](http://sourceforge.net/projects/cctool/files/)
2.  `brew install pkgconfig boost libusb`
3.  `tar -xzf cc-tool*.tgz ; cd cc-tool; ./configure && make`
4.  `./cc-tool -t`

I got back the following info:

    Programmer: CC Debugger
      Target: CC2540
      Device info:
       Name: CC Debugger
       Debugger ID: 0000
       Version: 0x05CC
       Revision: 0x0025

      Target info:
       Name: CC2540
       Revision: 0x21
       Internal ID: 0x8D
       ID: 0x2540
       Flash size: 128 KB
       Flash page size: 2
       RAM size: 8 KB
       Lock data size: 16 B
