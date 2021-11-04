---
title: "下载与安装"
date: 2019-11-15T00:00:00-06:00
draft: false
weight: 10
---

## 安装Anaconda或者Miniconda

推荐安装Python的科学计算发行版本**Anaconda**. 前往[Anaconda官网](https://www.anaconda.com/)下载最新版安装即可。个人使用可选择Individual Edition，是免费的。安装Anaconda不仅安装了Python, 并且一些常用的Python库，如Numpy, Pandas, scipy, matplotlib等也一并打包安装了，非常方便。我个人比较喜欢安装[Miniconda](https://docs.conda.io/en/latest/miniconda.html)，因为自带的东西很少，但是同样可以使用`conda`包管理器。

## conda管理Python环境

对于不同的项目，可能需要使用不同的Python环境。例如，某个项目需要使用Python 3.8, 另一个需要使用Python 3.9. 不同的项目可能还要求不同的package版本，这些package对Python本身的版本也有要求。如果只使用一个Python环境的话，将会非常混乱。

这时候就需要使用环境管理器来隔离和管理不同的Python环境，Anaconda和Miniconda都自带conda环境管理器。如何使用conda管理环境可参考[conda官方文档](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)。
