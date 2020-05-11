---
layout: post
title:  FAQ for Docker in Chinese
author: Bruce Liu
# last update date
published: 2019-05-11 15:15:00 +0100
# first published date
published: 2019-05-11 15:15:00 +0100
categories: [post]
tags: [docker, windows]
header-image: 
permalink: /docker_issues/
---
FAQ for Docker.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Docker issues

1. docker在windows 10上如何实现的？

	- windows上必须借助Linux Hyper-V Virtual Machine实现docker container架构。

1. 虚拟镜像文件存储位置在哪？如何修改？

	- vhdx文件默认存储路径：C:\Users\Public\Documents\Hyper-V\Virtual hard disks.
	- 可以通过Docker Desktop在设置(settings)->高级(advanced)中更改，自动迁移后，docker desktop自动重启。
	
1. localhost:<your port> 无法访问？

	- stop contianer
	- start contianer,如果可以正常重启，稍等几分钟，测试是否可以。如果不能正常重启，可能出现以下问题：
	
		Error1： driver failed programming external connectivity on endpoint		
		- 重启docker desktop即可解决。
		
		Error2： invalid mount config for type "bind": bind mount source path does not exist: <some path>		
		- 在docker desktop的settings中重新勾选shared driver，重启docker desktop即可解决。
	

1. Windows7如何安装docker？

	Win7 64为系统上可以安装[docker toolbox](https://docs.docker.com/toolbox/)，其借助虚拟机实现docker的使用，安装方法参见[Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)。
	
1. Windows7的docker环境中如何挂载windows文件夹？

	- 打开Oracle VM VirtualBox
	- 选中'default'虚拟机，设置（setting），打开共享文件夹（shared folders）选项，新建共享文件夹，根据需要设置好路径、文件夹名（例如mysharedfolder）
	- `docker run --mount type=bind,source=/mysharedfolder,target=/mysharedfolder`