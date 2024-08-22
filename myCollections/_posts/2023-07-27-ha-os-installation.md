---
layout: post
title:  The detailed steps of installing Home Assistant Operating System on Ubuntu
author: Bruce Liu
#last update date
date:   2024-08-22 14:10:00 +0800
#first published date
published:   2023-07-27 00:40:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu]
description: 
header-image: 
permalink: /install-haos-on-ubuntu
---

As the title, this is the detailed steps.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->


## Install [virt-manager]

`apt install virt-manager` or `sudo apt install virt-manager`

## Config internet

Check [Aephir's post](https://community.home-assistant.io/t/install-home-assistant-os-with-kvm-on-ubuntu-headless-cli-only/254941#2-set-up-network-8).

`apt install net-tools` or `sudo apt install net-tools`

`ifconfig` 

Mark the network interface, `eno1`, `enp1s0`..

Create a netplan `yaml` file in the `/etc/netplan/` directory with the following content.

```yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    eno1:
      dhcp4: true
  version: 2
  bridges:
    br0:
      dhcp4: yes
      interfaces:
             - eno1
      parameters:
        stp: true
```

Note replacing `eno1` with your bridge interface.

`netplan generate` or `sudo netplan generate`

`netplan apply` or `sudo netplan apply`

`apt install bridge-utils` or `sudo apt install bridge-utils`

`brctl show`

Mark the bridge adapter name, `br0` or something else.

## Prepare the image

- Download the [latest image](https://github.com/home-assistant/operating-system/releases).

- Decompress it, if needed. Note that some `.xz` files were broken. 

  `xz -d -v haos_ova-10.4.qcow2.xz`
  
  [360 zip](https://www.360totalsecurity.com/en/360zip/) works perfect.

## Install the HAOS VM

```bash
virt-install --import --name hass --description "Home Assistant OS" --os-variant=generic \
--memory 2048 --vcpus 2 --cpu host \
--disk <path to qcow2 file>,format=qcow2,bus=virtio \
--network bridge=br0,model=virtio \
--osinfo detect=on,require=off \
--graphics none \
--noautoconsole \
--boot uefi \
--autostart
```

## Then wait patiently.

## References

- [Install Home Assistant OS with KVM on Ubuntu headless (CLI only)](https://community.home-assistant.io/t/install-home-assistant-os-with-kvm-on-ubuntu-headless-cli-only/254941)


<!--links-->
[virt-manager]: https://help.ubuntu.com/community/KVM/VirtManager
