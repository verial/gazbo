I used a 'blue pill' STLink-v2 from EBAY.

Install Openocd

In windows from here http://gnutoolchains.com/arm-eabi/openocd/

## If flashing fro the first time, you will need to unlock your device

run go to the bin folder, and run 

openocd -f interface/stlink-v2.cfg -f target/stm32f1x.cfg

You need a telnet client, I use [Kitty Portable](https://portableapps.com/apps/internet/kitty-portable)

telnet to 127.0.0.1:4444 (as a raw TCP connection?)

type:

```
reset halt
stm32f1x unlock 0
```

Untested by me, but the following should work to unlock without telnet?:

`openocd -f interface/stlink-v2.cfg -f target/stm32f1x.cfg -c "reset" -c "stm32f1x unlock 0"`

## Once the device is unlocked

*Caveat: i wrote this some time ago, and have NO IDEA where the 'flash' program came from?*

*I KNOW that openOCD works.... no guarantees on the flash lines.*

*also consult [Building-and-flashing](Building-and-flashing)*

if you have a .hex file (like the repo contains):

`flash write_image erase C:\\DataNoBackup\\hoverboard\\src\\build\\hover.hex 0 ihex`

if you have a .bin file (like made by platformio):

`flash write_image firmware.bin 0`

programming the hover.hex from the original repo certainly operates the wheels, and generates debug output!

for platformio generated bin:

`flash write_image erase C:\\DataNoBackup\\hoverboard\\.pioenvs\\genericSTM32F103RC\\firmware.bin 0x08000000 bin`

both should work.......

(check diagnostic output if configured)


On linux (raspberian/debian), installing openocd from apt, I use:

`openocd -f /usr/share/openocd/scripts/interface/stlink-v2.cfg -f /usr/share/openocd/scripts/target/stm32f1x.cfg -c "program firmware.bin 0x08000000" -c "halt 100" -c "reset"`

to flash.  

This should also work from windows openocd.

My RpiZero is powered from the hoverboard, so I have to hold the power button until the board is restarted, else it powers off mid flash!.  When this happens, not only do I have to wait for 5 minutes for the Pi to boot again, but because the MCU is not running, I have to hold the power button for the whole time, entering the flashing commands one handed :).

