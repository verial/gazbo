# btsimonh
So, I picked up a defective hoverboard cheap off ebay; turned out it was the two separate controller type, one of which I promptly destroyed.  Replace the electronics with an ebay purchased single motherboard type...

My kids did not want me to destroy it, and no OSS firmware out there reproduced hoverboard functionality, so this repo came into being.

My hoverboard:

![](https://user-images.githubusercontent.com/3137332/56945320-b9afae00-6b1e-11e9-8610-7d587d70132d.jpg)

This now contains a RPiZeroW running Node-Red for control:

![](https://user-images.githubusercontent.com/3137332/59148928-b73a5100-8a06-11e9-8857-18d6996b7511.png)

It boots generally to Hoverboard mode (flash config for default boot mode).  If NOT in hoverboard mode, a double tap on the foot sensor will enable it.

For the moment, it does not serve any other specific purpose apart from as a dev platform for this repo.  Plans could include robot vacuum cleaner (looking for a 36v real vacuum - we have dogs that drop a lot of hair so 'standard' cheap robot vacuum cleaners are a waste of time), or a robot lawn mower (looking for a 36v mower!).

I've now drilled holes for attaching something to the board.  I chose to hijack an attachment hole for the upper plastic:

![](https://user-images.githubusercontent.com/3137332/59148951-19935180-8a07-11e9-994f-b2eadaaa8e66.png)

Removed the screw, and drilled it out to 6mm, all the way through the upper plastic:

![](https://user-images.githubusercontent.com/3137332/59148965-48a9c300-8a07-11e9-8fef-45722f7ef796.png)

Behind this hole will be a 3D printed part to retain an M6 nut, so that anything can be bolted to (and unbolted from) the top of the hoverboard.

![](https://user-images.githubusercontent.com/3137332/59149010-d84f7180-8a07-11e9-80d6-f17b93fa441e.png)


Technical: Because the sensor boards occupy USART2 and USART3, I use software serial on pins B2 and C9 at 9600 for machine control, using a USB to Serial adaptor from the RPiZeroW.  There is also an internally mounted USB hub and STLINK for firmware updating.  So my normal dev operational procedure is - 

* boot the hoverboard with the power button, wait for the RPiZeroW to boot to WLAN.
* SSH to RPiZero
* login to NodeRed remotely.
* Drop my new firmware (.pioenvs\genericSTM32F103RC\firmware.bin) through WinSCP onto the RPIZero.
* flash using a script running OpenOCD.
* if I want direct terminal to the Hoverboard, disable the NR flow, and use 'screen' to connect to the USB serial.


