---
layout: post
title:  "Connect to the ESP32 Command Prompt"
date:   2021-01-01 06:00:00 -0700
week: ""
number: ""
categories: recipes
permalink: /:title.html
---

### MacOS

1. plug your ESP32 into your Laptop's USB port
2. (in the Finder) Navigate to Applications > Utilities
3. find the Terminal, open it
4. in the Terminal type the following: `screen /dev/tty.`
5. hit the TAB key, one of the results should be `tty.SLAB_USBtoUART`
7. add an `SL` to the command above so it reads: `screen /dev/tty.SL`
8. hit the TAB key again, autocomplete should give you: `screen /dev/tty.SLAB_USBtoUART`
9. add the `BAUD` rate (`115200`) to the end of the command above: `screen /dev/tty.SLAB_USBtoUART 115200`
10. hit ENTER once to execute the command
11. hit ENTER a second time at the gray screen, which should bring up the `command prompt`: `>>>`

### Windows 10

1. plug your `ESP32` into your Laptop's USB port
2. check the list of identified `COM` ports in the Windows Device Manager
  * we need the `COM` number for the device labeled `Silicon Labs CP210x USB to UART Bridge (COM3)`, write this number down for use later
3. (in the Start Menu) Navigate to Putty
4. (in Putty) select Serial and set:
  * `Serial line to connect to`: `COM3` (use the `COM` number from step 2)
  * `Speed (baud)`: to `115200`
5. click `Open`
6. hit ENTER once to bring up the `command prompt`: `>>>`
