---
layout: post
title:  How to change the color of first word in Windows PowerShell
author: Bruce Liu
# last update date
date:   2020-02-28 13:30:00 +0100
# first published date
published: 2020-02-28 13:30:00 +0100
categories: [post]
tags: [PowerShell, cmder]
description: 
header-image: 
permalink: /first_word_color_ps/
---
By default, the color of first word in PowerShell is yellow. Sometimes it is not visible, especially when you changes the text background color.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->
See the output first.

<div align="center"><img width="900" src="/assets/pics/powershell01.png"/></div>

<br>
How to make it?

As shown in the above picture, type the command in your terminal directly. While it is one-time effective.

```shell
Set-PSReadlineOption -TokenKind Command -ForegroundColor Black
```

Place it in your `profile` and it will run when you launch PowerShell.

- If it is the first time you set your $profile, you have to enable running unsigned scripts.

	```shell
set-executionpolicy remotesigned
	```
	
	Then, add this script.
	
	```shell
'Set-PSReadlineOption -TokenKind Command -ForegroundColor Black' `
|Add-Content $Profile
	```

- Alternatively, you can add the followings to `Microsoft.PowerShell_profile.ps1` located in `C:\Users\<username>\Documents\WindowsPowerShell` by yourself.

```shell
Set-PSReadlineOption -TokenKind Command -ForegroundColor Black
```

- If you use some 3rd party terminal, such as [ConEmu](https://conemu.github.io/). You have to change the corresponding `profile.ps1`.

<br>

# Reference:

- [Set-PSReadLineOption](https://stackoverflow.com/a/43015533/12371819)
- [set-executionpolicy](https://superuser.com/a/106363)
