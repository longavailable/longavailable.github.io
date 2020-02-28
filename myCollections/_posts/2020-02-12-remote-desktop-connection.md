---
layout: post
title:  Remote desktop connection
author: Bruce Liu
# last update date
date:   2020-02-12 22:04:00 +0100
# first published date
published: 2020-02-12 22:04:00 +0100
categories: [post]
tags: [teamviewer, remote desktop connection, windows os]
header-image: 
permalink: /remote_connection/
---
How to connect another desktop remotely?
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# The easiest way
In my experience, the easiest way is to use a third-party tool. [TeamViewer](https://www.teamviewer.com/) can work from Windows, Mac, Linux, Android, iOS, etc. <br>

# Windows built-in Remote Desktop Connection

## Connect a desktop in LAN (local area network)

1. Enable Remote Desktop Connection on the host computer (which you want to connect or access remotely).
1. Launch Remote Desktop Connection utility on the client computer.
1. Connect to the host computer. If in LAN, enter the computer name.

## Connect a desktop in WAN (wide area network)

1. Enable Remote Desktop Connection on the host computer (which you want to connect or access remotely).
1. Forward TCP port [3389](https://www.speedguide.net/port.php?port=3389) to IP address of the host computer in router.
1. Launch Remote Desktop Connection utility on the client computer.
1. Connect to the host computer. Enter the public IP followed with the port number. 

Notice: Microsoft has a Remote Desktop app to support accessing a desktop from Android and iOS.

<br>
# Reference:
- [Setup a Remote Desktop Connection for LAN/WAN Access](https://learntomato.flashrouters.com/setup-remote-desktop-connection-lan-wan-access/)
- [How To Allow Remote Desktop Connections From Outside Your Home Or Office Network](https://www.linkedin.com/pulse/video-how-allow-remote-desktop-connections-from-outside-jerry-boutot)


