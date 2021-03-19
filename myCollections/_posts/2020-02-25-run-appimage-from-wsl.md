---
layout: post
title:  How to run an AppImage on WSL
author: Bruce Liu
# last update date
date:   2021-03-19 13:10:00 +0800
# first published date
published: 2020-02-25 15:30:00 +0100
categories: [post]
tags: [WSL, linux, appimage, Xming, VcXsrv]
description: 
header-image: 
permalink: /appimage_wsl/
---
Generally, an AppImage will work well on Linux. So how about a Windows Subsystem for Linux (WSL)? Not sure. Here is a way to solve my error.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->
Here was my error:

```
fuse: device not found, try 'modprobe fuse' first
Cannot mount AppImage, please check your FUSE setup.
```

I solved it as follows:

## Step1: install Linux GUI Apps on Windows.

- [Xming X Server for Windows](https://sourceforge.net/projects/xming/)
- [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/)

## Step2: install GTK graphical user interface library (libgtk2.0-0 or libgtk-3-0) in wsl

`sudo apt-get install libgtk2.0-0`

`sudo apt-get install libgtk-3-0`

`libgtk2.0-0` is an old version, and `libgtk-3-0` is the new version. While both works in the new release of ubuntu. More about [GTK GUI library](https://packages.ubuntu.com/search?keywords=libgtk&searchon=names&suite=eoan§ion=all).

## Step3: set the default display in wsl.

`export DISPLAY=:0`

Default display number is 0. You can change it in Xlaunch.

Of course, you can add it to your `.bashrc` or `.zshrc` file. Add followings to it.

`export DISPLAY=":0"`

## Step4: navigate to your AppImage folder. Dinamica is my case.

`cd  /mnt/d/dinamicaEGO/v5`

## Step5: set access mode of AppImage file

`chmod a+x Dinamica.AppImage`

`a`  -- all users

`x`  -- permission to execute the file

More about [chmod](https://www.geeksforgeeks.org/chmod-command-linux/).

## Step6: extract AppImage.

`./Dinamica.AppImage --appimage-extract`

Due to windows not support FUSE, AppImage have to be extracted and it will generate a folder named 'squashfs-root'.

## Step7: Run it

`./squashfs-root/AppRun`

<br>
**Although it works finally, I don't think it is the way.**

# Reference:

- [Run AppImage on Windows](https://discourse.appimage.org/t/run-appimage-on-windows/177)
- [How to run an AppImage using the Terminal](https://docs.appimage.org/introduction/quickstart.html#using-the-terminal)
- [Running GUI Linux applications in WSL 2](https://ramonh.dev/2020/09/30/wsl2-gui-apps/)
- [Running WSL GUI Apps on Windows 10](https://techcommunity.microsoft.com/t5/windows-dev-appconsult/running-wsl-gui-apps-on-windows-10/ba-p/1493242)
