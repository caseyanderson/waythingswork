---
layout: post
title:  "Counting Button Presses"
date: 2020-10-22 06:00:00 -0700
week: 6
number: 3
categories: labs
---

## Materials

* laptop
* internet access
* [Adafruit HUZZAH32](https://www.adafruit.com/product/3591)
* [USB cable - USB A to Micro-B - 3 foot long](https://www.adafruit.com/product/592) (or similar)
* 1x Breadboard
* 1x SPST button


## Hookup Pattern

![]({{site.url}}/assets/imgs/fritzing/button.png)


## button.py

### Code

```python
'''
button.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)

while True:
    if not button.value():
        print('Button pressed!')
    sleep_ms(20)
```

The example above is from Week 2 ([this](https://physcpu1.caseyanderson.com/2020/01/30/digitalIO.html) lab) and is, perhaps, the simplest way to detect a button press. Nonetheless, this example only detects whether a button is pressed or not currently.

In order to know how to improve upon the `button.py` example we can ask the following question: does `button.py` allow me to count the number of button presses? Take a moment to **run and use** `button.py` while asking yourself that question.

Another way to ask the same question while pressing the button: can I reliably press the button and get **only one** `Button pressed!` message?

![]({{site.url}}/assets/imgs/button_test_one_fail.png)

When one presses the button one invariably triggers more than one print statement (see the image above, I **swear** I barely touched the button).


## button_counter_basic.py

One way we could try to count button presses in `button.py` would be to `increment` a `variable` when our button is pressed. Send the following example to your `ESP32`.

### Code

```python
'''
button_counter_basic.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)

counter = 0

while True:
    if not button.value():
        counter+=1
        msg = ' '.join(['counter is', str(counter)])
        print(msg)
    sleep_ms(20)
```

Take a moment to **run and use** `button_counter_basic.py` while asking the following question: can I reliably press the button and only add 1 to `counter`? Try it!

![]({{site.url}}/assets/imgs/button_test_two_fail.png)

Again, no matter how hard I try I cannot help but send repeated triggers with this kind of structure.


## button_press_once.py

In the next example we use a more complex `if` structure to identify a button press: we check to see `if` the button is currently pressed **and** `if` the current value of the button is different than the previous value (`prev_val`). Send the following example to your `ESP32`.

### Code

```python
'''
button_press_once.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)
prev_val = button.value()

while True:
    if not button.value() and button.value() is not prev_val:
        print('Button pressed once!')
    prev_val = button.value()
    sleep_ms(20)
```

Take a moment to **run and use** `button_press_once.py` while asking the following question: can I reliably press the button and get only one Button pressed! message? Try it!

![]({{site.url}}/assets/imgs/button_test_three_win.png)

Even if I press and hold the button `button_press_once.py` only prints the message once and blocks repeated triggers. Hooray!


## button_press_counter.py

Now that we can reliably count a button press without repeat triggers we can rewrite `button_press_once.py` to count each button press. Send the following to your `ESP32`.

### Code

```python
'''
button_press_counter.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)
prev_val = button.value()
counter = 0

while True:
    if not button.value() and button.value() is not prev_val:
        counter+=1
        msg = ' '.join(['Button pressed', str(counter), 'times!'])
        print(msg)
    prev_val = button.value()
    sleep_ms(20)
```

Take a moment to **run and use** `button_press_counter.py` while asking the following, more interesting, question: can I reliably count four button presses? Try it!

![]({{site.url}}/assets/imgs/button_counter_working.png)


## button_press_counter_limit.py

```python
'''
button_press_counter_limit.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)
prev_val = button.value()
limit = 5
counter = 0

while True:
    if not button.value() and button.value() != prev_val:
        counter += 1
        msg = ' '.join(['Button pressed', str(counter), 'times!'])
        print(msg)
        if counter == limit:
            print('limit reached!')
#            counter = 0
            break
    prev_val = button.value()
    sleep_ms(20)
```

```python
'''
button_press_counter_cases_limit.py
'''

from machine import Pin
from time import sleep_ms

button = Pin(12, Pin.IN, Pin.PULL_UP)
prev_val = button.value()
limit = 5
counter = 0
action = 0

while True:
    if not button.value() and button.value() != prev_val:
        counter += 1
        if counter == limit:
            print('limit reached, resetting!')
            counter = 0
            action = 0
        else:
            action = counter
    if action == 1:
        print('interaction 1 is happening now!')
    elif action == 2:
        print('interaction 2 is happening now')
    elif action == 3:
        print('interaction 3 is happening now')
    elif action == 4:
        print('interaction 4 is happening now')
    prev_val = button.value()
    sleep_ms(20)
```
