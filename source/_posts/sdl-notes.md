---
title: SDL学习笔记之一
date: 2014-12-28 23:39:00
tags: [SDL]
---
写在前面：要说学习SDL的目的，其实是为了想开发一个自己的视频播放器。上网查了很多资料关于开发视频播放器，其中找到一篇博文写的用FFMPEG+SDL来实现一个用100行代码写的释放器。为了弄明白SDL到底是个什么东西，决定去学习一下SDL的API。我在学习SDL的时候，参考的是Lazy Foo老兄写的 Beginning Game Programming v2.0 。
这是他的网站地址：[http://lazyfoo.net/tutorials/SDL/index.php](http://lazyfoo.net/tutorials/SDL/index.php)

关于SDL：
SDL(Simple DirectMedia Layer)是一个跨平台的开发库，旨在提供低级的获取声音，键盘，鼠标，操纵杆和图形硬件通过OpenGL和Direct3D。它被用在视频播放软件，模拟器和流行的游戏上，包括Valve's award winning catalog和许多Humble Bundle游戏。
SDL的官网：[https://www.libsdl.org/](https://www.libsdl.org/)

下载SDL：
目前SDL已经更新到2.0版本。下载地址：[https://www.libsdl.org/download-2.0.php](https://www.libsdl.org/download-2.0.php) 我使用的操作系统是Win8.1，因为我搭建了MinGW环境，所以使用SDL2-devel-2.0.3-mingw.tar.gz (MinGW 32/64-bit)来进行开发。

使用SDL开发第一个程序：

