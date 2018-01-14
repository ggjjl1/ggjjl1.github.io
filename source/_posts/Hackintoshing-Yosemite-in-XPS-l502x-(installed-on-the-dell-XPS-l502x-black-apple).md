---
title: hackintoshing yosemite in xps l502x(在戴尔xps l502x上安装黑苹果）
date: 2015-01-03 00:45:00
tags: [Mac OSX,黑苹果]
---
由于想尝试在Mac OSX下做开发，之前在虚拟机中体验过，因为速度太慢实在无法忍受，所以决定在PC上面安装黑苹果。我的机器是戴尔XPS L502X，准备安装的系统是Apple最新的OS X Yosemite 10.10.1 。
硬件配置详情：
------鲁大师 Build V5.5.14.1065------

电脑型号: 戴尔 System XPS L502X 笔记本电脑
操作系统: Windows 8.1 专业版 64位

  处理器: 英特尔 第二代酷睿 i7-2630QM @ 2.00GHz 四核
    主板: 戴尔 0NJT03
    内存: 8 GB ( 金士顿 DDR3 1333MHz / 三星 DDR3 1333MHz )
  主硬盘: 西数 WDC WD7500BPKT-75PK4T0 ( 750 GB / 7200 转/分 )
    显卡: Nvidia GeForce GT 540M ( 2 GB / 戴尔 )
  显示器: 友达 AUO17ED ( 15.3 英寸 )
    光驱: 日立-LG DVD+-RW GT32N DVD刻录机
    声卡: 瑞昱 ALC665 高保真音频
    网卡: 瑞昱 RTL8168E PCI-E Gigabit Ethernet NIC / 戴尔

准备工作：
1.先对硬盘进行分区
从硬盘中分一块区域用来安装OSX，如果没有空闲的分区，可以在已经分出来的区域中（如E盘、F盘）进行压缩卷（压缩卷就是从E盘空闲的区域重新分一块新的区域出来

注：很多品牌电脑出厂自带OEM分区和Recovery分区，需要对这两个分区添加盘符，不然引导工具无法正确安装。
给分区添加盘符方法很简单，可以使用windows自带的diskpart工具。步骤如下
a.运行CMD
b.输入diskpart      #打开windows磁盘分区工具
c.list disk        #这一步会显示你电脑上有多少块硬盘
d.选择你要安装系统的磁盘，我这里选择sel disk 0
e.list part     #列出磁盘上所有的分区，找到OEM所对应的分区
f.sel part 1
g.set id 7   #给分区设置一个ID，数字随便给，这样就能显示出来了，如果还不行assign letter P，分配盘符

2.制作安装盘
我使用的是U盘安装，所以我只做了一个安装U盘。

完成这些步骤之后，拔出U盘然后再插上，在资源管理器中可以看到U盘的EFI分区。将解压得到的boot文件和EFI文件拷贝到安装U盘的EFI分区目录下。到此OSX的安装U盘制作完成。

3.安装OSX系统

