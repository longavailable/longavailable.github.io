---
layout: post
title:  Free ways to access home assistant remotely
author: Bruce Liu
#last update date
date:   2022-06-15 09:50:00 +0800
#first published date
published: 2022-06-15 09:50:00 +0800
categories: [post]
tags: [home assistant, cpolar, cloudflare, intranet penetration]
description: 
header-image: 
permalink: /remote-ha-access/
---
[Home Assistant] alives the devices at our home. That's really cool! Here are a few free ways to access [Home Assistant] remotely.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# [cpolar]

## Installation

China source:

```sh
curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash
```

Other:

```sh
curl -sL https://git.io/cpolar | sudo bash
```

## Registration and configuration

- Register from my referral link <https://i.cpolar.com/m/4OZZ>,

- Copy your authtoken <https://dashboard.cpolar.com/auth>,

- Config your local cpolar by

	```sh
cpolar authtoken <place your token here>
	```

## Intranet penetration

- Start a session with [screen]

	```sh
screen -R ha
	```

- Build a cpolar channel with the local port (defaut 8123) for [home assistant]

	```sh
cpolar tcp 8123
	```

- That's enough!

## Remote access

- Get your public link (refered as `cpolar link` below) from:

	- Live screen/terminal for cpolar channel
	
		![cpolar channel](/assets/pics/ha-build-cpolar-channel-linux.png)
		
	- cpolar online channel status <https://dashboard.cpolar.com/status>

- Visit it starting with a `http://` anywhere.

## Advance! Your domain!

If you have a domain, such <longlovemyu.com>, you can forward a custom link to the cpolar link.

I cloudflared <longlovemyu.com>. So I did a forwarding test by using [cloudflare] rules.

![cpolar channel](/assets/pics/ha-forward-cpolar-link.png)

Enjoy it!


<!--links-->
[cpolar]: https://i.cpolar.com/m/4OZZ
[screen]: https://www.gnu.org/software/screen
[home assistant]: https://www.home-assistant.io/
[Home Assistant]: https://www.home-assistant.io/
[cloudflare]: https://www.cloudflare.com/
