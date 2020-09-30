---
layout: post
title:  "Adafruit HUZZAH32 Pre-flight"
date:   2020-09-24 06:00:00 -0630
week: 2
number: 3
categories: labs
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)


## Install USB to Serial driver

1. Go [here](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)
2. Scroll down to **Download for Macintosh OSX**, click on **Download VCP (832 KB)** to download
3. Restart CPU


## Install software for ESP32

1. Go [here](https://micropython.org/download/#esp32)
2. Download and install the "Standard firmware"


## Setup ESP32

1. Connect the ESP32 to your CPU (via USB)
2. Open a Terminal and run the following command to identify your device: `ls /dev/tty*` (we are looking for a device that ends with `SLAB_USBtoUART`)
3. Erase the device: `esptool.py --chip esp32 -p /dev/tty.SLAB_USBtoUART erase_flash`
4. Navigate to `Downloads`: `cd Downloads`
5. Write the MicroPython software to the device: `esptool.py --chip esp32 -p /dev/tty.SLAB_USBtoUART write_flash -z 0x1000 nameOfMicroPythonVersion.bin`
6. Power cycle the ESP32


## Connect to ESP32 (via USB)

1. Open a Terminal and run the following to connect to your ESP32: `screen /dev/tty.SLAB_USBtoUART 115200`. If you see `>>>`, your command prompt, you have successfully connected to the device
2. Print "hello world" from the ESP32: `print("hello world!")`


## Disconnect from ESP32 (via USB)

1. Open a Terminal and run the following key-commands to disconnect from the ESP32 and exit `screen`: Ctrl-A Ctrl-\
2. Type `y` to confirm quit
