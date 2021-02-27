---
layout: post
title:  如何解决github访问慢的问题
author: Bruce Liu
#last update date
date:   2021-02-28 00:50:00 +0800
#first published date
published: 2021-02-28 00:50:00 +0800
categories: [post]
tags: [github, China]
description: 
header-image: 
permalink: /fasten-github/
---
最近回到国内，不知什么原因，访问Github时出现“无法下载release”、“克隆速度慢”、“raw文件无法查看”等问题。网上搜索后发现还有很多网友也碰到这一问题。在此梳理下解决方法。
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

以[voronoi-diagram-for-polygons]项目为例

项目链接：<https://github.com/longavailable/voronoi-diagram-for-polygons>

克隆命令：`git clone https://github.com/longavailable/voronoi-diagram-for-polygons.git`

release链接：<https://github.com/longavailable/voronoi-diagram-for-polygons/archive/v0.1.1.zip>

raw链接（示例）：<https://raw.githubusercontent.com/longavailable/voronoi-diagram-for-polygons/master/docs/pics/outputs.png>

# 国内镜像加速

## [fastgit.org]

作用：加速访问；加速克隆；加速release下载

使用方法：将`github.com`替换为`hub.fastgit.org`即可加速。

项目加速链接：<https://hub.fastgit.org/longavailable/voronoi-diagram-for-polygons>

加速克隆命令：`git clone https://hub.fastgit.org/longavailable/voronoi-diagram-for-polygons.git`

release加速下载链接：<https://hub.fastgit.org/longavailable/voronoi-diagram-for-polygons/archive/v0.1.1.zip>

raw加速访问链接：<https://raw.fastgit.com/longavailable/voronoi-diagram-for-polygons/master/docs/pics/outputs.png>


## [github.com.cnpmjs.org]

作用：加速访问；加速克隆；加速release下载

使用方法：与[fastgit.org]相似，将`github.com`替换为`github.com.cnpmjs.org`即可加速。


## [gitclone]

作用：加速克隆

使用方法：将`https://github.com`替换为`https://gitclone.com/github.com`即可加速。

加速克隆命令：`git clone https://gitclone.com/github.com/longavailable/voronoi-diagram-for-polygons.git`


## [7ed.net GRA]

作用：加速raw访问

使用方法：将`raw.githubusercontent.com`替换为`raw.sevencdn.com`。

raw加速访问链接：<https://raw.sevencdn.com/longavailable/voronoi-diagram-for-polygons/master/docs/pics/outputs.png>

## [gh.api.99988866.xyz]

作用：加速release下载；加速文件下载

使用方法：拷贝相应链接到该网站进行下载。

## [toolwa.com/github]

作用：加速release下载；加速文件下载

使用方法：拷贝相应链接到该网站进行下载。

## [d.serctl.com]

作用：加速项目下载/克隆；

使用方法：拷贝相应链接到该网站进行下载。

# 修改hosts文件

参考[国内加速访问Github的办法，超级简单](https://blog.csdn.net/qianglei6077/article/details/90051554)。

# 码云（Gitee）曲线加速

利用Gitee的“从github导入仓库”功能，再从Gitee克隆到本地。

# 参考/References

- [Github国内mirror加速](https://blog.csdn.net/networken/article/details/105122778)
- [国内加速访问Github的办法，超级简单](https://blog.csdn.net/qianglei6077/article/details/90051554)
- [一招搞定GitHub下载加速](https://zhuanlan.zhihu.com/p/112697807)
- [IPAddress.com](http://ipaddress.com/)


[voronoi-diagram-for-polygons]: https://github.com/longavailable/voronoi-diagram-for-polygons
[fastgit.org]: https://doc.fastgit.org/en-us/#about-fastgit
[gitclone.com]: https://www.gitclone.com/
[github.com.cnpmjs.org]: https://github.com.cnpmjs.org/
[7ed.net GRA]: https://7ed.net/gra/
[gh.api.99988866.xyz]：https://gh.api.99988866.xyz/
[toolwa.com/github]: https://toolwa.com/github/
[d.serctl.com]: https://d.serctl.com/






