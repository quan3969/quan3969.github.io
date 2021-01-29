---
layout: post
title:  "原版 WinPE 显示中文"
date:  2021-01-29 16:50:10 +0800  
categories: blog
---

> 如何在官方原版 WinPE 环境下，运行带有中文字符的脚本而不显示乱码。

原版 WinPE 一般是英文不带任何驱动或组件的，启动后就只有简单的 CMD。

要想显示中文字符或运行带有中文字符的脚本文件，一般需要满足三个条件：添加中文包，脚本文件以 GBK 格式保存，CMD 页面设置成支持中文。

#### 添加中文包

Mount WinPE 镜像后，用 DISM 工具添加：

语言包

```
Dism /Add-Package /Image:"C:\WinPE_amd64\mount" /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\zh-cn\lp.cab" 
```

字体包

```
Dism /Add-Package /Image:"C:\WinPE_amd64\mount" /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-FontSupport-ZH-CN.cab" 
```

#### 另存为 GBK 编码格式

GBK 是简体中文的编码格式。

如果使用中文版的 Windows 和自带的记事本，只要把字体脚本设置成“中文 GB2312”，并另存为 ANSI 格式即可。

![gbkNotepad](/assets/img/winpe-ch-cn/gbkNotepad.gif)

非中文版的系统可以借助第三方文字编辑器另存为 GBK 格式。如 VSCode 就可以以 GBK 格式保存或打开。

![gbkVSCode](/assets/img/winpe-ch-cn/gbkVSCode.gif)


#### 设置 CMD 页面字体

CMD 默认启动的页面字体会根据系统语言来配置，对于 WinPE，即使添加了中文字体也会以英文字体启动。

可用 [CHCP](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/chcp) 命令设置页面字体。英文 437，简体中文 936。

```
chcp 936
```

![cmdChcp](/assets/img/winpe-ch-cn/cmdChcp.gif)
