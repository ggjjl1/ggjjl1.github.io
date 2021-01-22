---
title: Mac OS X 10.11 上安装 MySQLdb 出现问题
date: 2015-11-14 16:39:00
tags: [Mac OSX]
---
**问题描述：**
更新Mac OS X 10.11后安装MySQLdb，进入ipython交互命令后，输入import MySQLdb  
```
    In [1]: import MySQLdb
    ---------------------------------------------------------------------------
    ImportError                               Traceback (most recent call last)
    <ipython-input-1-dd22983d5391> in <module>()
    ----> 1 import MySQLdb
    
    /Library/Python/2.7/site-packages/MySQL_python-1.2.4b4-py2.7-macosx-10.10-intel.egg/MySQLdb/__init__.py in <module>()
         17 from MySQLdb.release import __version__, version_info, __author__
         18 
    ---> 19 import _mysql
         20 
         21 if version_info != _mysql.version_info:
    
    ImportError: dlopen(/Library/Python/2.7/site-packages/MySQL_python-1.2.4b4-py2.7-macosx-10.10-intel.egg/_mysql.so, 2): Library not loaded: libmysqlclient.18.dylib
      Referenced from: /Library/Python/2.7/site-packages/MySQL_python-1.2.4b4-py2.7-macosx-10.10-intel.egg/_mysql.so
      Reason: image not found
```

**问题原因：**
由于EI Capitan 增加了System Integrity Protection 的功能，阻止了写入的操作的，默认是开启的，需要关闭。

**解决办法：**
重启电脑，开机时按住 cmd + R，进入 Recovery 模式。然后打开终端工具 ，输入命令：`csrutil disable`，然后再次重启电脑。
重启后，打开terminal输入以下命令：
```
    sudo ln -s /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/lib/libmysqlclient.18.dylib
```
如果不关闭写入操作，将会出现以下情况：
```
    ln: /usr/lib/libmysqlclient.18.dylib: Operation not permitted
```
**引用：**
[http://segmentfault.com/q/1010000003026543](http://segmentfault.com/q/1010000003026543)
