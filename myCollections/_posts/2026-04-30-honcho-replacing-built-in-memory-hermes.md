---
layout: post
title:  Hermes智能体Honcho配置指南：代替 Hermes 自带 Memory 机制
author: Bruce Liu, Doubao
#last update date
date:   2026-05-01 23:20:00 +0800
#first published date
published:   2026-04-30 22:30:00 +0800
categories: [post]
tags: [PostgreSQL, Ubuntu, Hermes agent, Honcho]
description: 
header-image: 
permalink: /install-config-postgresql-on-ubuntu
---

Hermes 作为一款强大的 LLM Agent 框架，自带了基础的记忆（Memory）机制，能够保存有限的固定记忆、简单的用户信息。但如果你需要**长期记忆、多会话持久化、用户画像、事实提取、多项目隔离**，原生 Memory 就会显得力不从心。这时，**Honcho** 就是 Hermes 官方推荐的、生产级的记忆替代方案。而部署 Honcho 前，必须先部署 PostgreSQL 并创建带有 vector 数据扩展的数据库——这是 Honcho 实现语义检索、向量存储的核心前提。

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Hermes 作为一款强大的 LLM Agent 框架，自带了基础的记忆（Memory）机制，能够保存有限的固定记忆、简单的用户信息。

但如果你需要**长期记忆、多会话持久化、用户画像、事实提取、多项目隔离**，原生 Memory 就会显得力不从心。

这时，**[Honcho]** 就是 Hermes 官方推荐的、生产级的记忆替代方案。而部署 [Honcho] 前，必须先部署 PostgreSQL 并创建带有 vector 数据扩展的数据库——这是 [Honcho] 实现语义检索、向量存储的核心前提。

## 一、为什么要用 [Honcho] 代替原生 Memory？

### 1. 记忆永久且无长度限制

Hermes 原生 Memory 的永久记忆存在明确字符限制，仅支持最多 2,200 characters，无法存储大量长期对话、关键事实及用户画像数据；而 [Honcho] 依托 PostgreSQL 持久化存储，可实现无限永久记忆，无论对话长度、事实数量多少，均可稳定保存，重启、跨会话均不会丢失。

### 2. 支持多项目/多目录隔离

配合 `per-directory` 策略：

- 每个项目一个目录

- 记忆完全隔离

- 机器人不会串项目

- 文件不会到处乱飞

### 3. 自动构建用户画像

[Honcho] 会自动从对话中提取：

- 用户偏好

- 关键事实

- 对话风格

- 长期目标

并生成 `peer card`，让 AI 真正“认识你”。

### 4. 强大的推理能力

`honcho_reasoning` 会自动：

- 总结对话

- 提炼事实

- 消除矛盾

- 生成结构化记忆

### 5. 多agent共享记忆

依托PostgreSQL统一存储，多个Hermes Agent可连接同一[Honcho]服务，共享会话记忆、用户画像及事实数据，实现多智能体协同工作

**注**：启用 [Honcho] 后，原生记忆机制仍正常工作，两者互不影响。

## 二、前置部署：PostgreSQL（带 vector 扩展）

