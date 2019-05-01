To program the firmware from the RPI:

Install openocd (sudo apt-get install openocd).

```
openocd -f /usr/share/openocd/scripts/interface/stlink-v2.cfg -f /usr/share/openocd/scripts/target/stm32f1x.cfg -c "program firmware.bin 0x08000000" -c "halt 100" -c "reset"
```
(You can make a script flash.sh, and copy the firmware.bin over with winscp over ssh).