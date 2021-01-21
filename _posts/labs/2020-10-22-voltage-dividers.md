---
layout: post
title:  "Voltage Dividers"
date: 2020-10-22 06:00:00 -0600
week: 6
number: 1
categories: labs
published: false
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)
* 1x Breadboard
* 1x LED (w/ Resistor [220, 270, 330 or similar])
* 1x Potentiometer

A voltage divider is a circuit that produces an output that is smaller than its input (where the output is voltage or current).

![]({{site.url}}/assets/imgs/voltage_divider.png)

The above schematic represents the most basic way to use two resistors (labeled as `Z1` and `Z2`) to take some voltage (`Vin`) and output a fraction of it (`Vout`). The amount of `Vin` that is output at `Vout` depends on the values of the two resistors. This is the basic wiring pattern for almost any analog sensor, btw.

If you need to calculate the value of `R1` and `R2` (fyi: in this case, I am using `Z` and `R` interchangeably, but `Z` refers to impedance and `R` refers to resistance) such that you can get a specific `Vout`, here is the formula:

![]({{site.url}}/assets/imgs/voltage_divider_formula2.jpg)

## Voltage Dividers = Sensors (Sometimes!)

### Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/ldr_voltage_divider.png)

1. Connect LDR Pin1 (`Z1` in Voltage Divider schematic above) to ESP32 `3V`
2. Connect LDR Pin2 to ESP32 `34`
3. Connect Resistor Pin2 (`Z2` in Voltage Divider schematic above) to ESP32 `GND`

There are a collection of voltage divider-based sensors that can be used interchangeably, from a hardware and software standpoint, for wildly different interactions. To name only a few:

* Potentiometer/knob: [1-turn](https://www.digikey.com/product-detail/en/3852C-282-103AL/3852C-282-103AL-ND/1088605) or [Continuous Turn](https://www.digikey.com/product-detail/en/6639S-1-103/6639S-1-103-ND/274005)
* [Light-dependent resistor](https://www.sparkfun.com/products/9088)
* [Force sensor](https://www.sparkfun.com/products/9375)
* [Flex Sensor](https://www.sparkfun.com/products/10264)
