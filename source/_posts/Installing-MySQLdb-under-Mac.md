---
title: Mac 下安装 MySQLdb
date: 2016-03-06 00:13:12
fags: 
---
<!--markdown-->环境
系统版本: Mac OS X EI Caption (version 10.11.1)
Python 版本: 2.7.10
virtualenv (14.0.6)

问题
安装 MySQLdb 出现 mysql_config not found
解决以上问题后，又出现 Reason: image not found
通过以下命令可以解决该问题
sudo ln -s /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/lib/libmysqlclient.18.dylib
但是，执行这条命令后又会出现 ln: /usr/lib/libmysqlclient.18.dylib: Operation not permitted 
这个问题。

最后，找到 stackoverflow 上给出的解决方案。
执行一下命令，即可解决问题。
/usr/local/mysql/lib/libmysqlclient.18.dylib /usr/local/lib/libmysqlclient.18.dylib





参考文章
http://blog.csdn.net/janronehoo/article/details/25207825
http://stackoverflow.com/questions/10557507/rails-mysql-on-osx-library-not-loaded-libmysqlclient-18-dylib

