---
layout: post
title:  "BT PLDR"
date:  2021-01-15 10:52:10 +0800  
categories: blog
---

> PLDR 是 Windows 提供的一种自动重设蓝牙设备的技术。

任何设备都不能保证能一直无故障的运行，当遇到问题后，我们需要手动重启设备。蓝牙设备也一样，在长时间运行时，难免会出现设备报错、丢失、功能失效等问题。传统的解决方法就是重启电脑。

但从 Windows 10 1803 版本开始，微软为这些问题提供了一种更方便的解决方法：当设备出现问题时，自动重设设备，用户甚至感知不到。这项技术叫 [Bluetooth Radio Reset and Recovery](https://docs.microsoft.com/en-us/windows-hardware/drivers/bluetooth/bluetooth-radio-error-recovery)，它包括 FLDR 和 PLDR。为进一步巩固这项功能，微软要求从 21H1/21H2 开始，所有带蓝牙设备的机器必须支持。

#### 设备需重设的情况
* 总线错误：总线一般有 USB/UART 两种，错误时一般表现为蓝牙设备 YB。
* 驱动错误：一般出现在设备更新了新的 FW 或通信失败。
* FW 错误：一般是 FW 遇到了问题。

#### 如何实现
首先蓝牙设备需要是内置的，即连接在主板上的，USB Dongle 不支持。当然这项技术一般由厂商来支持，包括 Intel 和微软等。

Driver 和 BIOS 层面需要有相关代码，系统做侦测功能，侦测到错误后会发送重设指令给 BIOS，之后实现设备的断电并重新上电，从而实现设备的重设
