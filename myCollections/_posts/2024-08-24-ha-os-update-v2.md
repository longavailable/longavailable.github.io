---
layout: post
title:  Update home assistant os from virsh guest console
author: Bruce Liu
#last update date
date:   2024-08-24 13:20:00 +0800
#first published date
published:   2024-08-24 13:20:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu, Docker, ghcr, DaoCloud]
description: 
header-image: 
permalink: /haos-update
---

[homeassistant] migrates image registry from [Docker Hub] to [Github] container registry. For example, the image link of supervisor changes from `home-assistant/amd64-hassio-supervisor:2024.08.0` to `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. It is very difficult to access ghcr.io directly in China. Therefore, it is impossible to directly update supervisor, etc. This post show a temporary solution.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

[homeassistant] migrates image registry from [Docker Hub] to [Github] container registry. For example, the image link of supervisor changes from `home-assistant/amd64-hassio-supervisor:2024.08.0` to `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. It is very difficult to access ghcr.io directly in China. Therefore, it is impossible to directly update supervisor, etc. This post show a temporary solution based on [DaoCloud/public-image-mirror].

## Set up a ready-to-go `ghcr` image source

Open a `sync-image` [issue](https://github.com/DaoCloud/public-image-mirror/issues/new?labels=sync+image&template=sync-image.yml).

Place the image sorce as a title with the format of `<domian>/<owner>/<image>:<tag>`. For example, `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. Mark the checkbox. And wait one or two minutes. You will received a email with the following content.

> 镜像 ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0 同步完成
> 请使用 m.daocloud.io/ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0 替代源镜像

Go to pull the image as normal.

## Update supervisor from a guest console

Open a guest console via [virsh].

`virsh console hass`

`root`

Pull the supervisor image from the alternative source.

`docker pull m.daocloud.io/ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`

Add the recognizable tags.

```
docker tag "m.daocloud.io/ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0" "ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0"
docker tag "ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0" "ghcr.io/home-assistant/amd64-hassio-supervisor:latest"
```

Stop current `hassio_supervisor` container.

`docker stop hassio_supervisor`

And reboot homeassistant os. hassos-supervisor script will recreate the container automatically. The deprecated images will be removed automatically as well.

## Useful commands

Normal method to update `hassio_supervisor`.

`ha su update` or `ha supervisor update`

Check jobs running on haos.

`ha job info`

List all containers:

`docker ps -a`

List images:

`docker images`

## References

- [home-assistant/version/update-supervisor.txt]https://github.com/home-assistant/version/blob/83f290b0a3d39a58efc26b1a452d31cc538abfba/update-supervisor.txt

- [DaoCloud/public-image-mirror]

<!--links-->
[homeassistant]: https://www.home-assistant.io
[Github]: https://github.com
[Docker Hub]: https://hub.docker.com
[DaoCloud/public-image-mirror]: https://github.com/DaoCloud/public-image-mirror
[virsh]: https://libvirt.org/manpages/virsh.html

