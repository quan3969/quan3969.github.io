---
layout: post
title:  "Ryzen 5 5600X 平台超频"
date:   2021-01-06 13:53:19 +0800
categories: blog
---

> 双十二入的 AMD YES! 香是真香，台式机打游戏可比笔记本好太多啦~

本文包括平台介绍、CPU 测试、内存测试和购买心得四部分。阅读本文，你可以获得购买电脑的一些建议，以及如何简单超频以获得最大化的性能。

## 平台介绍
这是博主在 2020.12.12 在天猫购入的组装主机，总共花费 7698 大洋。

配置如下：

| 部分 | 型号 |
| --- | --- |
| CPU | AMD Ryzen 5 5600X |
| 散热 | 九州风神玄冰 400 |
| 主板 | 华硕 TUF B550M GAMING PLUS (WiFi) |
| 显卡 | 影驰 GeForce RTX 3060Ti 8G 金属大师 OC |
| SSD | WD_BLACK SN850 500G NVMe |
| 内存 | 影驰 星耀 16G 3200 DDR4 (8*2) RGB 水晶内存 |
| 机箱 | 九州风神 MACUBE 魔方 110 / 黑色 |  
| 电源 | 鑫谷 GP700G 黑金版 600W / 金牌电源 |

这套配置在当时可谓是非常香了，因为 CPU 和显卡在当时，可是非常难买到的。如今又遇上了比特币矿潮，热门 3060ti 更是从原来的 2999 炒到了 4200+，想再以这样的价格买到配置可不容易。博主十分幸运买的早，但愿 2021 年 PC 行业能不缺货吧。

超频、更改 BIOS 设置可能导致系统无法启动。启动失败时不用慌张，断开电脑电源，清除主板 CMOS即可，最简单的做法把主板上的电池扣下来再重新装上。

当然有些主板厂商非常贴心，设置了清 CMOS 的跳针，将跳针短路也能起到清 CMOS 的作用。把跳针接到机箱上的 RESET 键上，就更方便不过了。

