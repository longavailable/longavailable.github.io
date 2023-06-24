---
layout: post
title:  Update home assistant core and os 
author: Bruce Liu
#last update date
date:   2023-06-24 13:20:00 +0800
#first published date
published:   2023-06-24 13:20:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu]
description: 
header-image: 
permalink: /ha-os-update
---

Recently I installed homeassistant os VM on my Ubuntu. When I tried to update the latest core and os, it return `'HomeAssistantCore.update' blocked from execution, no host internet connection` and `'OSManager.update' blocked from execution, no supervisor internet connection`. I posted the solutions in this post.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->


## Errors when I update my [Home Assistant][1] [Operating System]

- 'HomeAssistantCore.update' blocked from execution, no host internet connection

- 'OSManager.update' blocked from execution, no supervisor internet connection

**Comments:** They may be caused by `bridge` internet connection.

Check the internet infomation from terminal:

`virsh console hass`

`root`

`ha network info`

It will show that `host_internet: false` and `supervisor_internet: false`. That's the point.

## Solutions

`virsh console hass`

`root`

`ha jobs options --ignore-conditions internet_host`

`ha jobs options --ignore-conditions internet_system`

`ha core update`

`ha os update`

`ha jobs reset`

## References

- [Supervisor no internet?](https://community.home-assistant.io/t/supervisor-no-internet/305929)

- [Error updating Home Assistant Core ‘HomeAssistantCore.update’ blocked from execution, no host internet connection](https://community.home-assistant.io/t/error-updating-home-assistant-core-homeassistantcore-update-blocked-from-execution-no-host-internet-connection/453293/16)

- [Ignored job conditions](https://www.home-assistant.io/more-info/unsupported/job_conditions)

<!--links-->
[1]: https://www.home-assistant.io
[Operating System]: https://github.com/home-assistant/operating-system
