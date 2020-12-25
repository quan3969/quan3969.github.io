---
layout: post
title:  "Windows 注册表"
date:   2020-12-25 14:23:19 +0800
categories: blog
---

> 文章参考了许多网络上的资文献，所引用的文献地址可在文章中找到。阅读本文你可以理解 Windows 注册表是什么，注册表的用途以及实用注册表技巧。

## 简介 

### 注册表
Windows 注册表存储了系统和用户的配置信息，通过添加或删除它们，可以达到调整系统设置的目的，包括可以找到的和隐藏的设置项。

删除无用的注册表信息不会带来系统性能的提升，但错误的删除可能会导致系统的损坏，因此修改注册表前请[创建系统还原点](https://www.howtogeek.com/howto/windows-vista/create-a-restore-point-for-windows-vistas-system-restore)。 

注册表信息存储在 *`C:\Windows\System32\config`* 下，可通过 *`Win+R`* 并运行 *`regedit`* 打开注册表编辑器。 

### 注册列表项目 
> [查看原文](https://www.howtogeek.com/school/using-windows-admin-tools-like-a-pro/lesson5) 

1. HKEY_CLASSES_ROOT (HKCR) 
管理文件类型关联，关联到 *`HKLM\Software\Classes`* 
管理右键菜单项目 

2. HKEY_COUURENT_USER (HKCU) 
存储当前用户的设定值，关联到 *`HKEY_USERS\<SID-FOR-CURRENT-USER>`* 
最常用到 HKCU\Software 

3. HKEY_LOCAL_MACHINE (HKLM) 
存储系统设置，最常用到 HKLM\Software 

4. HKEY_USERS (HKCU) 
存储系统所有用户的设置 

5. HKEY_CURRENT_CONFIG 
存储当前硬件配置的信息，关联到 *`HKLM\SYSTEM\CurrentControlSet\Hardware\Profiles\Current`*

### 关键词和值 (Keys and Values) 
Keys 是带有文件夹图标的项目，在注册表的左边 
Valuses 在注册表的右边，包括 6 种类型，新建后需要起名字 

### 创建注册表

新建文本文件，添加注册表版本信息和需要修改的注册信息，保存后修改后缀为 *.reg。
```C 
Windows Registry Editor Version 5.00

["Key"]
"Name"=Type:Value
```
> 注意：不当操作可能会导致系统损坏，修改注册表前请[创建系统还原点](https://www.howtogeek.com/howto/windows-vista/create-a-restore-point-for-windows-vistas-system-restore/)。 

## 实用注册表 

### 修改“资源管理器”指向 
> [查看原文](https://www.tenforums.com/tutorials/3734-open-pc-quick-access-file-explorer-windows-10-a.html?__cf_chl_jschl_tk__=f038edee01e75069ec4ea6fe51c19c85c246e16c-1608183512-0-ARJ23MuUsgHY_DTUSSbz2Hfa4PEok6bJV1CgGSukL9Ko-NvtKFzLHT_6ioL5LYDsATBPCc_Y7LLJhw6DO2ZNKvkoj8o-pxNCh4UaCI4-BNwr0jje1K6gRwOMflQe-UjGRBEGJbgvBDBpcKDV-7vqfukXWYhl_3t-1sWSKCgsVKP1OYXFsfNzj2ERrIjz8a9YC78hcWLIzvZyqn_42qsk6TxKL1sIBpwVEDKprfqXMrvEQeSVmG7CqMwHpxEre47sJ1jnd8Frv35dg31mjzaYKOFjEwXbZ0AaJI0AcFNorLooiaQc14QbglMHupbQrm4aYt9rOAid2S3puqftwpzCvVN_YMnN1YmopZQr-wWrrVEnKcQi3q5JxnY8W7zNOxD-g_5MUdxaj3VCYYM3xRUcfMg) 

- 1 = "This PC" 
- 2 = "Qucik access" (Defualt) 
- 3 = "Download" 
```C 
[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced]
"LaunchTo"=dword:00000001
```

### 禁用“Windows Defender” 
- 1 = Disable 
- 0 = Enable (Default) 
```C
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender]
"DisableAntiSpyware"=dword:00000001
```

### 禁用摇晃最小化 
- 1 = Disable 
- 0 = Enable (Default) 
```C
[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced]
"DisallowShaking"=dword:00000001
```

### 禁用锁屏界面 
- 1 = Disable 
- 0 = Enable (Default) 
```C
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Personalization]
"NoLockScreen"=dword:00000001
```
 
### 隐藏开始菜单的“最近添加” 
> [查看原文](https://www.tenforums.com/tutorials/104828-enable-disable-recently-added-apps-start-menu-windows-10-a.html#option2s3) 

- 1 = Disable 
- 0 = Enable (Default) 
```C
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer]
"HideRecentlyAddedApps"=dword:00000001
```

### 禁用“Xbox Game Bar” 
- 1 = Enable (Default) 
- 0 = Disable 
```C
[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\GameDVR]
"AppCaptureEnabled"=dword:00000000
```

## 管理右键菜单项 

### 鼠标所点位置 
1. [文件夹与文件共有](https://www.howtogeek.com/howto/windows-vista/how-to-clean-up-your-messy-windows-context-menu) 
HKCR\*\shell' 
HKCR\*\shellex\ContextMenHandlers 
HKCR\AllFileSystemObjects\ShellEx 

2. [文件夹](https://www.howtogeek.com/howto/windows-vista/how-to-clean-up-your-messy-windows-context-menu) 
HKCR\Directory\shell 
HKCR\Directory\shellex\ContextMenuHandlers 

3. [特定文件后缀，如 .xlsx](https://www.howtogeek.com/howto/windows-vista/how-to-clean-up-your-messy-windows-context-menu) 
 HKCR\\\*.xlsx\ 下找到指定名字，目录则为 *`HKCR\Excel.Sheet.12\shell`* 

4. [“用其他方式打开”项目 ](https://www.howtogeek.com/howto/18119/remove-programs-from-open-with-menu-in-explorer)
HKCR\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FileExts 

5. [“发送到”项目 ](https://www.howtogeek.com/howto/windows-vista/customize-the-windows-vista-send-to-menu/) 
*`HKCR\AllFilesystemObjects\shellex\ContextMenuHandlers\Send To`* 
添加或删除 [7BA4C740-9E81-11CF-99D3-00AA004AE837](https://www.howtogeek.com/howto/windows-vista/disable-the-send-to-folder-on-the-windows-explorer-context-menu) 可使能或失能“发送到”目录 
该目录下的选项在 *`C:\Users\Q3an.Odin\AppData\Roaming\Microsoft\Windows\SendTo`* 中，可用 shell:sendto 打开 

### 禁用菜单项 
1. 项目在 *`HKCR\Directory\shell`* 下 
此目录下的项目通常出现在右击文件夹 
添加 *`"String": "LegacyDisable"`*，此时项目被禁用 
添加 *`"String": "Extended"`*，此时项目被移动至 `"Shift + right-click"` 中 
2. 项目在 *`HKCR\Directory\shellex\ContextMenuHandler`* 下 
此目录下的项目通常出现在按住 Shift 右击文件夹 
更改项目下的 (Default) 的值 
3. 项目在特定文件后缀下，如 *`HKCR\*.xlsx`* 
此目录下中找到指向的目录 *`HKCR\Excel.Sheet.12\shell`* 
禁用方法和上述相同 

### 添加菜单项 
在 shell\ 下添加新的 key ([Notepad](https://www.howtogeek.com/howto/windows-vista/add-any-application-to-the-desktop-right-click-menu-in-vista))  
添加新的 key (command) 
command 下的 (Default) 中添加 path (*`"c:\windows\system32\notepad.exe"`*) 