[Honcho] 依赖 PostgreSQL 存储记忆数据，且需要 vector 扩展实现语义检索功能，因此必须先部署 PostgreSQL 并完成配置。本文采用 Ubuntu 系统直接安装方式，版本选择 PostgreSQL 18（最新稳定版），详细步骤参考另一篇博客：[Ubuntu 部署 PostgreSQL 18 完整指南：局域网\+Tailscale 双网络访问配置](https://longlovemyu.com/install-config-postgresql-on-ubuntu)。


### 安装并启用 vector 扩展（Honcho 语义检索必需）

pgvector 扩展的详细安装方法可参考其官方仓库：[pgvector 官方仓库](https://github.com/pgvector/pgvector)，，安装前需先准备完整依赖：

安装pgvector扩展前，需先安装PostgreSQL 18的开发依赖包：

```bash
# 安装PostgreSQL 18开发依赖（pgvector扩展安装前提，不可省略）
sudo apt install -y postgresql-server-dev-18 git make gcc
```

```bash
# 克隆pgvector官方源码（官方推荐安装方式，适配PostgreSQL 18）
git clone --branch v0.8.2 https://github.com/pgvector/pgvector.git
cd pgvector
# 编译并安装pgvector扩展
make
sudo make install
```

在 PostgreSQL 命令行中，执行以下命令启用 vector 扩展并创建 Honcho 专用数据库和用户：

```bash
# 进入 PostgreSQL 命令行（切换到 postgres 系统用户）
sudo su - postgres
psql
```

```sql
-- 创建 Honcho 专用数据库（与后续 Honcho 配置一致，命名为 honcho_db）
CREATE DATABASE honcho_db;
-- 创建 Honcho 专用用户（替换 bruce 为自定义用户名，88888 为自定义密码）
CREATE USER bruce WITH PASSWORD '88888';
-- 授予用户超级权限（方便管理，可按需分配权限）
ALTER ROLE bruce SUPERUSER;
-- 更改所有者
ALTER DATABASE honcho_db2 OWNER TO bruce;
-- 切换到创建好的 honcho_db 数据库（必做，否则扩展会创建在默认数据库）
\c honcho_db
-- 启用 vector 扩展（Honcho 语义检索核心，不可省略）
CREATE EXTENSION IF NOT EXISTS vector;
-- 验证扩展是否生效（返回 vector 即成功）
\dx
-- 退出 PostgreSQL 命令行
\q
-- 退出 postgres 系统用户
exit
```

### 防火墙放行与服务重启

```bash
# 放行 PostgreSQL 默认端口 5432（允许 Honcho 访问）
sudo ufw allow 5432/tcp
sudo ufw reload
# 重启 PostgreSQL 18，使所有配置生效
sudo systemctl restart postgresql@18-main
# 再次验证服务状态，确保重启后正常运行
sudo systemctl status postgresql@18-main
```

注意：用户名（bruce）、密码（88888）、数据库名（honcho\_db）需牢记，后续配置 [Honcho] 时需完全对应，否则会出现数据库连接失败；vector 扩展安装完成后，可通过 `\\dx` 命令再次验证，确保扩展正常加载。

至此，Ubuntu 系统直接安装 PostgreSQL 18（带 vector 扩展）已完成，且已配置好 Honcho 所需的数据库、用户和访问权限，后续可直接部署 Honcho API 并关联该数据库。若需要实现局域网或 Tailscale 异地访问，可参考详细指南：[Ubuntu 部署 PostgreSQL 18 完整指南：局域网\+Tailscale 双网络访问配置](https://longlovemyu.com/install-config-postgresql-on-ubuntu)。

## 三、部署 Honcho API 并关联 PostgreSQL

**！！** Honcho 默认设置都是针对OpenAI模型，需要搭配OpenAI api来使用，而本地化配置难度较大。这里记录下本人利用本地模型配置过程。

本地安装Text Embedding模型，可以选择[gte-Qwen2-1.5B-instruct (1536固定)](https://huggingface.co/Alibaba-NLP/gte-Qwen2-1.5B-instruct) 、 [Qwen3-Embedding-4B (可降维，32-2560)](https://huggingface.co/Qwen/Qwen3-Embedding-4B) (因为它与OpenAI的text-embedding-3-small一样，是1536维的，而Honcho的Embeding架构的维度存在锁死在1536的问题。)

```bash
ollama pull miti99/gte-qwen2
```

本地LLM模型使用[llama3.1:8b](https://huggingface.co/meta-llama/Llama-3.1-8B) 。

```bash
ollama pull llama3.1:8b
```

由于修改Text Embedding模型、LLM模型，环境参数配置非常多。这里以*.env*文件形式完成，见<https://gist.github.com/longavailable/a6b79f934b37526b40f815948cc72d41>，其他模型可参照修改。

注：database配置也放置*.env*文件中。假设*.env*文件文件路径为`~/docker-composed/honcho/.env`。

接下来docker运行honcho。

```bash
# 先拉取 Honcho 官方镜像（部署前必做，确保获取最新版本，使用ghcr仓库地址）
docker pull ghcr.io/plastic-labs/honcho:latest
```

```
# 部署 Honcho API 并关联 PostgreSQL 
docker run -d \
  --name honcho-api \
  --network host \
  --env-file ~/docker-composed/honcho/.env \
  --restart always \  
  ghcr.io/plastic-labs/honcho:latest  
```

如果数据库配置没有放在*.env*文件中，也可以通过添加`-e DB_CONNECTION_URI=postgresql+psycopg://<username>:<password>@localhost:5432/honcho_db`参数，完整命令为：

```
# 部署 Honcho API 并关联 PostgreSQL 
docker run -d \
  --name honcho-api \
  --network host \
  --env-file ~/docker-composed/honcho/.env \
  --restart always \  
  -e DB_CONNECTION_URI=postgresql+psycopg://<username>:<password>@localhost:5432/honcho_db \
  ghcr.io/plastic-labs/honcho:latest
```

## 四、初始化 [Honcho] 数据库

```bash
# 进入 Honcho 容器
docker exec -it honcho-api bash

# 初始化数据库，前面创建的空白数据库缺表格
# 执行数据库迁移，自动创建 Honcho 所需表（workspaces、users 等）
alembic upgrade head

# 退出容器
exit

# 重启 Honcho 容器，使配置生效
docker restart honcho-api
```

Honcho API部署完成后，可通过以下curl命令快速判断服务是否正常启动：

```bash
# 方法1：访问健康检查接口（最简洁，快速判断服务状态）
curl http://localhost:8000/health
# 方法2：访问API文档接口（同时验证服务可用性和接口完整性）
curl http://localhost:8000/docs
```

若报错，可通过 `docker logs honcho\-api` 查看容器日志，排查部署或数据库连接问题。

## 五、配置 Hermes 关联 Honcho（使用 hermes memory setup 命令）

无需手动编辑配置文件，通过 Hermes 官方提供的 `hermes memory setup` 命令，可快速完成 Honcho 记忆提供者的配置。

执行命令后，按照以下交互式提示逐步操作（全程按实际情况选择/输入，适配 Honcho 配置）：

1. 选择记忆提供者：提示「Select memory provider」时，选择 `honcho`，回车确认（这一步会自动将 Hermes 记忆后端切换为 Honcho）。

2. 输入 Honcho 服务地址：提示「Enter Honcho host URL」时，输入 Honcho 服务地址 `http://localhost:8000`（若已自定义 Honcho 端口，需替换为对应端口，如 http://localhost:8080），回车确认。

结合 Hermes 官方文档（[https://hermes\-agent\.nousresearch\.com/docs/user\-guide/features/honcho](https://hermes-agent.nousresearch.com/docs/user-guide/features/honcho)），补充官方推荐的核心配置参数，确保配置合规且功能完整：

执行 `hermes memory setup` 交互式配置后，官方会自动生成标准配置，无需手动编辑；若需自定义高级参数，可参考 Hermes 官方文档（[https://hermes\-agent\.nousresearch\.com/docs/user\-guide/features/honcho](https://hermes-agent.nousresearch.com/docs/user-guide/features/honcho)），补充以下 Honcho 核心配置（需编辑 `\~/\.hermes/honcho\.json` 文件），所有参数均遵循官方规范：

```json
{
  // 遵循 Hermes 官方文档配置，Honcho 核心参数（需配置在 honcho.json 文件中）
  "session_strategy": "per-directory",  // 官方推荐会话策略：多项目隔离，适配 Honcho 多工作空间
  "observation_mode": "directional",  // 官方默认观察模式：定向观察，优化记忆提取效率
  "dialectic_reasoning_level": "medium"  // 官方推荐推理级别：平衡推理精度与性能，适配大多数场景
}
```

补充说明：配置完成后，建议重启 Hermes 服务，确保记忆提供者切换生效；若后续修改 [Honcho] 端口或服务地址，重新执行 `hermes memory setup` 命令重新配置即可。

## 六、验证是否生效

```bash
hermes honcho status
```

看到以下内容，代表 PostgreSQL、Honcho、Hermes 三者关联成功：

```bash
Connection... OK
```

检查日志，是否报错。需要与hermes聊天过程相结合，只有在聊天中，[Honcho]的logs没有错误，并能准确运行，才算正常使用。

```bash
docker logs honcho-api
docker logs --tail 50 honcho-api
docker logs --tail 500 honcho-api 2>&1 | grep -A 20 "error"
```

## 七、Honcho 常用命令（替代原生记忆）

|功能|Hermes 原生|Honcho|
|---|---|---|
|查看记忆|`memory`|`honcho\_context`|
|查看画像|无|`honcho\_profile`|
|搜索历史|无|`honcho\_search`|
|手动存事实|无|`honcho\_conclude`|
|推理总结|无|`honcho\_reasoning`|
|查看状态|无|`hermes honcho status`|

## 注意事项

- PostgreSQL 的 vector 扩展不可省略，否则 [Honcho] 语义检索功能会失效，部分记忆相关操作报错。

- [Honcho] 与 PostgreSQL 的连接信息（用户名、密码、数据库名）必须完全一致，否则会出现 `Peer data unavailable` 或数据库连接失败。

- Ubuntu 直接安装的 PostgreSQL 18，数据默认存储在 `/var/lib/postgresql/18/main/`，建议定期备份数据（ Honcho 所有记忆都存在 PostgreSQL 中），避免数据丢失。

对于任何生产环境、机器人、多智能体团队，**Honcho 是 Hermes 唯一正确的记忆选择**，而部署带 vector 扩展的 PostgreSQL，是使用 [Honcho] 的前提条件。

[Honcho]: https://github.com/plastic-labs/honcho