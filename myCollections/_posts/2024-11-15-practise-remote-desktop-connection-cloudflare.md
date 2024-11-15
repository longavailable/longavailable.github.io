---
layout: post
title:  利用Cloudflare Tunnel实现远程桌面访问
author: Bruce Liu
#last update date
date:   2024-10-15 15:00:00 +0800
#first published date
published:   2024-10-15 15:00:00 +0800
categories: [post]
tags: [Cloudflare, Windows, Remote Desktop, 内网穿透]
description: 
header-image: 
permalink: /remote-desktop-connection-using-cloudfare-tunnel
---

如题，本文主要介绍利用Cloudflare Tunnel来实现Windows远程桌面访问。

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->


## 创建一个Cloudflare tunnel

1. 登录[Cloudflare Zero Trust](https://one.dash.cloudflare.com/)

1. 左侧导航栏依次进入Networks→Tunnel

1. 创建一个隧道（Create a Tunnel）

1. 选择Cloudflared类型
    
	![Cloudflared类型](/assets/pics/cloudflare-tunnel-type.png)

1. 设置隧道名称（简洁、好记），并保存隧道

之后，网页自动进入配置页面（configure），不要关掉浏览器

## 配置被访问主机/服务器端

在隧道配置页面选择远程被访问主机/服务器端的运行系统、处理器架构（以window、64-bit为例）。

1. 在远程被访问主机/服务器端下载安装Cloudflared
    
    两种方法：
    
    - 在[cloudflare/cloudflared](https://github.com/cloudflare/cloudflared) Releases页下载msi安装文件
	<https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-windows-amd64.msi>
	直接运行安装
    
    - 在终端（PS）用winget命理安装：`winget install --id Cloudflare.cloudflared`
    
1. 使用管理员方法打开终端（PS或cmd）

1. 运行隧道连接服务，命令见配置网页（包含token，每个账户的都不一样）
    
	![Cloudflared连接服务](/assets/pics/cloudflare-tunnel-configure.png)

该服务随系统启动，后台自动运行。至此，远程被访问主机/服务器端配置完成。

## 回到第一步最后的浏览器，继续完成配置

在cloudflare上配置域名过程省略。

1. 点击next，选择连接一个应用（connect an application）

1. 设置子域名（subdomain），选择域名（domain）

1. 选择服务类型RDP，设置URL为localhost:3389

1. 保存主机名后，cloudflare会自动在域名管理中创建一个cname类型的DNS记录（record）。

1. 查看隧道状况。

## 配置本地电脑/客户端机

1. 在客户端机下载安装Cloudflared，方法同前

1. 运行RDP监听，命令如下
    
	`cloudflared access rdp --hostname rdp.example.com --url rdp://localhost:3389`
	
	注：如果3389端口被window自带服务监听，则可以改成其他端口

1. 打开远程桌面连接**Remote Desktop Connection**应用

1. 计算机输入localhost:3389，开始连接
    
	用户名、密码为远程主机用户名、密码

## 参考

- [Create a tunnel | Cloudflare Zero Trust](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/create-remote-tunnel/#1-create-a-tunnel)
- [Connect as a user | Cloudflare Zero Trust](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/use-cases/rdp/#2-connect-as-a-user)

<!--links-->

