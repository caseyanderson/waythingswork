---
layout: post
title:  "Analog Input"
date: 2020-10-08 06:00:00 -0630
week: 4
number: 4
categories: labs
published: false
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)
* 1x Breadboard
* 1x Potentiometer
* 1x LED (w/ 1x Resistor [220, 270, 330])

## analog_read.py

```python
# analog read

from machine import ADC, Pin
from time import sleep_ms

adc = ADC(Pin(34))
adc.atten(ADC.ATTN_11DB)

while True:
  print(adc.read())
  sleep_ms(20)
```

1. Open a Terminal, run Jupyter Notebook: `jupyter notebook`
2. Click `New`, Select `Text File`
3. Click on `Untitled.txt` and change it to `analog_read.py`
4. Copy and paste the code above into `analog_read.py`, save the file

### Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/analog_read.png)

1. Connect Pot1 to ESP32 `GND`
2. Connect Pot2 to ESP32 `34`
3. Connect Pot3 to ESP32 `3V`

