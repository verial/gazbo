You can install a Raspberry Pi (like a RPiZeroW) inside the hoverboard, powered from a DC-DC convertor off 12v, and connect to the hoverboard via an STLINK and a USB serial.

To program the firmware from the RPiZeroW:

Install openocd (sudo apt-get install openocd).

```
openocd -f /usr/share/openocd/scripts/interface/stlink-v2.cfg -f /usr/share/openocd/scripts/target/stm32f1x.cfg -c "program firmware.bin 0x08000000" -c "halt 100" -c "reset"
```

(I made a script flash.sh, and copy the firmware.bin over with winscp over ssh).

To connect to the serial, I use a USB serial dongle, and use 

```
screen /dev/ttyUSB0
```

again, another script 't.sh'.

For control, you can use Node-Red.