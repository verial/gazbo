The analog inputs are probably the easiest to use when starting a hoverboard project. Just attach a voltage between 0V and 3.3V to the two analog inputs on the sensor wire (Only one has analog inputs, same wire which can also be used for USART2 or PPM)

Make sure to only apply a voltage between 0V and 3.3V! Simply putting a poti on the sensor wire (which carries 15V) will kill the micro controller. A voltage regulator is a good solution to get the 15V down to 3.3V.
Consider what will happen when the analog wire is damaged or disconnected. When left open, the analog input will float to random values, the hoverboard can start moving without control. Adding a Pulldown (or pull-middle) close to the inputs helps.

# Sample Configurations
## Joystick
A joystick has to potentiometers, in the resting position, both values are at a mid point (around 1,6V).

```
#define CONTROL_ADC               // use ADC as input. disable DEBUG_SERIAL_USART2!
#define ADC1_MIN         0        // min ADC1-value while poti at minimum-position (0 - 4095)
#define ADC1_ZERO     2047        // ADC1-value while poti at zero-position (0 - 4095)
#define ADC1_MAX      4095        // max ADC1-value while poti at maximum-position (0 - 4095)
#define ADC1_MULT_NEG 1000.0f     // Use 1000.0f to calibrate from MIN to MAX
#define ADC1_MULT_POS 1000.0f     // Use 1000.0f to calibrate from MIN to MAX
#define ADC2_MIN         0        // min ADC2-value while poti at minimum-position (0 - 4095)
#define ADC2_ZERO     2047        // ADC2-value while poti at zero-position (0 - 4095)
#define ADC2_MAX      4095        // max ADC2-value while poti at maximum-position (0 - 4095)
#define ADC2_MULT_NEG 1000.0f     // Use 1000.0f to calibrate from MIN to MAX
#define ADC2_MULT_POS 1000.0f     // Use 1000.0f to calibrate from MIN to MAX
#define ADC_OFF_START    0          // Start Value of Area at which other inputs can be active (0 - 4095) Applies to Speed ADC
#define ADC_OFF_END      0          // End Value of Area at which other inputs can be active (0 - 4095) Applies to Speed ADC
#define ADC_OFF_FILTER 1.0          // Additional low pass Filter applied only to ADC Off functionality. 1.0=No Filter, 0.1 lots of Filtering
#define ADC_SWITCH_CHANNELS 0       // define if ADC1 is used for Steer and ADC2 for Speed
#define ADC_REVERSE_STEER 0         // define if ADC1 is used for Steer and ADC2 for Speed
#define ADC_TANKMODE 0              // define if each input should control one wheel
```
