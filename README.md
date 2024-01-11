# avr-Pulses

The Pulses module provides functions for starting and stopping a train of pulses at the desired frequency.

**WARNING: This library is not available for ESP32, as it uses the AVR timers.**

## Gettings started

### Prerequisites
1. The [Arduino IDE](http://www.arduino.cc) 1.8.0 or higher
2. The [Industrial Shields Arduino boards](http://blog.industrialshields.com/en/installing-industrial-shields-equipment-to-the-arduino-ide/) (optional, used in the examples)

### Installing
1. Download the [library](https://github.com/Industrial-Shields/avr-Pulses) from the GitHub as a "ZIP" file.
2. From the Arduino IDE, select the downloaded "ZIP" file in the menu "Sketch/Inlcude library/Add .ZIP library".
3. Now you can open any example from the "File/Examples/Pulses" menu.


## Usage

```c++
#include <Pulses.h>
```

The `startPulses(pin, frequency, precision)` function starts the train of pulses at the specified frequency and precision. The default frequency is 1kHz and the default precision is 3.

```c++
pinMode(3, OUTPUT);
startPulses(3, 2000, 3);
```

The `stopPulses(Pin)` function stops the train of pulses.

```c++
stopPulses(3);
```

On ARDBOX Analog it is possible to use this functions in outputs:

* TIMER0: Q0.1 and Q0.6
* TIMER1: Q0.2 and Q0.3
* TIMER3: Q0.5

On MDUINO-21, MDUINO-42 and MDUINO-58 it is possible to use this functions in outputs:

* TIMER0: Q0.5 and Q2.6
* TIMER1: Q2.5
* TIMER2: Q1.5 (Multiply the frequency x2)
* TIMER3: PIN2, PIN3 and Q0.6
* TIMER4: Q0.7, Q1.6 and Q1.7
* TIMER5: Q1.3, Q1.4 and Q2.0

**IMPORTANT**: It is not possible to have different frequencies between the same TIMER Pin’s. Some outputs share the same timer, so they work at the same frequency.

**CAUTION!!!** When the TIMER0 pins are used, all the time functions change their functionality as `delay()`, `millis()`,`micros()`,`delayMicroseconds()` and others.

Next it is showed recommended precision between different frequencies:

* Precision = 1: from 30Hz to 150Hz
* Precision = 2: from 150Hz to 500Hz
* Precision = 3: from 500Hz to 4kHz
* Precision = 4: from 4kHz to 32kHz
* Precision = 5: from 32kHz to 4MHz

To have a high precision on the desired frequency, it is recommended to use the closer precision to the values of the previous table.
