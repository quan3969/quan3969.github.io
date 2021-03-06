---
layout: post
date:   2021-01-30 19:27:11 +0800
title:  "CS:GO 自动配置"
permalink: /csgo
---
> “工欲善其事，必先利其器”，好的设置能让你在 CS:GO 比赛中获得更好的发挥。

本文分为五部分：常用指令、文件说明、游戏设置、视频设置和创意工坊地图推荐。

注意：此 CSGO 自动配置文件并 **不是外挂**，只是帮助玩家自动设置游戏，免去为了每次换机器或重装游戏后都要重新配置的烦恼。

**[下载最新版本](https://github.com/quan3969/csgo_auto_config/archive/main.zip)**

### 使用方法
1. 解压下载到的配置文件，并放在 `X:\Steam\userdata\yourID\730\local\cfg` 下，提示文件重复时，选择全部替换
2. 添加游戏启动项：`+exec auto.cfg`
	![startup](assets/img/2020-12-29-csgo-auto-script/startup.gif)
3. 运行游戏并在命令控制台中输入 auto
![ms](assets/img/2020-12-29-csgo-auto-script/ms.gif)
![kb1](assets/img/2020-12-29-csgo-auto-script/kb1.gif)
![kb2](assets/img/2020-12-29-csgo-auto-script/kb2.gif)
![kb3](assets/img/2020-12-29-csgo-auto-script/kb3.gif)

### 更新日志
* 2021.01.02
  * 分辨率改为 1440*1080，准星优化并放在 chr3 中。
  * 最大刷新率放开了，的确能感觉到有区别，于是灵敏度也改低到 0.35.

* 2021.01.30
  * 允许好友加入我的游戏，即使我在练枪、跑图服务器。
  * 调低灵敏度到 0.4.
  * 去掉了按 f 顺便清血渍。
  * 将 CAPSLOCK 键的“跳投”改为“快速切闪”，这个会比一直按切闪光弹快，适合快速打双闪。
  * dis 快速断开连接。
  * 取消了 F1~F3 切换道具。
  * 添加新的组合键：鼠标侧键 + 特定按键（q火，f烟，4雷，r诱饵，g丢c4），感谢 [BananaGaming](https://settings.gg/player/24801023)。
  * 添加 PgDn 键快速开/关游戏声音，练枪或特殊情况时用。
  * 导入了新的持枪视角，适合 4:3 拉伸。
  * prt 允许更多玩家同时在一个队伍。

* 2021.01.19
  * 由于游戏更新，多人游戏中 Bot 不再动作。因此移除了 practiceBot。
  * 去掉了投掷物准星，因为用的太少了。
  * 调低灵敏度到 0.45.
  * "z" 唤出雷达消息改为传统。
  * 增加了新准星，如今有 3 个准星，并且运行 auto 不再覆盖准星。
  * 取消按 "E" 进购买菜单。
  * F1~F3 分别改为烟、火、诱饵。
  * 默认改为观战时查看所有人的准星。
  * "c" 键换道具准星，改为放大小地图，同时小地图调大了一点。
  * "F, E" 现在都绑定了一键清血迹。
  * prt 配置增加 "\" 键加快时间，不用等待烟雾散了。
  * prt 配置增加获取位置和传送到特定位置的方法。
  * prt 配置增加 kni 指令，获取所有原版刀。

* 2020.12.29
  * 很早以前从网上下载的配置文件，应该是 [purp1e](https://github.com/Purple-CSGO/Cfg-Preset-By-Purp1e) 制作的。经过了自己的一些自定义后打包，精简了许多东西，自己用的舒服的版本。

## 常用指令
* 连接至指定服务器
```c
connect 192.168.1.1
```

* 与服务器断开连接
```c
disconnect
```

* 重连服务器
```c
retry
```

* 退出游戏
```c
quit/exit
```

* 设置鼠标灵敏度
```c
sensitivity 0.4
```

* 设置音量
```c
volume 1
```

* 立即自杀
```c
kill
```

## 文件说明
压缩包中包含 *.cfg 文件和 video.txt 文件，这些文件包含的都是修改过的参数，未修改的参数将维持默认，其中 *.cfg 文件用于配置游戏设置，video.txt 文件用于配置视频设置。

*.cfg 文件包含以下文件：
* auto.cfg 配置主要设置
* crosshair.cfg 准星文件
* crosshair_throw.cfg 道具准星
* practice.cfg 跑图配置
* practice_bot.cfg 机器人练习配置

通过添加启动项运行，文件中需包含 `host_writeconfig;`，以实现自动加载。

video.txt 文件是游戏启动时自动加载的。

## 游戏设置

### 杂项设置
* 关闭游戏教学和自动提示
```c
cl_autohelp "0"
cl_showhelp "0"
gameinstructor_enable "0"
```

* 关闭死亡自动回放
```c
spec_replay_autostart "1"
```

* 关闭拾取武器自动切换 
```c
cl_autowepswitch "0"
```

* 取消按 "E" 进入购买菜单
```c
cl_use_opens_buy_menu "0"
```

* 查看所有人的自定义准星
```c
cl_show_observer_crosshair "2"
```

* 启用命令控制台 
```c
con_enable "1"
```

* 显示网络、帧率等信息 
```c
net_graph "1"
```

* 关闭死亡竞赛自动购买武器
```c
cl_dm_buyrandomweapons "0"
```

* 打开枪口火光，看清单向烟后的敌人
```c
r_dynamic "1"
```

* 鼠标灵敏度

    eDPI = DPI x Sensitibity (880 = 1600 x 0.55)，其中 DPI 是鼠标的灵敏度，硬件参数，个人配置 1600 时比较舒服； sensitivity 是游戏的灵敏度 
    ```c
    sensitivity "0.55"
    ```
	![sensitivity](assets/img/2020-12-29-csgo-auto-script/sensitivity.gif)

### 小地图设置
```c
cl_radar_always_centered "0"
cl_radar_icon_scale_min "0.7"
cl_radar_scale "0.3"
```
![radar](assets/img/2020-12-29-csgo-auto-script/radar.gif)
### 按键绑定设置

* 清除弹壳和血迹: “F”
```c
bind "f" "+lookatweapon;r_cleardecals"
```

* 跳跃：“滚轮上”、“滚轮下”
```c
bind "MWHEELUP" "+jump"
bind "MWHEELDOWN" "+jump"
```

* 跳投：“V”，“大小写” （道具拉开保险时使用）
```c
alias "+jumpthrow" "+jump;-attack"
alias "-jumpthrow" "-jump"
bind "v" "+jumpthrow"
bind "CAPSLOCK" "+jumpthrow"
```

* 语音：“鼠标侧键上”，“鼠标侧键下”
```c
bind "MOUSE4" "+voicerecord"
bind "MOUSE5" "+voicerecord"
```

* 切换准星：“C”
```c
alias "+crosshair_throw" "exec crosshair_throw.cfg"
alias "-crosshair_throw" "exec crosshair.cfg"
bind "c" "+crosshair_throw"
```

* 放大小地图，看清混烟敌人和火、雷后的敌人：“C”
```c
bind "c" "toggle cl_radar_scale 1.0 0.4"
```

* 道具切换：“F1~F5”
```c
bind "F1" "slot6"
bind "F2" "slot7"
bind "F3" "slot8"
bind "F4" "slot9"
bind "F5" "slot10"
```

### 声音设置
* 总音量 50%，方便开黑语音
* 玩家阵亡音乐：0%
* 主菜单音乐：0%
* 声音缓冲区长度：10 毫秒
* 菜单选择音量：100%
* 回合结束音量：0%
* 炸弹 10 秒倒计时：5%

```c
volume "1"
snd_deathcamera_volume "0"
snd_menumusic_volume "0"
snd_mixahead "0.01"
snd_music_selection "2"
snd_mvp_volume "0"
snd_tensecondwarning_volume "0.1"
```
![volume](assets/img/2020-12-29-csgo-auto-script/volume.gif)

### 准星设置 
可通过 [NBCSGO](https://www.nbcsgo.com/zx) 进行自定义

* 通用准星

```c
cl_crosshairalpha "255"
cl_crosshaircolor "5"
cl_crosshaircolor_b "50"
cl_crosshaircolor_r "57"
cl_crosshaircolor_g "250"
cl_crosshairdot "0"
cl_crosshairgap "-2"
cl_crosshairsize "2"
cl_crosshairstyle "4"
cl_crosshairusealpha "1"
cl_crosshairthickness "0.5"
cl_fixedcrosshairgap "-2"
cl_crosshair_outlinethickness "1"
cl_crosshair_drawoutline "1"
```
![crosshair](assets/img/2020-12-29-csgo-auto-script/crosshair.gif)

* 投掷物准星

```c
cl_crosshairalpha "200"
cl_crosshaircolor "5"
cl_crosshaircolor_b "50"
cl_crosshaircolor_r "50"
cl_crosshaircolor_g "250"
cl_crosshairdot "0"
cl_crosshairgap "-5"         
cl_crosshairsize "3000"      
cl_crosshairstyle "4"
cl_crosshairusealpha "1"
cl_crosshairthickness "1" 
cl_fixedcrosshairgap "-4"
cl_crosshair_outlinethickness "0"
cl_crosshair_drawoutline "0"
```
![crosshair2](assets/img/2020-12-29-csgo-auto-script/crosshair2.gif)

### 跑图配置
使用此 cfg 文件前，先输入 map de_xxx 或 map cs_xxx 进入 C4 图或人质图。

进图后输入 `prt` 进行跑图练习，包括道具练习、身法练习等。

人物飞行：“T”。

道具回溯：“BackSpace键”。

### BOT 练习配置
同上，进入地图后输入 `bot` 进行机器人练习。

人物飞行：“T”。

爆破模式请选择 T，添加敌人 CT: “+”。

人质模式选择 CT，添加敌人 T: “-”。

## 视频设置
游戏视频设置的配置文件有 `videodefaults.txt` 和 `video.txt`，它们都位于 `X:\Steam\userdata\yourID\730\local\cfg` 下。

修改 `video.txt` 可以更改游戏视频设置。通常视频设置遵循默认设置即可，这里设置为 1024x768 全屏，不管信不信这个设置能让你看人物更清楚、帧数更高。

```JSON
"config"
{
	"setting.fullscreen"                "1"
	"setting.defaultres"                "1024"
	"setting.defaultresheight"          "768"
}
```

## 创意工坊地图推荐
* **FPS Benchmark** 跑分专用图

![mapFpsBenchmark](assets/img/2020-12-29-csgo-auto-script/mapFpsBenchmark.gif)

* **Skills Tranining Map** 全能练习图，竞技前热身专用

![mapCsgoHub](assets/img/2020-12-29-csgo-auto-script/mapCsgoHub.gif)

* **Aim Botz - Traning** 老牌经典 BOT 练习图

![mapAimBotz](assets/img/2020-12-29-csgo-auto-script/mapAimBotz.gif)

* **crzshz' Crosshair Generator v3** 准星配置图

![mapCrosshair](assets/img/2020-12-29-csgo-auto-script/mapCrosshair.gif)

* **Config Generator** 配置自定义图

![mapConfig](assets/img/2020-12-29-csgo-auto-script/mapConfig.gif)

* **Yprac Inferno Guide** 训练图系列，让你精通地图的各个细节

![mapYprac](assets/img/2020-12-29-csgo-auto-script/mapYprac.gif)
