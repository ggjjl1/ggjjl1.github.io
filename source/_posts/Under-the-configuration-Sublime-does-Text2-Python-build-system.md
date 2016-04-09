---
title: 配置Sublime Text2下Python的build system
date: 2015-01-19 22:24:28
fags: 
---
<!--markdown-->1.找到并点击Preferences->Browse Packages... 在打开的文件夹中找到python，打开这个文件夹，找到并打开文件python.sublime-build
2.添加修改文件：
{
	"cmd": ["python", "-u", "$file"],
	"path":"D:/Python27",
	"file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
	"selector": "source.python"
}

添加python安装目录的path路径，保存退出。
Ctrl+B运行python代码

