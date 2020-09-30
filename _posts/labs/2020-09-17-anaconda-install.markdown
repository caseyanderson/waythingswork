---
layout: post
title:  "Anaconda"
date:   2020-09-17 07:00:00 -0700
week: "1"
number: "1"
categories: "labs"
---

### Installation
#### MacOS
1. Click [here](https://repo.anaconda.com/archive/Anaconda3-2020.07-MacOSX-x86_64.pkg) to download the latest version of `Anaconda Navigator` for `MacOS`
2. Once the download has finished run the installer

#### Windows 10
1. Click [here](https://repo.anaconda.com/archive/Anaconda3-2020.07-Windows-x86_64.exe) to download the latest version of `Anaconda Navigator` for `Windows 10`
2. Once the download has finished run the installer


### Getting to the Command Line
#### MacOS
1. Navigate to Finder > Applications > Utilities > Terminal
2. Run the `Terminal`, you should see something that looks like this:

![]({{site.url}}/assets/imgs/mac_os_anaconda_terminal.png)

#### Windows 10
1. Navigate to `Anaconda Powershell` (it should be in the `Start` menu)
2. Run the Anaconda Powershell

Note: who would like to take a screenshot of the Anaconda Powershell and send it to me? Thx!


### Command Prompt
#### MacOs
`$`

#### Windows 10
`>`

The command prompt, illustrated above per operating system, indicates to a user where they can enter commands (type things)


### Create A Conda Environment

In the Terminal (MacOS) or Anaconda Powershell Prompt (Windows 10):

1. `conda create -n making_intro python=3.8`
2. `conda activate making_intro`
3. `pip install beautifulsoup4`
4. `conda list` (confirms that `beautifulsoup4` has been installed)
5. `conda activate`
