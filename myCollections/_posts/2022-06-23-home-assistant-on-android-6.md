---
layout: post
title:  
author: Bruce Liu
#last update date
date:   2022-06-23 11:50:00 +0800
#first published date
published: 2022-06-23 11:50:00 +0800
categories: [post]
tags: [home assistant, android, Redmi Pro, Termux, Ubuntu]
description: 
header-image: 
permalink: /ha-on-redmipro/
---
Recently, I am trying to make devices alive in my room. And I found Home Assistant the cool bean. It's easily to depoly it on a desktop of Windows or Linux. While, I prefer to choose a low-cost server without extra expense. So, I dug out my old android phone (Redmi Pro) from my treasure chest. Let's see what I can do.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# A glimpse of [Redmi Pro]

- Released in August 2016,

- OS: Android 6.0, MIUI 10 9.3.28,

- Rooted.

# Terminal emulator

- [Termux]
	
	- .. from [Google Play]: Absolutely NOT! 
	
	- .. from [F-Droid]: No. The latest version on [F-Droid] was released in January 2022. It is for only android >= 7.
	
	- .. from `Artifacts` section of [Github Build] action workflows (A Github account logged in is necessary). Download `termux-app_v***+***-apt-android-5-github-debug_universal` and install it on [Redmi Pro].
	
- [Linux Deploy]

	It is a potential solution. I tried a few times, but failed to deploy a linux on my [Redmi Pro].
	
So [Termux] for android 5 was which I chose finally.
	
# [Home Assistant][1] [Operating System], [Container], [Supervised], and [Core]

There is a [table](https://www.home-assistant.io/installation/#compare-installation-methods) to compare these installation methods.<https://www.home-assistant.io/installation/#compare-installation-methods>

Normally, I'd like a most powerful [Home assistant][1]. So I tried [Operating System], [Supervised], [Container], and [Core], sequentially.

- [Operating System] - Not working!
	
	Failed to install a virtual machine.
	
- [Supervised] - Not working!

	`apt`, `pkg`, and ... were permanenently locked against running as root.
	
	I can NOT install any package from my root access.
	
	I tried install the dependencies using current user. Failed to isntall `udisks2`, `libglib2.0-bin`, `network-manager`, and 	`dbus`.
	
- [Container] - Not working!

	Failed to install [docker-compose](https://docs.docker.com/compose).
	
- [Core] - Not working!

	Current user again (not root user).
	
	Python 3.9 or newer is suggested. <https://www.home-assistant.io/installation/linux#install-home-assistant-core>
	
	While, the latest python in the repos supported by [Termux] is 3.8 and there is no plan for support or package updates.<https://github.com/termux/termux-app/wiki/Termux-on-android-5-or-6>
	
	That's OK. I just ignored them and go on.
	
	Some denpendencies are Not supported. Ignore again.
	
	Finally, `pip install homeassistant`
	
	And failed at `ERROR: Failed building wheel for cryptography`. It need a rust `>=1.41`, while the latest rust is `1.38`.
	
	Failed again.

All were not working on [Termux] for android `5`.

# [PRoot]

- [proot-distro] is NOT supported on android 5/6.  💩

	Almost no way to proceed.

- [ubuntu-in-termux]

	Lucky. I've found a ready-to-use script to install Ubuntu from [Termux].

	It works like a charm.

	So I have a [Jellyfish] on my [Redmi Pro]. It will be easily to go on.

# [Home Assistant][1] [Core] on [ubuntu-in-termux]

- `su` user access,

- latest `python` (3.10),

- `python3-dev`, `python3-venv`, `python3-pip`, `libffi-dev`, `libssl-dev`, `libjpeg-dev`, `zlib1g-dev`, `autoconf`, `build-essential`, `libopenjp2-7`, `libtiff5`, `libturbojpeg0-dev`, and `tzdata`. All dependancies are supported. Perfect!

- `pip install homeassistant` worked as well.

- Go with your hass.

Note: Maybe a few bugs. I ignored them.

Enjoy [Home Assistant][1] on my [Redmi Pro]!

# Brainstorm

- Not root? Is it possible to work for [ubuntu-in-termux]?

- Refer to the script of [ubuntu-in-termux], is it to deply some other Linux distros?

No plan to test.


# Reference

- [Install Home Assistant (HASS) on Android (NO ROOT)](https://lucacesarano.medium.com/install-home-assistant-hass-on-android-no-root-fb65b2341126)

- [Home Assistant Core on Android Tablet](https://community.home-assistant.io/t/home-assistant-core-on-android-tablet)


<!--links-->
[Redmi Pro]: https://www.gsmarena.com/xiaomi_redmi_pro-8233.php
[Termux]: https://termux.com
[Google Play]: https://play.google.com
[F-Droid]: https://f-droid.org
[Github Build]: https://github.com/termux/termux-app/actions/workflows/debug_build.yml
[Linux Deploy]: https://github.com/meefik/linuxdeploy
[1]: https://www.home-assistant.io
[Operating System]: https://github.com/home-assistant/operating-system
[Container]: https://github.com/home-assistant/docker
[Supervised]: https://github.com/home-assistant/supervisor
[Core]: https://github.com/home-assistant/core
[PRoot]: https://wiki.termux.com/wiki/PRoot
[proot-distro]: https://github.com/termux/proot-distro
[ubuntu-in-termux]: https://github.com/MFDGaming/ubuntu-in-termux
[Jellyfish]: https://releases.ubuntu.com/22.04