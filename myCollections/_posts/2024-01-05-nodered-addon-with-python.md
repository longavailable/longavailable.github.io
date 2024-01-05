---
layout: post
title:  Deply python and install dependencies within Node-RED-addon in Homeassistant
author: Bruce Liu
#last update date
date:   2024-01-05 11:30:00 +0800
#first published date
published:   2024-01-05 11:30:00 +0800
categories: [post]
tags: [home assistant, Nodered, Node RED, Python, linux]
description: 
header-image: 
permalink: /python-nodered-in-hass
---

Node RED can be deployed within Home Assistant OS by using the community addon-node-red. Python is not a dependency for the running of node-red, so it was not a built-in in the image. How to add python and install needed dependencies in the addon container. 

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Frenck, the maintainer of [node-red-addon] declared,

> Python is not needed to run node-red.

<https://github.com/hassio-addons/addon-node-red/issues/1450#issuecomment-1260433209>

So [Python] is not built in the node-red addon.

Athough it support the options of `system_packages`, `npm_packages`, and `init_commands` to extend its function. While a explicit method to implement [Python] script is still needed.

## Nevigate to [node-red-addon] contianer from Terminal in HA

`docker exec -it addon_<your addon id>_nodered /bin/bash`

## Choose a comfortable source of [Alpine Linux] (skip if it's not needed)

`sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories`

## Add python and pip

`apk add py3-pip`

## Choose a comfortable source of [PyPI] (skip if it's not needed)

`pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/`

## Install necessary [Python] packages

`pip3 install requests beautifulsoup4`

## Implement the above in a flow

```json
[{"id":"05fbd5fa4cea99e8","type":"exec","z":"6defd24b07e25d51","command":"sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories && apk add py3-pip && pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/ && pip3 install requests beautifulsoup4","addpay":"","append":"","useSpawn":"false","timer":"","winHide":false,"oldrc":false,"name":"安装python脚本依赖项","x":440,"y":260,"wires":[["9bf90b61cf6ca404"],["9bf90b61cf6ca404"],["9bf90b61cf6ca404"]]}]
```

<!--links-->
[node-red-addon]: https://github.com/hassio-addons/addon-node-red
[Python]: https://www.python.org
[Alpine Linux]: https://www.alpinelinux.org
[PyPI]: https://pypi.org

