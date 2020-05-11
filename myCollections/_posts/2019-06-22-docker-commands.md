---
layout: post
title:  Docker commands in Chinese
author: Bruce Liu
# last update date
date:   2020-05-11 16:50:00 +0100
# first published date
published: 2019-07-26 11:20:00 +0100
categories: [post]
tags: [docker, 中文]
header-image: 
permalink: /docker_commands/
---
How to use docker, follow these commands.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# Docker commands

| Docker commands/命令        | Explanation in Chinese/中文解释  |
| ----------------------------|----------------------------------|
| ```docker info```       												| 查看整个docker系统信息			| 
| ```docker login -u <username> -p <password>``` 	| 登陆docker hub							| 
| <b>image的查询、新建、删除</b>  					||
| ```docker images```    			| 显示所有的image		| 
| ```docker rmi <image ID>``` | 删除一个image			| 
| ```docker build <......>``` | 从Dockerfile新建一个image			| 
| ```docker search <keywords>```	| 从ducker hub搜索image			| 
| ```docker pull <image/repository name>```    | 从ducker hub上下载并在本地新建一个image/repository，类似git clone			| 
| ```docker commit <existing-container> <hub-user>/<repo-name>[:<tag>]``` | 从Container新建或更新一个本地image					| 
| ```docker push <hub-user>/<repo-name>:<tag>```    | 将本地image/repository提交给docker hub			| 
| <b>container的查询、新建、删除</b>  				 ||
| ```docker ps```         					| 显示正在运行的(running)container		|
| ```docker container ls```         | 同上，显示正在运行的(running)container		|
| ```docker ps -a```      					| 显示所有container，包括正在运行的(running)，停止运行的(stop)			|
| ```docker container ls -a```      | 同上，显示所有container，包括正在运行的(running)，停止运行的(stop)			| 
| ```docker ps -a -f status=exited```   		| 显示停止运行的(stop)container, f是筛选filter命令		| 
| ```docker ps -aq```     									| 显示所有的container，但只显示ID			| 
| ```docker rm <container ID/name>```       					| 删除一个或多个container			| 
| ```docker container rm <container ID/name>```       | 同上，删除一个或多个container			| 
| ```docker rm 'docker ps -aq -f status=exited'``` 		| 删除所有不在运行的（stopped）container（在win10 cmd中多次尝试未成功）			| 
| ```docker container prune``` 												| 同上，删除所有不在运行的（stopped）container			| 
| ```docker create <container ID/name>```   | 新建一个container			| 
| ```docker run -it <image>```     					| 新建一个container（是否进入命令模式由image预设命令决定，ubuntu image latest可进入）			| 
| ```docker run -it --name <new container name> <image>```	|  新建一个container，并对其命名			| 
| ```docker run -it --mount type=bind,source=<local directory to be mounted>,target=/<> <image>``` 	| 挂载本地文件（只能在新建container时），[更多信息](https://docs.docker.com/storage/bind-mounts/)			|  
| ```docker start <container ID/name>```    | 启动一个container（后台运行）			| 
| ```docker stop <container ID/name>```     | 停止运行一个container（后台停止）			|
| ```docker exec -it <container ID/name> /bin/zsh```    | 进入一个正在运行的container的zsh命令模式			| 
| ```docker exec -it <container ID/name> /bin/bash```   | 进入一个正在运行的container的bash命令模式			| 
| ```exit```      | 退出container命令模式			| 
| ```docker rename <container ID/name> <new name>``` 	| 在新建（run或create）未对container命名时，系统会自动生成名字，如要进入，则每次得查container id，rename命令可以将container name改成自己期望的名字			| 
