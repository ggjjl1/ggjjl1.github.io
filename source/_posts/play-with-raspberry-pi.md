---
title: 玩转树莓派
date: 2015-01-07 15:46:00
tags: [Linux,树莓派]
---
### 简介
看到网上有很多人在玩Raspberry Pi(树莓派)，于是我也买了一个准备玩玩。关于树莓派的介绍就不多说了，想了解的自己gogole或者请戳 -> [http://www.raspberrypi.org/](http://www.raspberrypi.org/)

这是我从淘宝上买的树莓派和一些相关的附件
![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfbglv747wj31400u04qq.jpg)
（一张来自2020年的配图，配件还有一块电源适配器）

整个树莓派就一块很小的电路板，大小跟一张信用卡差不多。我买的是树莓派基金会最新出的Raspberry Pi B+版本，CPU是Broadcom BCM2835 700MHz ARM1176JZFS 内存：512M 4个USB接口 一个10/100 BaseT RJ45网口 一个HDMI接口 一个音频输出口 15路MPI CSI-2连接器 和 一个MicroSD卡插槽

> 来自2020年的说明：我的这个树莓派已经是早期的型号了，现在新出的内存都已经上8GB了。

### 给树莓派安装系统
1. 从官网下载树莓派系统 [http://www.raspberrypi.org/downloads/](http://www.raspberrypi.org/downloads/) 我下载的是raspbian
2. 下载Win32DiskImager，将raspbian系统烧录到SD卡上
3. 将SD卡插入树莓派卡槽
4. 将树莓派连接到路由器上面，登录路由器查看客户端列表，找到树莓派的ip，一般树莓派客户端名是raspberrypi。
5. 使用SSH连接到树莓派，这里我是用windows自带的CMD。
    在CMD中输入：ssh pi@树莓派的ip，输入密码raspberry，登录到树莓派。
6. 安装树莓派图形化界面
    在有网络的情况下，输入sudo apt-get install xrdp
7. 安装完成后，使用windows自带的远程桌面连接工具，运行mstsc，打开远程桌面连接，输入树莓派的ip，再输入用户名pi和密码raspberry即可登陆到树莓派的桌面。
