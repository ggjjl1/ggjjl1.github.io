---
title: 在 Linux 上搭建邮件服务器
date: 2014-12-20 23:04:12
tags: [Linux]
---
### 需要的软件：
* postfix
* mysql
* openssl
* sasl
### 安装：
1. mysql安装（略）
2. openssl安装
```
tar zxvf openssl-0.9.8e.tar.gz
cd openssl-0.9.8e
./config shared zlib
make
make test
make install
mv /usr/bin/openssl /usr/bin/openssl.OFF
mv /usr/include/openssl /usr/include/openssl.OFF
rm /usr/lib/libssl.so
ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl
ln -s /usr/local/ssl/include/openssl /usr/include/openssl
ln -sv /usr/local/ssl/lib/libssl.so.0.9.8 /usr/lib/libssl.so
```
### 配置库文件搜索路径
```
echo "/usr/local/ssl/lib" >> /etc/ld.so.conf
ldconfig -v
```
### 检测安装结果
```
openssl version
OpenSSL 0.9.8e 23 Feb 2007
```

