---
layout: post
title:  "Button Output Select"
date: 2021-04-08 06:00:00 -0600
week: 12
number: 1
category: labs
---

Let's revisit our homework assignment from last week and replace the prin statements with the code described the prin statement together.

```
from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)
prev_val = button.value()
counter = 0
limit = 5
action = 0

while True:
    # button counter
    if not button.value() and button.value() is not prev_val:
        counter+=1
        msg = ' '.join(['Button pressed', str(counter), 'times!'])
        print(msg)
        if counter == limit:
            print('limit reached!')
            counter = 0
        else:
            action = counter
    # output selector
    if action == 1:
        print('an led turns on')
    elif action == 2:
        print('a motor spins')
    elif action == 3:
        print('an analog sensor value is read')
    elif action == 4:
        print('another led fades in or out')
    prev_val = button.value()
    sleep_ms(20)
```
