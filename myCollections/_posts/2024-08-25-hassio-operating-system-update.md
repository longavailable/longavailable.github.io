---
layout: post
title:  Update home assistant operating system from virsh guest console
author: Bruce Liu
#last update date
date:   2024-08-25 14:00:00 +0800
#first published date
published:   2024-08-25 14:00:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu, Docker, Github]
description: 
header-image: 
permalink: /hassio-operating-system-update
---

Update to [Home Assistant Operating System] is based on the release in [Github]. It means we may fall in the `Error updating Home Assistant Operating System: Can't fetch OTA update from https://github.com/home-assistant/operating-system/releases/download/13.1/haos_ova-13.1.raucb` in the place where [GitHub] is not accessible.
This post show a temporary solution.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Update to [Home Assistant Operating System] is based on its [release](https://github.com/home-assistant/operating-system/releases) in [Github]. It means we may fall in the `Error updating Home Assistant Operating System: Can't fetch OTA update from https://github.com/home-assistant/operating-system/releases/download/13.1/haos_ova-13.1.raucb` in the place where [GitHub] is not accessible.

So we can make it by modifying the `release_url`.

## Proxying [Github]

Check my another post [如何解决github访问慢的问题（中文）](https://longlovemyu.com/fasten-github/){:target="_blank"}.

For example, add proxy link `https://gh.api.99988866.xyz/` ahead of the original release link. 

## Deep track it

Check the error log again.

> 2024-08-24 21:33:44.051 ERROR (MainThread) [homeassistant.components.websocket_api.http.connection] [139950367721920] Error updating Home Assistant Operating System: Can't fetch OTA update from https://github.com/home-assistant/operating-system/releases/download/13.1/haos_ova-13.1.raucb:
Traceback (most recent call last):
File "/usr/src/homeassistant/homeassistant/components/hassio/update.py", line 213, in async_install
await async_update_os(self.hass, version)
...

This script file `/usr/src/homeassistant/homeassistant/components/hassio/update.py` will be the key.

Let's have a look in its [source](https://github.com/home-assistant/core/blob/b63fb9f17f963221cb979316c40b46e896eabb0c/homeassistant/components/hassio/update.py).
It's easy to find out the following code snippet.

```python
class SupervisorOSUpdateEntity(HassioOSEntity, UpdateEntity):
    """Update entity to handle updates for the Home Assistant Operating System."""

    ...

    @property
    def release_url(self) -> str | None:
        """URL to the full release notes of the latest version available."""
        version = AwesomeVersion(self.latest_version)
        if version.dev or version.strategy == AwesomeVersionStrategy.UNKNOWN:
            return "https://github.com/home-assistant/operating-system/commits/dev"
        return (
            f"https://github.com/home-assistant/operating-system/releases/tag/{version}"
        )

    async def async_install(
        self, version: str | None, backup: bool, **kwargs: Any
    ) -> None:
        """Install an update."""
        try:
            await async_update_os(self.hass, version)
        except HassioAPIError as err:
            raise HomeAssistantError(
                f"Error updating Home Assistant Operating System: {err}"
            ) from err
```

There is a `release_url` function to generate the part of the link for the release. Then we have to modifying it to

```python
    @property
    def release_url(self) -> str | None:
        """URL to the full release notes of the latest version available."""
        version = AwesomeVersion(self.latest_version)
        if version.dev or version.strategy == AwesomeVersionStrategy.UNKNOWN:
            return "https://gh.api.99988866.xyz/https://github.com/home-assistant/operating-system/commits/dev"
        return (
            f"https://gh.api.99988866.xyz/https://github.com/home-assistant/operating-system/releases/tag/{version}"
        )
```

## Config it from [virsh] guest console

Open a guest console via [virsh].

`virsh console hass`

`root`

Check docker root directory.

`docker info` 

We can see the `Docker Root Dir` item. Mostly, it should be `/mnt/data/docker`.

Find the script file `/usr/src/homeassistant/homeassistant/components/hassio/update.py` with:

```shell
cd /
find . -path \*/usr/src/homeassistant/homeassistant/components/hassio/update.py
```

It will list all full path for this file. For example,

```shell
./mnt/data/docker/overlay2/356af2cef9b08a2162030badae8304fa4f2ae7f6544efb1a78b88e45472f7c90/diff/usr/src/homeassistant/homeassistant/components/hassio/update.py
./mnt/data/docker/overlay2/cc97cec3597fd6ed024f0f1af2a7e06e60df7a27ec03304342198257c7bb688d/diff/usr/src/homeassistant/homeassistant/components/hassio/update.py
./mnt/data/docker/overlay2/f8c72160e7488a7c152815e67a7f220f052e7b50d7fc606ee778099c2256237a/merged/usr/src/homeassistant/homeassistant/components/hassio/update.py
./var/lib/docker/overlay2/356af2cef9b08a2162030badae8304fa4f2ae7f6544efb1a78b88e45472f7c90/diff/usr/src/homeassistant/homeassistant/components/hassio/update.py
./var/lib/docker/overlay2/cc97cec3597fd6ed024f0f1af2a7e06e60df7a27ec03304342198257c7bb688d/diff/usr/src/homeassistant/homeassistant/components/hassio/update.py
./var/lib/docker/overlay2/f8c72160e7488a7c152815e67a7f220f052e7b50d7fc606ee778099c2256237a/merged/usr/src/homeassistant/homeassistant/components/hassio/update.py
```

I cannot recognize which is the right one. Then I modified the first three files (they are all under the Docker root directory).

`vi /mnt/data/docker/overlay2/356af2cef9b08a2162030badae8304fa4f2ae7f6544efb1a78b88e45472f7c90/diff/usr/src/homeassistant/homeassistant/components/hassio/update.py`

## Retry to update 

Go back to [homeassistant] lovelace and you can see the update task under the `Settings`.

It works this time for me. And best wishes to you.

<!--links-->
[Home Assistant Operating System]: https://github.com/home-assistant/operating-system
[homeassistant]: https://www.home-assistant.io
[Github]: https://github.com
[virsh]: https://libvirt.org/manpages/virsh.html

