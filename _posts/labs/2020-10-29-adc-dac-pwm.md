---
layout: post
title:  "ADC, DAC, & PWM"
date: 2020-10-29 06:00:00 -0630
week: 7
number: 2
categories: labs
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)
* 1x Breadboard
* 1x Potentiometer (or Voltage Divider Sensor)
* 1x LED (w/ 1x Resistor [220, 270, 330])


## Analog to Digital Conversion (ADC)

`Analog to Digital Conversion` (`ADC`) is the process of converting a varying `voltage` (`analog`) to a sequence of discrete `voltages` (`digital`). `MicroPython` provides a convenient interface for this via `ADC`, which can be used on any pin whose number is prepended with an `A` on the `ESP32` (pins `32` - `39`). In this class we will typically use `ADC` with `analog` sensor input so it's okay to associate this process with (`analog`) inputs generally (for now).

To create and store an instance of `ADC` on the pin labeled `A2`: `adc = ADC(Pin(34))`.

Take a moment to wire up a potentiometer, or other voltage divider sensor, to pin `34` on the `ESP32` and follow along:

*For Example*
1. Connect to the ESP32: `screen /dev/tty.SLAB_USBtoUART 115200`
2. import `ADC` and `Pin` from `machine`: `from machine import ADC, Pin`
3. create an instance of an `ADC` on pin `A2` (i.e. pin number `34`): `adc = ADC(Pin(34))`
4. set the attenuation (numerical range) for this `ADC` instance: `adc.atten(ADC.ATTN_11DB)`
5. read the voltage at pin `34`: `adc.read()`
6. repeat step 5.
7. repeat step 5. again
8. repeat step 5. one more time

* In step 4. we set the range of our `ADC` instance via `adc.atten()` (short for attenuate). Here `adc.atten(ADC.ATTN_11DB)` sets the input range to `0.0V` to `3.6V`
* In steps 6. - 8. we ran the same line of code three times and got three different values because the `voltage` is `analog` (varying). Some `analog` sensors produce `voltages` that are more varied than others.


## Digital to Analog Conversion (DAC) / Pulse Width Modulation (PWM)

![]({{site.url}}/assets/imgs/PWM_wikipedia.png)

Digital to Analog Conversion (DAC) is the opposite of `ADC`: a `DAC` converts a sequence of discrete `voltages` into a varying `voltage`. In order to approximate an analog voltage with a digital pin on the `ESP32` one typically uses `Pulse Width Modulation` (`PWM`). This is accomplished by toggling a digital pin on and off very quickly.

The image above is an example of `PWM` output. Note that it approximates an analog voltage but, if we look closely, we can still observe the discrete steps of the original digital signal.

### Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/blink_external_led.png)

In the following sequence we instantiate a `PWM` instance and associate it with an `ESP32` pin. Log in to your `ESP32` via `screen` and follow along:

*For Example*
1. import `Pin` and `PWM` from `machine`: `from machine import Pin, PWM`
2. store `PWM` pin number to the variable `pin`: `pin = Pin(27)`
3. create a `PWM` object and store it at `pwm27`: `pwm27 = PWM(pin)`

There are two parameters associated with `PWM`: `frequency` and `duty cycle`:
* the `frequency` controls the speed at which the pin is toggled `ON` and `OFF`
* the `duty cycle` is how long the pin is `HIGH` compared to the length of a single period (`LOW` plus `HIGH` time). Maximum `duty cycle` is when the pin is `HIGH` (`On`) all of the time, minimum is when it is `LOW` (`OFF`) all of the time.

Follow along to experiment with changing these settings:

*For Example*
1. set the `PWM` `frequency` to `1000`: `pwm27.freq(1000)`
2. set the `PWM` `duty cycle` to `200`: `pwm27.duty(512)` (i.e. 50% brightness)
3. change the `PWM` `duty cycle` to `0`: `pwm27.duty(0)` (i.e. off)
4. change the `PWM` `duty cycle` to `1023`: `pwm27.duty(1023)` (i.e. 100% brightness)
5. turn `PWM` on the pin off: `pwm27.deinit()`
6. Ctl-D to reboot

Alternately, one could declare and set values for a PWM pin all at once, which would like something like this: `pwm27 = PWM(Pin(27), freq=20000, duty=512)`


### Fading LEDs

Last week we discussed using `for` loops with Python's `range()` to count. Open Jupyter Notebook and run the following for a refresher:

*For Example*
```python
for i in range(5):
  print(i)
```

One can use a `for` loop with a `PWM` pin to create the effect that an `LED` is fading in or fading out by incrementally changing the `duty cycle`, or by counting until one reaches the desired LED brightness. Follow along on your `ESP32`:

*For Example*
```python
'''
fade_in.py
'''

from time import sleep
from machine import Pin, PWM

pwm = PWM(Pin(27), freq = 20000, duty = 0)

for i in range(1024):
    print(i)
    pwm.duty(i)
    sleep(0.01)

print("100%")

pwm.deinit()
```

So the counter, or iterator (`i`), is used to set `pwm.duty()`, resulting in an incrementally brighter `LED`.

*For Example*
```python
'''
fade_out.py
'''

from time import sleep
from machine import Pin, PWM

pwm = PWM(Pin(27), freq = 20000, duty = 1023)

for i in range(1023, -1, -1):
    print(i)
    pwm.duty(i)
    sleep(0.01)

print("OFF!")

pwm.deinit()
```

The code above is virtually identical to `fade_in.py`, however here the `for` loop starts at `1023` (100% brightness) and counts down to `0` (`Off`), and stopping at `-1`, resulting in a incrementally dimmer `LED`.


### Breathing LEDs

If one puts the for loop from `fade_in.py` **and** the for loop from `fade_out.py` into a `while` loop one can create a kind of breathing effect. Follow along on your `ESP32`:

*For Example*
```python
'''
    breathe.py
'''

from time import sleep
from machine import Pin, PWM

pwm = PWM(Pin(27))
pwm.freq(60)

while True:
    for i in range(1024):
        if i == 0:
            print("inhale")
        pwm.duty(i)
        sleep(0.001)
    for i in range(1023, -1, -1):
        if i == 1023:
            print("exhale")
        pwm.duty(i)
        sleep(0.001)
```
