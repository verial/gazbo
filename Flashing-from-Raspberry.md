To program the firmware from the RPI:

Install openocd (sudo apt-get install openocd).

```
openocd -f /usr/share/openocd/scripts/interface/stlink-v2.cfg -f /usr/share/openocd/scripts/target/stm32f1x.cfg -c "program firmware.bin 0x08000000" -c "halt 100" -c "reset"
```

(I made a script flash.sh, and copy the firmware.bin over with winscp over ssh).

To connect to the serial, if you use a USB serial dongle, use:
```
screen /dev/ttyUSB0
```
If you use GPIO UART, try:
```
screen /dev/ttyS0
```
OR
```
screen /dev/ttyAMA0
```

again, another script 't.sh'.

For control, you can use Node-Red.