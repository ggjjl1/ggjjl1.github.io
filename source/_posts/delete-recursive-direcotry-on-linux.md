---
title: linux删除当前目录及子目录下所有\*.xx文件
date: 2015-06-10 18:04:56
tags: [Linux]
---
尝试了下用rm -rf \*.xx的方式不行。

上网查了下需要用到组合命令：
find . -name "\*.xx" -exec rm -rf {} \;
