---
layout: post
title:  Ubuntu部署oh-my-zsh与自动补全插件
author: Bruce Liu
#last update date
date:   2026-05-25 20:30:00 +0800
#first published date
published:  2026-05-25 20:30:00 +0800
categories: [post]
tags: [Ubuntu, zsh, Oh My Zsh]
description: 
header-image: 
permalink: /install-zsh-autosuggestions
---

Ubuntu终端（Terminal）默认没有命令补全功能，非常考验用户对命令行的记忆。在这里推荐Oh My Zsh和zsh-autosuggestions插件来提示/补全历史命令。

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Ubuntu终端（Terminal）默认没有命令补全功能，非常考验用户对命令行的记忆。在这里推荐[Oh My Zsh]和[zsh-autosuggestions]插件来提示/补全历史命令。

## 完整安装命令

```bash
# 1. 安装 zsh 和 git 依赖
sudo apt install zsh git -y

# 2. 自动安装 Oh My Zsh, 安装过程中如果提示切换默认 shell，输入 y 确认即可
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 3. 安装 zsh 自动补全插件
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 4. 编辑配置文件启用插件
vim ~/.zshrc
```

打开配置文件后，找到这一行：

```
plugins=(git)
```

修改为：

```
plugins=(git zsh-autosuggestions)
```

保存退出（vim 操作：按 Esc → 输入 :wq 回车），最后执行：

```bash
source ~/.zshrc
```

## 效果说明

安装完成后，终端会自动记住你输入过的命令，输入开头就会灰色自动补全，按键盘右键 → 即可直接补全命令，再也不用重复敲长命令！

[Oh My Zsh]: https://github.com/ohmyzsh/ohmyzsh
[zsh-autosuggestions]: https://github.com/zsh-users/zsh-autosuggestions/