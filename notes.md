# Notes on the BLE112 #

## BLE112 ##
The BLE112 is a Bluetooth Low Energy (aka Bluetooth Smart) module from bluegiga. The [product page](http://www.bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/) has more information, but basically, it is a package that includes a bluetooth SoC module from TI, an antenna, certification, and some free developer tools.

*  [Product Page](http://www.bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/)
*  [Breakout Vendor](http://store.hardwarebreakout.com/index.php?route=product/product&product_id=61)
*  [Datasheet](https://www.bluetooth.org/tpg/RefNotes/BLE112_Datasheet1.pdf)
*  [Programming the BLE112 with IAR](http://blog.bluetooth-smart.com/2012/09/11/programming-the-ble112-with-c-code-using-iar/) - A good walkthough of getting the BLE112 set up, even if you do not have IAR, like me.
*  [Programming the BLE112 with BGScript](http://blog.bluetooth-smart.com/2012/09/16/programming-the-ble112-using-bgscript/) - A follow-up post to the first post that uses BGScript.  It also walks you through getting the SDK from bluegiga.

## CC2540 ##


The BLE112 is packaged implementation of the [CC2540 BLE SoC](http://www.ti.com/product/cc2540) from TI.

*  [Product Page](http://www.ti.com/product/cc2540)
*  [Datasheet](http://www.ti.com/lit/ds/symlink/cc2540.pdf)
*  [Microcontroller Datasheet](http://www.ti.com/lit/swru191) - swru191
*  [Developer Guide](http://www.ti.com/lit/swru271) - swru271
*  Flash Programming: [Application Note](http://www.ti.com/lit/swra410) - swra410, [Hardware Interface](http://www.ti.com/lit/swra124) - swra124

There are two ways to use the SoC, which is outlined the developer guide:

1.  Single-Device, where the controller, host, and application are all implemented on the SoC.  Apparently this is the lower-power option.  The application is implemented as a set of evented tasks that are registered with the Operating System Abstraction Layer (OSAL), which is described in the Developer Guide.

2.  Network Processor, where the contoller and host are on the SoC, and an external processor interacts with the SoC using SPI or UART.  The SoC can use a provided firmware called HostTestRelease.

My plan is to explore the Single-Device option, without purchasing the IAR Embedded Workbench, and before I use the BGScript tool packaged with the BLE112.  Here are the steps I have taken so far:

1.  Download the [BLE Stack] (http://www.ti.com/tool/ble-stack?DCMP=wbu-blestack&HQS=blestack).  You need to accept the export license agreement.  Also download the associated Developer Guide (link above).
2.  The CC2540 has a 8051 microcontroller in it.  The datasheet for the microcontroller itself is here [PDF](http://www.ti.com/lit/swru191). It is refered to in TI forums as swru191.  This contains the description of the chip itself.  8051-compatible microprocessors are primarily extendable through [Special Purpose Registers (SRUs)](http://www.8052.com/tutsfr.phtml).  The [Small Device C Compiler (SDCC)](http://sdcc.sourceforge.net/) has a [hardware-level description of the cc2530](http://sourceforge.net/p/sdcc/code/HEAD/tree/trunk/sdcc/device/include/mcs51/cc2530.h). 
