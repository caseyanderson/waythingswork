---
layout: post
title:  "Functions"
date: 2021-04-01 06:00:00 -0600
week: 11
number: 1
category: labs
---

A function is a re-usable block of instructions that performs an action. Python 3 has a handful of built-in functions, some of which you are already familiar with: `print()`, `len()`, `type()`, etc.. One doesn't need to know **how** each of these functions work, they just need to know what information each needs in order to perform an associated action.


## Function Definitions

One can write, or define, one's own function by prepending a name with `def` (short for definition)

*For Example*
```python
def hello():
    print("hello world!")
```

Above we define (`def`) a function named `hello()` and associate an action (`print("hello world")`) with it. Once a function has been defined it may be called, or used, as follows

*For Example*
```python
hello()
```

Which returns the message "hello world!".

Python knows what the function `hello()` does because of the function definition, and more specifically because of the indented lines of code following the colon in the function definition. Note that the indentation is equivalent to four spaces. Some people use tabs, others use spaces, hence this joke from Silicon Valley.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SsoOG6ZeyUI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Using Data

`Parameters` can be added to function definitions to allow data to be passed to a function when called.

*For Example*
```python
def happyBirthday(name):
    lines = []
    person = str(name)
    for i in range(4):
        if i == 2:
            msg = ' '.join(['Happy Birthday, dear', person])
            lines.append(msg)
        else:
            msg = 'Happy Birthday to you'
            lines.append(msg)
    return ' '.join(lines)
```

1. Execute the function definition in `jupyter notebook`
2. Call the function and pass it your name: `happyBirthday(YOURNAME)`

Some notes about the above:
* In order to properly `print` the full text of Happy Birthday a function call will need the person's name. Above we use a parameter named `name` to hold that data
* First we make an empty list called `lines`, which will soon hold the lines of the formatted song
* Next we make sure that the data passed to `happyBirthday()` is a `string`
* Then we use a `for` loop to iterate through lines of the song. Remember: Happy Birthday has four lines total. Three are identical (lines 1, 2, and 4), one is different (Line 3, when the celebrant's name is used). Our `for` loop needs to count to four, adding the same line to `lines` until the third line, hence the `if` statement at the top of the `for` loop.
* This `if` statement reads: `if i == 2` returns `True` format and write a different line for the song (with the person's name) and add it to `lines`, otherwise (`else`) write the same line (`Happy Birthday to you`) and add it to `lines`
* Finally our function produces, or `return`s, new data: the formatted Happy Birthday song.

In short one can think of parameters as inputs to a function and the data returned by a function as its output.