### 用到的工具
* [ZenTimings](https://zentimings.protonrom.com/) 
* [AIDA64](https://www.aida64.com/) 
* [MemTest86](https://www.memtest86.com/)

### 性能测试

* 3DMark 

 ![3DMark](/assets/img/2021-01-06-5600x-overclocking/3DMark.gif) 

* 3DMark 11 

![3DMark11](/assets/img/2021-01-06-5600x-overclocking/3DMark11.gif) 

* 鲁大师（新）

![LudashiNewBenchmark](/assets/img/2021-01-06-5600x-overclocking/LudashiNewBenchmark.gif) 

* 鲁大师（旧）

![LudashiBenchmark](/assets/img/2021-01-06-5600x-overclocking/LudashiBenchmark.gif) 

* CineBench R20

![CpuCinebench](/assets/img/2021-01-06-5600x-overclocking/CpuCinebench.gif)

* 内存

![memoryBenchmark](/assets/img/2021-01-06-5600x-overclocking/memoryBenchmark.gif)

* 硬盘

![SSDBenchmark](/assets/img/2021-01-06-5600x-overclocking/SSDBenchmark.gif)

* CSGO FPS Benchmark

![csgoBenchmark](/assets/img/2021-01-06-5600x-overclocking/csgoBenchmark.gif)


## CPU 测试
AMD Ryzen 5000 Series 官方参数
Cores / Threads	Clock speed/turbo (GHz)	Cache (total)	PCIe lanes 

| Cores / Threads | 6 / 12 |
| Clock speed/turbo (GHz) | 3.7 / 4.5 |
| Cache (total) | 3MB(L2), 32MB(L3) |
| PCIe lanes | 40 |
| Default TDP / TDP | 65W |
| Max Temps | 95℃ |
| Launch Date | 11/5/2020 |

### CPU 跑分
不得不说，这次 AMD 出货前就几乎把每一颗 CPU 的性能都榨干了，留给玩家超频的空间并不大。据 3DMark 和鲁大师跑分榜来看，超频到 5GHz 的少之又少。这种做法没什么不好，用户拿到不怎么用折腾就能获得不错的性能。

#### 默认频率
默认频率基本不需要多设置，打开 BIOS，Load default 就能获得，普通用户做完这一步，再把内存的 XMP 文件读取出来并保存就能进行日常使用了。

#### PBO2 自动超频
做法：主板自带的超频设置设为自动，在 AMD Overclock 中打开 PBO 的高级，将 Offset 设置到 200Mhz，将功耗墙解除，温度墙解除即可，主板会根据 CPU 的需要调节电压。

### 系统压力测试
CPU 和 GPU 双烤 30 min 后，如果不出现降频、黑屏死机等说明散热没问题，同时注意最高功率，对配备的电源是否有压力。

CPU 烤机用 AIDA 自带的压力测试，GPU 烤机用 Furmark 甜甜圈测试。


## 内存测试
Zen3 与 Zen2, Zen2+ 在内存频率的支持上大致相同，只要内存能往上，CPU 就没问题。

其中 3733Mhz 是分水岭，3733Mhz 之前内存频率比是 1:1，之后则是 2:1。直观的看就是读取虽然上去了，但时延却增加了。因此最佳内存频率应为 3733MHz。

### 内存跑分
#### 默认 XMP
(3200c16-18-18-38@1.35V)

#### 超频 3733
(3733c16-18-18-16@1.36V)

#### 超频 3600
(3733c16-18-18-36@1.35V)

注意：不同软件版本之间可能存在差异，结果仅供参考。

在这之前，先介绍一款锐龙平台，免费开源的内存时序查看工具 [ZenTimings](https://zentimings.protonrom.com/)。这款工具能更详细的看到内存的时序信息，但仅限 AMD 锐龙平台，Intel CPU 无法使用。

### 内存稳定性测试
内存超频后能正常开机，并不意味着超频的完成，频率和电压的不稳定会带来电脑的工作不稳定，如游戏闪退，程序报错，蓝屏死机等。

因此还需要对超频后的内存进行稳定性测试，测试软件 [MemTest86](https://www.memtest86.com/)。这是一款 UEFI 环境下运行的软件，自带中文，包含各式各样的测试项，单轮测试大概花费 40 分钟，完整一次压力测试需要 4 轮，总耗时近 3 小时。此外内存的测试还带来巨大 CPU 的使用率，对 CPU 稳定性也是一种考验。
![Memtest86]()

当然如此严苛的测试能通过，也意味着电脑长期稳定的工作在此状态也不在话下。因此建议此测试顺序放在其他硬件压力测试都通过之后。

但这似不是最好的稳定性测试方法，我的内存超频 3733 后的能跑过 Mentest86 不报错，进系统也不会报错。但运行《赛博朋克2077》 5 分钟就会闪退。这才意识到这个频率并不稳定。经过一番折腾最后发现 3600 频率才是稳定频率。

因此内存稳定测试还需结合高负载游戏来测试，跑 PUBG 录像就是一种不错的方法，3 轮跑下来如果还问题说明稳定性有保障。


## 购买心得
通过此次超频，电脑性能获得了 10% 的提升。像我这种臭打游戏的， 高刷新率、高配置和好的外设非常重要。

对于 CSGO 这款游戏，CPU 的单核性能影响非常大。

对于 PUBG 则是内存的性能影响跟高。

购买 PC，首先考虑的还是性价比。我原来的电脑是 2015 年买的笔记本，跑分 100%，花费 6300。而如今过了 5 年，2020 年，1000% 的性能，花费 10000。这中间性价比从“16”涨到“100”，相当值，下一次换电脑如果能达到“600”，即 6000% 的性能，花费 10000。让我们共同期待。

对于下一次买电脑，我首先会到评测网站 [guru3d](https://www.guru3d.com/) 调查一番再做决定。

对于 CPU 最重要的当然是 IPC，即同频率性能，其次再看它所能达到的最高频率。这些比较完后，再比较价格、功耗、发热量等。

对于显卡，当然是最求性价比，从老黄的显卡来看，xx60 系列是最香的。
