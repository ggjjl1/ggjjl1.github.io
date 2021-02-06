---
title: 在Linux上安装编译Python3
date: 2021-02-06 23:25:22
tags: [Linux,Python]
---
### 系统环境
CentOS 7.4
Python 3.9.1 可以去官网下载发行包 [https://www.python.org/downloads/release/python-391/](https://www.python.org/downloads/release/python-391/)

### 编译工具
在编译Python的时候，需要安装一些必要的模块。
```
yum -y install zlib zlib-devel
yum -y install bzip2 bzip2-devel
yum -y install ncurses ncurses-devel
yum -y install readline readline-devel
yum -y install openssl openssl-devel
yum -y install openssl-static
yum -y install xz lzma xz-devel
yum -y install sqlite sqlite-devel
yum -y install gdbm gdbm-devel
yum -y install tk tk-devel
yum -y install libffi libffi-devel
```

### 编译Python3
解压Python-3.9.1源码包
```
tar -zxvf Python-3.9.1.tar.gz
```
进入目录
```
cd Python-3.9.1
```
配置编译，设置安装目录，以及选择相应的模块
```
./configure --prefix=/usr/python3 \
    --enable-shared CFLAGS=-fPIC \
    LDFLAGS=-Wl,-rpath=/usr/local/openssl/lib:/usr/python3/lib \
    --with-openssl=/usr/local/openssl
```
编译安装
```
make

make install
```

### 创建软连接
```
ln -s /usr/python3/bin/python3 /usr/bin/python3
ln -s /usr/python3/bin/pip3 /usr/bin/pip3
```
安装完成。

**参考**
[https://www.cnblogs.com/freeweb/p/5181764.html](https://www.cnblogs.com/freeweb/p/5181764.html)
