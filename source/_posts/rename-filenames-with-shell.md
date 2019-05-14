---
title: 使用shell批量更改文件名
date: 2018-01-13 12:01:46
tags: [Linux,Shell]
---
**问题由来**
由于5D3默认使用的文件名前缀是【5P7A】，在拍了一大堆照片后才注意到这个前缀。后来在相机中重新设置文件名前缀为【IMG\_】，但是已经拍摄的照片文件名前缀没法在相机中更改。所以只能在电脑中通过程序批量更改这些文件名。于是想到了shell。

![截图](http://static.gaojunliang.cn/WechatIMG9930.jpeg)

**解决办法**
```
for i in `ls -a|grep 5P7A`;do mv $i ${i/5P7A/IMG_};done
```

一行代码搞定。
