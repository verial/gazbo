Analysis of data send TO the sensor boards:

On a 23000 baud board:

data for 'calibrate':

1E0 000 000 060 000 000

'normal' data:
108 000 000 000 000 000


word 0: 'colour'
0x01 -- headlamp flash when IR foot detector closed
0x02 - orange
0x04 - green
0x08 - red
0x10 - suppress headlamps
0x06 - yellow

word 1 - unknown

word 2 - flashcount

word 3 - calibrate - 0x00 or 0x60

word 4 & 5 - unknown

