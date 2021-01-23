---
title: 使用 Python 批量重命名文件名
date: 2015-01-06 22:49:00
tags: [Python]
---
可能由于一时鬼迷心窍，看网友说什么，Adobe RGB色彩空间多么多么好，显示效果多么丰富。于是，一个错误的决定带来了trouble，也可以说不是什么问题（由于本人强迫症严重）。Canon 70D设置成Adobe RGB色彩空间后文件的命名方式变成了_MG_1200.CR2、_MG_1001.JPG 本来是如IMG_8888.CR2、IMG_2000.JPG这样的命名。再加上我所有的照片都丢在一个文件夹里的，而Windows的文件排序方式居然以_*.***开头的，这就导致了我这部分拍摄的照片跑到了我之前拍摄的照片的前面，这让我，非常非常地，eggache！！！而且，我后来发现，原来AdobeRGB跟sRGB色彩空间的区别只出现在JPG格式上，而RAW格式是没有色彩空间这一属性的，就是说不管你设置的是AdobeRGB还是sRGB，RAW出来的片子是一样一样的。奇葩的是，命名却也变成了'_'开头的方式。。。而最可恨的是，用windows自带的图片查看器打开AdobeRGB的JPG图片时，由于色彩空间超出了所表示的范围，出现了严重的色彩指针。这。。。这的让我很难受啊。。。于是，问题来了。。。*如何在Windows下批量修改文件名或者删除指定文件？*

刚开始的时候我理所应当的想到windows自带的批处理文件，这个我们平时也经常用到。但是，我完全不熟悉windows批处理，然后上网查了一些教程学习之后，感觉bat批处理还是挺困难的。最后，放弃win批处理，投身python方式。

好了，说了这么多废话，终于要来重头戏了。接好！
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import os
import sys
import string

if __name__ == '__main__':
    srcfiles = os.listdir('.')
    for srcfile in srcfiles:
        filename, suffix = os.path.splitext(srcfile)
        if filename[0] == '_':
            if suffix.lower() == '.jpg':
                targetfile = os.path.join('./', srcfile)
                os.remove(targetfile)
                print u'删除' + filename + suffix
            else:
                destfile = './' + 'I'+filename[1:]+suffix
                os.rename(srcfile, destfile)
                print destfile

    print u'所有文件处理完毕!
```
这是一个python脚本文件，将该脚本拖到需要重命名文件的目录下双击运行即可（当然需要python环境）。
脚本主要特征，运行之后一个可以将_MG_1212.CR2文件改名为IMG_1212.CR2和将_MG_1313.JPG之类的文件删除，因为这类JPG文件色彩严重失真，你一定是不想要的！

这个python脚本仅供大家参考，有不懂的地方请大家自行google，最后，希望能够帮到大家！！！

声明：本脚本仅供各位朋友学习测试使用，如出现任何问题，本人概不负责！
