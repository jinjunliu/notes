---
title: "安装"
date: 2019-11-15T00:00:00-06:00
draft: false
weight: 10
---

## 下载与安装

### Windows

对于windows用户，首先前往[Python官网](https://www.python.org/downloads/windows/)下载64位安装包，目前最新版是`3.8.0`, 找到最新版的`Download Windows x86 executable installer`点击即可下载。如何安装可参考[廖雪峰的网站](https://www.liaoxuefeng.com/wiki/1016959663602400/1016959856222624)。

虽然对于64位的机器，既可以安装32位的也可以安装64位的，但最好能安装64位的版本，因为32位版本的Python可使用的内存只有`2G`左右，很容易发生内存不足的错误。参考[这篇博文](https://airbrake.io/blog/python-exception-handling/memoryerror)的这一段：

>If you’re using a 32-bit Python then the maximum memory allocation given to the Python process is exceptionally low. The specific maximum memory allocation limit varies and depends on your system, but it’s usually around 2 GB and certainly no more than 4 GB.

除了从官网安装之外的另一个选项是安装Anaconda. 前往[Anaconda官网](https://www.anaconda.com/)下载最新版安装即可。Anaconda是Python的科学计算发行版本，安装Anaconda不仅安装了Python, 并且一些常用的Python库，如Numpy, Pandas, scipy, matplotlib等也一并打包安装了，非常方便。关于Anaconda的介绍和安装可参考[Seisman的博文](https://blog.seisman.info/anaconda/).

### Linux

Linux下推荐安装Anaconda.