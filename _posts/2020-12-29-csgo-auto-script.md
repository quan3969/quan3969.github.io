---
layout: post
date:   2020-12-29 15:03:19 +0800
title:  "CS:GO 自动配置"
permalink: /csgo
---
> “工欲善其事，必先利其器”，好的设置能让你在 CS:GO 比赛中获得更好的发挥。

本文分为五部分：常用指令、文件说明、游戏设置、视频设置和创意工坊地图推荐。

注意：此 CSGO 自动配置文件并 **不是外挂**，只是帮助玩家自动设置游戏，免去为了每次换机器或重装游戏后都要重新配置的烦恼。

[下载配置文件](assets\csgo\cfg_v0.9.zip)

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
sensitivity 0.55
```

* 设置音量
```c
volume 1
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

### 使用方法
1. 运行一次游戏，使其生成默认配置文件
2. 解压下载到的配置文件，并放在 `X:\Steam\userdata\yourID\730\local\cfg` 下，提示文件重复时，选择全部替换
3. 添加游戏启动项：`+exec auto.cfg`


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

### 小地图设置
```c
cl_radar_always_centered "0"
cl_radar_icon_scale_min "0.7"
cl_radar_scale "0.3"
```

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

### 跑图配置
使用此 cfg 文件前，先输入 map de_xxx 或 map cs_xxx 进入 C4 图或人质图。

进图后输入 `prt` 进行跑图练习，包括道具练习、身法练习等。

人物飞行：“T”。

道具回溯：“BackSpace键”。

### BOT 练习配置
同上，进入地图后输入 `prtbot` 进行机器人练习。

爆破模式请选择 T，添加敌人 CT: “+”。

人质模式选择 CT，添加敌人 T: “-”。

## 视频设置
游戏视频设置的配置文件有 `videodefaults.txt` 和 `video.txt`，它们都位于 `X:\Steam\userdata\yourID\730\local\cfg` 下。修改 `video.txt` 可以更改游戏视频设置。

```JSON
"config"
{
	"setting.csm_quality_level"		"0"
	"setting.mat_software_aa_strength"		"1"
	"setting.fullscreen"		"1"
	"setting.nowindowborder"		"0"
	"setting.aspectratiomode"		"1"
	"setting.mat_vsync"		"0"
	"setting.mat_triplebuffered"		"0"
	"setting.mat_monitorgamma"		"2.200000"
	"setting.mat_queue_mode"		"-1"
	"setting.mat_motion_blur_enabled"		"0"
	"setting.gpu_mem_level"		"2"
	"setting.gpu_level"		"3"
	"setting.mat_antialias"		"8"
	"setting.mat_aaquality"		"0"
	"setting.mat_forceaniso"		"1"
	"setting.cpu_level"		"1"
	"setting.videoconfig_version"		"1"
	"setting.mem_level"		"2"
	"setting.defaultres"		"1920"
	"setting.defaultresheight"		"1080"
	"setting.r_player_visibility_mode"		"1"
	"setauto.mat_enable_uber_shaders"		"1"
}
```

## 创意工坊地图推荐

