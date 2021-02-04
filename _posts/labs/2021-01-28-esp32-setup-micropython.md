---
layout: post
title:  "ESP32 Setup for Micropython"
date:   2021-01-28 06:00:00 -0600
week: 2
number: 1
categories: labs
---

## Materials
* laptop (MacOS or Windows 10)
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)


### Install USB to Serial driver

1. Go [here](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)
2. Scroll to find the appropriate Download link for your Operating System (**Download for Macintosh OSX** or **Download for Windows 10 Universal**) and click on **Download VCP** under the appropriate driver heading


## Download Micropython Firmware for ESP32

1. Go [here](https://micropython.org/download/#esp32)
2. Download and install the "Standard firmware"


## Erase Default ESP32 Software

### MacOS

1. Connect the ESP32 to your CPU (via USB)
2. Open a Terminal
3. Activate your `micropython` `conda` `environment`: `conda activate NAME`
4. Run the following command to identify your device: `ls /dev/tty*` (we are looking for a device that ends with `SLAB_USBtoUART`)
3. Erase the device: `esptool.py --chip esp32 -p /dev/tty.SLAB_USBtoUART erase_flash`


### Windows 10

1. Connect your `ESP32` to your PC
2. Open **Device Manager**
3. Scroll to **Ports** and click to expand
4. Find the line reading **Silicon Labs CP210x USB to UART Bridge**. At the end of that line you should see `COM` followed by a number (example: `COM3`). This identifies where your ESP32 is on your PC so write it down somewhere for use later.
6. `cd Downloads` (or wherever you downloaded the `micropython` `firmware`)
7. Erase the software that is already on the `ESP32`: `esptool --port COM3 erase_flash`


## Install Micropython Firmware on ESP32

### MacOS

1. `ls` to confirm that the `.bin` file is visible where you are in the command line, if not navigate to wherever you downloaded it
2. Write the MicroPython software to the device: `esptool.py --chip esp32 -p /dev/tty.SLAB_USBtoUART write_flash -z 0x1000 nameOfMicroPythonVersion.bin`


### Windows 10

1. `ls` to confirm that the `.bin` file is visible where you are in the command line, if not navigate to wherever you downloaded it
2. Drivers in windows are a little wonky (sorry), so one of the following steps should write the `.bin` file to the ESP32. Start with the first one and, if you get errors, try the second one:
    * v1: `esptool --port COM3 --baud 460800 write_flash --flash_size=detect 0 esp32-XXXXXXXX-vX.X.X.bin`
    * v2: `esptool --port COM3 write_flash 0x1000 esp32-XXXXXXXX-vX.X.X.bin`
3. When `esptool` is done activate the default `conda` environment to shut it down: `conda activate`
4. Quit the **Anaconda Powershell Prompt**


## Connect to ESP32 REPL (via USB)

`REPL` stands for `Return Execute Print Loop`. It is similar to the `Command Prompt` in a `Command Line Interface`

### MacOS

1. Open a `Terminal` and run the following to connect to your `ESP32`: `screen /dev/tty.SLAB_USBtoUART 115200`. If you see `>>>`, your command prompt, you have successfully connected to the device
2. Print `hello world` from the `ESP32`: `print("hello world!")`

### Windows 10

`Putty` is an `ssh` and `serial` connection client for Windows

1. Go to the Putty download site [here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. Find the header **MSI (‘Windows Installer’)**, underneath it you should see a link to download putty 64-bit (`putty-64bit-0.71-installer.msi` as of this writing).
3. Install Putty
4. Go to the Start menu, locate and launch Putty
5. Set Putty to a serial connection and then enter the following information:
    * `Serial Port`: `COM3` (note: see **Device Manager** to confirm the port number for your ESP32)
    * `Baud Rate`: 115200
6. Click Open. You will probably see a bunch of startup text and then the micropython command prompt: `>>>`
7. Print `hello world!` with the `micropython` `REPL`: `print("hello world!")`


## Disconnect from ESP32 REPL (via USB)

### MacOS

1. Open a Terminal and run the following key-commands to disconnect from the ESP32 and exit `screen`: Ctrl-A Ctrl-\
2. Type `y` to confirm quit


### Windows 10

1. Close `Putty` to shut down the connection to the `ESP32`
