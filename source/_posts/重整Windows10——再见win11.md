---
title: 重整Windows10——再见win11
description: 重装一下系统，试着维护一个干净稳定的win10
categories: 杂
tags:
  - Windows
  - bug
  - 开源
abbrlink: 3097
date: 2022-03-24 22:39:00
---

# 前言

## 受够你了，Win11

该死

为什么你总是出现各种各样的bug

烦了

不想写

## 受够你了，软件管理

乱七八糟

烦死了

**总之就是想要个干净的操作系统**

# 复盘

## 软件列表

软件还是挺多的，这里简单分个类，考虑一下解决方案

### 音视频处理

#### Adobe全家桶

这个没办法了，还是用@vposy大佬的破解版本即可

#### Davinci Resolve

必装

#### Melodyne

melodyne还是会用到的，有必要装一下

#### OBS

#### Studio One/Cubase

没想好整哪个。。

#### Riffstation

还听哈用的

#### 剪映

#### AudioNodes

一个模块化的DAW

https://www.audionodes.com

#### Music Brainz Picard

一个mp3元数据标签编辑工具

https://picard.musicbrainz.org

#### HandBrake

一个拥有良好界面的高性能视频编码和转换工具

https://handbrake.fr

### 文件阅读和处理

#### 操作系统激活

使用这个工具

https://github.com/TGSAN/CMWTAT_Digital_Edition

#### Office

使用这位朋友提供的工具

https://github.com/YerongAI/Office-Tool

https://www.coolhub.top/archives/42

#### PDF查看和编辑

#### WPS

试着找一下破解版

应该有国际版

#### Guitar Pro

找一下新版的破解吧

#### Potplayer

老牌免费播放器

https://potplayer.daum.net

#### Blendeer

开源的3D设计工具

https://www.blender.org

### 运行环境、驱动程序和管理软件

#### AMD Radeon Software

#### Intel的驱动

#### Nvdia Control Panel

记得装Studio版本的驱动

#### 联想提供的驱动包

#### .Net环境

#### vc运行库

使用vcpkg进行管理

https://github.com/microsoft/vcpkg/blob/master/README_zh_CN.md

### 开发

#### Git

用windows的包管理试一试

#### Jetbrains全家

#### JDK

#### Visual Studio

宇宙第一IDE

#### VSCode及各种配置

#### Matlab

都装上吧。。

#### Unity

#### WSL

配置好WSL

#### Windows Terminal&Zsh

#### 包管理

考虑下面三个

- winget：微软自家的包管理工具
- scoop：蛮火的
- choco

#### sandBox

windows自带的沙盒

#### hyper

开源终端

https://hyper.is

### 小工具

#### 背景更换工具

https://github.com/Krutonium/Windows-10-Login-Background-Changer

#### EasyConnect

不但要装还要**配置一下学校的VPN**

#### Everything

经典

#### 7-Zip

https://www.7-zip.org

#### X-rite color

#### 坚果云

真的很好用

#### 百度网盘

真的很难用

#### TranslucentTB

一个任务栏透明小工具

https://github.com/TranslucentTB/TranslucentTB

#### QuickLook

神器好吧

也是被macOS惯坏了

但预览真的很重要不是吗！

https://github.com/QL-Win/QuickLook

#### Wox

新一代文件定位工具，堪称 Windows 上的 Alfred

#### Snipaste

可取代QQ/微信的强大截图工具，还能把截图当便利贴用

#### Nvdia RTX Voice

NV提供的AI降噪工具

https://www.nvidia.com/en-us/geforce/guides/nvidia-rtx-voice-setup-guide/

#### PowerToys

微软自家的增强工具

https://github.com/microsoft/PowerToys

#### Typora

找个破解版

#### OpenHashTab

右键查看Hash、MD5等

https://github.com/namazso/OpenHashTab

#### AutoHotKey

开源的脚本语言

https://www.autohotkey.com

### 娱乐

#### Steam

Steam永远不会缺席

顺便试一下这个小东西

https://github.com/BeyondDimension/SteamTools

#### Epic Game

其实是为了启动虚幻引擎

