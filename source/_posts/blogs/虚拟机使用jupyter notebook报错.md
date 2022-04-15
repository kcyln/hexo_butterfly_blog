---
title: ubuntu 16.04虚拟机使用jupyter notebook报错
tags:
  - jupyter notebook
  - ubuntu
  - Python
categories:
  - 技术杂谈
abbrlink: 2157fcb1
date: 2019-10-01 12:00:00
updated: 2019-10-01 12:00:00
keywords: ubuntu,juptyer notebook
description: ubuntu 16.04虚拟机使用jupyter notebook报错
---

本来打算使用下jupyter notebook，结果运行时报错了

![](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2020/07/28/e0e1a1a313b4fdd21b92fbbe206b1bdf.png)


> 然后，根据搜索引擎结果尝试卸载重装

```shell
sudo -H pip uninstall jupyter notebook
sudo -H pip install jupyter notebook
```

> 安装时又提示错误    `Cannot uninstall 'ipython'`  

![](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2020/07/28/11df463c51409c3e8436a11973c7771b.png)

根据上面的提示又直接使用命令安装ipython `pip install ipython`，发现并没有解决问题

最终搜索到解决方法，运行下面的命令强制更新，更新完成后，重新打开jupyter notebook成功。

```shell
sudo pip3 install --ignore-installed ipython --upgrade
```

<br>

参考链接： https://www.jianshu.com/p/94caf01dd9a6

