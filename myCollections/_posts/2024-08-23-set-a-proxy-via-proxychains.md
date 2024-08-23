---
layout: post
title:  Set a application-level proxy via proxychains
author: Bruce Liu
#last update date
date:   2024-08-23 16:00:00 +0800
#first published date
published:    2024-08-23 16:00:00 +0800
categories: [post]
tags: [proxychains, proxy, linux]
description: 
header-image: 
permalink: /proxy-via-proxychains
---

This is a short guide to set up a proxy on a Linux system. 

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## Install [ProxyChains]

`sudo apt install proxychains`

`apk add proxychains-ng`	[alpine linux]

## Configure [ProxyChains]

Add the following content in the configuration file `/etc/proxychains.conf` or `/etc/proxychains/proxychains.conf`.

`http	<your server ip>	<port>` For example, `http	192.168.31.138	10811`

## Use / test [ProxyChains]

`proxychains curl ifconfig.me/ip`

<!--links-->
[ProxyChains]:https://proxychains.sourceforge.net
[alpine linux]: https://pkgs.alpinelinux.org/package

