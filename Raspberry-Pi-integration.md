You can install a Raspberry Pi (like a RPiZeroW or a RPI3) inside the hoverboard, powered from a DC-DC convertor off 12v or 38v, and connect to the hoverboard via an STLINK if you want to program it via the RPI and a USB serial.

***
:warning: If you want to use a Raspberry 3 with UART on GPIO, please follow [this guide](Using-Raspberry-Pi-3-GPIO-UART)
***

Also, on any RPI **don't forget to [make your serial port transparent](Making-your-serial-port-transparent)** before using it

## Accessing serial interface
* If you use a USB serial dongle, use:
  ```
  screen /dev/ttyUSB0
  ```
* If you use GPIO UART, try:
  ```
  screen /dev/ttyS0
  ```
  OR
  ```
  screen /dev/ttyAMA0
  ```
For control, you can use Node-Red.

## Flashing from RPI
See [this page](Flashing-from-Raspberry)