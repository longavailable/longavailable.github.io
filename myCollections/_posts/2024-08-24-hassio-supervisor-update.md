---
layout: post
title:  Update home assistant supervisor/core from virsh guest console
author: Bruce Liu
#last update date
date:   2025-08-05 09:30:00 +0800
#first published date
published:   2024-08-24 13:20:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu, Docker, ghcr, DaoCloud]
description: 
header-image: 
permalink: /hassio-supervisor-update
---

[homeassistant] migrates image registry from [Docker Hub] to [Github] container registry. For example, the image link of supervisor changes from `home-assistant/amd64-hassio-supervisor:2024.08.0` to `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. It is very difficult to access ghcr.io directly in China. Therefore, it is impossible to directly update supervisor, etc. This post show a temporary solution. By the way, it works for [Homeassistant core] as well.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## [Supervisor]

[homeassistant] migrates image registry from [Docker Hub] to [Github] container registry. For example, the image link of supervisor changes from `home-assistant/amd64-hassio-supervisor:2024.08.0` to `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. It is very difficult to access ghcr.io directly in China. Therefore, it is impossible to directly update supervisor, etc. This post show a temporary solution based on [DaoCloud/public-image-mirror].

### Set up a ready-to-go `ghcr` image source

Open a `sync-image` [issue](https://github.com/DaoCloud/public-image-mirror/issues/new?labels=sync+image&template=sync-image.yml).

Place the image sorce as a title with the format of `<domian>/<owner>/<image>:<tag>`. For example, `ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0`. Mark the checkbox. And wait one or two minutes. You will received a email with the following content.

> 镜像 ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0 同步完成
> 请使用 m.daocloud.io/ghcr.io/home-assistant/amd64-hassio-supervisor:2024.08.0 替代源镜像

Let's go to pull the image with the new source.

### Update supervisor from a guest console

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

Note that, you can do this on Terminal addon from [homeassistant] lovelace.

### Useful commands

Normal method to update `hassio_supervisor`.

`ha su update` or `ha supervisor update`

Check jobs running on haos.

`ha job info`

List all containers:

`docker ps -a`

List images:

`docker images`

## [Core] commands

`docker pull m.daocloud.io/ghcr.io/home-assistant/qemux86-64-homeassistant:2024.12.4`

`docker tag m.daocloud.io/ghcr.io/home-assistant/qemux86-64-homeassistant:2024.12.4 ghcr.io/home-assistant/qemux86-64-homeassistant:2024.12.4`

`ha core update`

## Derect scripts

I place two ready-to-go scripts to make them on [Github Gist]. And you can run it directly from terminal.

[Supervisor]:

`curl -l https://gh.api.99988866.xyz/https://gist.githubusercontent.com/longavailable/40df661bb53da392e5bd136fdc0481f9/raw/77bd64b4efc55029d4ee670f24aca748acf5781f/update-ha-supervisor-amd64-hassio-supervisor.sh | bash`

[Core]:

`curl -l https://gh.api.99988866.xyz/https://gist.githubusercontent.com/longavailable/44af7d42ac76ac501fe7d7e832519084/raw/9adda982dc74d95ce5dfe2c1faa36829411f72c8/update-ha-core-qemux86-64-homeassistant.sh | bash`

Both [virsh] and Terminal addon work.


## References

- [home-assistant/version/update-supervisor.txt](https://github.com/home-assistant/version/blob/83f290b0a3d39a58efc26b1a452d31cc538abfba/update-supervisor.txt)

- [DaoCloud/public-image-mirror]

<!--links-->
[homeassistant]: https://www.home-assistant.io
[Homeassistant core]: https://github.com/home-assistant/core
[Core]: https://github.com/home-assistant/core
[Supervisor]: https://github.com/home-assistant/supervisor
[Github]: https://github.com
[Docker Hub]: https://hub.docker.com
[DaoCloud/public-image-mirror]: https://github.com/DaoCloud/public-image-mirror
[virsh]: https://libvirt.org/manpages/virsh.html
[Github Gist]: https://gist.github.com/longavailable/44af7d42ac76ac501fe7d7e832519084

