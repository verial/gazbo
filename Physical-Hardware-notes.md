# Powering a controller

The battery is 36-41v.  This is generally too high to be inside the specification of easily available DC-DC convertors.  I (btsimonh) power my RPiZero (~500ma?) from a DC-DC driven from the 12V which normally goes to a sensor board.  The 12V available on the Hoverboard main board is probably quite capable, being normally used for LED headlamps (but don't blame me if it blows because you pull too much!).

The GND connection to the controller is important - e.g. if you take GND direct from the battery, you may find that under load, you will see a lot of motor noise when comparing this GND with the hoverboard signal GND.  This noise directly translates to noise on the serial lines.....  So ensure that the GND connection you use is from the Hoverboard signal GND.

