---
layout: post
title:  "如何找到某个设置对应的注册列表"
date:  2021-01-06 19:54:34 +0800  
categories: blog
---

> 找到该设置的注册列表，创建它的注册表注册文件，完成简单漂亮的一键设置！

本[教程](https://www.howtogeek.com/school/sysinternals-pro/lesson5/)用到的关键工具：

[Process Monitor](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon)

步骤如下：

1. 打开 promon64.exe 的监测功能

2. 改变设置，例如：打开 -> 关闭 

3. 关闭 promon64.exe 的监测功能 

4. 添加过滤条件：Operation: RegSetValue 

5. 在过滤过后的项目中找关键字

6. 跳到注册表，确认是否对应：改变设置并按 F5 刷新，看值是否改变

### 实操
#### 一键开关蓝牙设备
要找的设置值如下图所示：

![setting](/assets/img/2021-01-06-find-registry-hacks/setting.gif)

操作步骤 1~4 找到关键信息：

![promon](/assets/img/2021-01-06-find-registry-hacks/promon.gif)

关闭/打开设置，值的确改变，说明正确找到，接下来导出注册表文件

![regedit](/assets/img/2021-01-06-find-registry-hacks/regedit.gif)