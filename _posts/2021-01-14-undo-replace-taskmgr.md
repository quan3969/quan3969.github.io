---
layout: post
title:  "如何取消替换任务管理器"
date:  2021-01-14 16:05:20 +0800  
categories: blog
---

> 在 Process Explorer 中设置了取代系统任务管理器，却没有方法设置回去了？本文帮助恢复原来的设置。

Process Explorer 是 Windows 管理工具三板斧之一，其功能十分强大，它在系统内置管理器的基础上加上了 DLL 查看器、任务树、堆栈查看、TCP 连接查看等众多功能。

但在替换系统默认任务管理器后，日常使用反而觉得功能太多，信息太多太杂了。比如想要找到前排某个软件关闭要在众多任务中逐个逐个找、没有管理员权限查看网络流量信息等。

所以对于日常使用来说，系统默认的任务管理器会更方便。Process Explorer 适合在排错或者查找详细信息时使用更合适。

![replaceTaskmgr](/assets/img/undo-replace-taskmgr/replaceTaskmgr.gif)

回到标题，如何取消替换任务管理器呢？我尝试在 Autoruns 中找它的注册信息，但遗憾未能成功。最后在网上找到这篇[博客](https://bianchengnan.gitee.io/articles/replace-task-manager-with-process-explorer/)。

替换系统任务管理器，其实就是在 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\taskmgr.exe` 下添加了一个 Debugger 这个值指向 Process Explorer。用户打开任务管理器时，系统会先判断有没有这个 Debugger，有则打开。

![registryTaskmgr](/assets/img/undo-replace-taskmgr/registryTaskmgr.gif)

因此我们只需要将这个注册列表删除即可。