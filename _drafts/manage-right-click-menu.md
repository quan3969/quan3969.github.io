---
layout: post
title:  "如何管理右键菜单项"
---

> 右键菜单项太多太杂？用 Autoruns 工具轻松清理。

本[教程](https://www.howtogeek.com/school/sysinternals-pro/lesson6/)用到的关键工具：

[Autoruns](https://docs.microsoft.com/en-us/sysinternals/downloads/autoruns)

这是一款非常强大的系统加载管理工具，它能帮助用户查看开机加载，右键菜单加载，IE 浏览器加载，运行加载等，总之任何系统需要加载的东西它都能列出来并进行修改。虽然软件本身已经将系统必要的加载项隐藏起来了，但在禁用任何一项加载项前，请先了解它的作用，以免造成系统的损坏。

Autoruns 由微软本部开发者开发，相对小众，但不影响它强大。我愿称它为 Windows 三板斧之一，另外两个分别是 Process Explorer 和 Process Moitor。本篇将介绍如何用它来管理右键菜单项。

直入主题：如何管理右键菜单项？
1. 用管理员身份打开 Autoruns 并找到 Explorer 项。

2. 找到你想禁用的菜单项并取消勾选即可，就这么简单~

但此工具似乎只检测 *.dll 文件的右键菜单项，像 VSCode *.exe 的启动并不能检测到。

### 实操
