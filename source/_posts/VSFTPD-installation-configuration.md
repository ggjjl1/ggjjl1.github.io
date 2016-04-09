---
title: vsftpd安装配置
date: 2014-12-21 23:33:26
fags: 
---
<!--markdown-->vsftpd简介
vsftpd是一个运行在类unix上的FTP服务器程序，能运行在linux，BSD，Soliars等多个平台上

vsftpd安装
1.使用yum安装或者在ubuntu上面使用apt-get方式
2.去官网下载源码包
[root@localhost ~]# tar zxvf vsftpd-2.0.3.tar.gz
[root@localhost ~]# cd vsftpd-2.0.3
[root@localhost ~]# make && make install
[root@localhost ~]# cp vsftpd.conf /etc
然后修改/etc/vsftpd.conf ，在配置文件的最后一行加入下面一行；
listen=yes

vsftpd配置



