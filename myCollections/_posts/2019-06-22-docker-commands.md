---
layout: post
title:  Docker commands & issues (中文)
author: Bruce Liu
# last update date
date:   2019-07-26 11:20:00 +0100
# first published date
published: 2019-07-26 11:20:00 +0100
categories: [post]
tags: [docker, 中文]
header-image: 
permalink: /docker_guide/
---
How to use docker, follow these commands.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Docker commands

| Docker commands/命令        | Explanation in Chinese/中文解释  |
| ----------------------------|:--------------------------------:|
| ```docker info```       | 查看整个docker系统信息			| 
| ```docker login -u <username> -p <password>``` 	| 登陆docker hub			| 
| <b>imaged的查询、新建、删除</b>  					||
| ```docker images```    			| 显示所有的image			| 
| ```docker rmi <image ID>``` | 删除一个image			| 
| ```docker build <......>``` | 从Dockerfile新建一个image			| 
| ```docker search <keywords>```	| 从ducker hub搜索image			| 
| ```docker pull <image/repository name>```    | 从ducker hub上下载并在本地新建一个image/repository，类似git clone			| 
| ```docker push <image/repository name>```    | 将本地image/repository提交给docker hub			| 
| <b>container的查询、新建、删除</b>  				 ||
| ```docker ps```         | 显示正在运行的(running)container		| 
| ```docker ps -a```      | 显示所有container，包括正在运行的(running)，停止运行的(stop)			| 
| ```docker ps -a -f status=exited```   | 显示停止运行的(stop)container, f是筛选filter命令		| 
| ```docker ps -aq```     | 显示所有的container，但只显示ID			| 
| ```docker rm <container ID/name>```       | 删除一个container			| 
| ```docker rm 'docker ps -aq -f status=exited'``` 	| 删除所有不在运行的（stopped）container（在win10 cmd中多次尝试未成功）			| 
| ```docker create <container ID/name>```   | 新建一个container			| 
| ```docker run -it <image>```     | 新建一个container（是否进入命令模式由image预设命令决定，ubuntu image latest可进入）			| 
| ```docker run -it --name <new container name> <image>```	|  新建一个container，并对其命名			| 
| ```docker run -it --mount type=bind,source=<local directory to be mounted>,target=/<> <image>``` 	| 挂载本地文件（只能在新建container时），[更多信息](https://docs.docker.com/storage/bind-mounts/)			| 
| ```docker stop <container ID/name>```     | 停止运行一个container（后台停止）			| 
| ```docker start <container ID/name>```    | 开始运行一个container（后台运行）			| 
| ```docker exec -it <container ID/name> /bin/zsh```    | 进入一个正在运行的container的zsh命令模式			| 
| ```docker exec -it <container ID/name> /bin/bash```   | 进入一个正在运行的container的bash命令模式			| 
| ```exit```      | 退出container命令模式			| 
| ```docker rename <container ID/name> <new name>``` 	| 在新建（run或create）未对container命名时，系统会自动生成名字，如要进入，则每次得查container id，rename命令可以将container name改成自己期望的名字			| 

# Docker issues
1. docker在windows上如何实现的？<br>
  windows上必须借助Linux Hyper-V Virtual Machine实现docker container架构。
1. 虚拟镜像文件存储位置在哪？如何修改？<br>
	- vhdx文件默认存储路径：C:\Users\Public\Documents\Hyper-V\Virtual hard disks.
	- 可以通过Docker Desktop在设置(settings)->高级(advanced)中更改，自动迁移后，docker desktop自动重启。
1. localhost:<your port> 无法访问？<br>
	1. stop contianer
	1. start contianer,如果可以正常重启，稍等几分钟，测试是否可以。如果不能正常重启，可能出现以下问题：
		- error1： driver failed programming external connectivity on endpoint
			- 重启docker desktop即可解决。
		- error2： invalid mount config for type "bind": bind mount source path does not exist: <some path>
			- 在docker desktop的settings中重新勾选shared driver，重启docker desktop即可解决。
