---
title: linux下配置VPN
date: 2015-03-16 16:53:00
tags: [Linux,VPN]
---
**前置依赖**
软件：pptpd、ppp
官网：[http://www.poptop.org/](http://www.poptop.org/)
下载地址：[http://poptop.sourceforge.net/yum/stable/rhel6Server/x86_64/](http://poptop.sourceforge.net/yum/stable/rhel6Server/x86_64/)
下载地址：[http://poptop.sourceforge.net/yum/stable/rhel6Server/x86_64/ppp-2.4.5-33.0.rhel6.x86_64.rpm](http://poptop.sourceforge.net/yum/stable/rhel6Server/x86_64/ppp-2.4.5-33.0.rhel6.x86_64.rpm)
安装时会提示 ppp = 2.4.5 is needed by pptpd-1.4.0-1.el6.x86_64
下载 pptpd-1.4.0-1.el6.x86_64.rpm 使用rpm命令安装 

**配置pptpd**
1.修改主配置文件/etc/pptpd.conf 在最后添加：
localip 118.23.2.144  #这行是给VPN服务器设置一个隧道ip
remoteip 192.168.1.1-254  #自动分配给客户端ip地址范围

2.修改配置文件/etc/ppp/options.pptpd设定分配给客户端的dns 
把ms-dns前的注释号去掉，改成可用dns 如ms-dns 8.8.8.8
为了方便查看调试信息，把debug行前面的注释取消即可。Dump前的注释也取消。

3.添加pptpd账号，编辑文件/etc/ppp/chap-secrets
编辑内容为（IP中\*号代表所有）：
```
    # Secrets for authentication using CHAP
    # client        server  secret                  IP addresses
    用户名          pptpd   密码                \*
    用户名         pptpd   密码               192.168.0.3
    用户名         pptpd   密码               192.168.0.4
```
4.运行pptpd 执行命令service pptpd start

5.设置路由转发
按照以上步骤配置完vpn服务器后，通过客户端连接vpn服务器是不能直接访问vpn所在私有网络或者通过vpn访问互联网，需要设置路由转发。
（一）开启ip转发功能：修改配置文件/etc/sysctl.conf,使net.ipv4.iph_forward = 1
（二）写个脚本文件，实现路由，其内容大致如下：
```
    [root@max-vpn ~]# more /usr/local/bin/vpn_route.sh   
    #!/bin/bash  
    /sbin/iptables -t nat -A POSTROUTING -s 192.168.195.0/24 -o eth0 -j SNAT --to-source 118.23.2.144  
    /sbin/iptables -t nat -A POSTROUTING -s 172.16.195.0/24 -o eth1 -j SNAT --to-source 192.168.195.166  
    /sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE  
```
目标网络/vpn的内部网络为192.168.195.0/24,vpn服务器有2个网卡，其中一个连接公网（eth0），ip地址是61.135.251.51，另外一个网卡连私有网络，ip是192.168.195.166。这样就能正常地路由所涉及的网络了。手动执行一下这个脚本，看客户端（windows）是否能访问目标网络里的机器：最简单的方法就是ping，假定目标网络里有一个192.168.195.100的机器，并请允许icmp通过，ping 192.168.195.100 ,正常的话，再进一步访问这个服务器（如远程登录）。没有问题的话，把它加在开机自启里面。为安全起见，你可以在这个脚本里加更多的iptables规则。
这样就可以在CentOS安装pptpd了。大家可以顺利的使用pptpd了。

6.linux系统电脑连接vpn服务器
配置pptp client  地址：[http://pptpclient.sourceforge.net/](http://pptpclient.sourceforge.net/)


## 参考链接
1. [http://www.cnblogs.com/sixiweb/archive/2012/11/20/2778732.html](http://www.cnblogs.com/sixiweb/archive/2012/11/20/2778732.html)
