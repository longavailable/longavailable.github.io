---
layout: post
title:  Ubuntu 部署 PostgreSQL 18 完整指南：局域网+Tailscale 双网络访问配置
author: Bruce Liu, Microsoft Copilot
#last update date
date:   2026-04-24 14:50:00 +0800
#first published date
published:   2026-04-24 14:50:00 +0800
categories: [post]
tags: [PostgreSQL, Ubuntu, Windows, tailscale]
description: 
header-image: 
permalink: /install-config-postgresql-on-ubuntu
---

在本地开发或小型团队协作中，我们常常需要在Ubuntu服务器部署PostgreSQL数据库，并实现「局域网本地访问」和「异地Tailscale远程访问」的双重需求。本文结合实际操作场景，从PostgreSQL 18的安装、配置安全访问、Win11连接三个维度，整理了一套可直接复制执行的完整流程，适合新手快速上手，也可作为生产环境基础配置参考。

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

在本地开发或小型团队协作中，我们常常需要在Ubuntu服务器部署PostgreSQL数据库，并实现「局域网本地访问」和「异地Tailscale远程访问」的双重需求。本文结合实际操作场景，从PostgreSQL 18的安装、配置安全访问、Win11连接三个维度，整理了一套可直接复制执行的完整流程，适合新手快速上手，也可作为生产环境基础配置参考。

## 一、说明

本文基于以下环境完成：

- 服务器系统：Ubuntu（本文以24.04为例）

- PostgreSQL版本：全新直接安装18（最新稳定版）

- 访问需求：Win11局域网访问 + Tailscale异地访问

- 安全要求：拒绝公网裸奔，仅放行信任网段，使用官方推荐加密方式

## 二、PostgreSQL 18 安装流程

### 1. 系统更新与依赖准备

安装前先更新系统软件包，确保依赖齐全，避免安装过程中出现报错：

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. 添加PostgreSQL官方源

Ubuntu默认系统源可能未包含PostgreSQL 18最新版本，需添加官方源以获取稳定版本，确保安装的是PostgreSQL 18：

```bash
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```

执行过程中一路回车/选Y，完成官方源的配置与密钥导入，确保后续能正常下载安装包。

### 3. 安装PostgreSQL 18 （服务、客户端均自动安装）

```bash
sudo apt update
sudo apt install -y postgresql-18
```

安装完成后，系统会自动完成以下操作，无需手动干预：
              
- 创建PostgreSQL 18的配置目录（`/etc/postgresql/18/main/`）和数据目录（`/var/lib/postgresql/18/main/`）
              
- 自动启动PostgreSQL 18服务，并设置开机自启
              
- 创建默认的`postgres`系统用户和数据库管理员账户

### 4. 验证安装是否成功

安装完成后，执行以下命令，验证服务是否正常运行：

```bash
sudo systemctl status postgresql@18-main
```

若输出显示「active (running)」，说明服务启动正常；同时可验证客户端版本，确认安装的是18版本：

```bash
psql --version
```

正常输出应为「psql (PostgreSQL) 18.x」，表示安装成功。

### 5. 配置PostgreSQL 18（端口\+监听）

默认配置仅允许本机访问，需修改配置文件，确保监听所有网卡（支持局域网和Tailscale虚拟网卡），并使用默认端口5432（无需修改Win11连接配置）：

```bash
sudo vim /etc/postgresql/18/main/postgresql.conf
```

找到以下两行，取消注释（删除开头的 #）并修改：

```ini
# 原配置（注释状态）
#listen_addresses = 'localhost'

# 修改后配置（取消注释+修改值）
listen_addresses = '*'
```

`port = 5432`为默认。

保存退出。

## 三、关键配置：局域网\+Tailscale 双网络访问

仅允许「本地局域网设备」和「Tailscale组网设备」访问，拒绝公网访问，兼顾安全和实用性。

### 1. 获取关键网段信息

- 局域网网段：在Ubuntu终端执行 `ip a`，找到本机局域网IP（如192.168.1.100），对应的网段为192.168.1.0/24（90%家用路由器通用）。

- Tailscale网段：执行 `tailscale ip -4`，获取本机Tailscale IP（如100.96.226.51），Tailscale官方默认网段为100.64.0.0/10（所有Tailscale节点均在此网段内）。

### 2. 配置pg_hba.conf（访问控制规则）

编辑访问控制文件，精准放行信任网段，使用最安全的`scram-sha-256`认证方式：

```bash
sudo vim /etc/postgresql/18/main/pg_hba.conf
```

保留文件原有默认配置，在末尾添加局域网和Tailscale访问规则，最终完整配置如下（可直接复制替换）：

```ini
# 允许本地局域网所有设备访问（替换为你的实际网段）
host    all             all             192.168.1.0/24          scram-sha-256
# 允许所有Tailscale设备访问（官方默认网段）
host    all             all             100.64.0.0/10           scram-sha-256
```

### 3. 创建远程登录用户（自定义用户名 + 密码）

PostgreSQL 安装后会自动创建系统用户 postgres，进入数据库命令行：

```bash
sudo su - postgres
psql
```

创建远程登录用户（自定义用户名 + 密码）：

```sql
-- 创建用户（替换 username 和 your_password 为你自己的）
CREATE USER username WITH PASSWORD 'your_password';

-- 授予超级权限（方便管理，也可按需分配权限）
ALTER ROLE username SUPERUSER;

-- 创建数据库（可选）
CREATE DATABASE test_db;

-- 退出 psql
\q
```

退出 postgres 用户：

```bash
exit
```

### 4. 防火墙放行端口

放行PostgreSQL默认端口5432，允许局域网和Tailscale流量通过：

```bash
sudo ufw allow 5432/tcp
sudo ufw reload
```

### 6. 重启PostgreSQL 18生效

```bash
sudo systemctl restart postgresql@18-main
```

验证服务状态（确保为active (running)）：

```bash
sudo systemctl status postgresql@18-main
```

## 四、Win11 连接方式

配置完成后，Win11使用pgAdmin（官方推荐图形化工具）来连接。

### 1. 局域网连接

- Host：Ubuntu的局域网IP（如192.168.1.100）

- Port：5432

- Username：数据库用户名（如postgres）

- Password：重新设置的密码

### 2. Tailscale异地连接

- Host：Ubuntu的Tailscale IP（执行`tailscale ip -4`获取）

- Port：5432

- Username/Password：与局域网连接一致

- 前提：Win11已登录同一个Tailscale账号，组网成功。


按照本文配置后，你可以在Win11上无缝切换局域网和Tailscale方式访问Ubuntu上的PostgreSQL 18数据库，无需重复修改配置。若遇到连接问题，可检查防火墙端口、配置文件语法或Tailscale组网状态。

