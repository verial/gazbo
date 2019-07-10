# PowerOn problems:
## Unwanted powerOn and bleep at poweroff
Measure resistances between legs of TIP127. 
![](https://user-images.githubusercontent.com/10248772/60805888-c3d6d400-a181-11e9-95f8-35e1e0e16a9b.png)
If the resistances is below nominal values (they could be different up to 100 ohms) :
<a href="https://drive.google.com/uc?export=view&id=1bfl2lfsM5YBt4qTxe_IL2oUwzCCVv14w"><img src="https://drive.google.com/uc?export=view&id=1bfl2lfsM5YBt4qTxe_IL2oUwzCCVv14w" style="width: 500px; max-width: 50%; height: auto" title="Click for the larger version." /></a>

 or there is short between other legs, you need to replace TIP127.

Problem could be related with [Issue #51](https://github.com/bipropellant/bipropellant-hoverboard-firmware/issues/51#issue-461023728). For me it started happening when board started to measure really high temperatures(140C) and powered off.
# Motor problems
## Motor has no torque
There could be a couple of problems related to this issue.
1. Broken/badly soldered phase wire. Especially if you are using self made extensions or replaced connectors.
2. Burned/damaged motor coils. (There is a possibility but very low, as no one has encountered this issue yet)
3. Burned mosfets. Check with diode mode.
4. Bad code.