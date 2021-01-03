---
layout: post
title:  "安装原版 Windows"
date:   2020-12-26 15:29:49 +0800
categories: blog
---
> Windows 随着使用时间变长，积累的冗余文件变多，程序和服务变多，这就导致电脑的运行速度变慢。此时重装系统就能获得原本飞快的体验。

### 制作安装盘 
#### 下载最新镜像
网上有许多定制版的 Windows 镜像资源，它们大致可归类为两种， Ghost 版和 Wim 版。Ghost 版是用户自由定制化的二次打包版本，安装方法一般为磁盘安装，Dos 启动；Wim 版则是用户通过离线注入的方式进行定制化，安装方法为软件安装，支持 DOS/UEFI 启动。

官方原版镜像看作是 Wim 原滋原味版本，启动方法也用推荐 UEFI。

下载地址：
1. [微软官方](https://www.microsoft.com/en-us/software-download/windows10) 可下载英文原版镜像，制作方便。

2. [I Tell You](https://msdn.itellyou.cn/) 旧版网址，可下载中文原版镜像，已停止更新，最终版本 1909。

3. [I Tell You](https://next.itellyou.cn/) 新版网址，需要登陆账号，作者持续更新。

#### 导入文件 
1. 准备一个 8G 以上 U 盘并格式化成 FAT32 的格式。

    （*UEFI 只 FAT32 格式的启动，如果使用 NTFS, exFAT启动，需要在 BIOS 中更改设置。* ） 

    ![FormatDisk](/assets/img/2020-12-26-install-clean-windows\2020-12-26-format.gif)

    如果 U 盘大小超过 32G，可能会导致无法格式成 FAT32 格式，有以下两种解决方法：
    1. 格式化成 NTFS 格式，并用非 UEFI 的方法启动。
    2. 用第三方硬盘工具软件，这里推荐 [DiskGenius](https://www.diskgenius.cn). 它包含免费版本，不管多大容量，能轻松格式化成 FAT32 格式。

2. 把镜像里所有文件复制到 U 盘根目录下。若提示有个文件大于 4GB 不可复制，则进行镜像分割。

3. 至此，安装盘制作完成。完成后的安装盘依然可以存放个人文件的，只要不更改原来的东西。

#### 镜像分割 
1. 将镜像目录下 .\sources\install.wim 复制到 C 盘根目录下 

2. 在 C 盘根目录下以管理员的身份运行命令行 

    ![RunAsAdmin](/assets/img/2020-12-26-install-clean-windows/2020-12-26-run-as-admin.gif)

3. 运行以下命令分割镜像 
    ```c
    dism /split-image /imagefile:install.wim /swmfile:install.swm /filesize:2048
    ```
    ![DismSplitImage](\assets\img\2020-12-26-install-clean-windows\2020-12-26-dism-split-image.gif)

4. 将分割完的文件复制到 U 盘 .\sources 下 
    ![InstallSwm](\assets\img\2020-12-26-install-clean-windows\2020-12-26-install-swm.gif)

### 安装 Windows
1. 在 BIOS 中选择 U 盘启动
    1. FAT32 可直接选择 U 盘 UEFI 启动
    2. NTFS, exFAT 更改 boot 设置为 CSM/Legacy 后再选择 U 盘启动

2. 按提示选择自定义安装，并将目标硬盘的全部分区删除
    ![OptionSetupCustom](\assets\img\2020-12-26-install-clean-windows\2020-12-26-option-setup_custom.gif)
    ![Windows10Setup](\assets\img\2020-12-26-install-clean-windows\2020-12-26-windows10-step.gif)

3. 等待安装完成后，系统会自动重启并开始配置用户信息，推荐使用离线账户