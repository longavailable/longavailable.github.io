---
layout: post
title:  在Ubuntu上使用libvirt/KVM运行Home Assistant OS（NAT 模式）并实现局域网访问
author: Bruce Liu, Microsoft Copilot
#last update date
date:   2026-03-19 20:10:00 +0800
#first published date
published:   2026-03-19 20:10:00 +0800
categories: [post]
tags: [home assistant, virsh, Ubuntu]
description: 
header-image: 
permalink: /install-haos-on-ubuntu-nat-mode
---

本教程介绍如何在Ubuntu + libvirt/KVM环境中运行Home Assistant OS (HAOS)，并在NAT模式下实现局域网设备访问 HAOS。

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->


## 1. 前言

本教程介绍如何在**Ubuntu + libvirt/KVM**环境中运行**Home Assistant OS (HAOS)**，并在**NAT 模式**下实现局域网设备访问 HAOS。

相比桥接（[br0](https://longlovemyu.com/install-haos-on-ubuntu)），NAT 模式具有以下优势：

- 不依赖路由器 DHCP  
- 不受 netplan / NetworkManager 干扰  
- 不会出现 IPv4 ready: false  
- 不会导致主机网络中断

但 NAT 默认是隔离网络，局域网无法直接访问 HAOS。本教程将完整解决这一问题。

## 2. 环境说明

- **主机系统**：Ubuntu 24.04  
- **虚拟化**：libvirt + KVM + virt-manager  
- **HAOS 版本**：17.x  
- **网络模式**：libvirt 默认 NAT 网络（virbr0）  
- **目标**：  
  - HAOS 获得 NAT IP（如 `192.168.122.88`）  
  - 局域网通过 Ubuntu 主机访问 HAOS（如 `http://192.168.1.52:8123`）

## 3. 创建 HAOS 虚拟机（NAT 模式）

在 virt-manager 中：

1. 新建虚拟机  
2. 选择 HAOS qcow2 镜像  
3. **网络接口选择：Virtual network 'default' (NAT)**  
4. 启动虚拟机

也可通过命令行创建：

```bash
virt-install --import --name hass --description "Home Assistant OS" --os-variant=generic \
--memory 2048 --vcpus 2 --cpu host \
--disk <path to qcow2 file>,format=qcow2,bus=virtio \
--network network=default,model=virtio \
--osinfo detect=on,require=off \
--graphics none \
--noautoconsole \
--boot uefi \
--autostart
```

启动后，HAOS 会自动获得 NAT 地址，例如：
`192.168.122.88`

## 4. 验证 HAOS 网络

在 HAOS 控制台运行：

```bash
ha network info
```

你应该看到：

```bash
ipv4:
  address: 192.168.122.88/24
  gateway: 192.168.122.1
  ready: true
```

这说明NAT网络正常。

此时，可以在Ubuntu主机上使用<http://homeassistant.local:8123/>访问Home Assistant，但是<http://192.168.122.88:8123>、<http://192.168.1.52:8123>不可访问。

## 5. 为什么局域网无法访问 NAT 网络？

libvirt 默认NAT网络是**隔离的**：

- Ubuntu 主机可以访问 HAOS

- HAOS 可以访问互联网（需配置域名等）

- 但局域网设备不能访问 HAOS

原因是 libvirt 的 nftables 规则默认阻止：

`局域网 → Ubuntu 主机 → virbr0 → HAOS`

必须手动放行。

## 6. 解决方案：端口转发
目标：

```bash
局域网 → Ubuntu 主机 (192.168.1.52:8123)
        → HAOS (192.168.122.88:8123)
```

### 6.1 添加 DNAT（局域网 → HAOS）

`sudo iptables -t nat -A PREROUTING -p tcp --dport 8123 -j DNAT --to 192.168.122.88:8123`

### 6.2 添加 MASQUERADE（HAOS → 局域网）

`sudo iptables -t nat -A POSTROUTING -p tcp -d 192.168.122.88 --dport 8123 -j MASQUERADE`

## 7. 关键修复：libvirt FORWARD 链阻挡

libvirt 的 nftables 规则默认拒绝外部进入 virbr0 的新连接。

必须插入一条高优先级规则：

`sudo iptables -I FORWARD 1 -p tcp -d 192.168.122.92 --dport 8123 -j ACCEPT`

解释：

- -I FORWARD 1：插入到最前面，优先于 libvirt 的拒绝规则

- 允许局域网 → HAOS 的新连接

这是整个**最关键的一步**。

## 8. 测试访问

从局域网任意设备访问<http://192.168.1.52:8123>，如果能打开 HAOS，则配置成功。

## 9. 规则持久化

安装：

`sudo apt install iptables-persistent`

保存：

`sudo netfilter-persistent save`

## 10. 完整规则示例（可直接使用）

```bash
# DNAT：局域网 → HAOS
sudo iptables -t nat -A PREROUTING -p tcp --dport 8123 -j DNAT --to 192.168.122.88:8123

# MASQUERADE：HAOS → 局域网
sudo iptables -t nat -A POSTROUTING -p tcp -d 192.168.122.88 --dport 8123 -j MASQUERADE

# 允许转发（最关键）
sudo iptables -I FORWARD 1 -p tcp -d 192.168.122.88 --dport 8123 -j ACCEPT
```

Home Assistant的`4357`端口也是类似设置。

## 11. 总结

- NAT 模式更稳定、更安全

- libvirt 默认隔离 virbr0

- 只需三条规则即可让局域网访问 HAOS

- 适合所有 Ubuntu + KVM 环境

## 相关命令

防火墙状态检查：`sudo ufw status`或`sudo systemctl status firewalld`或`sudo nft list ruleset`。

## References

- [桥连模式，安装步骤](https://longlovemyu.com/install-haos-on-ubuntu/install-haos-on-ubuntu-bridge-mode)


<!--links-->
[virt-manager]: https://help.ubuntu.com/community/KVM/VirtManager
