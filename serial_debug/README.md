# Serial/Console/UART Debugging with the BLE112 #

While I developed the beacon project, and the toggle led project modifications, I was debugging using a single LED to represent whether a line of code was reached, or whether a return code was zero.  I decided to take a day to learn how to wire up a proper serial console for "println" debugging.


## Parts ##
1.  All parts from [programming.md](/programming.md) - The BLE board, CC Debugger, Bluegiga Tools, License Key.
2.  A USB to serial adapter.  I'm using the [FTDI Friend from adafruit](http://www.adafruit.com/products/284)
3.  4 Male to Male jumper cables to connect your BLE board to the adapter
4.  A serial terminal.  I'm using [RealTerm](http://sourceforge.net/projects/realterm/files/)
5.  The official [FTDI VCP driver] (http://www.ftdichip.com/Drivers/VCP.htm) - The automatically installed Windows Update one is not the correct driver.  Remember to right-click, Run as Administrator on the extracted driver.
6.  Peripheral Pinout from the [BLE112 datasheet](http://bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/documentation/), Page 8.  Under Data Sheets, once you log in using the gear in the top-right corner.  Here is an older, public datasheet with the same info, less clearly laid out: [old BLE112 datasheet](https://www.bluetooth.org/tpg/RefNotes/BLE112_Datasheet1.pdf), Page 9.

## Pinout ##
Here is the BLE Breakout Pinout, with the 6 CC Debugger Pin numbers outlined in green, and the 4 Serial Pins outlined in purple:

![BLE Breakout Pinout](http://cl.ly/image/0p3N0S370W0Q/ble-breakout-pinout-cc-debugger-serial.png)

This configuration is USART Channel 1 Alternate 1, shown on Page 8 of the datasheet.

<table>
  <tr>
    <th>BLE Pin</th>
	<th>BLE Name</th>
	<th>FTDI Name</th>
	<th>FTDI Color</th>
	<th>Notes</th>
  </tr>
  <tr><td>P0_2</td><td>CT</td><td>RTS</td><td>Green</td><td/></tr>
  <tr><td>P0_3</td><td>RT</td><td>CTS</td><td>Brown</td><td/></tr>
  <tr><td>P0_4</td><td>TX</td><td>RX</td><td>Yellow</td><td/></tr>
  <tr><td>P0_5</td><td>RX</td><td>TX</td><td>Orange</td><td/></tr>
  <tr><td>GND</td><td></td><td>GND</td><td>Black</td><td>Optional</td></tr>
  <tr><td></td><td></td><td>VCC</td><td>Red</td><td>N/C</td></tr>
</table>

Each pin on the BLE side is matched to its corresponding pin on the FTDI (computer) side, so transmit on the device is matched to receive on the FTDI.


## Code ##
I have consolidated bits of helpful code and advice from a few different sources:
- Advice and bluegiga sample project: [http://www.ambientsensors.com/bluetooth-low-energy-projects/](http://www.ambientsensors.com/bluetooth-low-energy-projects/)
- Additional information [http://www.sureshjoshi.com/development/ble112-uart-watermarks-example/](http://www.sureshjoshi.com/development/ble112-uart-watermarks-example/)

In `project.xml`, the usart hardware configuration is defined:

    <usart channel="1" alternate="1" baud="115200" endpoint="none" />

Refer to the "Bluetooth Smart Configuration Guide", Page 19, which can be found in the [bluegiga documents](http://bluegiga.com/en-US/products/bluetooth-4.0-modules/ble112-bluetooth--smart-module/documentation/) section.  The first two settings are relevant to the pins you use on the board, and the endpoint constant you use in BGScript.  The rest of the options are relevant for setting up RealTerm.

- Channel: 1
- Alternate: 1
- Baud: 115200
- Hardware flow control: true (default), means CTS/RTS lines are connected and enabled
- Stop bits: 1 (default)
- Data bits: 8 (cannot be changed)
- Parity: none (cannot be changed)

In `serial_debug.bgs`, the correct endpoint is set:

    endpoint = system_endpoint_uart1

And the string is sent over the wire:

    call system_endpoint_tx(endpoint, 11, "\n\rBooted!\n\r")(result)

Note that you need to indicate the length of the value you are sending over the wire!  Any string manipulation will have to be done manually on the buffer.  I included a few lines of gross int-to-string conversion code, since I expect that to be useful for future projects.

## Results ##
Once you hook up the serial lines, and program the device using the `bgbuild.exe` on the `project.xml` file in this directory, you should see a counter that increments every second:

![RealTerm Results](http://cl.ly/image/3I0v2V2x0W3X/realterm_serial_debug_capture.PNG)

Take a look at the RealTerm settings I have in the screenshot if you are having trouble.  My FTDI Friend registered as COM3, which is why my port is set to 3.  You can find your COM port under Device Manager in Windows if you expand the "Ports (COM & LPT)" section.