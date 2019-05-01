On RPI3, the native UART is used to control Bluetooth Module.

You have 3 choices (don't forget to reboot your Raspberry Pi after):

## Option 1: disable Bluetooth module (recommended if you don't use it)
1. Edit **/boot/config.txt** and add:
```
dtoverlay = pi3-disable-bt
```
2. Edit **cmdline.txt** and remove (if it's still here):
```
console=serial0,115200
```

## Option 2: Use both Bluetooth with high speed and UART
### CAUTION: If you choose a high speed (500MHz), this method can make your processor heat a lot! Don't forget to add a fan and a heatsink!
With this method, the processor clock will be fixed to a slow speed (250MHz) or to a high speed (500MHz?):

Edit **/boot/config.txt** and add:
```
enable_uart = 1
```
This will affect processor performance because it controls the speed of the L2 cache, and there will also be a reduction in analog audio quality.
If you opt for the high clock speed (it will really require a fan and a heatsink), to keep the processor performance and audio quality, also add:
```
force_turbo = 1
```
in **/boot/config.txt**

## Option 3: Use both Bluetooth with slow speed and UART
1. Edit **/boot/config.txt** and add:
```
dtoverlay = pi3-miniuart-bt
```
2. Edit **/boot/config.txt** and add:
```
core_freq = 250
```
This will affect the performance of the processor. If you prefer to keep higher performance do not add the line `core_freq = 250` but rather the line `force_turbo = 1` **but it requires to use a fan and a heatsink**.

***
Thanks to Framboise314 for they [great article](https://www.framboise314.fr/le-port-serie-du-raspberry-pi-3-pas-simple/) describing theses methods!