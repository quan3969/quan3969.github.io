---
layout: post
date:   2021-11-06 18:41:54 +0800
title:  "用 EDK II 编译 EFI Shell"
---

```
// 生成当前时间
date "+%Y-%m-%d %H:%M:%S"
```

## 前言

编译一个 EFI Shell 这个想法很早就有，但一直没有真正去做。如今工作岗位调整为 BIOS，再想搁置也不合情理，于是趁今天周末把它一口气做好。  

UEFI 本身东西很多，初学者如我，根本就不知道从何入手。关于 BIOS，工作中接触的最多便是刷 BIOS，每次刷 BIOS 都需要制作 EFI Shell 的启动盘，随后在里面敲入命令才可以刷。虽然不知道这命令含义，工具的用法，但 EFI Shell 已然成为我进入 BIOS 世界的入口。  

Intel 有自家维护的 UEFI 开源社区，和社区引以为傲的 tianocore，OEM/ODM 的 BIOS 代码不出意外也来自这。于是我便到 Github 上的 tianocore 组织寻找开源教程（Youtube 上也找过，但没有找到），整理了一些链接如下：  

[tianocore](https://www.tianocore.org/getting-started.html)  
[EDK II Docs](https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Documents)  
[Using EDK II with Native GCC](https://github.com/tianocore/tianocore.github.io/wiki/Using-EDK-II-with-Native-GCC)  
[Common EDK II Build Instructions for Linux](https://github.com/tianocore/tianocore.github.io/wiki/Common-instructions)  
[How to build OVMF](https://github.com/tianocore/tianocore.github.io/wiki/How-to-build-OVMF)  
[How to run OVMF](https://github.com/tianocore/tianocore.github.io/wiki/How-to-run-OVMF)  

## 编译
编译的过程大概分几步：  
1. 安装 Linux 和依赖环境
2. 配置 EDK II 编译环境
3. 修改配置文件开始编译

### 安装 Linux 和依赖环境
教程中支持 Windows 和 Linux 下的编译，出于方便，我选择了 Linux。  
教程中 Linux 用是 Ubuntu 的 16.04 LTS/16.10 版本，但我用 20.04 LTS 也可以编译通过。  
```
// 更新库
sudo apt update

// 安装依赖环境
sudo apt install build-essential uuid-dev iasl git nasm python3
```

### 配置 EDK II 编译环境
这一步把 github 上的文件拉取到本地编译。  
```
mkdir ~/src && cd ~/src
git clone https://github.com/tianocore/edk2.git
cd edk2
git submodule update --init

make -C BaseTools
. edksetup.sh
```

### 修改配置文件开始编译
配置文件位于 `Conf/target.txt`，修改以下：  
```
// 修改需要编译的文件
ACTIVE_PLATFORM       = ShellPkg/ShellPkg.dsc
TOOL_CHAIN_TAG        = GCC5
TARGET_ARCH           = X64
```

随后开始编译：  
```
build
```

编译完后，可以在 `Build/Shell/DEBUG_GCC5/X64/` 下找到我们需要的 `efi` 文件，这里是 `Shell_7C04A583-9E3E-4f1c-AD65-E05268D0B4D1.efi`，将此文件复制到 `FAT32` 的 U 盘 `EFI/Boot/` 文件夹下，并重命名为 `bootx64.efi` 即可运行当作启动 U 盘使用。  


## 测试
`tianocore` 还提供了一种虚拟机测试的环境 `OVMF`。安装的步骤有：安装 QEMU，编译 OVMF 环境，配置环境。

### 安装 QEMU
在 Linux 下安装；  
```
sudo apt install qemu-system-x86
```

### 编译 OVMF
方法同上，修改编译配置文件如下：  
```
// 修改需要编译的文件
ACTIVE_PLATFORM       = OvmfPkg/OvmfPkgX64.dsc
TOOL_CHAIN_TAG        = GCC5
TARGET_ARCH           = X64
```
编译后我们需要的 `OVMF.fd` 文件在 `Build/OvmfX64/DEBUG_GCC5/FV` 下。  
以我目前的理解，`OVMF.fd` 是最小的 UEFI BIOS 文件。  

### 配置环境
这一步在新的文件夹下进行。  
```
mkdir ~/run-ovmf && cd ~/run-ovmf
cp ~/src/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin

// 作为硬盘使用，后期可将 efi 文件放到这运行
mkdir hda-contents 

// 运行环境
qemu-system-x86_64 -pflash bios.bin -drive format=raw,file=fat:rw:hda-contents -net none
```

