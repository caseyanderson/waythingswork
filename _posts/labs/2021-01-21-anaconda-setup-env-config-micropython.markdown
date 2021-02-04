---
layout: post
title:  "Anaconda Setup & Environment Config for ESP32"
date:   2021-01-21 07:00:00 -0700
week: "1"
number: "1"
categories: "labs"
---

## Materials
* laptop (MacOS or Windows 10)
* internet access


### Installation
1. Go [ here ](https://www.anaconda.com/products/individual) to download the `Python 3.8 64-Bit Graphical Installer` for your operating system
2. Once the download has finished run the installer


### Environment Setup
1. Run `Anaconda Navigator`
2. Click `Environments`
3. Click `Create`
4. Name your `Environment`: `physcpu`
5. Make sure that `Python 3.8` is selected in `Packages`
6. Click `Create`
7. Click on the arrow and select `Open Terminal`
8. Install `esptool` to our `Environment`: `pip install esptool`
6. Install `ampy` to our `Environment`: `pip install adafruit-ampy`
7. Type `exit` and hit Enter to close the `Terminal`


### Application Setup
#### Windows 10
1. Click `Home`
2. Make sure `Applications on` is set to `physcpu`
3. Locate `Powershell Prompt`, click `Install`
4. Locate `Jupyter Notebook`, click `Install`


#### MacOS
1. Click `Home`
2. Make sure `Applications on` is set to `physcpu`
3. Locate `Jupyter Notebook`, click `Install`


### Starting your Development Environment
#### Windows 10
1. Run `Anaconda Navigator`
2. Click `Home`
3. Make sure `Applications on` is set to `physcpu`
4. Launch `Jupyter Notebook`
5. Launch `Powershell Prompt`


#### MacOS
1. Run `Anaconda Navigator`
2. Click `Home`
3. Make sure `Applications on` is set to `physcpu`
4. Launch `Jupyter Notebook`
5. In Finder navigate to `Terminal`, launch it
6. Activate the `physcpu` `Environment` in the `Terminal`: `conda activate physcpu`