#### Origin

#### Yuzu

一个Switch模拟器

#### Dopamine

一个音频播放器

http://www.digimezzo.com/software/dopamine/

## 文件的备份

有哪些需要备份的数据呢。。

### 色彩配置文件

# 思路

> 多多尝试包管理
>
> 多多尝试开源工具

## 系统优化

### 关掉他妈的自动更新

> 参考资料
>
> https://zhuanlan.zhihu.com/p/38070514
>
> https://os.51cto.com/article/661443.html

### 补驱动

先用联想自己的搞一搞

然后Nv、AMD

### 解压缩工具、开启WSL和Terminal、包管理

解压缩先用7-zip吧

WSL单独开一个文章讲

Terminal得先搞一下

搞完Terminal搞包管理，最后整WSL

### 安装各种运行库

先用vcpkg

其他的VS基本都会补上去

## 开发环境

### Java环境

### python环境

## 开发工具的配置

## 专业应用的安装和管理

## 运行环境的管理

## 小工具

# 过程记录

## 前期准备

其实前期准备没什么可说的了，上面的内容就是前期准备

非要说的话也有一些

### 准备PE和镜像

很奇怪啊现在的人都不用PE了，但我还是爱微PE

### 清理数据

先不动启动分区和恢复分区了

主分区格式化一下

数据盘删点东西

### 安装

说实话好久没有安装过了，这里使用WinNTSetup来安装

驱动器位置也就是格式为FAT32的小分区，一般也就是256M

出现一个尴尬点的问题，忘了windows10版本怎么分了，这里摘录一下

先来几个图

