---
layout: post
title:  "Windows S Mode 介绍"
date:  2021-01-19 13:24:54 +0800  
categories: blog
---

> 如果说 Windows 就如安卓一般可让用户自定义，那 Windows S Mode 就是 iOS，不能随意修改，但运行速度飞快。

### 什么是 Windows S Mode

[Windows S Mode](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-10-s-overview ) 下软件只能通过微软商店下载，浏览器使用 Edge，搜索引擎默认 Bing 并且不能修改，命令行、注册表和脚本文件等不能运行，但好处是所有的软件和驱动都是通过验证的，不会使得系统速度不会被拖慢，病毒不会误运行。S Mode 可随时切换为普通的模式，但此操作不可逆。

### S Mode 发展历史

* 1703 (RS2) 首次公布，并通过一个单独镜像安装，取名 Windows 10 S 

* 1709 (RS3) 和其他版本镜像集成，S edition 

* 1803 (RS4) 更名为 S Mode，所有版本都可以使用 

* 1809 (RS5) 可以单独改为 S Mode 

### 如何进入 S Mode

* 将 wim 镜像 mount 出来
* 新建 Panther 文件夹并将 S Mode 的 [unattend.xml](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-10-s-enable-s-mode ) 文件放入 
* 运行 DISM 命令 
```
dism /image:C:\mount\windows /apply-unattend:C:\mount\windows\windows\panther\unattend.xml 
```

### unattend.xml 

部署一般分为 [7 个步骤](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#customize-windows-with-an-answer-file )
1. windowsPE 这部分可以用来修改 Windows 的安装盘文件 

2. offlineServicing 镜像 mount 后的修改，常见用于修改 S Mode 

4. specialize 镜像 apply 后的修改，常用于添加更新，添加驱动 

6. auditUser 进入审计模式时做修改

7. oobeSystem 进入解封装模式时修改，但改自动进入审计模式时例外 
