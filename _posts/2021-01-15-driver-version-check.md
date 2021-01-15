---
layout: post
title:  "检测所安装的驱动版本"
date:  2021-01-15 20:08:05 +0800  
categories: blog
---

> 安装驱动后和更新驱动前都有关键的一步，检测当前的驱动版本。手动检查驱动版本固然简单，但如何用程序或命令行检查版本信息呢？

安装驱动主要有两种方法，Setup 安装和 PnPUtil 安装。

Setup 安装一般通过厂商提供的安装包（“下一步，下一步，完成”）来安装，这样的安装有时会伴随厂商的一些自定义，包括将版本信息注册到特定的注册列表。

PnPUtil 安装的情景有很多，包括用户在设备管理器中搜索安装、命令行安装、WU、右键 *inf 文件 Install 等。这些安装一般不含厂商的自定义，安装动作一致并由系统决定。

### MEI 驱动

#### Setup 安装
Setup 安装包目录下非常简洁，因为驱动文件都被压缩并包在 Setup 文件中了，解压后便可找到。

![meiSetup](/assets/img/driver-version-check/meiSetup.gif)

对于 MEI 的驱动，安装后的版本信息非常好找：`HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Intel\ME`.

![meiSetupReg](/assets/img/driver-version-check/meiSetupReg.gif)

#### PnPUtil 安装
Pnputil 的安装目录下一般不含可执行文件，但会有 *.inf 文件，这是驱动安装的必要文件。右键点击会出现“安装”的选项。

![meiPnp](/assets/img/driver-version-check/meiPnp.gif)

但这种方法安装后的注册信息放在哪里了呢？

通过不断寻找（花费将近一下午），终于找到了：

`HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{4d36e97d-e325-11ce-bfc1-08002be10318}` 

对于 MEI 驱动，它还存在一个特定的 *.sys 文件：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Publishers\{e1da8995-85bc-452b-b62b-0913306a430e}`

![meiPnpReg](/assets/img/driver-version-check/meiPnpReg.gif)

从这个目录得知它所安装的位置，随后再通过如下命令得知其版本信息，这也是驱动的版本信息：

```
wmic datafile where "Name= 'c:\\windows\\System32\\DriverStore\\FileRepository\\heci.inf_amd64_2b46c98546456811\\x64\\TeeDriverW10x64.sys'" get Version
```

#### 引申

对于 PnPUtil 的实现方法暂时未知，但可以推测，这个目录应该是我们打开“设备管理器” -> “按连接列出设备” -> “基于 ACPI x64 的电脑” -> “Microsoft ACPI-Compliant System” 下的设备。

![deviceMgr](/assets/img/driver-version-check/deviceMgr.gif)

恰好这个目录下包含了我们所关心的一般设备。因此通过咨询注册列表我们便可获得所有驱动的信息：

```
reg query HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\{4d36e97d-e325-11ce-bfc1-08002be10318} /s
```

同时设备管理器中的所有设备的硬件信息都能在如下目录中找到：

`HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\DeviceContainers\{00000000-0000-0000-FFFF-FFFFFFFFFFFF}\BaseContainers\{00000000-0000-0000-FFFF-FFFFFFFFFFFF}`

这时我们便可以通过以下命令判断电脑是否包含某个设备：

```
reg query HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\DeviceContainers\{00000000-0000-0000-FFFF-FFFFFFFFFFFF}\BaseContainers\{00000000-0000-0000-FFFF-FFFFFFFFFFFF} /s | find "PCI\VEN_8086&DEV_02E0"
```

知道以上方法后，便能实现以下功能：

1. 安装驱动：
    1. 获取硬件信息
    2. 判断是否存在某个设备，存在则安装，不存在则结束
2. 更新驱动：
    1. 获取硬件信息
    2. 判断是否存在某个设备，存在则下一步，不存在结束
    3. 获取所有驱动信息并检测这个设备，不存在或版本低则安装，否则则结束
