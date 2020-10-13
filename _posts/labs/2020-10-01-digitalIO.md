---
layout: post
title:  "Digital Input / Digital Output"
date: 2020-10-01 06:00:00 -0700
week: 3
number: 3
categories: labs
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)
* 1x Breadboard
* 1x Resistor (220, 270, or 330 Ohms)
* 1x LED
* 1x SPST button


## Digital Input

### button.py

```python
'''
button.py
'''

import machine
import time

button = machine.Pin(12, machine.Pin.IN, machine.Pin.PULL_UP)

while True:
    if not button.value():
        print('Button pressed!')
    time.sleep_ms(20)

```

### Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/button.png)

1. Connect 1 button pin to ESP32 Pin 12
2. Connect another button pin to ESP32 GND


## Digital Input / Digital Output

### button_led.py

```python
'''
button_led.py
'''

import machine
import time

button = machine.Pin(12, machine.Pin.IN, machine.Pin.PULL_UP)
led = machine.Pin(27, machine.Pin.OUT)

while True:
    if not button.value():
        led.value(1)
    else:
        led.value(0)
    time.sleep_ms(20)
```

### Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/button_led.png)

1. Connect 1 button pin to ESP32 Pin `12`
2. Connect ESP32 `GND` to a blue bus on the side of your breadboard
3. Connect another button pin to the same blue bus on the side of your breadboard
4. From pin `27`, connect the following in series: a Resistor to an LED to GND (blue bus)