![img](https://pica.zhimg.com/80/941c41be5cb441d5f1aedf5ccc469168_1440w.jpg?source=1940ef5c)

微软官网的比较

https://www.microsoft.com/zh-cn/windowsforbusiness/compare

最后还是来个最牛逼的吧

然后直接安装就可以了

## 系统的基本优化

安装的时候依旧登录了微软账号，桌面和浏览器记录都得到了保存。我们来顺便看一眼目最干净的目录结构

```
|-- C:
	|-- PerfLogs
	|-- Program Files
	|-- Program Files(x86)
	|-- Windows
	|-- Users
```

简单删除一下，目前的软件列表如下（不说明的就是不可移除），共21个

```
|-- HEIF图像拓展
|-- Microsoft Edge
|-- Microsoft Edge Update
|-- Microsoft Store
|-- NVDIA Control Panel（可移除）
|-- NVDIA图形驱动程序466.81.1（可移除）
|-- Realtek Audio Console（可移除）
|-- Web媒体扩展（可移除）
|-- Webp图像扩展
|-- Xbox（可移除）
|-- Xbox Game Bar（可移除）
|-- Xbox Live（可移除）
|-- 获取帮助
|-- 计算器（可移除）
|-- 截图和草图（可移除）
|-- 录音机（可移除）
|-- 闹钟和时钟
|-- 人脉
|-- 相机
|-- 应用安装程序
|-- 照片
```

现在有哪些问题捏

- 登录界面背景图片
- 任务栏美化
- 桌面图标美化
- 系统还没有激活
- 一些基本的设置
- 没有关闭更新



### 先进行一个激活和更新的关闭

用奶牛快传真方便

使用自动模式激活`ProfessionalWorkstation`版本，几秒钟之后激活成功

接下来再看一眼应用列表和文件夹，嗯，很好，没什么变化

试着将它移除后重启，看看激活会不会掉

nice，一点儿事都没有，看来是永久激活了

然后`win+R`运行`services.msc`打开服务，找到`Windows Update`，停止顺便禁用掉

然后进一下组策略，运行`gpedit.msc`，`计算机配置-管理模板-Windows更新-配置自动更新`，进行一个禁用

上面的操作属于是双重保险了，应该没啥问题

重启看一眼，提示“某些设置由你的组织来管理”，OK

### 安装一下7-zip

差点把他忘了。。

直接官网开冲，安装在`C:\Program Files\7-Zip`里，然后应用列表里会出现一条`7-Zip 21.07(x64)`，截至目前共有22个应用

### 梯子

Clash安放在`C:\Program Files\Clash`里，启动一下订阅，安装Service Mode，开启系统代理和自启动

### 进行一梭子驱动的补

联想驱动管理安装在`C:\Program Files(x86)\Lenovo Driveers Management`，完事儿进行一套驱动的安装，最后把他干掉

安装一下联想电脑管家，路径在`C:\Program Files(x86)\Lenovo\`，启动开盖开机，关闭其他自启动和提示

此时多出以下三个应用（25），更新一个版本

```
|-- NVDIA HD 音频驱动程序1.3.38.60
|-- NVDIA PhysX 系统软件9.21.0713
|-- 联想电脑管家
|-- NVDIA图形驱动程序466.81.1 => 472.56
```

NVDIA驱动安装在`C:\Program Files\NVDIA\`，安装会增加三项（28），以及两个VC运行库（30）

``` 
|-- NVDIA FrameView SDK
|-- NVDIA GeForce Experience
|-- NVDIA USBC Driver
|-- VC++ 2015-2019 Redistributable(x64) 14.22.27821
|-- VC++ 2015-2019 Redistributable(x86) 14.22.27821
```

> NV的驱动套装一共有五项，分别是
>
> - NVDIA HD音频驱动程序
> - NVDIA PhysX
> - NVDIA USBC Driver
> - NVDIA图形驱动程序
> - NVDIA Geforce Experience

AMD芯片组驱动安装到`C:\AMD`下，自解压安装，添加一项`AMD Chipset Software`（31）

截至目前，系统目录还很干净，但发现另一个问题

- 商店不可用

### 修复win10商店0x8013 1500

1. 运行`inetcpl.cpl`，高级- 使用TLS1.2

   寄了

2. 相同页面恢复高级设置

3. 相同页面重置

### 安装配置Windows Terminal

直接在微软商店安装`Terminal(Pre)`顺便安装`Windows Package Manager Source(winget)`（33）

### 安装WSL

运行`WSL --install`安装最新的Ubuntu发行版，配置用户名和密码，安装以下应用（37）

```
|-- Windows Subsystem for Linux Update
|-- Ubuntu
|-- Microsoft Windows Desktop Runtime - 3.1.22(x64)
|-- Microsoft Windows Desktop Runtime - 6.0.2(x64)
```



### 安装Devtoys和Powertoys

前往GitHub安装即可，增加`DevToys`和`PowerToys(Preview)`（39）

> 不知为何出现了一项`Microsoft Edge WebView2 Runtime`和`Xbox Live`（40）

这一段就先这样吧，优化和美化回头再说，眼看着运行库越来越多了，先打个包

### 安装和配置Git

前往Git-scm下载安装在`C:\Program Files\Git`，应用添加一行`Git`（41）

运行`git config --global user.name "name"`和`git config --global user.email email_address`

生成一下SSHKey，运行`ssh-keygen -t rsa -b 4096 -C "email_address"`

生成的key将会被保存在`~/.ssh/id_rsa.pub`中

### VC++运行库

前往官网下载安装`VC_redist.x64`

应该会补全了。。回头Steam再补一次

### Windows Sandbox

微软官方文档

https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview

搜索启用或关闭Windows功能，勾选Windows沙盒，等待安装完成后重启。沙盒不会作为应用程序出现在应用列表里

### 安装scoop和chocolatey

https://scoop.sh

安装scoop时，需要先添加环境变量`C:\Users\<account>\scoop\shims`

先运行`scoop install openssh`安装ssh，再添加几个源

```shell
scoop bucket add extras
scoop bucket add versions
```



## 常用软件的安装

目前为止算是可以放心用了

### 尝试用winget管理一些软件

安装一梭子软件(54)

```
|-- TIM
|-- WeChat
|-- OBS Studio
|-- QuickLook
|-- Wox
|-- AutoHotKey
|-- OpenHashTab
|-- PotPlayer
|-- MusicBrainz Picard
|-- HandBrake
|-- Nutstore
|-- Dopamine
|-- 百度网盘
```

## 开发

### Visual Studio

