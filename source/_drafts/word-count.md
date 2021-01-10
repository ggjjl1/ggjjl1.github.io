---
title: 用多种方式实现wordcount程序
date: 2020-11-23 22:22:23
tags: 算法&数据结构
---
使用多种方式来实现 word count 程序。做过大数据开发的同学应该都认识这个入门级别的程序，统计一个文件中单词出现的频率。

### 使用awk统计文件中单词词频
假如有一个文件 sample.txt 包含内容：
```
this is a sample file
this file will be used for testing
```

对于普通的文本文件，统计文本中每个单词出现频率，如果数据量不是特别大可以直接使用 awk 文本处理工具。