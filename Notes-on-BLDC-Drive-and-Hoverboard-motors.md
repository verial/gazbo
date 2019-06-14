A place for notes about our motors and drive.

The hoverboard motors are 3 phase synchronous BLDC devices.

The three coils are 'Wye' connected (search BLDC in wikipedia).

# How the BLDC signals are driven in the firmware

## PWM

The firmware runs 'center aligned' PWM generating three pairs of square wave signals per wheel.
Each pair of signals is one which drives a FET connected to GND, and one which drives a FET connected to +Vbat.
The PWM is configured with a 'Dead Time' to prevent both FETs being active at the same time, which would result in smoke.

The PWM pulses occur at 16khz, determined by TIM1/TIM8 (slaved together).
This timer also triggers the reading of 10 ADC values (ADC1 and ADC2, 5 values each), the reading of which triggers a DMA transfer into ram.
When the DMA transfer finishes, it causes an interrupt routine, DMA1_Channel1_IRQHandler(), which occurs at the 16Khz frequency, and within which new PWM values are set.

## numbers
The PWM values are 16khz timer frequency are 0-2000.
In the firmware we use a 'drive' of -1000 - 1000, so pwml = 0 equates to a timer channel PWM value of 1000.
A timer PWM value of 1000 results in roughly equal 'up' and 'down' drive - driving each phase to ~15V.  (or thought of another way, equal low resistance current sink and source capability).
This is why when the motors are enabled with pwml=0, there is more drag on the wheels than when the motors are disabled - you turning the wheels generates a current in the coils, which is opposed by the low resistance drive.

## connection and currents
Wye connection means that our drive into a channel is not driving a single coil, but instead the combination of all the drive signals determines the current through the three real coils.

If we nominate the drive signals as u, v, w, and the coils as a, b, c, then the coil current in a static state with coil resistance R (assuming no dead time and that Vu, Vv, Vw can be directly equated to our PWM signals):

```
Ia = (Vu - Vv)/R + (Vu - Vw)/R = (2Vu - Vv - Vw)/R 
Ib = (Vv - Vw)/R + (Vv - Vu)/R = (2Vv - Vw - Vu)/R; 
Ic = (Vw - Vu)/R + (Vw - Vv)/R = (2Vw - Vu - Vv)/R;
```

* Dead Time

Dead time affects the currents by reducing the *amplitude* of the difference terms (e.g. (Vu - Vv)) by a fixed value.

* PWM and difference terms

Because of the way the PWM and Current works, with center aligned PWM you can simplify the thoughts down to looking at half the PWM waveform:

```
For u > v
u+          -------------¦-------------       
     -------             ¦             -------
u-   ------              ¦              ------
           --------------¦--------------      
           *             ¦             *      
v+                 ------¦------              
     --------------      ¦      --------------
v-   -------------       ¦       -------------
                  -------¦-------             
                  *      ¦      *             
u-v +       ------       ¦       ------       
    0------*      *------¦------*      *------
    -                    ¦                    


For v > u
u+                 ------¦------              
     --------------      ¦      --------------
u-   -------------       ¦       -------------
                  -------¦-------             
                  *      |      *             
v+          -------------¦-------------       
     -------             ¦             -------
v-   ------              ¦              ------
           --------------¦--------------      
           *             ¦             *      
u-v +                    ¦                    
    0------*      *------¦------*      *------
    -       ------       ¦       ------       
```
The PWM value for u and v are actually represented  by the falling edge of u- and v-.

The * represents dead time, when neither FET is active for this signal.

So from this, we can see that the resulting (u-v) signal is driven +v for (u-v-d) when u > v, and negative for (v-u-d) when v > u.

so the resulting current equation becomes:

Iuv = (u>v)? (u-v-d):(u-v+d)

or more accurately:

```
if (u-v-d > 0) Iuv = u-v-d;
if (u-v+d < 0) Iuv = u-v+d;
```

*This complicates things if dead time is to be taken into account.*

Our deadtime is configured to 32 counts at T ck_int, which I believe equates directly to 32 counts of u/v/w, so actually it's effect IS quite large (motors start turning at ~40, probably because below this Iuv is zero...).

## Towards a quieter drive

The ideal would be to drive sinusoidal currents in Ia, Ib, Ic.  To do this, we need to derive equations to equate u, v, w values to desired Ia, Ib, Ic values.

```
Iuv = Ivw = Iwu = 0
if (u-v-d > 0) Iuv = u-v-d;
if (u-v+d < 0) Iuv = u-v+d;
if (v-w-d > 0) Ivw = v-w-d;
if (v-w+d < 0) Ivw = v-w+d;
if (w-u-d > 0) Iwu = w-u-d;
if (w-u+d < 0) Iwu = w-u+d;

Ia = Iuv - Iwu 
Ib = Ivw - Iuv; 
Ic = Iwu - Ivw;
```




