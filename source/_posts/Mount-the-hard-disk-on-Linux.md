---
title: 在 Linux 上挂载硬盘
date: 2015-11-26 14:21:00
fags: 
---
<!--markdown-->1.先执行如下命令 `df -h` 查看当前系统磁盘信息。

    root@host01:/opt/hadoop-2.6.2/etc/hadoop# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        25G  4.4G   19G  19% /
    none            4.0K     0  4.0K   0% /sys/fs/cgroup
    udev            7.9G   12K  7.9G   1% /dev
    tmpfs           1.6G  408K  1.6G   1% /run
    none            5.0M     0  5.0M   0% /run/lock
    none            7.9G     0  7.9G   0% /run/shm
    none            100M     0  100M   0% /run/user
    /dev/vdc1        50G   52M   47G   1% /data


2.执行 `fdisk -l` 查看系统中是否存在未挂载磁盘。

    root@host01:/opt/hadoop-2.6.2/etc/hadoop# fdisk -l
    
    Disk /dev/vda: 26.8 GB, 26843545600 bytes
    255 heads, 63 sectors/track, 3263 cylinders, total 52428800 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x0008d3a3
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    52426751    26212352   83  Linux
    
    Disk /dev/vdb: 17.2 GB, 17179869184 bytes
    255 heads, 63 sectors/track, 2088 cylinders, total 33554432 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x000d5b4e
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vdb1              63    33543719    16771828+  82  Linux swap / Solaris
    
    Disk /dev/vdc: 53.7 GB, 53687091200 bytes
    255 heads, 63 sectors/track, 6527 cylinders, total 104857600 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x000e4ad7
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vdc1              63   104856254    52428096   83  Linux
    
    Disk /dev/vdd: 2147.5 GB, 2147483648000 bytes
    14 heads, 61 sectors/track, 4911362 cylinders, total 4194304000 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0xd15b19e1
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vdd1            2048  4194303999  2097150976   83  Linux
    
    Disk /dev/vde: 2147.5 GB, 2147483648000 bytes
    14 heads, 61 sectors/track, 4911362 cylinders, total 4194304000 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0xef776a1b
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vde1            2048  4194303999  2097150976   83  Linux

3.对磁盘分区。
执行 fdisk /dev/vdd1 命令，对磁盘进行分区。
依次输入，n，p，1，两次回车，再输入 wq 分区自动进行，并且很快完成。

4.查看分区 fdisk -l 可以看到，分区已经新建。

5.格式化新分区，输入 mkfs.ext3 /dev/xvdb1 进行格式化分区。

6.添加分区信息
使用“echo '/dev/xvdb1  /mnt ext3    defaults    0  0' >> /etc/fstab”（不含引号）命令写入新分区信息。
然后使用“cat /etc/fstab”命令查看，出现以下信息就表示写入成功。

注：ubuntu12.04不支持barrier，所以正确写法是：echo '/dev/xvdb1  /mnt ext3    barrier=0  0  0' >> /etc/fstab

*  如果需要把数据盘单独挂载到某个文件夹，比如单独用来存放网页，可以修改以上命令中的/mnt部分

7.挂载分区
使用“mount -a”命令挂载新分区，然后用“df -h”命令查看，出现以下信息就说明挂载成功，可以开始使用新的分区了。


参考文章：http://help.aliyun.com/knowledge_detail/5974154.htm
